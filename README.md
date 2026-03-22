<!DOCTYPE html>
<html lang="ms">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SMK Mentakab PRO MAX</title>

<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

<style>
body{
  font-family:'Plus Jakarta Sans',sans-serif;
  background:#0f172a;
  color:white;
  margin:0;
}
.center{text-align:center;margin-top:80px}
.card{background:white;color:black;padding:15px;margin:15px;border-radius:12px}
.logo{width:80px}
.banner{width:100%;height:180px;object-fit:cover;border-radius:10px}
button{padding:10px 15px;border:none;border-radius:8px;background:#2563eb;color:white;cursor:pointer}
.drop{
  border:2px dashed #aaa;padding:30px;text-align:center;border-radius:10px;
}
.hidden{display:none}
</style>
</head>

<body>

<!-- LOGIN -->
<div id="loginScreen" class="center">
  <img id="logoPreview" src="assets/logo.png" class="logo">
  <h2>Sistem PRO MAX</h2>

  <select id="staffSelect"></select>
  <button onclick="login()">Masuk</button>

  <div class="card">
    <p>🔧 Tukar Logo</p>
    <input type="file" onchange="changeLogo(event)">
  </div>
</div>

<!-- MAIN -->
<div id="app" class="hidden">

  <div class="card">
    <img id="bannerPreview" src="assets/banner.jpg" class="banner">
    <input type="file" onchange="changeBanner(event)">
    <h2 id="userName"></h2>
  </div>

  <!-- NOTIFICATION -->
  <div class="card">
    🔔 <span id="notif">Tiada notifikasi</span>
  </div>

  <!-- DRAG DROP -->
  <div class="card drop" id="dropZone">
    Drag & Drop Fail atau Klik
    <input type="file" id="fileInput" hidden>
  </div>

  <!-- PREVIEW -->
  <div class="card" id="preview"></div>

  <!-- STATUS -->
  <div class="card">
    Status: <span id="status">-</span>
  </div>

  <!-- CHART -->
  <div class="card">
    <canvas id="chart"></canvas>
  </div>

</div>

<script type="module">

import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
import { getFirestore, collection, doc, setDoc, onSnapshot, serverTimestamp }
from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
import { getStorage, ref, uploadBytes, getDownloadURL }
from "https://www.gstatic.com/firebasejs/11.6.1/firebase-storage.js";

const firebaseConfig = PASTE_FIREBASE_CONFIG;

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);
const storage = getStorage(app);

let currentUser = null;

// STAFF LIST
const staff = [
"Afifah","Ida Zarina","Azian","Fatimah",
"Zainun","Noraini","Fakarullah","Azam"
];

const select = document.getElementById("staffSelect");
staff.forEach(s=>{
  const o=document.createElement("option");
  o.value=s;o.textContent=s;
  select.appendChild(o);
});

// LOGIN
window.login=()=>{
  currentUser = select.value;
  document.getElementById("loginScreen").style.display="none";
  document.getElementById("app").classList.remove("hidden");
  document.getElementById("userName").innerText=currentUser;

  initChart();
};

// LOGO & BANNER
window.changeLogo=(e)=>{
  const file=e.target.files[0];
  document.getElementById("logoPreview").src=URL.createObjectURL(file);
}
window.changeBanner=(e)=>{
  const file=e.target.files[0];
  document.getElementById("bannerPreview").src=URL.createObjectURL(file);
}

// DRAG DROP
const drop = document.getElementById("dropZone");
const input = document.getElementById("fileInput");

drop.onclick=()=>input.click();

drop.ondragover=(e)=>{e.preventDefault();}
drop.ondrop=(e)=>{
  e.preventDefault();
  handleFile(e.dataTransfer.files[0]);
};

input.onchange=(e)=>handleFile(e.target.files[0]);

async function handleFile(file){
  const path = `uploads/${currentUser}/${Date.now()}_${file.name}`;
  const storageRef = ref(storage, path);

  await uploadBytes(storageRef, file);
  const url = await getDownloadURL(storageRef);

  await setDoc(doc(db,"submissions",currentUser),{
    user:currentUser,
    file:url,
    name:file.name,
    time:serverTimestamp(),
    status:"Dihantar"
  });

  showPreview(url,file);
  checkLate();
}

// PREVIEW
function showPreview(url,file){
  const p=document.getElementById("preview");

  if(file.type.startsWith("image")){
    p.innerHTML=`<img src="${url}" width="100%">`;
  } else if(file.type==="application/pdf"){
    p.innerHTML=`<iframe src="${url}" width="100%" height="400"></iframe>`;
  } else {
    p.innerHTML=`<a href="${url}" target="_blank">Buka Fail</a>`;
  }
}

// AUTO STATUS + NOTIFICATION
function checkLate(){
  const d=new Date().getDay();

  if(d===5){
    document.getElementById("status").innerText="Lewat";
    document.getElementById("notif").innerText="⚠️ Hantar sebelum Jumaat!";
  } else {
    document.getElementById("status").innerText="Dihantar";
  }
}

// CHART LIVE
function initChart(){
  const ctx=document.getElementById("chart");

  onSnapshot(collection(db,"submissions"),snap=>{
    let done=0;

    snap.forEach(()=>done++);

    new Chart(ctx,{
      type:'pie',
      data:{
        labels:['Hantar'],
        datasets:[{data:[done]}]
      }
    });
  });
}

</script>

</body>
</html>
