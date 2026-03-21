<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-app.js";
  import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-auth.js";
  import {
    getFirestore, doc, setDoc, onSnapshot, serverTimestamp
  } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-firestore.js";
  import {
    getStorage, ref, uploadBytes, getDownloadURL, deleteObject
  } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-storage.js";

  const STAFF_LIST = [
    { id:1,  nama:"'Afifah Binti Abdul Aziz",          kat:1 },
    { id:2,  nama:"Ida Zarina Binti Idris",            kat:1 },
    { id:3,  nama:"Azian Binti Mohamad",               kat:1 },
    { id:4,  nama:"Fatimah Binti Latiff",              kat:1 },
    { id:5,  nama:"Zainun Binti Mohamed Ramthan",      kat:1 },
    { id:6,  nama:"Nor'aini Binti Md Yusoff",          kat:1 },
    { id:7,  nama:"Fakarullah Amer Bin Zainal Abidin", kat:1 },
    { id:8,  nama:"Abdul Azam Bin Mohamed",            kat:1 },
    { id:9,  nama:"Nor Faiza Binti Mustaffa Kamal",    kat:2 },
    { id:10, nama:"Wan Azlena Binti Wan Deraman",      kat:2 },
    { id:11, nama:"Mohd Faizal Bin Zainal",            kat:2 },
    { id:12, nama:"Juhaida Binti Abd Rasid",           kat:3 },
    { id:13, nama:"Junainah Binti Hassan",             kat:3 },
    { id:14, nama:"Rafidah Binti Sidek",               kat:3 },
    { id:15, nama:"Muhammad Fahmi Bin Hamidin",        kat:4 },
    { id:16, nama:"Nursyaza Aina Binti Mohd Adaha",    kat:4 }
  ];

  const KAT_NAMES = {
    1:"Pembantu Makmal",
    2:"Pembantu Pengurusan Murid",
    3:"Pembantu Tadbir",
    4:"Pembantu Khidmat Am"
  };

  const KAT_CSS = { 1:"kat-1", 2:"kat-2", 3:"kat-3", 4:"kat-4" };

  const firebaseConfig = {
    apiKey: "PASTE_API_KEY",
    authDomain: "PASTE_AUTH_DOMAIN",
    projectId: "PASTE_PROJECT_ID",
    storageBucket: "PASTE_STORAGE_BUCKET",
    messagingSenderId: "PASTE_MESSAGING_SENDER_ID",
    appId: "PASTE_APP_ID"
  };

  function hasPlaceholderConfig(cfg){
    return Object.values(cfg).some(v => String(v).includes("PASTE_") || !String(v).trim());
  }

  let app = null;
  let auth = null;
  let db = null;
  let storage = null;

  let firebaseReady = false;
  let firebaseUid = null;

  let currentWeekOffset = 0;
  let currentRole = null; // pengetua | admin | null
  let currentLoginTab = "pengetua";
  let currentStaffId = null;

  let pendingCancelId = null;
  let pendingPengesahanId = null;

  let submissions = {};
  let weekSignatures = {};
  let settingsData = {
    bannerUrl: null,
    bannerPath: null,
    logoUrl: null,
    logoPath: null
  };

  let autosaveTimer = null;
  let unsubmissions = null;
  let unweeksig = null;
  let unsettings = null;

  function escapeHtml(str){
    return String(str ?? "")
      .replace(/&/g,"&amp;")
      .replace(/</g,"&lt;")
      .replace(/>/g,"&gt;")
      .replace(/"/g,"&quot;")
      .replace(/'/g,"&#039;");
  }

  function showToast(msg, type=""){
    const container = document.getElementById("toastContainer");
    const toast = document.createElement("div");
    toast.className = `toast ${type}`;
    const icons = {
      success:"fa-check-circle",
      error:"fa-times-circle",
      warning:"fa-exclamation-triangle",
      default:"fa-info-circle"
    };
    toast.innerHTML = `<i class="fas ${icons[type] || icons.default}"></i> ${escapeHtml(msg)}`;
    container.appendChild(toast);

    setTimeout(() => {
      toast.style.opacity = "0";
      toast.style.transition = "opacity .4s";
      setTimeout(() => toast.remove(), 400);
    }, 3000);
  }

  function triggerAutosave(){
    const ind = document.getElementById("autosaveIndicator");
    ind.classList.add("visible");
    clearTimeout(autosaveTimer);
    autosaveTimer = setTimeout(() => ind.classList.remove("visible"), 2200);
  }

  function openModal(id){
    document.getElementById(id).classList.add("open");
    document.body.style.overflow = "hidden";
  }

  function closeModal(id){
    document.getElementById(id).classList.remove("open");
    if(!document.querySelector(".modal-overlay.open")){
      document.body.style.overflow = "";
    }
  }

  window.closeModal = closeModal;

  document.querySelectorAll(".modal-overlay").forEach(overlay => {
    overlay.addEventListener("click", e => {
      if(e.target === overlay){
        overlay.classList.remove("open");
        if(!document.querySelector(".modal-overlay.open")){
          document.body.style.overflow = "";
        }
      }
    });
  });

  function getWeekStart(offset=0){
    const now = new Date();
    const day = now.getDay();
    const diff = day === 0 ? -6 : 1 - day;
    const monday = new Date(now);
    monday.setDate(now.getDate() + diff + offset * 7);
    monday.setHours(0,0,0,0);
    return monday;
  }

  function getWeekEnd(offset=0){
    const mon = getWeekStart(offset);
    const fri = new Date(mon);
    fri.setDate(mon.getDate() + 4);
    fri.setHours(23,59,59,999);
    return fri;
  }

  function getWeekKey(offset=currentWeekOffset){
    const mon = getWeekStart(offset);
    return `week_${mon.getFullYear()}_${mon.getMonth()+1}_${mon.getDate()}`;
  }

  function getWeekNumber(offset=0){
    const mon = getWeekStart(offset);
    const jan1 = new Date(mon.getFullYear(), 0, 1);
    const days = Math.floor((mon - jan1) / 86400000);
    return Math.ceil((days + jan1.getDay() + 1) / 7);
  }

  function formatDate(d){
    const days = ["Ahad","Isnin","Selasa","Rabu","Khamis","Jumaat","Sabtu"];
    const months = ["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];
    return `${days[d.getDay()]}, ${d.getDate()} ${months[d.getMonth()]} ${d.getFullYear()}`;
  }

  function formatDateShort(d){
    const months = ["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];
    return `${d.getDate()} ${months[d.getMonth()]} ${d.getFullYear()}`;
  }

  function updateWeekDisplay(){
    const mon = getWeekStart(currentWeekOffset);
    const fri = getWeekEnd(currentWeekOffset);
    const wn = getWeekNumber(currentWeekOffset);
    const months = ["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];

    document.getElementById("weekLabel").textContent = `Minggu ${wn}`;
    document.getElementById("weekDates").textContent = `${formatDate(mon)} – ${formatDate(fri)}`;
    document.getElementById("tableSubtitle").textContent =
      `${mon.getDate()} ${months[mon.getMonth()]} – ${fri.getDate()} ${months[fri.getMonth()]} ${fri.getFullYear()}`;
  }

  function prevWeek(){
    currentWeekOffset--;
    updateWeekDisplay();
    subscribeWeekData();
  }

  function nextWeek(){
    currentWeekOffset++;
    updateWeekDisplay();
    subscribeWeekData();
  }

  function goToCurrentWeek(){
    currentWeekOffset = 0;
    updateWeekDisplay();
    subscribeWeekData();
  }

  window.prevWeek = prevWeek;
  window.nextWeek = nextWeek;
  window.goToCurrentWeek = goToCurrentWeek;

  function isLate(offset){
    return new Date() > getWeekEnd(offset);
  }

  function computeStatus(staffId, weekOffset){
    const key = getWeekKey(weekOffset);
    const sub = (submissions[key] || {})[staffId];
    if(!sub) return isLate(weekOffset) ? "Lewat" : "Belum Hantar";
    return sub.status || "Disahkan";
  }

  function populateStaffSelect(){
    const select = document.getElementById("staffSelect");
    select.innerHTML = `<option value="">Pilih nama staf untuk upload</option>`;

    STAFF_LIST.forEach(staff => {
      const opt = document.createElement("option");
      opt.value = String(staff.id);
      opt.textContent = staff.nama;
      select.appendChild(opt);
    });

    const savedStaff = localStorage.getItem("smkm_selected_staff");
    if(savedStaff){
      select.value = savedStaff;
      currentStaffId = Number(savedStaff);
    }
  }

  window.selectStaffLogin = function(staffId){
    currentStaffId = staffId ? Number(staffId) : null;

    if(currentStaffId){
      localStorage.setItem("smkm_selected_staff", String(currentStaffId));
      const staff = STAFF_LIST.find(s => s.id === currentStaffId);
      showToast(`Staf aktif: ${staff?.nama || "Dipilih"}`, "success");
    } else {
      localStorage.removeItem("smkm_selected_staff");
      showToast("Pilihan staf dikosongkan.", "warning");
    }

    renderTable();
  };

  function setFirebaseStatus(text){
    document.getElementById("firebaseStatusText").textContent = text;
  }

  function applyBrandingToUI(){
    const bannerImg = document.getElementById("bannerImg");
    const logoImg = document.getElementById("logoImg");
    const logoText = document.getElementById("logoText");

    if(settingsData.bannerUrl){
      bannerImg.src = settingsData.bannerUrl;
      bannerImg.style.display = "block";
    } else {
      bannerImg.removeAttribute("src");
      bannerImg.style.display = "none";
    }

    if(settingsData.logoUrl){
      logoImg.src = settingsData.logoUrl;
      logoImg.style.display = "block";
      logoText.style.display = "none";
    } else {
      logoImg.removeAttribute("src");
      logoImg.style.display = "none";
      logoText.style.display = "inline";
    }
  }

  async function initFirebase(){
    if(hasPlaceholderConfig(firebaseConfig)){
      setFirebaseStatus("Sila lengkapkan config Firebase");
      showToast("Gantikan semua nilai PASTE_* dalam firebaseConfig dahulu.", "error");
      renderTable();
      updateStats();
      updatePrincipalSection();
      return;
    }

    try{
      app = initializeApp(firebaseConfig);
      auth = getAuth(app);
      db = getFirestore(app);
      storage = getStorage(app);

      await signInAnonymously(auth);

      onAuthStateChanged(auth, user => {
        if(user){
          firebaseUid = user.uid;
          firebaseReady = true;
          setFirebaseStatus("Tersambung");
          subscribeSettings();
          subscribeWeekData();
        } else {
          firebaseReady = false;
          firebaseUid = null;
          setFirebaseStatus("Belum log masuk");
        }
      });
    }catch(err){
      console.error(err);
      firebaseReady = false;
      setFirebaseStatus("Gagal sambung Firebase");
      showToast("Gagal sambung Firebase. Semak config dan rules.", "error");
    }
  }

  function subscribeSettings(){
    if(!firebaseReady || !db) return;
    if(unsettings) unsettings();

    const settingsRef = doc(db, "systemSettings", "branding");
    unsettings = onSnapshot(settingsRef, snap => {
      settingsData = snap.exists()
        ? {
            bannerUrl: snap.data().bannerUrl || null,
            bannerPath: snap.data().bannerPath || null,
            logoUrl: snap.data().logoUrl || null,
            logoPath: snap.data().logoPath || null
          }
        : {
            bannerUrl: null,
            bannerPath: null,
            logoUrl: null,
            logoPath: null
          };

      applyBrandingToUI();
    }, err => {
      console.error(err);
      showToast("Gagal baca tetapan branding.", "error");
    });
  }

  function subscribeWeekData(){
    if(!firebaseReady || !db) return;

    const weekKey = getWeekKey();

    if(unsubmissions) unsubmissions();
    if(unweeksig) unweeksig();

    const submissionsRef = doc(db, "weeklySubmissions", weekKey);
    unsubmissions = onSnapshot(submissionsRef, snap => {
      const data = snap.exists() ? snap.data() : { records:{} };
      submissions[weekKey] = data.records || {};
      renderTable();
    }, err => {
      console.error(err);
      showToast("Gagal baca data penghantaran.", "error");
    });

    const sigRef = doc(db, "weeklySignatures", weekKey);
    unweeksig = onSnapshot(sigRef, snap => {
      weekSignatures[weekKey] = snap.exists() ? snap.data() : {};
      updatePrincipalSection();
    }, err => {
      console.error(err);
      showToast("Gagal baca pengesahan pengetua.", "error");
    });
  }

  async function saveWeekSubmissions(weekKey){
    await setDoc(doc(db, "weeklySubmissions", weekKey), {
      records: submissions[weekKey] || {},
      updatedAt: serverTimestamp()
    }, { merge:true });
    triggerAutosave();
  }

  async function saveWeekSignature(weekKey){
    await setDoc(doc(db, "weeklySignatures", weekKey), {
      ...weekSignatures[weekKey],
      updatedAt: serverTimestamp()
    }, { merge:true });
    triggerAutosave();
  }

  async function saveBranding(){
    await setDoc(doc(db, "systemSettings", "branding"), {
      bannerUrl: settingsData.bannerUrl || null,
      bannerPath: settingsData.bannerPath || null,
      logoUrl: settingsData.logoUrl || null,
      logoPath: settingsData.logoPath || null,
      updatedAt: serverTimestamp()
    }, { merge:true });
    triggerAutosave();
  }

  function applyFilters(){
    renderTable();
  }
  window.applyFilters = applyFilters;

  function renderTable(){
    const search = (document.getElementById("searchInput")?.value || "").toLowerCase();
    const filterKat = document.getElementById("filterKat")?.value || "";
    const filterStatus = document.getElementById("filterStatus")?.value || "";

    const key = getWeekKey();
    const mon = getWeekStart(currentWeekOffset);
    const fri = getWeekEnd(currentWeekOffset);
    const weekRange = `${formatDateShort(mon)} – ${formatDateShort(fri)}`;

    const filtered = STAFF_LIST.filter(s => {
      if(search && !s.nama.toLowerCase().includes(search)) return false;
      if(filterKat && String(s.kat) !== filterKat) return false;
      const st = computeStatus(s.id, currentWeekOffset);
      if(filterStatus && st !== filterStatus) return false;
      return true;
    });

    document.getElementById("filterCount").textContent = `Paparan: ${filtered.length} / ${STAFF_LIST.length} rekod`;

    const tbody = document.getElementById("tableBody");
    tbody.innerHTML = "";

    filtered.forEach((staff, idx) => {
      const sub = (submissions[key] || {})[staff.id];
      const status = computeStatus(staff.id, currentWeekOffset);
      const statusClass = status === "Disahkan" ? "status-disahkan" : status === "Lewat" ? "status-lewat" : "status-belum";
      const isOwnRow = currentStaffId === staff.id;

      let ftBadge = '<span class="empty-cell">–</span>';
      if(sub){
        const ext = (sub.fileType || "").toLowerCase();
        const cls = ext === "pdf" ? "ft-pdf" : (ext === "doc" || ext === "docx") ? "ft-doc" : "ft-img";
        ftBadge = `<span class="file-type-badge ${cls}">${escapeHtml(ext.toUpperCase())}</span>`;
      }

      const uploadCell = sub
        ? `<span style="font-size:12px;color:var(--emerald)"><i class="fas fa-check-circle"></i> Dimuat naik</span>`
        : isOwnRow
          ? `<label class="upload-label" for="fileInput_${staff.id}">
               <i class="fas fa-upload"></i> Muat Naik
             </label>
             <input type="file" id="fileInput_${staff.id}" accept=".pdf,.jpg,.jpeg,.png,.doc,.docx" onchange="handleUpload(event, ${staff.id})">`
          : `<span class="empty-cell">–</span>`;

      let actions = "";
      if(sub){
        actions += `<button class="btn-sm btn-secondary" type="button" onclick="previewFile(${staff.id})"><i class="fas fa-eye"></i> Lihat</button>`;
        if(isOwnRow || currentRole === "admin" || currentRole === "pengetua"){
          actions += `<button class="btn-sm btn-danger" type="button" onclick="openCancelConfirm(${staff.id})"><i class="fas fa-times"></i> Batal</button>`;
        }
      } else {
        actions = '<span class="empty-cell">–</span>';
      }

      const semakanVal = sub ? (sub.semakan || "") : "";
      const semakanCell =
        (currentRole === "admin" || currentRole === "pengetua")
          ? `<textarea class="semakan-input" rows="2" placeholder="Catatan semakan..." onchange="saveSemakan(${staff.id}, this.value)">${escapeHtml(semakanVal)}</textarea>`
          : (semakanVal
              ? `<span style="font-size:12px;white-space:normal;line-height:1.45">${escapeHtml(semakanVal)}</span>`
              : '<span class="empty-cell">–</span>');

      let pengesahanCell = "";
      const pengesahan = sub ? sub.pengesahan : null;

      if(pengesahan){
        pengesahanCell = `
          <div class="pengesahan-cell">
            <span class="pengesahan-badge pengesahan-disahkan"><i class="fas fa-check-circle"></i> Disahkan</span>
            <span class="catatan-text">${escapeHtml(pengesahan.catatan || "")}</span>
            <span style="font-size:10.5px;color:var(--slate)">${escapeHtml(pengesahan.tarikh || "")}</span>
          </div>
        `;
      } else if(sub && currentRole === "pengetua"){
        pengesahanCell = `<button class="btn-sm btn-gold" type="button" onclick="openPengesahan(${staff.id})"><i class="fas fa-stamp"></i> Sahkan</button>`;
      } else if(sub){
        pengesahanCell = `<span class="pengesahan-badge pengesahan-pending"><i class="fas fa-hourglass-half"></i> Menunggu</span>`;
      } else {
        pengesahanCell = '<span class="empty-cell">–</span>';
      }

      const tr = document.createElement("tr");
      tr.innerHTML = `
        <td class="bil-cell">${idx + 1}</td>
        <td class="nama-cell td-wrap">${escapeHtml(staff.nama)}${isOwnRow ? ' <span style="font-size:11px;color:var(--amber)">(Anda)</span>' : ''}</td>
        <td><span class="kat-badge ${KAT_CSS[staff.kat]}">${escapeHtml(KAT_NAMES[staff.kat])}</span></td>
        <td style="font-size:12px">${escapeHtml(weekRange)}</td>
        <td>${uploadCell}</td>
        <td>${ftBadge}</td>
        <td style="max-width:160px;overflow:hidden;text-overflow:ellipsis;font-size:12px">${sub ? escapeHtml(sub.fileName) : '<span class="empty-cell">–</span>'}</td>
        <td style="font-size:12px">${sub ? escapeHtml(sub.tarikhHantar) : '<span class="empty-cell">–</span>'}</td>
        <td><span class="status-badge ${statusClass}">
          <i class="fas ${status === 'Disahkan' ? 'fa-check-circle' : status === 'Lewat' ? 'fa-exclamation-circle' : 'fa-clock'}"></i> ${escapeHtml(status)}
        </span></td>
        <td><div class="action-group">${actions}</div></td>
        <td class="semakan-cell">${semakanCell}</td>
        <td>${pengesahanCell}</td>
      `;
      tbody.appendChild(tr);
    });

    updateStats();
    updateNotifications();
    updatePrincipalSection();
  }

  window.handleUpload = async function(event, staffId){
    try{
      if(!firebaseReady || !storage || !db){
        showToast("Firebase belum sedia.", "error");
        return;
      }

      if(currentStaffId !== staffId){
        showToast("Hanya staf terpilih boleh upload fail sendiri.", "error");
        event.target.value = "";
        return;
      }

      const file = event.target.files?.[0];
      if(!file) return;

      const allowed = ["pdf","jpg","jpeg","png","doc","docx"];
      const ext = file.name.split(".").pop().toLowerCase();

      if(!allowed.includes(ext)){
        showToast("Jenis fail tidak dibenarkan.", "error");
        event.target.value = "";
        return;
      }

      const weekKey = getWeekKey();
      const now = new Date();
      const safeName = file.name.replace(/[^\w.\-]+/g, "_");
      const storagePath = `submissions/${weekKey}/${staffId}/${Date.now()}_${safeName}`;
      const storageRef = ref(storage, storagePath);

      showToast("Sedang upload fail...", "warning");
      await uploadBytes(storageRef, file);
      const fileUrl = await getDownloadURL(storageRef);

      if(!submissions[weekKey]) submissions[weekKey] = {};

      const oldRecord = submissions[weekKey][staffId];
      if(oldRecord?.storagePath){
        try{
          await deleteObject(ref(storage, oldRecord.storagePath));
        }catch(e){
          console.warn("Fail lama tidak ditemui semasa penggantian.", e);
        }
      }

      submissions[weekKey][staffId] = {
        staffId,
        fileName: file.name,
        fileType: ext,
        fileUrl,
        storagePath,
        tarikhHantar: formatDateShort(now),
        status: isLate(currentWeekOffset) ? "Lewat" : "Disahkan",
        semakan: oldRecord?.semakan || "",
        pengesahan: oldRecord?.pengesahan || null,
        uploadedByName: STAFF_LIST.find(s => s.id === staffId)?.nama || "",
        updatedAtMs: Date.now()
      };

      await saveWeekSubmissions(weekKey);
      showToast("Fail berjaya dimuat naik!", "success");
      renderTable();
    }catch(err){
      console.error(err);
      showToast("Upload gagal. Semak Storage Rules dan config.", "error");
    }finally{
      event.target.value = "";
    }
  };

  window.openCancelConfirm = function(staffId){
    pendingCancelId = staffId;
    openModal("confirmModal");
  };

  window.confirmCancelSubmission = async function(){
    try{
      const weekKey = getWeekKey();
      const row = submissions[weekKey]?.[pendingCancelId];
      if(!row) return;

      const canDelete = currentStaffId === pendingCancelId || currentRole === "admin" || currentRole === "pengetua";
      if(!canDelete){
        showToast("Anda tidak dibenarkan membatalkan rekod ini.", "error");
        return;
      }

      if(row.storagePath){
        try{
          await deleteObject(ref(storage, row.storagePath));
        }catch(e){
          console.warn("Fail storage mungkin sudah tiada.", e);
        }
      }

      delete submissions[weekKey][pendingCancelId];
      await saveWeekSubmissions(weekKey);
      renderTable();
      showToast("Penghantaran berjaya dibatalkan.", "warning");
    }catch(err){
      console.error(err);
      showToast("Gagal batalkan penghantaran.", "error");
    }finally{
      closeModal("confirmModal");
      pendingCancelId = null;
    }
  };

  window.previewFile = function(staffId){
    const weekKey = getWeekKey();
    const sub = submissions[weekKey]?.[staffId];
    if(!sub) return;

    document.getElementById("previewFileName").textContent = sub.fileName || "";
    const container = document.getElementById("previewContainer");
    container.innerHTML = "";

    const ext = (sub.fileType || "").toLowerCase();

    if(["jpg","jpeg","png"].includes(ext)){
      const img = document.createElement("img");
      img.src = sub.fileUrl;
      img.alt = sub.fileName || "Preview";
      container.appendChild(img);
    } else if(ext === "pdf"){
      const iframe = document.createElement("iframe");
      iframe.src = sub.fileUrl;
      iframe.title = sub.fileName || "PDF Preview";
      container.appendChild(iframe);
    } else {
      container.innerHTML = `
        <div class="preview-placeholder">
          <i class="fas fa-file-alt" style="font-size:28px;margin-bottom:8px"></i>
          <p>Pratonton tidak tersedia untuk jenis fail ini.<br><strong>${escapeHtml(sub.fileName || "")}</strong></p>
          <p style="margin-top:10px">
            <a href="${sub.fileUrl}" target="_blank" rel="noopener">Buka fail</a>
          </p>
        </div>
      `;
    }

    openModal("previewModal");
  };

  window.saveSemakan = async function(staffId, value){
    try{
      if(currentRole !== "admin" && currentRole !== "pengetua") return;

      const weekKey = getWeekKey();
      if(!submissions[weekKey]?.[staffId]) return;

      submissions[weekKey][staffId].semakan = value;
      await saveWeekSubmissions(weekKey);
    }catch(err){
      console.error(err);
      showToast("Gagal simpan semakan.", "error");
    }
  };

  window.openPengesahan = function(staffId){
    pendingPengesahanId = staffId;
    const staff = STAFF_LIST.find(s => s.id === staffId);
    document.getElementById("pengesahanStaffName").textContent = staff?.nama || "";
    document.getElementById("pengesahanCatatan").value = "";
    document.getElementById("pengesahanError").style.display = "none";
    openModal("pengesahanModal");
  };

  window.submitPengesahan = async function(){
    try{
      if(currentRole !== "pengetua"){
        document.getElementById("pengesahanError").style.display = "block";
        return;
      }

      const weekKey = getWeekKey();
      if(!submissions[weekKey]?.[pendingPengesahanId]) return;

      submissions[weekKey][pendingPengesahanId].pengesahan = {
        tarikh: formatDateShort(new Date()),
        catatan: document.getElementById("pengesahanCatatan").value || ""
      };
      submissions[weekKey][pendingPengesahanId].status = "Disahkan";

      await saveWeekSubmissions(weekKey);
      closeModal("pengesahanModal");
      renderTable();
      showToast("Pengesahan berjaya disimpan!", "success");
    }catch(err){
      console.error(err);
      showToast("Gagal simpan pengesahan.", "error");
    }
  };

  function updatePrincipalSection(){
    const key = getWeekKey();
    const sig = weekSignatures[key] || {};
    const isPrincipal = currentRole === "pengetua";

    document.getElementById("principalAccessNote").style.display = isPrincipal ? "none" : "block";
    document.getElementById("principalForm").style.display = isPrincipal && !sig.signed ? "grid" : "none";

    const stamp = document.getElementById("principalStamp");
    const signedInfo = document.getElementById("principalSignedInfo");

    if(sig.signed){
      stamp.className = "principal-stamp signed";
      stamp.innerHTML = `
        <div class="stamp-sign">&#10003;</div>
        <div class="stamp-name">Hajah Aniza Binti Baharuddin</div>
        <div class="stamp-date">Tarikh Semakan: ${escapeHtml(sig.date || "")}</div>
      `;
      signedInfo.style.display = "block";
      document.getElementById("principalSignedDetails").textContent =
        `Catatan: ${sig.notes || "Tiada catatan"} | Tarikh: ${sig.date || ""}`;
    } else {
      stamp.className = "principal-stamp";
      stamp.innerHTML = `
        <i class="fas fa-pen-to-square" style="font-size:24px;color:var(--slate);opacity:.4"></i>
        <p style="font-size:12.5px;color:var(--slate)">Belum disahkan</p>
      `;
      signedInfo.style.display = "none";
    }

    if(isPrincipal){
      const today = new Date();
      const yyyy = today.getFullYear();
      const mm = String(today.getMonth()+1).padStart(2,"0");
      const dd = String(today.getDate()).padStart(2,"0");
      document.getElementById("principalDate").value = `${yyyy}-${mm}-${dd}`;
    }
  }

  window.signPrincipal = async function(){
    try{
      if(currentRole !== "pengetua"){
        showToast("Hanya Pengetua boleh menandatangani.", "error");
        return;
      }

      const key = getWeekKey();
      const dateVal = document.getElementById("principalDate").value;
      const notesVal = document.getElementById("principalNotes").value;

      weekSignatures[key] = {
        signed: true,
        date: dateVal ? formatDateShort(new Date(dateVal)) : formatDateShort(new Date()),
        notes: notesVal || ""
      };

      await saveWeekSignature(key);
      updatePrincipalSection();
      showToast("Pengesahan pengetua berjaya disimpan!", "success");
    }catch(err){
      console.error(err);
      showToast("Gagal simpan tandatangan pengetua.", "error");
    }
  };

  function updateStats(){
    let disahkan = 0, belum = 0, lewat = 0;

    STAFF_LIST.forEach(s => {
      const st = computeStatus(s.id, currentWeekOffset);
      if(st === "Disahkan") disahkan++;
      else if(st === "Lewat") lewat++;
      else belum++;
    });

    document.getElementById("statTotal").textContent = STAFF_LIST.length;
    document.getElementById("statDisahkan").textContent = disahkan;
    document.getElementById("statBelum").textContent = belum;
    document.getElementById("statLewat").textContent = lewat;
    document.getElementById("leg1").textContent = disahkan;
    document.getElementById("leg2").textContent = belum;
    document.getElementById("leg3").textContent = lewat;

    drawPie(disahkan, belum, lewat);
  }

  function drawPie(d,b,l){
    const canvas = document.getElementById("pieChart");
    const ctx = canvas.getContext("2d");
    const total = d + b + l;
    const cssSize = Math.min(canvas.clientWidth || 180, 180);
    const ratio = window.devicePixelRatio || 1;

    canvas.width = cssSize * ratio;
    canvas.height = cssSize * ratio;
    canvas.style.width = `${cssSize}px`;
    canvas.style.height = `${cssSize}px`;

    ctx.setTransform(ratio,0,0,ratio,0,0);
    ctx.clearRect(0,0,cssSize,cssSize);

    const cx = cssSize / 2;
    const cy = cssSize / 2;
    const r = Math.max(50, cssSize / 2 - 10);

    const data = [
      { val:d, color:"#1a7a4a" },
      { val:b, color:"#d4820a" },
      { val:l, color:"#c0392b" }
    ];

    if(total === 0){
      ctx.beginPath();
      ctx.arc(cx, cy, r, 0, Math.PI * 2);
      ctx.fillStyle = "#ddd";
      ctx.fill();
      return;
    }

    let angle = -Math.PI / 2;

    data.forEach(seg => {
      if(!seg.val) return;
      const slice = (seg.val / total) * Math.PI * 2;

      ctx.beginPath();
      ctx.moveTo(cx, cy);
      ctx.arc(cx, cy, r, angle, angle + slice);
      ctx.closePath();
      ctx.fillStyle = seg.color;
      ctx.fill();
      ctx.strokeStyle = "#fff";
      ctx.lineWidth = 2;
      ctx.stroke();

      angle += slice;
    });

    ctx.beginPath();
    ctx.arc(cx, cy, Math.max(28, r * 0.45), 0, Math.PI * 2);
    ctx.fillStyle = "#fff";
    ctx.fill();

    ctx.fillStyle = "#1e293b";
    ctx.font = 'bold 13px "Plus Jakarta Sans"';
    ctx.textAlign = "center";
    ctx.textBaseline = "middle";
    ctx.fillText(String(total), cx, cy - 6);

    ctx.fillStyle = "#64748b";
    ctx.font = '10px "Plus Jakarta Sans"';
    ctx.fillText("staf", cx, cy + 10);
  }

  function updateNotifications(){
    const key = getWeekKey();
    const items = [];

    STAFF_LIST.forEach(s => {
      const sub = submissions[key]?.[s.id];
      if(!sub){
        items.push({ type:"amber", msg:`${s.nama.split(" ")[0]} belum hantar` });
      } else if(sub.status === "Lewat"){
        items.push({ type:"red", msg:`${s.nama.split(" ")[0]} lewat` });
      }
    });

    const shortList = items.slice(0, 5);
    document.getElementById("notifBadge").textContent = shortList.length;

    const list = document.getElementById("notifList");
    list.innerHTML = "";

    if(shortList.length === 0){
      list.innerHTML = `<div class="notif-item"><div class="notif-dot green"></div><span>Semua rekod terkini terkawal.</span></div>`;
      return;
    }

    shortList.forEach(it => {
      const div = document.createElement("div");
      div.className = "notif-item";
      div.innerHTML = `<div class="notif-dot ${it.type}"></div><span>${escapeHtml(it.msg)}</span>`;
      list.appendChild(div);
    });
  }

  window.toggleNotif = function(){
    document.getElementById("notifPanel").classList.toggle("open");
  };

  document.addEventListener("click", function(e){
    const wrapper = document.querySelector(".notif-wrapper");
    if(wrapper && !wrapper.contains(e.target)){
      document.getElementById("notifPanel").classList.remove("open");
    }
  });

  window.openReport = function(){
    const key = getWeekKey();
    const mon = getWeekStart(currentWeekOffset);
    const fri = getWeekEnd(currentWeekOffset);
    const wn = getWeekNumber(currentWeekOffset);
    const months = ["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];
    const weekStr = `${mon.getDate()} ${months[mon.getMonth()]} – ${fri.getDate()} ${months[fri.getMonth()]} ${fri.getFullYear()}`;

    let d=0,b=0,l=0;
    STAFF_LIST.forEach(s => {
      const st = computeStatus(s.id, currentWeekOffset);
      if(st === "Disahkan") d++;
      else if(st === "Lewat") l++;
      else b++;
    });

    const sig = weekSignatures[key] || {};
    let rows = "";

    STAFF_LIST.forEach((s,i) => {
      const sub = submissions[key]?.[s.id];
      const st = computeStatus(s.id, currentWeekOffset);
      const stColor = st === "Disahkan" ? "#1a7a4a" : st === "Lewat" ? "#c0392b" : "#d4820a";
      const peng = sub?.pengesahan ? `✓ ${sub.pengesahan.tarikh}` : "–";

      rows += `
        <tr>
          <td>${i+1}</td>
          <td>${escapeHtml(s.nama)}</td>
          <td>${escapeHtml(KAT_NAMES[s.kat])}</td>
          <td>${sub ? escapeHtml(sub.fileName) : "–"}</td>
          <td>${sub ? escapeHtml(sub.tarikhHantar) : "–"}</td>
          <td style="font-weight:700;color:${stColor}">${escapeHtml(st)}</td>
          <td>${escapeHtml(peng)}</td>
        </tr>
      `;
    });

    document.getElementById("reportBody").innerHTML = `
      <div style="background:var(--gold-pale);border:1px solid var(--gold);border-radius:var(--radius-sm);padding:14px 16px;margin-bottom:16px">
        <p><strong>Sekolah:</strong> Sekolah Menengah Kebangsaan Mentakab</p>
        <p><strong>Pengetua:</strong> Hajah Aniza Binti Baharuddin</p>
        <p><strong>Minggu:</strong> Minggu ${wn} (${weekStr})</p>
        <p><strong>Tarikh Laporan:</strong> ${formatDateShort(new Date())}</p>
        <p style="margin-top:8px">
          <span style="color:var(--emerald);font-weight:700">✓ Disahkan: ${d}</span>
          &nbsp;|&nbsp;
          <span style="color:var(--amber);font-weight:700">Belum Hantar: ${b}</span>
          &nbsp;|&nbsp;
          <span style="color:var(--crimson);font-weight:700">Lewat: ${l}</span>
        </p>
        <p style="margin-top:6px;font-size:12px">
          <strong>Status Pengesahan Pengetua:</strong>
          ${sig.signed
            ? `<span style="color:var(--emerald);font-weight:700">✓ Disahkan pada ${escapeHtml(sig.date || "")}</span>`
            : '<span style="color:var(--slate)">Belum Disahkan</span>'}
        </p>
      </div>

      <div style="overflow-x:auto">
        <table class="report-table">
          <thead>
            <tr>
              <th>Bil</th><th>Nama Staf</th><th>Kategori</th><th>Nama Fail</th><th>Tarikh Hantar</th><th>Status</th><th>Pengesahan Pengetua</th>
            </tr>
          </thead>
          <tbody>${rows}</tbody>
        </table>
      </div>

      ${sig.notes ? `<p style="margin-top:14px;font-size:12.5px;color:var(--navy)"><strong>Catatan Pengetua:</strong> ${escapeHtml(sig.notes)}</p>` : ""}
    `;

    openModal("reportModal");
  };

  window.setLoginRole = function(role){
    currentLoginTab = role;
    document.getElementById("btnRolePengetua").className = role === "pengetua" ? "btn-sm btn-primary" : "btn-sm btn-secondary";
    document.getElementById("btnRoleAdmin").className = role === "admin" ? "btn-sm btn-primary" : "btn-sm btn-secondary";
  };

  window.openLogin = function(){
    if(currentRole){
      logout();
      return;
    }

    document.getElementById("loginPass").value = "";
    document.getElementById("loginError").style.display = "none";
    setLoginRole("pengetua");
    openModal("loginModal");
  };

  window.doLogin = function(){
    const pass = document.getElementById("loginPass").value;
    const correct = currentLoginTab === "pengetua" ? "1234" : "0000";

    if(pass !== correct){
      document.getElementById("loginError").style.display = "block";
      return;
    }

    currentRole = currentLoginTab;
    closeModal("loginModal");

    const roleLabel = currentRole === "pengetua" ? "Pengetua" : "Admin";
    document.getElementById("adminBtnText").textContent = `Log Keluar (${roleLabel})`;
    document.getElementById("adminBtn").classList.add("logged-in");

    if(currentRole === "admin"){
      document.getElementById("adminBar").classList.add("visible");
    } else {
      document.getElementById("adminBar").classList.remove("visible");
    }

    showToast(`Selamat datang, ${roleLabel}!`, "success");
    renderTable();
  };

  function logout(){
    currentRole = null;
    document.getElementById("adminBtnText").textContent = "Log Masuk";
    document.getElementById("adminBtn").classList.remove("logged-in");
    document.getElementById("adminBar").classList.remove("visible");
    renderTable();
    showToast("Anda telah log keluar.", "warning");
  }
  window.logout = logout;

  async function uploadBrandingFile(file, type){
    const safeName = file.name.replace(/[^\w.\-]+/g, "_");
    const filePath = `branding/${type}/${Date.now()}_${safeName}`;
    const fileRef = ref(storage, filePath);

    await uploadBytes(fileRef, file);
    const url = await getDownloadURL(fileRef);

    return { url, path: filePath };
  }

  window.changeBanner = async function(event){
    try{
      if(currentRole !== "admin"){
        showToast("Hanya admin boleh tukar banner.", "error");
        return;
      }

      if(!firebaseReady || !storage){
        showToast("Firebase belum sedia.", "error");
        return;
      }

      const file = event.target.files?.[0];
      if(!file) return;

      showToast("Sedang memuat naik banner...", "warning");
      const result = await uploadBrandingFile(file, "banner");

      if(settingsData.bannerPath){
        try{
          await deleteObject(ref(storage, settingsData.bannerPath));
        }catch(e){
          console.warn("Banner lama tidak dijumpai.", e);
        }
      }

      settingsData.bannerUrl = result.url;
      settingsData.bannerPath = result.path;

      applyBrandingToUI();
      await saveBranding();
      showToast("Banner berjaya diubah!", "success");
    }catch(err){
      console.error(err);
      showToast("Gagal simpan banner.", "error");
    }finally{
      event.target.value = "";
    }
  };

  window.changeLogo = async function(event){
    try{
      if(currentRole !== "admin"){
        showToast("Hanya admin boleh tukar logo.", "error");
        return;
      }

      if(!firebaseReady || !storage){
        showToast("Firebase belum sedia.", "error");
        return;
      }

      const file = event.target.files?.[0];
      if(!file) return;

      showToast("Sedang memuat naik logo...", "warning");
      const result = await uploadBrandingFile(file, "logo");

      if(settingsData.logoPath){
        try{
          await deleteObject(ref(storage, settingsData.logoPath));
        }catch(e){
          console.warn("Logo lama tidak dijumpai.", e);
        }
      }

      settingsData.logoUrl = result.url;
      settingsData.logoPath = result.path;

      applyBrandingToUI();
      await saveBranding();
      showToast("Logo berjaya diubah!", "success");
    }catch(err){
      console.error(err);
      showToast("Gagal simpan logo.", "error");
    }finally{
      event.target.value = "";
    }
  };

  window.addEventListener("resize", updateStats);

  populateStaffSelect();
  updateWeekDisplay();
  renderTable();
  updateStats();
  updatePrincipalSection();
  initFirebase();
</script>