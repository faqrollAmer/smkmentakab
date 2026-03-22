<!DOCTYPE html>

<html lang="ms">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>Sistem Penghantaran Mingguan – SMK Mentakab</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet"/>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css"/>
<style>
:root {
  --bg:        #111218;
  --bg2:       #18191f;
  --card:      #f3f4f8;
  --card2:     #ecedf3;
  --white:     #ffffff;
  --navy:      #12193d;
  --navy2:     #1e2a5e;
  --slate:     #7b8096;
  --border:    #e4e5ec;
  --purple:    #6c5ce7;
  --purple-pale:#ede9ff;
  --green:     #00b894;
  --green-pale:#e0faf4;
  --amber:     #f0a500;
  --amber-pale:#fff5dc;
  --red:       #e84393;
  --red-pale:  #fde8f3;
  --blue:      #2563eb;
  --font:"Plus Jakarta Sans",sans-serif;
  --r:20px;
  --r-sm:14px;
  --r-xs:10px;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{
  font-family:var(--font);
  background:var(--bg);
  color:var(--navy);
  min-height:100vh;
  font-size:14px;
}

/* ── Toast ── */
#toastContainer{position:fixed;top:16px;right:16px;z-index:10000;display:flex;flex-direction:column;gap:8px;pointer-events:none}
.toast{display:flex;align-items:center;gap:10px;padding:11px 16px;border-radius:12px;background:#1e293b;color:#fff;font-size:13px;font-weight:500;box-shadow:0 8px 32px rgba(0,0,0,.3);animation:toastIn .22s ease;max-width:320px}
.toast.success{background:#065f46}
.toast.error{background:#991b1b}
.toast.warning{background:#92400e}
@keyframes toastIn{from{opacity:0;transform:translateX(16px)}to{opacity:1;transform:none}}

/* ── Autosave ── */
#autosaveIndicator{position:fixed;bottom:20px;right:20px;z-index:9999;background:#1e293b;color:#fff;padding:7px 14px;border-radius:20px;font-size:11.5px;font-weight:600;display:flex;align-items:center;gap:6px;opacity:0;transform:translateY(6px);transition:opacity .3s,transform .3s;pointer-events:none}
#autosaveIndicator.visible{opacity:1;transform:none}
#autosaveIndicator i{color:var(–green)}

/* ── App shell ── */
.app-wrap{max-width:480px;margin:0 auto;min-height:100vh;display:flex;flex-direction:column}

/* ── Top bar ── */
.topbar{
background:var(–bg2);
padding:16px 20px 14px;
display:flex;align-items:center;justify-content:space-between;
border-bottom:1px solid rgba(255,255,255,.06);
position:sticky;top:0;z-index:100;
}
.topbar-left{display:flex;align-items:center;gap:10px}
.topbar-logo{width:36px;height:36px;border-radius:10px;overflow:hidden;background:rgba(255,255,255,.1);display:flex;align-items:center;justify-content:center;font-size:16px;color:#fff;font-weight:800;flex-shrink:0}
#logoImg{width:100%;height:100%;object-fit:cover;display:none}
#logoText{color:#fff;font-size:15px;font-weight:800}
.topbar-title{color:#fff;font-size:13px;font-weight:700;line-height:1.3}
.topbar-title span{display:block;font-size:10.5px;color:rgba(255,255,255,.45);font-weight:400;margin-top:1px}
.topbar-right{display:flex;align-items:center;gap:8px}
.topbar-icon-btn{
width:34px;height:34px;border-radius:50%;
background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.12);
color:rgba(255,255,255,.7);cursor:pointer;
display:flex;align-items:center;justify-content:center;
font-size:14px;position:relative;transition:background .2s;
}
.topbar-icon-btn:hover{background:rgba(255,255,255,.16)}
#notifBadge{
position:absolute;top:-3px;right:-3px;
background:#e84393;color:#fff;
font-size:8.5px;font-weight:700;
min-width:15px;height:15px;border-radius:8px;
display:flex;align-items:center;justify-content:center;
padding:0 3px;border:2px solid var(–bg2);
}
.login-btn{
padding:6px 14px;border-radius:20px;
background:var(–purple);color:#fff;
font-size:11.5px;font-weight:700;
border:none;cursor:pointer;transition:opacity .2s;
display:flex;align-items:center;gap:5px;
}
.login-btn:hover{opacity:.85}
.login-btn.logged-in{background:var(–green)}

/* ── Scroll area ── */
.scroll-area{flex:1;overflow-y:auto;padding:20px 16px 100px}
.scroll-area::-webkit-scrollbar{width:0}

/* ── Week card ── */
.week-card{
background:var(–card);
border-radius:var(–r);
padding:22px 20px;
margin-bottom:16px;
text-align:center;
}
.week-nav-row{display:flex;align-items:center;justify-content:center;gap:16px;margin-bottom:6px}
.wk-arrow{
width:36px;height:36px;border-radius:50%;
background:rgba(18,25,61,.06);border:none;
color:var(–slate);font-size:14px;
display:flex;align-items:center;justify-content:center;
cursor:pointer;transition:background .15s,color .15s;
flex-shrink:0;
}
.wk-arrow:hover{background:var(–navy);color:#fff}
#weekLabel{font-size:30px;font-weight:800;color:var(–navy);line-height:1}
.week-date-row{
display:inline-flex;align-items:center;gap:6px;
margin-top:8px;
color:var(–blue);font-size:12px;font-weight:700;
letter-spacing:.06em;text-transform:uppercase;
}
.week-date-row i{font-size:12px}
.week-btn-row{display:flex;justify-content:center;margin-top:14px;gap:8px}
.chip-btn{
padding:6px 16px;border-radius:20px;
background:rgba(18,25,61,.07);border:none;
font-family:var(–font);font-size:11.5px;font-weight:600;color:var(–navy2);
cursor:pointer;transition:background .15s;display:flex;align-items:center;gap:5px;
}
.chip-btn:hover{background:rgba(18,25,61,.13)}
.chip-btn.gold{background:var(–amber);color:#fff}
.chip-btn.gold:hover{opacity:.85}

/* ── Donut card ── */
.donut-card{
background:var(–card);
border-radius:var(–r);
padding:18px 20px;
margin-bottom:16px;
display:flex;align-items:center;gap:20px;
}
.donut-wrap{position:relative;flex-shrink:0}
#donutCanvas{display:block}
.donut-center{
position:absolute;inset:0;
display:flex;flex-direction:column;align-items:center;justify-content:center;
pointer-events:none;
}
.donut-pct{font-size:15px;font-weight:800;color:var(–navy);line-height:1}
.donut-lbl{font-size:9px;color:var(–slate);font-weight:600;margin-top:1px;letter-spacing:.04em}
.donut-legend{flex:1}
.dl-item{
display:flex;align-items:center;justify-content:space-between;
padding:6px 0;border-bottom:1px solid var(–border);
}
.dl-item:last-child{border-bottom:none}
.dl-left{display:flex;align-items:center;gap:9px}
.dl-dot{width:11px;height:11px;border-radius:50%;flex-shrink:0}
.dl-label{font-size:11px;font-weight:700;color:var(–navy);letter-spacing:.04em;text-transform:uppercase}
.dl-val{font-size:15px;font-weight:800;color:var(–navy)}

/* ── Staff selector card ── */
.selector-card{
background:var(–card);
border-radius:var(–r);
padding:16px 18px;
margin-bottom:16px;
}
.selector-card label{
display:block;font-size:11px;font-weight:700;
color:var(–amber);text-transform:uppercase;letter-spacing:.06em;margin-bottom:8px;
}
.selector-card select{
width:100%;padding:10px 14px;
border:1.5px solid var(–border);border-radius:var(–r-sm);
font-family:var(–font);font-size:13px;font-weight:600;color:var(–navy);
background:var(–white);outline:none;cursor:pointer;appearance:none;
background-image:url(“data:image/svg+xml,%3Csvg xmlns=‘http://www.w3.org/2000/svg’ width=‘12’ height=‘12’ viewBox=‘0 0 12 12’%3E%3Cpath fill=’%237b8096’ d=‘M6 8L1 3h10z’/%3E%3C/svg%3E”);
background-repeat:no-repeat;background-position:right 12px center;
padding-right:36px;
}
.selector-card select:focus{border-color:var(–amber)}
.active-staff-badge{
margin-top:10px;
display:none;align-items:center;gap:8px;
padding:8px 14px;border-radius:var(–r-sm);
background:var(–amber-pale);border:1.5px solid var(–amber);
}
.active-staff-badge.show{display:flex}
.active-staff-badge i{color:var(–amber);font-size:13px}
.active-staff-badge span{font-size:12.5px;font-weight:700;color:var(–navy)}

/* ── Filter strip ── */
.filter-strip{
display:flex;gap:8px;margin-bottom:14px;overflow-x:auto;padding-bottom:4px;
}
.filter-strip::-webkit-scrollbar{height:0}
.f-chip{
flex-shrink:0;padding:7px 14px;border-radius:20px;
background:var(–card);border:1.5px solid transparent;
font-family:var(–font);font-size:11.5px;font-weight:600;color:var(–slate);
cursor:pointer;transition:all .15s;white-space:nowrap;
}
.f-chip.active{background:var(–navy);color:#fff;border-color:var(–navy)}
.f-chip.green.active{background:var(–green);border-color:var(–green);color:#fff}
.f-chip.amber.active{background:var(–amber);border-color:var(–amber);color:#fff}
.f-chip.red.active{background:var(–red);border-color:var(–red);color:#fff}

/* ── Search ── */
.search-wrap{position:relative;margin-bottom:14px}
.search-wrap i{position:absolute;left:13px;top:50%;transform:translateY(-50%);color:var(–slate);font-size:13px;pointer-events:none}
.search-wrap input{
width:100%;padding:11px 14px 11px 38px;
border:none;border-radius:var(–r-sm);
background:var(–card);
font-family:var(–font);font-size:13px;color:var(–navy);outline:none;
}
.search-wrap input::placeholder{color:var(–slate)}

/* ── Record count ── */
.rec-count{font-size:11px;color:var(–slate);font-weight:500;margin-bottom:12px;padding:0 2px}

/* ── Staff cards ── */
.staff-card{
background:var(–white);
border-radius:var(–r);
padding:16px 18px;
margin-bottom:12px;
box-shadow:0 2px 8px rgba(18,25,61,.07);
transition:box-shadow .2s;
cursor:pointer;
}
.staff-card:hover{box-shadow:0 4px 20px rgba(18,25,61,.12)}
.staff-card-top{display:flex;align-items:flex-start;justify-content:space-between;margin-bottom:12px}
.staff-avatar{
width:52px;height:52px;border-radius:var(–r-sm);
background:var(–purple-pale);
display:flex;align-items:center;justify-content:center;
font-size:15px;font-weight:800;color:var(–purple);
flex-shrink:0;letter-spacing:.5px;
}
.staff-avatar.mine{
background:linear-gradient(135deg,var(–purple-pale),#d9f0ff);
box-shadow:0 0 0 3px var(–purple);
}
.status-chip{
padding:5px 11px;border-radius:20px;
font-size:10.5px;font-weight:700;letter-spacing:.04em;text-transform:uppercase;
}
.sc-belum{background:var(–card2);color:var(–slate)}
.sc-disahkan{background:var(–green-pale);color:#00695c}
.sc-lewat{background:var(–red-pale);color:#c0007a}

.staff-name{font-size:14px;font-weight:800;color:var(–navy);margin-bottom:3px;letter-spacing:.01em;text-transform:uppercase}
.staff-kat{font-size:10.5px;font-weight:600;color:var(–slate);text-transform:uppercase;letter-spacing:.06em}

/* Staff card bottom (upload / file info) */
.staff-card-bottom{margin-top:12px;padding-top:12px;border-top:1px solid var(–border)}
.upload-row{display:flex;align-items:center;gap:10px;flex-wrap:wrap}
.upload-btn-label{
display:inline-flex;align-items:center;gap:6px;
padding:8px 16px;border-radius:var(–r-sm);
background:var(–purple);color:#fff;
font-size:12px;font-weight:700;cursor:pointer;
transition:opacity .15s;border:none;
}
.upload-btn-label:hover{opacity:.85}
.upload-btn-label input{display:none}
.file-info{
display:flex;align-items:center;gap:8px;flex:1;min-width:0;
}
.file-ext-badge{
padding:3px 8px;border-radius:6px;
font-size:10px;font-weight:800;letter-spacing:.05em;flex-shrink:0;
}
.fe-pdf{background:#fee2e2;color:#991b1b}
.fe-doc{background:#dbeafe;color:#1e40af}
.fe-img{background:#dcfce7;color:#14532d}
.file-name{font-size:11.5px;color:var(–slate);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.file-date{font-size:10.5px;color:var(–slate);white-space:nowrap;margin-left:auto}

.card-actions{display:flex;gap:7px;margin-top:10px;flex-wrap:wrap}
.act-btn{
padding:7px 13px;border-radius:var(–r-xs);
font-family:var(–font);font-size:11.5px;font-weight:700;
border:none;cursor:pointer;display:flex;align-items:center;gap:5px;
transition:opacity .15s;
}
.act-btn:hover{opacity:.82}
.act-view{background:var(–card);color:var(–navy)}
.act-del{background:var(–red-pale);color:var(–red)}
.act-stamp{background:var(–amber-pale);color:var(–amber)}

.semakan-area{
margin-top:10px;
width:100%;padding:8px 11px;
border:1px solid var(–border);border-radius:var(–r-xs);
font-family:var(–font);font-size:12px;color:var(–navy);
resize:vertical;outline:none;background:var(–card);
min-height:52px;
}
.semakan-area:focus{border-color:var(–purple)}

.pengesahan-row{
margin-top:8px;display:flex;align-items:center;gap:7px;
padding:7px 11px;border-radius:var(–r-xs);
background:var(–green-pale);
}
.pengesahan-row i{color:var(–green);font-size:12px}
.pengesahan-row span{font-size:11.5px;font-weight:600;color:#00695c}

/* ── Notif panel ── */
#notifPanel{
position:fixed;top:62px;right:16px;
width:270px;background:var(–white);
border-radius:var(–r-sm);
box-shadow:0 8px 40px rgba(0,0,0,.2);
overflow:hidden;z-index:500;
opacity:0;transform:translateY(-8px) scale(.96);
pointer-events:none;transition:opacity .2s,transform .2s;
}
#notifPanel.open{opacity:1;transform:none;pointer-events:all}
.notif-hdr{padding:11px 14px;background:var(–navy);color:#fff;font-size:11.5px;font-weight:700;text-transform:uppercase;letter-spacing:.05em}
.notif-item{display:flex;align-items:center;gap:9px;padding:10px 14px;font-size:12px;color:var(–navy);border-bottom:1px solid var(–border)}
.notif-item:last-child{border-bottom:none}
.nd{width:8px;height:8px;border-radius:50%;flex-shrink:0}
.nd.a{background:var(–amber)}
.nd.r{background:var(–red)}
.nd.g{background:var(–green)}

/* ── Admin bar ── */
#adminBar{
background:var(–navy2);
padding:10px 16px;
display:none;
gap:10px;flex-wrap:wrap;align-items:center;
border-bottom:1px solid rgba(255,255,255,.08);
}
#adminBar.visible{display:flex}
#adminBar>span{font-size:10.5px;color:rgba(255,255,255,.4);font-weight:700;text-transform:uppercase;letter-spacing:.06em}
.adm-label{
display:inline-flex;align-items:center;gap:5px;
padding:5px 12px;border-radius:20px;
background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.14);
color:rgba(255,255,255,.7);font-size:11.5px;font-weight:600;cursor:pointer;transition:background .15s;
}
.adm-label:hover{background:rgba(255,255,255,.16);color:#fff}
.adm-label input{display:none}

/* ── Banner img ── */
#bannerImg{width:100%;max-height:100px;object-fit:cover;display:none}

/* ── Principal section ── */
.principal-card{
background:var(–card);border-radius:var(–r);
padding:18px;margin-bottom:12px;
}
.pc-title{font-size:11px;font-weight:700;color:var(–slate);text-transform:uppercase;letter-spacing:.07em;margin-bottom:12px;display:flex;align-items:center;gap:6px}
.principal-stamp{
border:2px dashed var(–border);border-radius:var(–r-sm);
padding:18px;text-align:center;display:flex;flex-direction:column;align-items:center;gap:5px;
transition:border-color .2s;margin-bottom:10px;
}
.principal-stamp.signed{border:2px solid var(–green);background:var(–green-pale)}
.stamp-check{font-size:28px;color:var(–green);font-weight:700}
.stamp-name{font-size:13px;font-weight:700;color:#00695c}
.stamp-date{font-size:10.5px;color:var(–slate)}
.principal-form{display:grid;gap:10px}
.pc-note{font-size:11.5px;color:var(–slate);padding:10px 12px;background:var(–card2);border-radius:var(–r-xs);border-left:3px solid var(–border)}
.pf-label{font-size:11px;font-weight:700;color:var(–slate);text-transform:uppercase;letter-spacing:.05em;margin-bottom:4px}
.pf-input{width:100%;padding:9px 12px;border:1.5px solid var(–border);border-radius:var(–r-xs);font-family:var(–font);font-size:13px;color:var(–navy);outline:none;transition:border-color .15s;background:var(–white)}
.pf-input:focus{border-color:var(–purple)}
.pf-textarea{resize:vertical;min-height:50px}
.pf-btn{width:100%;padding:11px;border-radius:var(–r-xs);background:var(–amber);color:#fff;border:none;font-family:var(–font);font-size:13px;font-weight:700;cursor:pointer;display:flex;align-items:center;justify-content:center;gap:7px;transition:opacity .15s}
.pf-btn:hover{opacity:.85}
.signed-info{display:none;margin-top:8px;padding:10px 12px;background:var(–green-pale);border-radius:var(–r-xs);border-left:3px solid var(–green);font-size:11.5px;color:#00695c;font-weight:600}

/* ── Modals ── */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.65);backdrop-filter:blur(4px);z-index:800;display:flex;align-items:flex-end;justify-content:center;padding:0;opacity:0;pointer-events:none;transition:opacity .22s}
.modal-overlay.open{opacity:1;pointer-events:all}
.modal{
background:var(–white);
border-radius:var(–r) var(–r) 0 0;
width:100%;max-width:480px;
max-height:90vh;overflow-y:auto;
transform:translateY(20px);transition:transform .22s;
padding-bottom:env(safe-area-inset-bottom,16px);
}
.modal-overlay.open .modal{transform:none}
.modal-handle{width:36px;height:4px;background:var(–border);border-radius:2px;margin:12px auto 4px}
.modal-header{padding:12px 20px 14px;border-bottom:1px solid var(–border);display:flex;align-items:center;justify-content:space-between}
.modal-header h2{font-size:16px;font-weight:800;color:var(–navy)}
.modal-close{width:28px;height:28px;border-radius:50%;background:var(–card);border:none;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:13px;color:var(–slate)}
.modal-body{padding:18px 20px}
.modal-footer{padding:14px 20px;border-top:1px solid var(–border);display:flex;justify-content:flex-end;gap:10px}
.form-group{margin-bottom:14px}
.form-group label{display:block;font-size:11px;font-weight:700;color:var(–slate);text-transform:uppercase;letter-spacing:.05em;margin-bottom:5px}
.form-group input,.form-group textarea,.form-group select{width:100%;padding:10px 13px;border:1.5px solid var(–border);border-radius:var(–r-xs);font-family:var(–font);font-size:13px;color:var(–navy);outline:none;resize:vertical;background:var(–white)}
.form-group input:focus,.form-group textarea:focus,.form-group select:focus{border-color:var(–purple)}
.error-msg{display:none;padding:8px 12px;background:#fee2e2;color:#991b1b;border-radius:var(–r-xs);font-size:12px;font-weight:600;margin-bottom:12px}
.role-tabs{display:flex;gap:8px;margin-bottom:16px}
.role-tab{flex:1;padding:9px;border-radius:var(–r-xs);border:none;font-family:var(–font);font-size:13px;font-weight:700;cursor:pointer;transition:all .15s;display:flex;align-items:center;justify-content:center;gap:6px}
.role-tab.active{background:var(–purple);color:#fff}
.role-tab:not(.active){background:var(–card);color:var(–slate)}

/* Preview modal */
#previewModal .modal{border-radius:var(–r)}
#previewContainer img{max-width:100%;border-radius:var(–r-xs);display:block;margin:0 auto}
#previewContainer iframe{width:100%;height:60vh;border:none;border-radius:var(–r-xs)}
.preview-placeholder{text-align:center;padding:40px 20px;color:var(–slate)}
.preview-placeholder a{color:var(–purple);font-weight:700;text-decoration:none}

/* Report modal */
#reportModal .modal{border-radius:var(–r) var(–r) 0 0;max-height:92vh}
.report-table{width:100%;border-collapse:collapse;font-size:12px}
.report-table th{background:var(–navy);color:rgba(255,255,255,.8);padding:8px 10px;text-align:left;font-size:10px;font-weight:700;letter-spacing:.05em;text-transform:uppercase}
.report-table td{padding:8px 10px;border-bottom:1px solid var(–border);color:var(–navy)}
.report-meta{background:#fffbeb;border:1px solid #fde68a;border-radius:var(–r-xs);padding:13px;margin-bottom:14px;font-size:12.5px;line-height:1.7}

/* Bottom nav placeholder */
.bottom-space{height:20px}

@media(min-width:481px){
.modal{border-radius:var(–r)}
.modal-overlay{align-items:center;padding:20px}
}
</style>

</head>
<body>

<div id="toastContainer"></div>
<div id="autosaveIndicator"><i class="fas fa-circle fa-xs"></i> Autosimpan…</div>

<div class="app-wrap">

  <!-- TOP BAR -->

  <div class="topbar">
    <div class="topbar-left">
      <div class="topbar-logo">
        <img id="logoImg" alt="Logo"/>
        <span id="logoText">S</span>
      </div>
      <div class="topbar-title">
        SMK Mentakab
        <span>Sistem Penghantaran Mingguan</span>
      </div>
    </div>
    <div class="topbar-right">
      <div style="position:relative">
        <button class="topbar-icon-btn" onclick="toggleNotif()" title="Notifikasi">
          <i class="fas fa-bell"></i>
          <span id="notifBadge">0</span>
        </button>
        <div id="notifPanel">
          <div class="notif-hdr"><i class="fas fa-bell"></i>&nbsp; Notifikasi</div>
          <div id="notifList"></div>
        </div>
      </div>
      <button class="login-btn" id="adminBtn" onclick="openLogin()">
        <i class="fas fa-user-shield"></i>
        <span id="adminBtnText">Masuk</span>
      </button>
    </div>
  </div>

  <!-- BANNER -->

  <img id="bannerImg" alt="Banner"/>

  <!-- ADMIN BAR -->

  <div id="adminBar">
    <span><i class="fas fa-sliders"></i> Admin</span>
    <label class="adm-label">
      <i class="fas fa-image"></i> Banner
      <input type="file" accept="image/*" onchange="changeBanner(event)"/>
    </label>
    <label class="adm-label">
      <i class="fas fa-circle-dot"></i> Logo
      <input type="file" accept="image/*" onchange="changeLogo(event)"/>
    </label>
    <div style="margin-left:auto;font-size:11px;color:rgba(255,255,255,.35)" id="firebaseStatusText">Memuat…</div>
  </div>

  <!-- SCROLL AREA -->

  <div class="scroll-area">

```
<!-- WEEK CARD -->
<div class="week-card">
  <div class="week-nav-row">
    <button class="wk-arrow" onclick="prevWeek()"><i class="fas fa-chevron-left"></i></button>
    <span id="weekLabel">Minggu –</span>
    <button class="wk-arrow" onclick="nextWeek()"><i class="fas fa-chevron-right"></i></button>
  </div>
  <div class="week-date-row">
    <i class="fas fa-calendar-days"></i>
    <span id="weekDates">–</span>
  </div>
  <div class="week-btn-row">
    <button class="chip-btn" onclick="goToCurrentWeek()">
      <i class="fas fa-rotate-left"></i> Minggu Ini
    </button>
    <button class="chip-btn gold" onclick="openReport()">
      <i class="fas fa-file-alt"></i> Laporan
    </button>
  </div>
</div>

<!-- DONUT CARD -->
<div class="donut-card">
  <div class="donut-wrap">
    <canvas id="donutCanvas" width="100" height="100"></canvas>
    <div class="donut-center">
      <span class="donut-pct" id="donutPct">0%</span>
      <span class="donut-lbl">selesai</span>
    </div>
  </div>
  <div class="donut-legend">
    <div class="dl-item">
      <div class="dl-left"><div class="dl-dot" style="background:var(--green)"></div><span class="dl-label">Siap Disahkan</span></div>
      <span class="dl-val" id="statDisahkan">0</span>
    </div>
    <div class="dl-item">
      <div class="dl-left"><div class="dl-dot" style="background:var(--amber)"></div><span class="dl-label">Belum Hantar</span></div>
      <span class="dl-val" id="statBelum">0</span>
    </div>
    <div class="dl-item">
      <div class="dl-left"><div class="dl-dot" style="background:var(--red)"></div><span class="dl-label">Penghantaran Lewat</span></div>
      <span class="dl-val" id="statLewat">0</span>
    </div>
  </div>
</div>

<!-- STAFF SELECTOR -->
<div class="selector-card">
  <label><i class="fas fa-user-circle"></i> &nbsp;Log masuk sebagai staf</label>
  <select id="staffSelect" onchange="selectStaffLogin(this.value)">
    <option value="">— Pilih nama anda —</option>
  </select>
  <div class="active-staff-badge" id="activeBadge">
    <i class="fas fa-check-circle"></i>
    <span id="activeBadgeName"></span>
  </div>
</div>

<!-- PRINCIPAL CARD -->
<div class="principal-card" id="principalSection">
  <div class="pc-title"><i class="fas fa-stamp"></i> Pengesahan Pengetua</div>
  <div id="principalAccessNote" class="pc-note" style="margin-bottom:10px">
    <i class="fas fa-lock"></i> Log masuk sebagai Pengetua untuk menandatangani.
  </div>
  <div id="principalStamp" class="principal-stamp">
    <i class="fas fa-pen-to-square" style="font-size:22px;color:var(--slate);opacity:.4"></i>
    <p style="font-size:12px;color:var(--slate)">Belum disahkan</p>
  </div>
  <div class="signed-info" id="principalSignedInfo">
    <p id="principalSignedDetails"></p>
  </div>
  <div id="principalForm" class="principal-form" style="display:none">
    <div>
      <div class="pf-label">Tarikh Semakan</div>
      <input type="date" id="principalDate" class="pf-input"/>
    </div>
    <div>
      <div class="pf-label">Catatan (pilihan)</div>
      <textarea id="principalNotes" class="pf-input pf-textarea" placeholder="Catatan…"></textarea>
    </div>
    <button class="pf-btn" onclick="signPrincipal()">
      <i class="fas fa-stamp"></i> Sahkan Minggu Ini
    </button>
  </div>
</div>

<!-- FILTER + SEARCH -->
<div class="filter-strip" id="filterStrip">
  <button class="f-chip active" data-filter="" onclick="setFilter(this,'')">Semua</button>
  <button class="f-chip green" data-filter="Disahkan" onclick="setFilter(this,'Disahkan')">Disahkan</button>
  <button class="f-chip amber" data-filter="Belum Hantar" onclick="setFilter(this,'Belum Hantar')">Belum Hantar</button>
  <button class="f-chip red" data-filter="Lewat" onclick="setFilter(this,'Lewat')">Lewat</button>
</div>

<div class="search-wrap">
  <i class="fas fa-search"></i>
  <input type="text" id="searchInput" placeholder="Cari nama staf…" oninput="renderCards()"/>
</div>

<div class="rec-count" id="recCount"></div>

<!-- STAFF CARDS -->
<div id="staffCards"></div>

<div class="bottom-space"></div>
```

  </div><!-- /scroll-area -->
</div><!-- /app-wrap -->

<!-- ═══ MODALS ═══ -->

<!-- Confirm cancel -->

<div class="modal-overlay" id="confirmModal">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-header">
      <h2><i class="fas fa-triangle-exclamation" style="color:#e84393"></i> Batalkan?</h2>
      <button class="modal-close" onclick="closeModal('confirmModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body">
      <p style="font-size:14px;color:var(--slate)">Penghantaran dan fail akan dipadam. Teruskan?</p>
    </div>
    <div class="modal-footer">
      <button class="act-btn act-view" onclick="closeModal('confirmModal')" style="padding:10px 18px">Batal</button>
      <button class="act-btn act-del" onclick="confirmCancelSubmission()" style="padding:10px 18px"><i class="fas fa-trash"></i> Padam</button>
    </div>
  </div>
</div>

<!-- Preview -->

<div class="modal-overlay" id="previewModal">
  <div class="modal" style="border-radius:var(--r)">
    <div class="modal-handle"></div>
    <div class="modal-header">
      <h2 style="font-size:14px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap"><i class="fas fa-eye" style="color:var(--purple)"></i> <span id="previewFileName"></span></h2>
      <button class="modal-close" onclick="closeModal('previewModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body"><div id="previewContainer"></div></div>
  </div>
</div>

<!-- Pengesahan PK -->

<div class="modal-overlay" id="pengesahanModal">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-header">
      <h2><i class="fas fa-stamp" style="color:var(--amber)"></i> Pengesahan PK</h2>
      <button class="modal-close" onclick="closeModal('pengesahanModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body">
      <p style="font-size:13px;color:var(--slate);margin-bottom:12px">Staf: <strong id="pengesahanStaffName"></strong></p>
      <div id="pengesahanError" class="error-msg"><i class="fas fa-times-circle"></i> Hanya Pengetua boleh mengesahkan.</div>
      <div class="form-group">
        <label>Catatan (pilihan)</label>
        <textarea id="pengesahanCatatan" rows="3" placeholder="Catatan…"></textarea>
      </div>
    </div>
    <div class="modal-footer">
      <button class="act-btn act-view" onclick="closeModal('pengesahanModal')" style="padding:10px 18px">Batal</button>
      <button class="act-btn act-stamp" onclick="submitPengesahan()" style="padding:10px 18px"><i class="fas fa-stamp"></i> Sahkan</button>
    </div>
  </div>
</div>

<!-- Report -->

<div class="modal-overlay" id="reportModal">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-header">
      <h2><i class="fas fa-file-alt" style="color:var(--amber)"></i> Laporan Mingguan</h2>
      <button class="modal-close" onclick="closeModal('reportModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body" id="reportBody"></div>
    <div class="modal-footer">
      <button class="act-btn act-view" onclick="closeModal('reportModal')" style="padding:10px 18px">Tutup</button>
    </div>
  </div>
</div>

<!-- Login -->

<div class="modal-overlay" id="loginModal">
  <div class="modal">
    <div class="modal-handle"></div>
    <div class="modal-header">
      <h2><i class="fas fa-user-shield" style="color:var(--purple)"></i> Log Masuk</h2>
      <button class="modal-close" onclick="closeModal('loginModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body">
      <div class="role-tabs">
        <button class="role-tab active" id="btnRolePengetua" onclick="setLoginRole('pengetua')">
          <i class="fas fa-user-tie"></i> Pengetua
        </button>
        <button class="role-tab" id="btnRoleAdmin" onclick="setLoginRole('admin')">
          <i class="fas fa-user-cog"></i> Admin
        </button>
      </div>
      <div id="loginError" class="error-msg"><i class="fas fa-times-circle"></i> Kata laluan tidak sah.</div>
      <div class="form-group">
        <label>Kata Laluan</label>
        <input type="password" id="loginPass" placeholder="Kata laluan…" onkeydown="if(event.key==='Enter') doLogin()"/>
      </div>
    </div>
    <div class="modal-footer">
      <button class="act-btn act-view" onclick="closeModal('loginModal')" style="padding:10px 18px">Batal</button>
      <button class="act-btn" onclick="doLogin()" style="padding:10px 20px;background:var(--purple);color:#fff"><i class="fas fa-right-to-bracket"></i> Masuk</button>
    </div>
  </div>
</div>

<!-- ═══ SCRIPT ═══ -->

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-app.js";
import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-auth.js";
import { getFirestore, doc, setDoc, onSnapshot, serverTimestamp } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-firestore.js";
import { getStorage, ref, uploadBytes, getDownloadURL, deleteObject } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-storage.js";

/* ─── DATA ─── */
const STAFF_LIST = [
  { id:1,  nama:"'Afifah Binti Abdul Aziz",          kat:1, jawatan:"Ketua Pembantu Makmal" },
  { id:2,  nama:"Ida Zarina Binti Idris",            kat:1, jawatan:"Pembantu Makmal" },
  { id:3,  nama:"Azian Binti Mohamad",               kat:1, jawatan:"Pembantu Makmal" },
  { id:4,  nama:"Fatimah Binti Latiff",              kat:1, jawatan:"Pembantu Makmal" },
  { id:5,  nama:"Zainun Binti Mohamed Ramthan",      kat:1, jawatan:"Pembantu Makmal" },
  { id:6,  nama:"Nor'aini Binti Md Yusoff",          kat:1, jawatan:"Pembantu Makmal" },
  { id:7,  nama:"Fakarullah Amer Bin Zainal Abidin", kat:1, jawatan:"Pembantu Makmal" },
  { id:8,  nama:"Abdul Azam Bin Mohamed",            kat:1, jawatan:"Pembantu Makmal" },
  { id:9,  nama:"Nor Faiza Binti Mustaffa Kamal",    kat:2, jawatan:"Pembantu Pengurusan Murid" },
  { id:10, nama:"Wan Azlena Binti Wan Deraman",      kat:2, jawatan:"Pembantu Pengurusan Murid" },
  { id:11, nama:"Mohd Faizal Bin Zainal",            kat:2, jawatan:"Pembantu Pengurusan Murid" },
  { id:12, nama:"Juhaida Binti Abd Rasid",           kat:3, jawatan:"Pembantu Tadbir" },
  { id:13, nama:"Junainah Binti Hassan",             kat:3, jawatan:"Pembantu Tadbir" },
  { id:14, nama:"Rafidah Binti Sidek",               kat:3, jawatan:"Pembantu Tadbir" },
  { id:15, nama:"Muhammad Fahmi Bin Hamidin",        kat:4, jawatan:"Pembantu Khidmat Am" },
  { id:16, nama:"Nursyaza Aina Binti Mohd Adaha",    kat:4, jawatan:"Pembantu Khidmat Am" }
];

const firebaseConfig = {
  apiKey:"PASTE_API_KEY",
  authDomain:"PASTE_AUTH_DOMAIN",
  projectId:"PASTE_PROJECT_ID",
  storageBucket:"PASTE_STORAGE_BUCKET",
  messagingSenderId:"PASTE_MESSAGING_SENDER_ID",
  appId:"PASTE_APP_ID"
};

function hasPlaceholderConfig(c){ return Object.values(c).some(v=>String(v).includes("PASTE_")||!String(v).trim()); }

/* ─── STATE ─── */
let app=null,auth=null,db=null,storage=null;
let firebaseReady=false;
let currentWeekOffset=0,currentRole=null,currentLoginTab="pengetua",currentStaffId=null;
let pendingCancelId=null,pendingPengesahanId=null;
let submissions={},weekSignatures={};
let settingsData={bannerUrl:null,bannerPath:null,logoUrl:null,logoPath:null};
let autosaveTimer=null,unsubmissions=null,unweeksig=null,unsettings=null;
let activeFilter="";

/* ─── HELPERS ─── */
function esc(s){ return String(s??"").replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;").replace(/'/g,"&#039;"); }

function showToast(msg,type=""){
  const c=document.getElementById("toastContainer");
  const t=document.createElement("div"); t.className=`toast ${type}`;
  const ic={success:"fa-check-circle",error:"fa-times-circle",warning:"fa-exclamation-triangle"};
  t.innerHTML=`<i class="fas ${ic[type]||"fa-info-circle"}"></i> ${esc(msg)}`;
  c.appendChild(t);
  setTimeout(()=>{t.style.opacity="0";t.style.transition="opacity .4s";setTimeout(()=>t.remove(),400);},3000);
}

function triggerAutosave(){
  const el=document.getElementById("autosaveIndicator");
  el.classList.add("visible"); clearTimeout(autosaveTimer);
  autosaveTimer=setTimeout(()=>el.classList.remove("visible"),2200);
}

function openModal(id){ document.getElementById(id).classList.add("open"); document.body.style.overflow="hidden"; }
function closeModal(id){
  document.getElementById(id).classList.remove("open");
  if(!document.querySelector(".modal-overlay.open")) document.body.style.overflow="";
}
window.closeModal=closeModal;

document.querySelectorAll(".modal-overlay").forEach(o=>{
  o.addEventListener("click",e=>{
    if(e.target===o){ o.classList.remove("open"); if(!document.querySelector(".modal-overlay.open")) document.body.style.overflow=""; }
  });
});

/* ─── WEEK ─── */
function getWeekStart(offset=0){
  const now=new Date(),day=now.getDay(),diff=day===0?-6:1-day;
  const mon=new Date(now); mon.setDate(now.getDate()+diff+offset*7); mon.setHours(0,0,0,0); return mon;
}
function getWeekEnd(offset=0){
  const mon=getWeekStart(offset),fri=new Date(mon);
  fri.setDate(mon.getDate()+4); fri.setHours(23,59,59,999); return fri;
}
function getWeekKey(offset=currentWeekOffset){
  const mon=getWeekStart(offset); return `week_${mon.getFullYear()}_${mon.getMonth()+1}_${mon.getDate()}`;
}
function getWeekNumber(offset=0){
  const mon=getWeekStart(offset),jan1=new Date(mon.getFullYear(),0,1);
  return Math.ceil((Math.floor((mon-jan1)/86400000)+jan1.getDay()+1)/7);
}
const MONTHS=["JAN","FEB","MAC","APR","MEI","JUN","JUL","OGO","SEP","OKT","NOV","DIS"];
const MONTHS_SHORT=["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];
function formatDate(d){ return `${d.getDate()} ${MONTHS[d.getMonth()]} ${d.getFullYear()}`; }
function formatDateShort(d){ return `${d.getDate()} ${MONTHS_SHORT[d.getMonth()]} ${d.getFullYear()}`; }
function isLate(offset){ return new Date()>getWeekEnd(offset); }

function updateWeekDisplay(){
  const mon=getWeekStart(currentWeekOffset),fri=getWeekEnd(currentWeekOffset);
  document.getElementById("weekLabel").textContent=`Minggu ${getWeekNumber(currentWeekOffset)}`;
  document.getElementById("weekDates").textContent=`${formatDate(mon)} — ${formatDate(fri)}`;
}

function prevWeek(){ currentWeekOffset--; updateWeekDisplay(); subscribeWeekData(); }
function nextWeek(){ currentWeekOffset++; updateWeekDisplay(); subscribeWeekData(); }
function goToCurrentWeek(){ currentWeekOffset=0; updateWeekDisplay(); subscribeWeekData(); }
window.prevWeek=prevWeek; window.nextWeek=nextWeek; window.goToCurrentWeek=goToCurrentWeek;

/* ─── STATUS ─── */
function computeStatus(staffId,weekOffset){
  const key=getWeekKey(weekOffset),sub=(submissions[key]||{})[staffId];
  if(!sub) return isLate(weekOffset)?"Lewat":"Belum Hantar";
  return sub.status||"Disahkan";
}

/* ─── INITIALS ─── */
function getInitials(nama){
  const parts=nama.replace(/^'/,"").trim().split(/\s+/);
  if(parts.length===1) return parts[0].substring(0,2).toUpperCase();
  return (parts[0][0]+(parts[1]?.[0]||"")).toUpperCase();
}

/* ─── STAFF SELECT ─── */
function populateStaffSelect(){
  const sel=document.getElementById("staffSelect");
  sel.innerHTML=`<option value="">— Pilih nama anda —</option>`;
  STAFF_LIST.forEach(s=>{
    const o=document.createElement("option"); o.value=String(s.id); o.textContent=s.nama; sel.appendChild(o);
  });
  const saved=localStorage.getItem("smkm_selected_staff");
  if(saved){ sel.value=saved; currentStaffId=Number(saved); updateActiveBadge(currentStaffId); }
}

function updateActiveBadge(id){
  const badge=document.getElementById("activeBadge");
  const nm=document.getElementById("activeBadgeName");
  if(id){ const s=STAFF_LIST.find(x=>x.id===id); nm.textContent=s?.nama||""; badge.classList.add("show"); }
  else { badge.classList.remove("show"); }
}

window.selectStaffLogin=function(val){
  currentStaffId=val?Number(val):null;
  if(currentStaffId){ localStorage.setItem("smkm_selected_staff",String(currentStaffId)); const s=STAFF_LIST.find(x=>x.id===currentStaffId); showToast(`Aktif: ${s?.nama||""}`, "success"); }
  else { localStorage.removeItem("smkm_selected_staff"); showToast("Pilihan dikosongkan.","warning"); }
  updateActiveBadge(currentStaffId);
  renderCards();
};

/* ─── FILTER ─── */
window.setFilter=function(btn,val){
  activeFilter=val;
  document.querySelectorAll(".f-chip").forEach(b=>b.classList.remove("active"));
  btn.classList.add("active");
  renderCards();
};

/* ─── FIREBASE ─── */
function setFirebaseStatus(t){ document.getElementById("firebaseStatusText").textContent=t; }

function applyBrandingToUI(){
  const bi=document.getElementById("bannerImg"),li=document.getElementById("logoImg"),lt=document.getElementById("logoText");
  if(settingsData.bannerUrl){ bi.src=settingsData.bannerUrl; bi.style.display="block"; } else { bi.removeAttribute("src"); bi.style.display="none"; }
  if(settingsData.logoUrl){ li.src=settingsData.logoUrl; li.style.display="block"; lt.style.display="none"; } else { li.removeAttribute("src"); li.style.display="none"; lt.style.display="inline"; }
}

async function initFirebase(){
  if(hasPlaceholderConfig(firebaseConfig)){
    setFirebaseStatus("Config belum lengkap");
    showToast("Gantikan nilai PASTE_* dalam firebaseConfig.","error");
    renderCards(); updateDonut(); updatePrincipalSection(); return;
  }
  try{
    app=initializeApp(firebaseConfig);
    auth=getAuth(app); db=getFirestore(app); storage=getStorage(app);
    await signInAnonymously(auth);
    onAuthStateChanged(auth,user=>{
      if(user){ firebaseReady=true; setFirebaseStatus("Tersambung"); subscribeSettings(); subscribeWeekData(); }
      else { firebaseReady=false; setFirebaseStatus("Belum log masuk"); }
    });
  }catch(err){ console.error(err); firebaseReady=false; setFirebaseStatus("Gagal sambung"); showToast("Gagal sambung Firebase.","error"); }
}

function subscribeSettings(){
  if(!firebaseReady||!db) return;
  if(unsettings) unsettings();
  unsettings=onSnapshot(doc(db,"systemSettings","branding"),snap=>{
    settingsData=snap.exists()?{bannerUrl:snap.data().bannerUrl||null,bannerPath:snap.data().bannerPath||null,logoUrl:snap.data().logoUrl||null,logoPath:snap.data().logoPath||null}:{bannerUrl:null,bannerPath:null,logoUrl:null,logoPath:null};
    applyBrandingToUI();
  },err=>{ console.error(err); });
}

function subscribeWeekData(){
  if(!firebaseReady||!db) return;
  const weekKey=getWeekKey();
  if(unsubmissions) unsubmissions();
  if(unweeksig) unweeksig();
  unsubmissions=onSnapshot(doc(db,"weeklySubmissions",weekKey),snap=>{
    submissions[weekKey]=(snap.exists()?snap.data().records:null)||{};
    renderCards();
  },err=>{ console.error(err); showToast("Gagal baca data.","error"); });
  unweeksig=onSnapshot(doc(db,"weeklySignatures",weekKey),snap=>{
    weekSignatures[weekKey]=snap.exists()?snap.data():{};
    updatePrincipalSection();
  },err=>{ console.error(err); });
}

async function saveWeekSubmissions(weekKey){
  await setDoc(doc(db,"weeklySubmissions",weekKey),{records:submissions[weekKey]||{},updatedAt:serverTimestamp()},{merge:true});
  triggerAutosave();
}
async function saveWeekSignature(weekKey){
  await setDoc(doc(db,"weeklySignatures",weekKey),{...weekSignatures[weekKey],updatedAt:serverTimestamp()},{merge:true});
  triggerAutosave();
}
async function saveBranding(){
  await setDoc(doc(db,"systemSettings","branding"),{...settingsData,updatedAt:serverTimestamp()},{merge:true});
  triggerAutosave();
}

/* ─── RENDER CARDS ─── */
function renderCards(){
  const search=(document.getElementById("searchInput")?.value||"").toLowerCase();
  const key=getWeekKey();

  const filtered=STAFF_LIST.filter(s=>{
    if(search&&!s.nama.toLowerCase().includes(search)) return false;
    const st=computeStatus(s.id,currentWeekOffset);
    if(activeFilter&&st!==activeFilter) return false;
    return true;
  });

  document.getElementById("recCount").textContent=`${filtered.length} daripada ${STAFF_LIST.length} staf`;

  const container=document.getElementById("staffCards");
  container.innerHTML="";

  filtered.forEach(staff=>{
    const sub=(submissions[key]||{})[staff.id];
    const status=computeStatus(staff.id,currentWeekOffset);
    const isOwn=(currentStaffId===staff.id);
    const initials=getInitials(staff.nama);

    /* Status chip */
    const scClass=status==="Disahkan"?"sc-disahkan":status==="Lewat"?"sc-lewat":"sc-belum";
    const scLabel=status==="Disahkan"?"Disahkan":status==="Lewat"?"Lewat":"Belum Hantar";

    /* Avatar */
    const avatarClass=isOwn?"staff-avatar mine":"staff-avatar";

    /* File badge */
    let filePart="";
    if(sub){
      const ext=(sub.fileType||"").toLowerCase();
      const cls=ext==="pdf"?"fe-pdf":(ext==="doc"||ext==="docx")?"fe-doc":"fe-img";
      filePart=`
        <div class="staff-card-bottom">
          <div class="upload-row">
            <div class="file-info">
              <span class="file-ext-badge ${cls}">${esc(ext.toUpperCase())}</span>
              <span class="file-name">${esc(sub.fileName)}</span>
            </div>
            <span class="file-date">${esc(sub.tarikhHantar)}</span>
          </div>
          <div class="card-actions">
            <button class="act-btn act-view" onclick="previewFile(${staff.id})"><i class="fas fa-eye"></i> Lihat</button>
            ${isOwn||currentRole==="admin"||currentRole==="pengetua"?`<button class="act-btn act-del" onclick="openCancelConfirm(${staff.id})"><i class="fas fa-trash"></i> Padam</button>`:""}
            ${currentRole==="pengetua"&&!sub.pengesahan?`<button class="act-btn act-stamp" onclick="openPengesahan(${staff.id})"><i class="fas fa-stamp"></i> Sahkan</button>`:""}
          </div>
          ${(currentRole==="admin"||currentRole==="pengetua")?`<textarea class="semakan-area" placeholder="Catatan semakan…" onchange="saveSemakan(${staff.id},this.value)">${esc(sub.semakan||"")}</textarea>`:(sub.semakan?`<p style="font-size:12px;color:var(--slate);margin-top:8px">${esc(sub.semakan)}</p>`:"")}

```
      ${sub.pengesahan?`<div class="pengesahan-row"><i class="fas fa-check-circle"></i><span>Disahkan ${esc(sub.pengesahan.tarikh||"")} ${sub.pengesahan.catatan?("· "+esc(sub.pengesahan.catatan)):""}</span></div>`:""}
    </div>`;
} else if(isOwn){
  filePart=`
    <div class="staff-card-bottom">
      <label class="upload-btn-label" for="fi_${staff.id}">
        <i class="fas fa-upload"></i> Muat Naik Fail
      </label>
      <input type="file" id="fi_${staff.id}" accept=".pdf,.jpg,.jpeg,.png,.doc,.docx" onchange="handleUpload(event,${staff.id})">
    </div>`;
}

const card=document.createElement("div");
card.className="staff-card";
card.innerHTML=`
  <div class="staff-card-top">
    <div class="${avatarClass}">${esc(initials)}</div>
    <span class="status-chip ${scClass}">${scLabel}</span>
  </div>
  <div class="staff-name">${esc(staff.nama)}</div>
  <div class="staff-kat">${esc(staff.jawatan)}</div>
  ${filePart}
`;
container.appendChild(card);
```

});

updateDonut();
updateNotifications();
updatePrincipalSection();
}

/* ─── UPLOAD ─── */
window.handleUpload=async function(event,staffId){
try{
if(!firebaseReady||!storage||!db){ showToast(“Firebase belum sedia.”,“error”); return; }
if(currentStaffId!==staffId){ showToast(“Hanya staf terpilih boleh upload.”,“error”); event.target.value=””; return; }
const file=event.target.files?.[0]; if(!file) return;
const allowed=[“pdf”,“jpg”,“jpeg”,“png”,“doc”,“docx”];
const ext=file.name.split(”.”).pop().toLowerCase();
if(!allowed.includes(ext)){ showToast(“Jenis fail tidak dibenarkan.”,“error”); event.target.value=””; return; }
const weekKey=getWeekKey(),now=new Date();
const safeName=file.name.replace(/[^\w.-]+/g,”_”);
const storagePath=`submissions/${weekKey}/${staffId}/${Date.now()}_${safeName}`;
const storageRef=ref(storage,storagePath);
showToast(“Sedang upload…”,“warning”);
await uploadBytes(storageRef,file);
const fileUrl=await getDownloadURL(storageRef);
if(!submissions[weekKey]) submissions[weekKey]={};
const old=submissions[weekKey][staffId];
if(old?.storagePath){ try{ await deleteObject(ref(storage,old.storagePath)); }catch(e){ console.warn(e); } }
submissions[weekKey][staffId]={
staffId,fileName:file.name,fileType:ext,fileUrl,storagePath,
tarikhHantar:formatDateShort(now),
status:isLate(currentWeekOffset)?“Lewat”:“Disahkan”,
semakan:old?.semakan||””,
pengesahan:old?.pengesahan||null,
uploadedByName:STAFF_LIST.find(s=>s.id===staffId)?.nama||””,
updatedAtMs:Date.now()
};
await saveWeekSubmissions(weekKey);
showToast(“Fail berjaya dimuat naik!”,“success”);
renderCards();
}catch(err){ console.error(err); showToast(“Upload gagal. Semak Storage Rules.”,“error”); }
finally{ event.target.value=””; }
};

/* ─── CANCEL ─── */
window.openCancelConfirm=function(id){ pendingCancelId=id; openModal(“confirmModal”); };
window.confirmCancelSubmission=async function(){
try{
const weekKey=getWeekKey(),row=submissions[weekKey]?.[pendingCancelId]; if(!row) return;
const ok=currentStaffId===pendingCancelId||currentRole===“admin”||currentRole===“pengetua”;
if(!ok){ showToast(“Tidak dibenarkan.”,“error”); return; }
if(row.storagePath){ try{ await deleteObject(ref(storage,row.storagePath)); }catch(e){ console.warn(e); } }
delete submissions[weekKey][pendingCancelId];
await saveWeekSubmissions(weekKey);
renderCards(); showToast(“Penghantaran dibatalkan.”,“warning”);
}catch(err){ console.error(err); showToast(“Gagal batalkan.”,“error”); }
finally{ closeModal(“confirmModal”); pendingCancelId=null; }
};

/* ─── PREVIEW ─── */
window.previewFile=function(staffId){
const sub=submissions[getWeekKey()]?.[staffId]; if(!sub) return;
document.getElementById(“previewFileName”).textContent=sub.fileName||””;
const c=document.getElementById(“previewContainer”); c.innerHTML=””;
const ext=(sub.fileType||””).toLowerCase();
if([“jpg”,“jpeg”,“png”].includes(ext)){
const img=document.createElement(“img”); img.src=sub.fileUrl; img.alt=sub.fileName||””; c.appendChild(img);
} else if(ext===“pdf”){
const iframe=document.createElement(“iframe”); iframe.src=sub.fileUrl; iframe.title=sub.fileName||””; c.appendChild(iframe);
} else {
c.innerHTML=`<div class="preview-placeholder"><i class="fas fa-file-alt" style="font-size:32px;margin-bottom:10px"></i><p>Pratonton tidak tersedia.<br><strong>${esc(sub.fileName||"")}</strong></p><p style="margin-top:10px"><a href="${sub.fileUrl}" target="_blank" rel="noopener">Buka fail</a></p></div>`;
}
openModal(“previewModal”);
};

/* ─── SEMAKAN ─── */
window.saveSemakan=async function(staffId,value){
try{
if(currentRole!==“admin”&&currentRole!==“pengetua”) return;
const weekKey=getWeekKey();
if(!submissions[weekKey]?.[staffId]) return;
submissions[weekKey][staffId].semakan=value;
await saveWeekSubmissions(weekKey);
}catch(err){ console.error(err); showToast(“Gagal simpan semakan.”,“error”); }
};

/* ─── PENGESAHAN PK ─── */
window.openPengesahan=function(staffId){
pendingPengesahanId=staffId;
const staff=STAFF_LIST.find(s=>s.id===staffId);
document.getElementById(“pengesahanStaffName”).textContent=staff?.nama||””;
document.getElementById(“pengesahanCatatan”).value=””;
document.getElementById(“pengesahanError”).style.display=“none”;
openModal(“pengesahanModal”);
};
window.submitPengesahan=async function(){
try{
if(currentRole!==“pengetua”){ document.getElementById(“pengesahanError”).style.display=“block”; return; }
const weekKey=getWeekKey();
if(!submissions[weekKey]?.[pendingPengesahanId]) return;
submissions[weekKey][pendingPengesahanId].pengesahan={tarikh:formatDateShort(new Date()),catatan:document.getElementById(“pengesahanCatatan”).value||””};
submissions[weekKey][pendingPengesahanId].status=“Disahkan”;
await saveWeekSubmissions(weekKey);
closeModal(“pengesahanModal”); renderCards();
showToast(“Pengesahan disimpan!”,“success”);
}catch(err){ console.error(err); showToast(“Gagal simpan pengesahan.”,“error”); }
};

/* ─── PRINCIPAL ─── */
function updatePrincipalSection(){
const key=getWeekKey(),sig=weekSignatures[key]||{};
const isPrincipal=currentRole===“pengetua”;
document.getElementById(“principalAccessNote”).style.display=isPrincipal?“none”:“block”;
document.getElementById(“principalForm”).style.display=isPrincipal&&!sig.signed?“block”:“none”;
const stamp=document.getElementById(“principalStamp”);
const si=document.getElementById(“principalSignedInfo”);
if(sig.signed){
stamp.className=“principal-stamp signed”;
stamp.innerHTML=`<div class="stamp-check">&#10003;</div><div class="stamp-name">Hajah Aniza Binti Baharuddin</div><div class="stamp-date">Tarikh: ${esc(sig.date||"")}</div>`;
si.style.display=“block”;
document.getElementById(“principalSignedDetails”).textContent=`Catatan: ${sig.notes||"Tiada catatan"} | ${sig.date||""}`;
} else {
stamp.className=“principal-stamp”;
stamp.innerHTML=`<i class="fas fa-pen-to-square" style="font-size:22px;color:var(--slate);opacity:.4"></i><p style="font-size:12px;color:var(--slate)">Belum disahkan</p>`;
si.style.display=“none”;
}
if(isPrincipal){
const t=new Date();
document.getElementById(“principalDate”).value=`${t.getFullYear()}-${String(t.getMonth()+1).padStart(2,"0")}-${String(t.getDate()).padStart(2,"0")}`;
}
}
window.signPrincipal=async function(){
try{
if(currentRole!==“pengetua”){ showToast(“Hanya Pengetua boleh menandatangani.”,“error”); return; }
const key=getWeekKey(),dateVal=document.getElementById(“principalDate”).value;
weekSignatures[key]={signed:true,date:dateVal?formatDateShort(new Date(dateVal+“T00:00:00”)):formatDateShort(new Date()),notes:document.getElementById(“principalNotes”).value||””};
await saveWeekSignature(key);
updatePrincipalSection();
showToast(“Pengesahan disimpan!”,“success”);
}catch(err){ console.error(err); showToast(“Gagal simpan.”,“error”); }
};

/* ─── DONUT CHART ─── */
function updateDonut(){
let d=0,b=0,l=0;
STAFF_LIST.forEach(s=>{ const st=computeStatus(s.id,currentWeekOffset); if(st===“Disahkan”) d++; else if(st===“Lewat”) l++; else b++; });
document.getElementById(“statDisahkan”).textContent=d;
document.getElementById(“statBelum”).textContent=b;
document.getElementById(“statLewat”).textContent=l;
const pct=STAFF_LIST.length?Math.round((d/STAFF_LIST.length)*100):0;
document.getElementById(“donutPct”).textContent=pct+”%”;
drawDonut(d,b,l);
}

function drawDonut(d,b,l){
const canvas=document.getElementById(“donutCanvas”);
const ctx=canvas.getContext(“2d”);
const total=d+b+l;
const size=100,ratio=window.devicePixelRatio||1;
canvas.width=size*ratio; canvas.height=size*ratio;
canvas.style.width=size+“px”; canvas.style.height=size+“px”;
ctx.setTransform(ratio,0,0,ratio,0,0);
ctx.clearRect(0,0,size,size);
const cx=size/2,cy=size/2,r=38,inner=24,lw=r-inner;

if(total===0){
ctx.beginPath(); ctx.arc(cx,cy,r,0,Math.PI*2);
ctx.strokeStyle=”#e4e5ec”; ctx.lineWidth=lw; ctx.stroke(); return;
}

let angle=-Math.PI/2;
[{val:d,color:”#00b894”},{val:b,color:”#f0a500”},{val:l,color:”#e84393”}].forEach(seg=>{
if(!seg.val) return;
const slice=(seg.val/total)*Math.PI*2;
ctx.beginPath(); ctx.arc(cx,cy,r+(lw/2),angle,angle+slice);
ctx.strokeStyle=seg.color; ctx.lineWidth=lw; ctx.lineCap=“butt”; ctx.stroke();
angle+=slice;
});
}

/* ─── NOTIFICATIONS ─── */
function updateNotifications(){
const key=getWeekKey(),items=[];
STAFF_LIST.forEach(s=>{
const sub=submissions[key]?.[s.id];
if(!sub) items.push({type:“a”,msg:`${s.nama.split(" ")[0]} belum hantar`});
else if(sub.status===“Lewat”) items.push({type:“r”,msg:`${s.nama.split(" ")[0]} lewat`});
});
const sl=items.slice(0,5);
document.getElementById(“notifBadge”).textContent=sl.length;
const list=document.getElementById(“notifList”); list.innerHTML=””;
if(!sl.length){ list.innerHTML=`<div class="notif-item"><div class="nd g"></div><span>Semua rekod terkawal.</span></div>`; return; }
sl.forEach(it=>{ const div=document.createElement(“div”); div.className=“notif-item”; div.innerHTML=`<div class="nd ${it.type}"></div><span>${esc(it.msg)}</span>`; list.appendChild(div); });
}

window.toggleNotif=function(){ document.getElementById(“notifPanel”).classList.toggle(“open”); };
document.addEventListener(“click”,e=>{
const p=document.getElementById(“notifPanel”);
const btn=document.querySelector(”.topbar-icon-btn”);
if(p&&!p.contains(e.target)&&btn&&!btn.contains(e.target)) p.classList.remove(“open”);
});

/* ─── REPORT ─── */
window.openReport=function(){
const key=getWeekKey(),mon=getWeekStart(currentWeekOffset),fri=getWeekEnd(currentWeekOffset);
const wn=getWeekNumber(currentWeekOffset);
const weekStr=`${formatDateShort(mon)} – ${formatDateShort(fri)}`;
let d=0,b=0,l=0;
STAFF_LIST.forEach(s=>{ const st=computeStatus(s.id,currentWeekOffset); if(st===“Disahkan”) d++; else if(st===“Lewat”) l++; else b++; });
const sig=weekSignatures[key]||{};
let rows=””;
STAFF_LIST.forEach((s,i)=>{
const sub=submissions[key]?.[s.id];
const st=computeStatus(s.id,currentWeekOffset);
const stColor=st===“Disahkan”?”#00b894”:st===“Lewat”?”#e84393”:”#f0a500”;
rows+=`<tr><td>${i+1}</td><td>${esc(s.nama)}</td><td>${esc(s.jawatan)}</td><td>${sub?esc(sub.fileName):"–"}</td><td>${sub?esc(sub.tarikhHantar):"–"}</td><td style="font-weight:700;color:${stColor}">${esc(st)}</td><td>${sub?.pengesahan?"&#10003; "+esc(sub.pengesahan.tarikh||""):"–"}</td></tr>`;
});
document.getElementById(“reportBody”).innerHTML=` <div class="report-meta"> <p><strong>Sekolah:</strong> Sekolah Menengah Kebangsaan Mentakab</p> <p><strong>Pengetua:</strong> Hajah Aniza Binti Baharuddin</p> <p><strong>Minggu ${wn}:</strong> ${weekStr}</p> <p><strong>Tarikh:</strong> ${formatDateShort(new Date())}</p> <p style="margin-top:6px"> <span style="color:#00b894;font-weight:700">&#10003; ${d} Disahkan</span>&nbsp;&nbsp; <span style="color:#f0a500;font-weight:700">${b} Belum</span>&nbsp;&nbsp; <span style="color:#e84393;font-weight:700">${l} Lewat</span> </p> <p style="margin-top:4px;font-size:11.5px"><strong>Pengesahan PK:</strong> ${sig.signed?`<span style="color:#00b894">✓ ${esc(sig.date||””)}</span>`:"Belum"}</p> </div> <div style="overflow-x:auto"> <table class="report-table"> <thead><tr><th>#</th><th>Nama</th><th>Jawatan</th><th>Fail</th><th>Tarikh</th><th>Status</th><th>PK</th></tr></thead> <tbody>${rows}</tbody> </table> </div> ${sig.notes?`<p style="margin-top:12px;font-size:12px"><strong>Catatan PK:</strong> ${esc(sig.notes)}</p>`:""} `;
openModal(“reportModal”);
};

/* ─── LOGIN / LOGOUT ─── */
window.setLoginRole=function(role){
currentLoginTab=role;
document.getElementById(“btnRolePengetua”).className=role===“pengetua”?“role-tab active”:“role-tab”;
document.getElementById(“btnRoleAdmin”).className=role===“admin”?“role-tab active”:“role-tab”;
};
window.openLogin=function(){
if(currentRole){ logout(); return; }
document.getElementById(“loginPass”).value=””;
document.getElementById(“loginError”).style.display=“none”;
setLoginRole(“pengetua”); openModal(“loginModal”);
};
window.doLogin=function(){
const pass=document.getElementById(“loginPass”).value;
const correct=currentLoginTab===“pengetua”?“1234”:“0000”;
if(pass!==correct){ document.getElementById(“loginError”).style.display=“block”; return; }
currentRole=currentLoginTab; closeModal(“loginModal”);
const label=currentRole===“pengetua”?“Pengetua”:“Admin”;
document.getElementById(“adminBtnText”).textContent=`Keluar`;
document.getElementById(“adminBtn”).classList.add(“logged-in”);
document.getElementById(“adminBar”).classList[currentRole===“admin”?“add”:“remove”]("visible");
showToast(`Selamat datang, ${label}!`,“success”);
renderCards();
};
function logout(){
currentRole=null;
document.getElementById(“adminBtnText”).textContent=“Masuk”;
document.getElementById(“adminBtn”).classList.remove(“logged-in”);
document.getElementById(“adminBar”).classList.remove(“visible”);
renderCards(); showToast(“Anda telah log keluar.”,“warning”);
}
window.logout=logout;

/* ─── BRANDING ─── */
async function uploadBrandingFile(file,type){
const safeName=file.name.replace(/[^\w.-]+/g,”_”);
const filePath=`branding/${type}/${Date.now()}_${safeName}`;
const fileRef=ref(storage,filePath);
await uploadBytes(fileRef,file);
return {url:await getDownloadURL(fileRef),path:filePath};
}
window.changeBanner=async function(e){
try{
if(currentRole!==“admin”){ showToast(“Hanya admin boleh tukar banner.”,“error”); return; }
if(!firebaseReady||!storage){ showToast(“Firebase belum sedia.”,“error”); return; }
const file=e.target.files?.[0]; if(!file) return;
showToast(“Memuat naik banner…”,“warning”);
const r=await uploadBrandingFile(file,“banner”);
if(settingsData.bannerPath){ try{ await deleteObject(ref(storage,settingsData.bannerPath)); }catch(ex){ console.warn(ex); } }
settingsData.bannerUrl=r.url; settingsData.bannerPath=r.path;
applyBrandingToUI(); await saveBranding(); showToast(“Banner dikemas kini!”,“success”);
}catch(err){ console.error(err); showToast(“Gagal simpan banner.”,“error”); }
finally{ e.target.value=””; }
};
window.changeLogo=async function(e){
try{
if(currentRole!==“admin”){ showToast(“Hanya admin boleh tukar logo.”,“error”); return; }
if(!firebaseReady||!storage){ showToast(“Firebase belum sedia.”,“error”); return; }
const file=e.target.files?.[0]; if(!file) return;
showToast(“Memuat naik logo…”,“warning”);
const r=await uploadBrandingFile(file,“logo”);
if(settingsData.logoPath){ try{ await deleteObject(ref(storage,settingsData.logoPath)); }catch(ex){ console.warn(ex); } }
settingsData.logoUrl=r.url; settingsData.logoPath=r.path;
applyBrandingToUI(); await saveBranding(); showToast(“Logo dikemas kini!”,“success”);
}catch(err){ console.error(err); showToast(“Gagal simpan logo.”,“error”); }
finally{ e.target.value=””; }
};

/* ─── INIT ─── */
window.addEventListener(“resize”, updateDonut);
populateStaffSelect();
updateWeekDisplay();
renderCards();
updateDonut();
updatePrincipalSection();
initFirebase();
</script>

</body>
</html>