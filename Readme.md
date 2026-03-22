<!DOCTYPE html>
<html lang="ms">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SMK Mentakab – Sistem Penghantaran Mingguan</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
  <style>
    :root{
      --bg:#05070d;
      --panel:#edf1f5;
      --blue:#0145f2;
      --blue2:#2450e6;
      --text:#0d1633;
      --muted:#64748b;
      --line:#d9e0ea;
      --ok:#10b981;
      --warn:#f59e0b;
      --late:#ec4899;
      --white:#fff;
      --radius:24px;
      --font:"Plus Jakarta Sans",sans-serif;
    }
    *{box-sizing:border-box;margin:0;padding:0}
    body{font-family:var(--font);background:linear-gradient(180deg,#02040a,#071020 45%,#02040a);color:var(--text)}
    .app{max-width:500px;margin:0 auto;min-height:100vh;padding-bottom:100px}
    .topbar{
      position:sticky;top:0;z-index:20;
      display:flex;justify-content:space-between;align-items:center;
      padding:16px 18px;background:rgba(5,7,13,.75);backdrop-filter:blur(10px)
    }
    .brand{display:flex;align-items:center;gap:10px;color:#fff}
    .logo{width:38px;height:38px;border-radius:12px;background:var(--blue);display:flex;align-items:center;justify-content:center;font-weight:800}
    .brand small{display:block;color:#94a3b8;font-size:11px}
    .top-actions{display:flex;gap:8px}
    .icon-btn,.login-btn{
      border:none;cursor:pointer
    }
    .icon-btn{
      width:38px;height:38px;border-radius:50%;background:rgba(255,255,255,.08);color:#fff
    }
    .login-btn{
      height:38px;padding:0 14px;border-radius:999px;background:var(--blue);color:#fff;font-weight:700
    }

    .hero{
      margin:14px 14px 0;
      overflow:hidden;border-radius:30px;background:var(--panel);box-shadow:0 20px 60px rgba(0,0,0,.28)
    }
    .hero-top{
      padding:22px 22px 96px;background:var(--panel);position:relative
    }
    .mini-label{font-size:12px;font-weight:700;color:var(--blue2);letter-spacing:.04em}
    .page-no{position:absolute;right:22px;top:22px;color:var(--blue2);font-weight:800}
    .hero-title{
      text-align:center;margin-top:90px;font-size:40px;line-height:.95;font-weight:800;color:var(--blue);
      text-transform:uppercase;text-shadow:0 3px 10px rgba(1,69,242,.16)
    }
    .hero-pills{display:flex;justify-content:center;gap:12px;margin-top:14px;flex-wrap:wrap}
    .pill{
      border:2px solid rgba(1,69,242,.65);color:var(--blue2);padding:9px 20px;border-radius:999px;font-weight:700;background:transparent
    }

    .combo-wrap{position:relative}
    .combo-dot{
      position:absolute;left:50%;top:-52px;transform:translateX(-50%);
      width:120px;height:120px;border-radius:50%;background:#000;color:#c7d4ff;
      display:flex;align-items:center;justify-content:center;text-align:center;font-size:15px;font-weight:800;line-height:1.05;
      border:4px solid #000;box-shadow:0 10px 30px rgba(0,0,0,.28)
    }
    .hero-bottom{
      background:var(--blue);color:#fff;padding:120px 22px 26px
    }
    .hero-bottom h2{
      text-align:center;font-size:40px;line-height:.95;font-weight:800;text-transform:uppercase
    }
    .hero-bottom .hero-pills .pill{
      border-color:rgba(255,255,255,.68);color:#fff
    }
    .hero-foot{
      margin-top:120px;display:flex;justify-content:space-between;align-items:center;color:rgba(255,255,255,.78);font-weight:600
    }

    .card{
      margin:14px;background:#fff;border-radius:24px;padding:18px;box-shadow:0 8px 30px rgba(0,0,0,.14)
    }
    .card-title{font-size:12px;font-weight:800;letter-spacing:.08em;color:var(--blue);text-transform:uppercase;margin-bottom:12px}

    .week-box{display:flex;justify-content:space-between;align-items:center;gap:10px}
    .nav-btn{
      width:40px;height:40px;border:none;border-radius:50%;background:#eef3ff;color:var(--blue);font-size:15px;cursor:pointer
    }
    .week-center{text-align:center;flex:1}
    .week-center h3{font-size:30px;font-weight:800}
    .week-center p{margin-top:6px;color:var(--muted);font-size:12px;font-weight:700}

    .stats{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
    .stat{
      border-radius:20px;padding:16px 12px;color:#fff;text-align:center
    }
    .stat.ok{background:linear-gradient(135deg,#10b981,#059669)}
    .stat.warn{background:linear-gradient(135deg,#f59e0b,#d97706)}
    .stat.late{background:linear-gradient(135deg,#ec4899,#db2777)}
    .stat b{display:block;font-size:24px}
    .stat span{font-size:11px;font-weight:700;opacity:.95}

    select,input,textarea{
      width:100%;border:1.5px solid var(--line);border-radius:16px;padding:12px 14px;font-family:var(--font);outline:none
    }
    .row{display:flex;gap:10px;flex-wrap:wrap}
    .btn{
      border:none;border-radius:16px;padding:11px 14px;font-family:var(--font);font-weight:700;cursor:pointer
    }
    .btn-blue{background:var(--blue);color:#fff}
    .btn-light{background:#edf4ff;color:var(--blue)}
    .btn-red{background:#ffe7f3;color:#db2777}
    .btn-amber{background:#fff2d9;color:#b45309}

    .filter{display:flex;gap:8px;overflow:auto}
    .chip{
      flex:0 0 auto;padding:8px 14px;border-radius:999px;border:none;background:#eef2f7;color:#475569;font-weight:700;cursor:pointer
    }
    .chip.active{background:var(--blue);color:#fff}

    .staff-list{display:grid;gap:12px}
    .staff{
      border:1px solid #edf0f5;border-radius:22px;padding:16px;background:#fff
    }
    .staff-top{display:flex;justify-content:space-between;align-items:flex-start;gap:10px}
    .avatar{
      width:52px;height:52px;border-radius:16px;background:#e8eeff;color:var(--blue);
      display:flex;align-items:center;justify-content:center;font-weight:800
    }
    .badge{
      padding:7px 10px;border-radius:999px;font-size:11px;font-weight:800;text-transform:uppercase
    }
    .b-ok{background:#dcfce7;color:#047857}
    .b-warn{background:#fef3c7;color:#b45309}
    .b-late{background:#fce7f3;color:#be185d}
    .staff-name{margin-top:10px;font-weight:800;font-size:14px;text-transform:uppercase}
    .staff-role{margin-top:4px;font-size:11px;color:var(--muted);font-weight:700}
    .staff-actions{display:flex;gap:8px;flex-wrap:wrap;margin-top:12px}
    .file-note{margin-top:10px;font-size:12px;color:var(--muted)}
    .hidden{display:none}

    .modal{
      position:fixed;inset:0;background:rgba(0,0,0,.65);display:none;align-items:center;justify-content:center;padding:18px;z-index:50
    }
    .modal.show{display:flex}
    .modal-box{
      width:100%;max-width:460px;background:#fff;border-radius:24px;padding:18px
    }
    .modal-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:14px}
    .modal-head h3{font-size:18px}
    .close{border:none;background:#eef2f7;border-radius:50%;width:34px;height:34px;cursor:pointer}

    .toast-wrap{position:fixed;top:16px;right:16px;z-index:100;display:grid;gap:8px}
    .toast{background:#111827;color:#fff;padding:10px 14px;border-radius:12px;font-size:13px}
  </style>
</head>
<body>
  <div class="toast-wrap" id="toastWrap"></div>

  <div class="app">
    <div class="topbar">
      <div class="brand">
        <div class="logo" id="logoBox">SM</div>
        <div>
          <strong>SMK Mentakab</strong>
          <small>Sistem Penghantaran Mingguan</small>
        </div>
      </div>
      <div class="top-actions">
        <button class="icon-btn" onclick="openReport()"><i class="fa-solid fa-file-lines"></i></button>
        <button class="login-btn" onclick="openLogin()">Masuk</button>
      </div>
    </div>

    <div class="hero">
      <div class="hero-top">
        <div class="mini-label">LEARN DESIGN</div>
        <div class="page-no">PAGE 02</div>
        <div class="hero-title">Canvas Cloud</div>
        <div class="hero-pills">
          <div class="pill">Hex ⟶</div>
          <div class="pill">#EDF1F5</div>
        </div>
      </div>
      <div class="combo-wrap">
        <div class="combo-dot">COMBO<br>02</div>
      </div>
      <div class="hero-bottom">
        <h2>Electric Blue</h2>
        <div class="hero-pills">
          <div class="pill">Hex ⟶</div>
          <div class="pill">#0145F2</div>
        </div>
        <div class="hero-foot">
          <span>@smk.mentakab</span>
          <span>◌ ◌ ◉</span>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-title">Minggu Semasa</div>
      <div class="week-box">
        <button class="nav-btn" onclick="changeWeek(-1)"><i class="fa-solid fa-chevron-left"></i></button>
        <div class="week-center">
          <h3 id="weekLabel">Minggu 1</h3>
          <p id="weekDate">Tarikh minggu</p>
        </div>
        <button class="nav-btn" onclick="changeWeek(1)"><i class="fa-solid fa-chevron-right"></i></button>
      </div>
      <div class="row" style="margin-top:12px">
        <button class="btn btn-light" onclick="goCurrentWeek()">Minggu Ini</button>
      </div>
    </div>

    <div class="card">
      <div class="card-title">Ringkasan</div>
      <div class="stats">
        <div class="stat ok"><b id="countOk">0</b><span>Disahkan</span></div>
        <div class="stat warn"><b id="countWarn">0</b><span>Belum Hantar</span></div>
        <div class="stat late"><b id="countLate">0</b><span>Lewat</span></div>
      </div>
    </div>

    <div class="card">
      <div class="card-title">Log Masuk Staf</div>
      <select id="staffSelect"></select>
    </div>

    <div class="card">
      <div class="card-title">Carian & Filter</div>
      <input id="searchInput" placeholder="Cari nama staf..." oninput="render()" />
      <div class="filter" style="margin-top:10px">
        <button class="chip active" onclick="setFilter(this,'')">Semua</button>
        <button class="chip" onclick="setFilter(this,'Disahkan')">Disahkan</button>
        <button class="chip" onclick="setFilter(this,'Belum Hantar')">Belum Hantar</button>
        <button class="chip" onclick="setFilter(this,'Lewat')">Lewat</button>
      </div>
    </div>

    <div class="card">
      <div class="card-title">Senarai Staf</div>
      <div class="staff-list" id="staffList"></div>
    </div>
  </div>

  <div class="modal" id="loginModal">
    <div class="modal-box">
      <div class="modal-head">
        <h3>Log Masuk</h3>
        <button class="close" onclick="closeModal('loginModal')"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <div class="row" style="margin-bottom:10px">
        <button class="btn btn-light" onclick="setRole('admin')">Admin</button>
        <button class="btn btn-light" onclick="setRole('pengetua')">Pengetua</button>
      </div>
      <input type="password" id="loginPass" placeholder="Kata laluan" />
      <div class="row" style="margin-top:12px">
        <button class="btn btn-blue" onclick="doLogin()">Masuk</button>
      </div>
    </div>
  </div>

  <div class="modal" id="reportModal">
    <div class="modal-box">
      <div class="modal-head">
        <h3>Laporan Mingguan</h3>
        <button class="close" onclick="closeModal('reportModal')"><i class="fa-solid fa-xmark"></i></button>
      </div>
      <div id="reportBody"></div>
    </div>
  </div>

  <script type="module">
    import { firebaseConfig } from "./firebase-config.js";
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-app.js";
    import { getAuth, signInAnonymously } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-auth.js";
    import { getFirestore, doc, getDoc, setDoc } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-firestore.js";
    import { getStorage, ref, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-storage.js";

    const STAFF = [
      { id:1, nama:"'Afifah Binti Abdul Aziz", jawatan:"Ketua Pembantu Makmal" },
      { id:2, nama:"Ida Zarina Binti Idris", jawatan:"Pembantu Makmal" },
      { id:3, nama:"Azian Binti Mohamad", jawatan:"Pembantu Makmal" },
      { id:4, nama:"Fatimah Binti Latiff", jawatan:"Pembantu Makmal" },
      { id:5, nama:"Zainun Binti Mohamed Ramthan", jawatan:"Pembantu Makmal" },
      { id:6, nama:"Nor'aini Binti Md Yusoff", jawatan:"Pembantu Makmal" },
      { id:7, nama:"Fakarullah Amer Bin Zainal Abidin", jawatan:"Pembantu Makmal" },
      { id:8, nama:"Abdul Azam Bin Mohamed", jawatan:"Pembantu Makmal" },
      { id:9, nama:"Nor Faiza Binti Mustaffa Kamal", jawatan:"Pembantu Pengurusan Murid" },
      { id:10, nama:"Wan Azlena Binti Wan Deraman", jawatan:"Pembantu Pengurusan Murid" },
      { id:11, nama:"Mohd Faizal Bin Zainal", jawatan:"Pembantu Pengurusan Murid" },
      { id:12, nama:"Juhaida Binti Abd Rasid", jawatan:"Pembantu Tadbir" },
      { id:13, nama:"Junainah Binti Hassan", jawatan:"Pembantu Tadbir" },
      { id:14, nama:"Rafidah Binti Sidek", jawatan:"Pembantu Tadbir" },
      { id:15, nama:"Muhammad Fahmi Bin Hamidin", jawatan:"Pembantu Khidmat Am" },
      { id:16, nama:"Nursyaza Aina Binti Mohd Adaha", jawatan:"Pembantu Khidmat Am" }
    ];

    const PASSWORDS = { admin:"0000", pengetua:"1234" };

    let app, auth, db, storage;
    let currentRole = null;
    let loginRole = "admin";
    let selectedStaffId = null;
    let weekOffset = 0;
    let filterStatus = "";
    let weekData = {};

    function toast(msg){
      const wrap = document.getElementById("toastWrap");
      const el = document.createElement("div");
      el.className = "toast";
      el.textContent = msg;
      wrap.appendChild(el);
      setTimeout(()=>el.remove(),2500);
    }

    function openModal(id){ document.getElementById(id).classList.add("show"); }
    function closeModal(id){ document.getElementById(id).classList.remove("show"); }
    window.closeModal = closeModal;

    function setRole(role){ loginRole = role; toast("Role: " + role); }
    window.setRole = setRole;

    window.openLogin = ()=>openModal("loginModal");

    window.doLogin = function(){
      const pass = document.getElementById("loginPass").value;
      if(pass !== PASSWORDS[loginRole]) return toast("Kata laluan salah");
      currentRole = loginRole;
      closeModal("loginModal");
      toast("Log masuk berjaya");
      render();
    };

    function getWeekStart(offset=0){
      const now = new Date();
      const day = now.getDay();
      const diff = day === 0 ? -6 : 1 - day;
      const mon = new Date(now);
      mon.setDate(now.getDate() + diff + offset * 7);
      mon.setHours(0,0,0,0);
      return mon;
    }

    function getWeekEnd(offset=0){
      const mon = getWeekStart(offset);
      const fri = new Date(mon);
      fri.setDate(mon.getDate() + 4);
      return fri;
    }

    function getWeekKey(){
      const d = getWeekStart(weekOffset);
      return `week_${d.getFullYear()}_${d.getMonth()+1}_${d.getDate()}`;
    }

    function fmt(d){
      return d.toLocaleDateString("ms-MY",{day:"2-digit",month:"short",year:"numeric"});
    }

    function isLateCurrentWeek(){
      return new Date() > getWeekEnd(weekOffset);
    }

    function statusOf(id){
      const row = weekData[id];
      if(!row) return isLateCurrentWeek() ? "Lewat" : "Belum Hantar";
      return row.status || "Disahkan";
    }

    async function initFirebase(){
      app = initializeApp(firebaseConfig);
      auth = getAuth(app);
      db = getFirestore(app);
      storage = getStorage(app);
      await signInAnonymously(auth);
      await loadWeek();
      render();
    }

    async function loadWeek(){
      const snap = await getDoc(doc(db,"weeklySubmissions",getWeekKey()));
      weekData = snap.exists() ? (snap.data().records || {}) : {};
    }

    async function saveWeek(){
      await setDoc(doc(db,"weeklySubmissions",getWeekKey()),{ records: weekData },{ merge:true });
    }

    function initials(name){
      const p = name.replace(/^'/,"").split(" ");
      return ((p[0]?.[0] || "") + (p[1]?.[0] || "")).toUpperCase();
    }

    function fillStaffSelect(){
      const s = document.getElementById("staffSelect");
      s.innerHTML = `<option value="">— Pilih nama anda —</option>`;
      STAFF.forEach(x=>{
        s.innerHTML += `<option value="${x.id}">${x.nama}</option>`;
      });
      s.onchange = e => {
        selectedStaffId = Number(e.target.value) || null;
        localStorage.setItem("smk_staff_id", selectedStaffId || "");
        render();
      };
      const saved = Number(localStorage.getItem("smk_staff_id") || 0);
      if(saved){
        selectedStaffId = saved;
        s.value = saved;
      }
    }

    function updateWeekUI(){
      const start = getWeekStart(weekOffset);
      const end = getWeekEnd(weekOffset);
      document.getElementById("weekLabel").textContent = "Minggu " + getWeekNumber(start);
      document.getElementById("weekDate").textContent = `${fmt(start)} – ${fmt(end)}`;
    }

    function getWeekNumber(date){
      const first = new Date(date.getFullYear(),0,1);
      return Math.ceil((((date - first) / 86400000) + first.getDay() + 1) / 7);
    }

    function countStats(){
      let ok=0,warn=0,late=0;
      STAFF.forEach(s=>{
        const st = statusOf(s.id);
        if(st==="Disahkan") ok++;
        else if(st==="Lewat") late++;
        else warn++;
      });
      document.getElementById("countOk").textContent = ok;
      document.getElementById("countWarn").textContent = warn;
      document.getElementById("countLate").textContent = late;
    }

    function badgeClass(status){
      if(status==="Disahkan") return "b-ok";
      if(status==="Lewat") return "b-late";
      return "b-warn";
    }

    function render(){
      updateWeekUI();
      countStats();

      const q = document.getElementById("searchInput").value.toLowerCase();
      const list = document.getElementById("staffList");

      const items = STAFF.filter(s=>{
        if(q && !s.nama.toLowerCase().includes(q)) return false;
        const st = statusOf(s.id);
        if(filterStatus && st !== filterStatus) return false;
        return true;
      });

      list.innerHTML = "";
      items.forEach(s=>{
        const st = statusOf(s.id);
        const row = weekData[s.id];
        const mine = selectedStaffId === s.id;

        const div = document.createElement("div");
        div.className = "staff";
        div.innerHTML = `
          <div class="staff-top">
            <div class="avatar">${initials(s.nama)}</div>
            <div class="badge ${badgeClass(st)}">${st}</div>
          </div>
          <div class="staff-name">${s.nama}</div>
          <div class="staff-role">${s.jawatan}</div>
          ${row ? `<div class="file-note">Fail: ${row.fileName} • ${row.tarikh}</div>` : `<div class="file-note">Belum ada penghantaran</div>`}
          <div class="staff-actions">
            ${mine ? `<input type="file" id="f_${s.id}" class="hidden" accept=".pdf,.jpg,.jpeg,.png,.doc,.docx" onchange="uploadFile(event,${s.id})">
            <button class="btn btn-blue" onclick="document.getElementById('f_${s.id}').click()">Muat Naik</button>` : ``}
            ${row ? `<button class="btn btn-light" onclick="window.open('${row.fileUrl}','_blank')">Lihat</button>` : ``}
            ${(currentRole==="pengetua" && row) ? `<button class="btn btn-amber" onclick="sahkan(${s.id})">Sahkan</button>` : ``}
          </div>
        `;
        list.appendChild(div);
      });
    }

    window.setFilter = function(btn,val){
      filterStatus = val;
      document.querySelectorAll(".chip").forEach(x=>x.classList.remove("active"));
      btn.classList.add("active");
      render();
    };

    window.changeWeek = async function(step){
      weekOffset += step;
      await loadWeek();
      render();
    };

    window.goCurrentWeek = async function(){
      weekOffset = 0;
      await loadWeek();
      render();
    };

    window.uploadFile = async function(event, staffId){
      const file = event.target.files?.[0];
      if(!file) return;
      if(selectedStaffId !== staffId) return toast("Pilih nama staf anda dahulu");

      try{
        const path = `submissions/${getWeekKey()}/${staffId}/${Date.now()}_${file.name.replace(/[^\w.-]+/g,"_")}`;
        const r = ref(storage, path);
        await uploadBytes(r, file);
        const url = await getDownloadURL(r);

        weekData[staffId] = {
          fileName: file.name,
          fileUrl: url,
          tarikh: new Date().toLocaleDateString("ms-MY"),
          status: isLateCurrentWeek() ? "Lewat" : "Disahkan"
        };

        await saveWeek();
        toast("Upload berjaya");
        render();
      }catch(e){
        console.error(e);
        toast("Upload gagal");
      }finally{
        event.target.value = "";
      }
    };

    window.sahkan = async function(staffId){
      if(!weekData[staffId]) return;
      weekData[staffId].status = "Disahkan";
      weekData[staffId].pengesahan = new Date().toLocaleDateString("ms-MY");
      await saveWeek();
      toast("Pengesahan berjaya");
      render();
    };

    window.openReport = function(){
      let html = `<div style="display:grid;gap:8px">`;
      STAFF.forEach((s,i)=>{
        const r = weekData[s.id];
        const st = statusOf(s.id);
        html += `<div style="padding:10px;border:1px solid #e5e7eb;border-radius:14px;font-size:13px">
          <b>${i+1}. ${s.nama}</b><br>
          ${s.jawatan}<br>
          Status: <b>${st}</b><br>
          Fail: ${r?.fileName || "-"}
        </div>`;
      });
      html += `</div>`;
      document.getElementById("reportBody").innerHTML = html;
      openModal("reportModal");
    };

    fillStaffSelect();
    initFirebase();
  </script>
</body>
</html>
