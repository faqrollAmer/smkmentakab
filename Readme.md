<!DOCTYPE html>
<html lang="ms">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
  <title>Senarai Penghantaran Tugasan Harian – SMK Mentakab (Firebase)</title>

  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Merriweather:wght@400;700&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

  <style>
    :root{
      --navy:#0f2444;
      --navy-mid:#1a3a6e;
      --navy-light:#2a5298;
      --gold:#c9a84c;
      --gold-light:#f0c96a;
      --gold-pale:#fdf6e3;
      --emerald:#1a7a4a;
      --emerald-light:#e6f7ef;
      --crimson:#c0392b;
      --crimson-light:#fdecea;
      --amber:#d4820a;
      --amber-light:#fff3e0;
      --slate:#64748b;
      --slate-light:#f1f5f9;
      --bg:#f0f4f8;
      --border:#dbe4ef;
      --shadow-sm:0 2px 8px rgba(15,36,68,0.08);
      --shadow-md:0 4px 20px rgba(15,36,68,0.12);
      --shadow-lg:0 8px 40px rgba(15,36,68,0.16);
      --radius:12px;
      --radius-sm:8px;
      --transition:all .2s ease;
    }

    *,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
    html,body{width:100%;overflow-x:hidden}
    body{
      font-family:'Plus Jakarta Sans',sans-serif;
      background:var(--bg);
      color:#1e293b;
      min-height:100vh;
      font-size:14px;
      -webkit-tap-highlight-color:transparent;
    }
    img,canvas,iframe{max-width:100%}
    button,input,select,textarea{font:inherit}

    .site-header{
      background:linear-gradient(135deg,var(--navy) 0%,var(--navy-mid) 60%,var(--navy-light) 100%);
      color:#fff;
      position:sticky;top:0;z-index:100;
      box-shadow:var(--shadow-lg);
    }
    .header-inner{
      display:flex;align-items:center;justify-content:space-between;
      padding:14px 18px;gap:14px;flex-wrap:wrap;
    }
    .header-left{
      display:flex;align-items:center;gap:12px;min-width:0;flex:1 1 320px;
    }
    .school-logo{
      width:52px;height:52px;border-radius:50%;
      border:2.5px solid var(--gold);
      background:#fff;display:flex;align-items:center;justify-content:center;
      color:var(--navy);font-size:20px;font-weight:800;overflow:hidden;flex-shrink:0;
    }
    .school-logo img{width:100%;height:100%;object-fit:cover;border-radius:50%}
    .school-info{min-width:0}
    .school-info h1{
      font-family:'Merriweather',serif;
      font-size:15px;font-weight:700;line-height:1.3;word-break:break-word;
    }
    .school-info p{font-size:11.5px;opacity:.82;margin-top:2px;line-height:1.4}

    .header-right{display:flex;align-items:center;gap:8px;flex-wrap:wrap;justify-content:flex-end}
    .btn-icon{
      width:42px;height:42px;min-width:42px;border-radius:50%;
      background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.25);
      color:#fff;cursor:pointer;display:flex;align-items:center;justify-content:center;
      font-size:15px;transition:var(--transition);position:relative;
    }
    .btn-icon:hover{background:rgba(255,255,255,.28)}
    .notif-badge{
      position:absolute;top:-3px;right:-3px;background:#ef4444;color:#fff;border-radius:50%;
      min-width:18px;height:18px;padding:0 4px;font-size:9px;font-weight:700;
      display:flex;align-items:center;justify-content:center;border:1.5px solid var(--navy);
    }

    .btn-admin{
      min-height:42px;padding:8px 14px;background:rgba(255,255,255,.15);
      border:1px solid rgba(255,255,255,.3);color:#fff;border-radius:20px;
      font-size:12px;font-weight:600;cursor:pointer;display:flex;align-items:center;gap:6px;
      transition:var(--transition);white-space:nowrap;
    }
    .btn-admin:hover{background:rgba(255,255,255,.28)}
    .btn-admin.logged-in{background:rgba(201,168,76,.35);border-color:var(--gold)}

    .login-staff-wrap{
      display:flex;align-items:center;gap:8px;flex-wrap:wrap;
      background:rgba(255,255,255,.12);padding:6px 8px;border-radius:12px;
      border:1px solid rgba(255,255,255,.18);
    }
    .login-staff-wrap label{font-size:11px;font-weight:700;color:#fff;opacity:.9}
    .staff-select{
      min-height:36px;padding:7px 10px;border-radius:10px;border:none;outline:none;
      background:#fff;color:#1e293b;min-width:160px;max-width:240px;
    }

    .banner-section{
      width:100%;min-height:88px;
      background:linear-gradient(135deg,var(--navy-mid) 0%,#1e4d8c 50%,var(--navy-light) 100%);
      position:relative;overflow:hidden;display:flex;align-items:center;justify-content:center;
      padding:16px 12px;
    }
    .banner-section img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;opacity:.4}
    .banner-text{position:relative;z-index:1;text-align:center;color:#fff;padding:0 8px}
    .banner-text h2{font-family:'Merriweather',serif;font-size:17px;font-weight:700;line-height:1.3}
    .banner-text p{font-size:12px;opacity:.85;margin-top:4px;line-height:1.4}

    .admin-bar{
      display:none;background:#fff8e6;border-bottom:2px solid var(--gold);
      padding:10px 16px;align-items:center;gap:10px;flex-wrap:wrap;
    }
    .admin-bar.visible{display:flex}
    .admin-bar-label{font-size:12px;font-weight:700;color:var(--amber);display:flex;align-items:center;gap:6px}

    .week-bar{
      background:#fff;border-bottom:2px solid var(--border);padding:10px 16px;
      display:grid;grid-template-columns:1fr auto;gap:10px 12px;align-items:center;
      box-shadow:var(--shadow-sm);
    }
    .week-nav{display:flex;align-items:center;gap:10px;min-width:0;flex-wrap:wrap}
    .week-nav button{
      width:38px;height:38px;min-width:38px;border-radius:var(--radius-sm);
      background:var(--slate-light);border:1px solid var(--border);color:var(--navy);
      cursor:pointer;display:flex;align-items:center;justify-content:center;transition:var(--transition);
    }
    .week-nav button:hover{background:var(--navy);color:#fff}
    .week-label{
      font-size:13.5px;font-weight:700;color:var(--navy);padding:6px 14px;
      background:var(--gold-pale);border:1px solid var(--gold);border-radius:20px;white-space:nowrap;
    }
    .week-dates{grid-column:1/-1;font-size:12px;color:var(--slate);font-weight:500;line-height:1.5}
    .week-bar-right{display:flex;gap:8px;align-items:center;flex-wrap:wrap;justify-content:flex-end}

    .main-wrap{max-width:1400px;margin:0 auto;padding:18px 12px 36px}

    .stats-grid{
      display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:14px;margin-bottom:20px;
    }
    .stat-card{
      background:#fff;border-radius:var(--radius);padding:16px 18px;box-shadow:var(--shadow-sm);
      border:1px solid var(--border);display:flex;align-items:center;gap:12px;min-width:0;
    }
    .stat-icon{
      width:46px;height:46px;border-radius:var(--radius-sm);display:flex;align-items:center;justify-content:center;
      font-size:20px;flex-shrink:0;
    }
    .stat-card.total .stat-icon{background:#e8f0fe;color:var(--navy-light)}
    .stat-card.disahkan .stat-icon{background:var(--emerald-light);color:var(--emerald)}
    .stat-card.belum .stat-icon{background:var(--amber-light);color:var(--amber)}
    .stat-card.lewat .stat-icon{background:var(--crimson-light);color:var(--crimson)}
    .stat-info p{font-size:11px;color:var(--slate);font-weight:500;text-transform:uppercase;letter-spacing:.5px}
    .stat-info h3{font-size:28px;font-weight:800;margin-top:2px;line-height:1.1}
    .stat-card.total .stat-info h3{color:var(--navy-light)}
    .stat-card.disahkan .stat-info h3{color:var(--emerald)}
    .stat-card.belum .stat-info h3{color:var(--amber)}
    .stat-card.lewat .stat-info h3{color:var(--crimson)}

    .panel{
      background:#fff;border-radius:var(--radius);box-shadow:var(--shadow-sm);
      border:1px solid var(--border);overflow:hidden;margin-bottom:18px;
    }
    .panel-header{
      padding:14px 16px;border-bottom:1px solid var(--border);
      display:flex;align-items:center;justify-content:space-between;gap:10px;flex-wrap:wrap;
      background:linear-gradient(90deg,#f8fafd,#fff);
    }
    .panel-title{
      font-size:14px;font-weight:700;color:var(--navy);display:flex;align-items:center;gap:8px;
    }
    .panel-title i{color:var(--navy-light)}

    .charts-row{display:grid;grid-template-columns:300px 1fr;gap:16px;margin-bottom:18px}
    .pie-container{display:flex;flex-direction:column;align-items:center;padding:18px 14px}
    #pieChart{width:180px;height:180px;max-width:100%}
    .pie-legend{margin-top:14px;width:100%}
    .pie-legend-item{display:flex;align-items:center;gap:8px;padding:5px 0;font-size:12.5px;line-height:1.4}
    .pie-dot{width:11px;height:11px;border-radius:50%;flex-shrink:0}
    .pie-legend-item span:last-child{margin-left:auto;font-weight:700}

    .filters-row{
      display:grid;grid-template-columns:minmax(180px,1.4fr) minmax(160px,1fr) minmax(160px,1fr) auto;
      gap:8px;align-items:center;padding:12px 16px;
    }
    .filter-input,.filter-select,.form-input,.semakan-input,.principal-notes{
      width:100%;padding:10px 12px;border:1px solid var(--border);
      border-radius:var(--radius-sm);background:var(--slate-light);outline:none;transition:var(--transition);
      color:#1e293b;
    }
    .filter-input:focus,.filter-select:focus,.form-input:focus,.semakan-input:focus,.principal-notes:focus{
      border-color:var(--navy-light);background:#fff;box-shadow:0 0 0 3px rgba(42,82,152,.08);
    }

    .table-wrap{overflow-x:auto;-webkit-overflow-scrolling:touch;width:100%}
    table{width:100%;min-width:1280px;border-collapse:collapse;font-size:13px}
    thead th{
      background:linear-gradient(180deg,var(--navy),var(--navy-mid));
      color:#fff;padding:11px 12px;text-align:left;font-weight:600;font-size:11.5px;
      white-space:nowrap;border-right:1px solid rgba(255,255,255,.1);
    }
    tbody tr{border-bottom:1px solid var(--border)}
    tbody tr:hover{background:#f7f9fc}
    tbody td{padding:10px 12px;vertical-align:middle;white-space:nowrap}
    .td-wrap{white-space:normal;min-width:150px;line-height:1.45}
    .bil-cell{font-weight:700;color:var(--slate);font-size:12px}
    .nama-cell{font-weight:600;color:var(--navy)}

    .kat-badge{
      display:inline-block;padding:4px 9px;border-radius:20px;font-size:10.5px;font-weight:600;white-space:nowrap;
    }
    .kat-1{background:#e8f0fe;color:#1a56db}
    .kat-2{background:#fce8f3;color:#9b1c7b}
    .kat-3{background:#fef3c7;color:#92400e}
    .kat-4{background:#d1fae5;color:#065f46}

    .status-badge{
      display:inline-flex;align-items:center;gap:5px;padding:4px 10px;border-radius:20px;
      font-size:11.5px;font-weight:600;white-space:nowrap;
    }
    .status-disahkan{background:var(--emerald-light);color:var(--emerald)}
    .status-belum{background:var(--amber-light);color:var(--amber)}
    .status-lewat{background:var(--crimson-light);color:var(--crimson)}

    .file-type-badge{
      display:inline-block;padding:3px 8px;border-radius:4px;font-size:10.5px;font-weight:700;
      letter-spacing:.5px;text-transform:uppercase;
    }
    .ft-pdf{background:#fee2e2;color:#b91c1c}
    .ft-img{background:#dbeafe;color:#1d4ed8}
    .ft-doc{background:#e0f2fe;color:#0369a1}

    .action-group{display:flex;gap:5px;align-items:center;flex-wrap:wrap}
    .btn-sm{
      min-height:38px;padding:7px 11px;border-radius:var(--radius-sm);font-size:11.5px;font-weight:600;
      cursor:pointer;border:none;display:inline-flex;align-items:center;justify-content:center;gap:5px;
      transition:var(--transition);white-space:nowrap;text-align:center;
    }
    .btn-primary{background:var(--navy-light);color:#fff}
    .btn-primary:hover{background:var(--navy)}
    .btn-success{background:var(--emerald);color:#fff}
    .btn-success:hover{background:#155d38}
    .btn-danger{background:var(--crimson);color:#fff}
    .btn-danger:hover{background:#a93226}
    .btn-secondary{background:var(--slate-light);color:var(--navy);border:1px solid var(--border)}
    .btn-secondary:hover{background:var(--border)}
    .btn-gold{background:var(--gold);color:var(--navy)}
    .btn-gold:hover{background:var(--gold-light)}

    .upload-label{
      min-height:38px;padding:7px 11px;border-radius:var(--radius-sm);font-size:11.5px;font-weight:600;
      cursor:pointer;background:var(--navy-light);color:#fff;display:inline-flex;align-items:center;justify-content:center;
      gap:5px;transition:var(--transition);white-space:nowrap;
    }
    .upload-label:hover{background:var(--navy)}
    input[type="file"]{display:none}

    .pengesahan-cell{display:flex;flex-direction:column;gap:4px;min-width:160px}
    .pengesahan-badge{
      display:inline-flex;align-items:center;gap:5px;padding:3px 9px;border-radius:20px;
      font-size:11px;font-weight:600;width:fit-content;
    }
    .pengesahan-disahkan{background:var(--emerald-light);color:var(--emerald)}
    .pengesahan-pending{background:var(--slate-light);color:var(--slate)}
    .catatan-text{
      font-size:11px;color:var(--slate);font-style:italic;max-width:150px;white-space:normal;line-height:1.45;
    }

    .principal-header{display:flex;align-items:center;gap:14px;margin-bottom:16px}
    .principal-avatar{
      width:52px;height:52px;border-radius:50%;background:linear-gradient(135deg,var(--navy),var(--navy-light));
      display:flex;align-items:center;justify-content:center;color:#fff;font-size:20px;flex-shrink:0;
      border:2px solid var(--gold);
    }
    .principal-info h3{font-size:15px;font-weight:700;color:var(--navy);line-height:1.4}
    .principal-info p{font-size:12px;color:var(--slate)}
    .principal-stamp{
      border:2px dashed var(--gold);border-radius:var(--radius);padding:16px 20px;text-align:center;
      background:rgba(255,255,255,.7);min-height:80px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px;
    }
    .principal-stamp.signed{border-style:solid;border-color:var(--emerald);background:var(--emerald-light)}
    .stamp-date{font-size:11.5px;color:var(--slate)}
    .stamp-name{font-size:13px;font-weight:700;color:var(--navy)}
    .stamp-sign{font-size:22px;font-weight:800;color:var(--emerald);font-family:'Merriweather',serif}
    .principal-form{display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-top:14px}
    .principal-notes{resize:vertical;min-height:72px;grid-column:1/-1}

    .modal-overlay{
      display:none;position:fixed;inset:0;background:rgba(10,20,40,.65);z-index:1000;
      align-items:center;justify-content:center;padding:16px;backdrop-filter:blur(4px);
    }
    .modal-overlay.open{display:flex}
    .modal{
      background:#fff;border-radius:16px;box-shadow:var(--shadow-lg);width:100%;max-width:440px;
      overflow:hidden;max-height:calc(100vh - 32px);display:flex;flex-direction:column;
    }
    .modal-header{
      background:linear-gradient(135deg,var(--navy),var(--navy-mid));color:#fff;
      padding:18px 20px;display:flex;align-items:center;justify-content:space-between;gap:10px;
    }
    .modal-header h3{font-size:15px;font-weight:700;display:flex;align-items:center;gap:8px}
    .modal-close{
      background:rgba(255,255,255,.15);border:none;color:#fff;width:32px;height:32px;border-radius:50%;
      cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;
    }
    .modal-body{padding:20px;overflow-y:auto}
    .modal-footer{
      padding:14px 20px;border-top:1px solid var(--border);
      display:flex;gap:10px;justify-content:flex-end;flex-wrap:wrap;background:#fff;
    }

    .notif-panel{
      display:none;position:absolute;top:50px;right:0;
      width:min(260px,calc(100vw - 20px));
      background:#fff;border-radius:10px;box-shadow:var(--shadow-md);
      border:1px solid var(--border);z-index:200;overflow:hidden;
    }
    .notif-panel.open{display:block}
    .notif-panel-header{padding:12px 14px;background:var(--navy);color:#fff;font-size:13px;font-weight:700}
    .notif-list{max-height:200px;overflow-y:auto}
    .notif-item{
      padding:10px 12px;border-bottom:1px solid var(--border);font-size:12px;
      display:flex;align-items:flex-start;gap:8px;line-height:1.4;
    }
    .notif-item:last-child{border-bottom:none}
    .notif-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;margin-top:5px}
    .notif-dot.red{background:var(--crimson)}
    .notif-dot.amber{background:var(--amber)}
    .notif-dot.green{background:var(--emerald)}
    .notif-wrapper{position:relative}

    .preview-container{
      width:100%;min-height:280px;display:flex;align-items:center;justify-content:center;
      background:#f0f4f8;border-radius:var(--radius-sm);overflow:hidden;
    }
    .preview-container img{max-width:100%;max-height:70vh;object-fit:contain}
    .preview-container iframe{width:100%;height:70vh;min-height:320px;border:none;background:#fff}
    .preview-placeholder{text-align:center;color:var(--slate);padding:40px 20px;line-height:1.5}

    .report-table{width:100%;border-collapse:collapse;font-size:12.5px;margin-top:10px}
    .report-table th{background:var(--navy);color:#fff;padding:8px 10px;text-align:left}
    .report-table td{padding:7px 10px;border-bottom:1px solid var(--border);line-height:1.45}

    .semakan-cell{min-width:140px}
    .semakan-input{min-height:64px;resize:vertical;font-size:12px}
    .empty-cell{color:var(--slate);font-style:italic;font-size:12px}

    .toast-container{
      position:fixed;bottom:20px;right:16px;left:16px;z-index:9999;
      display:flex;flex-direction:column;gap:8px;align-items:flex-end;pointer-events:none;
    }
    .toast{
      background:var(--navy);color:#fff;padding:10px 16px;border-radius:var(--radius-sm);
      font-size:13px;font-weight:500;box-shadow:var(--shadow-md);display:flex;align-items:center;gap:8px;
      min-width:min(280px,100%);max-width:100%;pointer-events:auto;
    }
    .toast.success{background:var(--emerald)}
    .toast.error{background:var(--crimson)}
    .toast.warning{background:var(--amber)}

    .autosave-indicator{
      position:fixed;bottom:84px;right:16px;background:var(--emerald);color:#fff;padding:7px 12px;
      border-radius:20px;font-size:11.5px;font-weight:600;display:none;align-items:center;gap:5px;
      z-index:500;box-shadow:var(--shadow-sm);max-width:calc(100vw - 32px);
    }
    .autosave-indicator.visible{display:flex}

    .firebase-status{
      margin:8px 0 0;font-size:12px;color:var(--slate);display:flex;align-items:center;gap:8px;flex-wrap:wrap;
    }
    .firebase-pill{
      display:inline-flex;align-items:center;gap:6px;padding:5px 10px;border-radius:999px;
      font-size:11px;font-weight:700;background:#eef4ff;color:var(--navy-light);
    }

    @media (max-width:1100px){
      .stats-grid{grid-template-columns:repeat(2,minmax(0,1fr))}
      .charts-row{grid-template-columns:1fr}
      .filters-row{grid-template-columns:1fr 1fr}
    }
    @media (max-width:768px){
      .header-inner{padding:12px 14px}
      .header-right{width:100%;justify-content:flex-start}
      .school-info h1{font-size:13.5px}
      .week-bar{grid-template-columns:1fr}
      .week-bar-right{justify-content:flex-start}
      .main-wrap{padding:14px 10px 28px}
      .filters-row{grid-template-columns:1fr;padding:12px 14px}
      .principal-form{grid-template-columns:1fr}
      .modal-body{padding:16px}
      .modal-footer{padding:12px 16px}
      .login-staff-wrap{width:100%}
      .staff-select{max-width:none;width:100%}
    }
    @media (max-width:600px){
      .school-info p{display:none}
      .btn-admin span{display:none}
      .btn-admin{width:42px;min-width:42px;padding:0;justify-content:center;border-radius:50%}
      .stats-grid{grid-template-columns:1fr}
      .stat-card{padding:14px 16px}
      .stat-info h3{font-size:24px}
      .banner-text h2{font-size:15px}
      .banner-text p{font-size:11.5px}
      #pieChart{width:160px;height:160px}
      .toast-container{left:10px;right:10px;bottom:14px}
      .toast{width:100%}
      .autosave-indicator{right:10px;bottom:72px}
    }
  </style>
</head>
<body>
  <div class="toast-container" id="toastContainer"></div>
  <div class="autosave-indicator" id="autosaveIndicator">
    <i class="fas fa-check-circle"></i> Data disimpan
  </div>

  <header class="site-header">
    <div class="header-inner">
      <div class="header-left">
        <div class="school-logo">
          <span id="logoText">SMK</span>
          <img id="logoImg" src="" alt="Logo Sekolah" style="display:none">
        </div>
        <div class="school-info">
          <h1>Sekolah Menengah Kebangsaan Mentakab</h1>
          <p><i class="fas fa-user-tie" style="font-size:10px"></i> Pengetua: Hajah Aniza Binti Baharuddin</p>
        </div>
      </div>

      <div class="header-right">
        <div class="login-staff-wrap">
          <label for="staffSelect">Staf</label>
          <select id="staffSelect" class="staff-select" onchange="selectStaffLogin(this.value)">
            <option value="">Pilih nama staf untuk upload</option>
          </select>
        </div>

        <div class="notif-wrapper">
          <button class="btn-icon" type="button" onclick="toggleNotif()" title="Notifikasi">
            <i class="fas fa-bell"></i>
            <span class="notif-badge" id="notifBadge">0</span>
          </button>
          <div class="notif-panel" id="notifPanel">
            <div class="notif-panel-header"><i class="fas fa-bell"></i> Notifikasi Ringkas</div>
            <div class="notif-list" id="notifList"></div>
          </div>
        </div>

        <button class="btn-icon" type="button" onclick="openReport()" title="Laporan">
          <i class="fas fa-chart-bar"></i>
        </button>

        <button class="btn-admin" id="adminBtn" type="button" onclick="openLogin()">
          <i class="fas fa-shield-alt"></i>
          <span id="adminBtnText">Log Masuk</span>
        </button>
      </div>
    </div>
  </header>

  <div class="admin-bar" id="adminBar">
    <span class="admin-bar-label"><i class="fas fa-tools"></i> Mod Admin Aktif</span>

    <label class="btn-sm btn-secondary" style="cursor:pointer">
      <i class="fas fa-image"></i> Tukar Banner
      <input type="file" id="bannerUpload" accept="image/*" onchange="changeBanner(event)">
    </label>

    <label class="btn-sm btn-secondary" style="cursor:pointer">
      <i class="fas fa-school"></i> Tukar Logo
      <input type="file" id="logoUpload" accept="image/*" onchange="changeLogo(event)">
    </label>

    <button class="btn-sm btn-danger" type="button" onclick="logout()">
      <i class="fas fa-sign-out-alt"></i> Log Keluar
    </button>
  </div>

  <div class="banner-section" id="bannerSection">
    <img id="bannerImg" src="" alt="" style="display:none">
    <div class="banner-text">
      <h2>SENARAI PENGHANTARAN TUGASAN HARIAN</h2>
      <p>Sistem Pengurusan Rekod Mingguan – Staf Sokongan</p>
      <div class="firebase-status">
        <span class="firebase-pill"><i class="fas fa-cloud"></i> Firebase Realtime Aktif</span>
        <span id="firebaseStatusText">Menyambung...</span>
      </div>
    </div>
  </div>

  <div class="week-bar">
    <div class="week-nav">
      <button type="button" onclick="prevWeek()" title="Minggu Lepas"><i class="fas fa-chevron-left"></i></button>
      <span class="week-label" id="weekLabel">Minggu 1</span>
      <button type="button" onclick="nextWeek()" title="Minggu Akan Datang"><i class="fas fa-chevron-right"></i></button>
    </div>

    <div class="week-bar-right">
      <button class="btn-sm btn-primary" type="button" onclick="goToCurrentWeek()">
        <i class="fas fa-calendar-check"></i> Minggu Semasa
      </button>
      <button class="btn-sm btn-secondary" type="button" onclick="openReport()">
        <i class="fas fa-print"></i> Laporan
      </button>
    </div>

    <div class="week-dates" id="weekDates">Isnin – Jumaat</div>
  </div>

  <div class="main-wrap">
    <div class="stats-grid">
      <div class="stat-card total">
        <div class="stat-icon"><i class="fas fa-users"></i></div>
        <div class="stat-info"><p>Jumlah Staf</p><h3 id="statTotal">16</h3></div>
      </div>
      <div class="stat-card disahkan">
        <div class="stat-icon"><i class="fas fa-check-circle"></i></div>
        <div class="stat-info"><p>Disahkan</p><h3 id="statDisahkan">0</h3></div>
      </div>
      <div class="stat-card belum">
        <div class="stat-icon"><i class="fas fa-clock"></i></div>
        <div class="stat-info"><p>Belum Hantar</p><h3 id="statBelum">16</h3></div>
      </div>
      <div class="stat-card lewat">
        <div class="stat-icon"><i class="fas fa-exclamation-triangle"></i></div>
        <div class="stat-info"><p>Lewat</p><h3 id="statLewat">0</h3></div>
      </div>
    </div>

    <div class="charts-row">
      <div class="panel">
        <div class="panel-header">
          <span class="panel-title"><i class="fas fa-chart-pie"></i> Carta Pai Status</span>
        </div>
        <div class="pie-container">
          <canvas id="pieChart" width="180" height="180"></canvas>
          <div class="pie-legend">
            <div class="pie-legend-item"><div class="pie-dot" style="background:#1a7a4a"></div>Disahkan <span id="leg1">0</span></div>
            <div class="pie-legend-item"><div class="pie-dot" style="background:#d4820a"></div>Belum Hantar <span id="leg2">16</span></div>
            <div class="pie-legend-item"><div class="pie-dot" style="background:#c0392b"></div>Lewat <span id="leg3">0</span></div>
          </div>
        </div>
      </div>

      <div class="panel">
        <div class="panel-header">
          <span class="panel-title"><i class="fas fa-stamp"></i> Pengesahan Pengetua</span>
          <span id="principalAccessNote" style="font-size:11.5px;color:var(--slate)">
            <i class="fas fa-lock"></i> Log masuk sebagai Pengetua untuk mengesahkan
          </span>
        </div>

        <div style="padding:18px">
          <div class="principal-header">
            <div class="principal-avatar"><i class="fas fa-user-tie"></i></div>
            <div class="principal-info">
              <h3>Hajah Aniza Binti Baharuddin</h3>
              <p>Pengetua – SMK Mentakab</p>
            </div>
          </div>

          <div class="principal-stamp" id="principalStamp">
            <i class="fas fa-pen-to-square" style="font-size:24px;color:var(--slate);opacity:.4"></i>
            <p style="font-size:12.5px;color:var(--slate)">Belum disahkan</p>
          </div>

          <div class="principal-form" id="principalForm" style="display:none">
            <div>
              <label style="font-size:12px;font-weight:600;color:var(--navy);display:block;margin-bottom:5px">Tarikh Semakan</label>
              <input type="date" class="form-input" id="principalDate">
            </div>
            <div style="display:flex;align-items:flex-end">
              <button class="btn-sm btn-success" type="button" style="width:100%" onclick="signPrincipal()">
                <i class="fas fa-signature"></i> Sahkan Rekod Minggu Ini
              </button>
            </div>
            <textarea class="principal-notes" id="principalNotes" placeholder="Catatan / ulasan pengetua..."></textarea>
          </div>

          <div id="principalSignedInfo" style="display:none;margin-top:12px;padding:10px 14px;background:var(--emerald-light);border-radius:var(--radius-sm);font-size:12.5px;color:var(--emerald)">
            <i class="fas fa-check-circle"></i> <strong>Telah Disahkan</strong>
            <div id="principalSignedDetails" style="margin-top:4px;font-size:11.5px;color:#2d7a4a"></div>
          </div>
        </div>
      </div>
    </div>

    <div class="panel">
      <div class="panel-header">
        <span class="panel-title"><i class="fas fa-table"></i> Jadual Penghantaran Tugasan</span>
        <span style="font-size:12px;color:var(--slate)" id="tableSubtitle"></span>
      </div>

      <div class="filters-row">
        <input type="text" class="filter-input" id="searchInput" placeholder="Cari nama staf..." oninput="applyFilters()">

        <select class="filter-select" id="filterKat" onchange="applyFilters()">
          <option value="">Semua Kategori</option>
          <option value="1">Pembantu Makmal</option>
          <option value="2">Pembantu Pengurusan Murid</option>
          <option value="3">Pembantu Tadbir</option>
          <option value="4">Pembantu Khidmat Am</option>
        </select>

        <select class="filter-select" id="filterStatus" onchange="applyFilters()">
          <option value="">Semua Status</option>
          <option value="Disahkan">Disahkan</option>
          <option value="Belum Hantar">Belum Hantar</option>
          <option value="Lewat">Lewat</option>
        </select>

        <span style="font-size:12px;color:var(--slate);margin-left:auto" id="filterCount"></span>
      </div>

      <div class="table-wrap">
        <table>
          <thead>
            <tr>
              <th>Bil</th>
              <th>Nama Staf</th>
              <th>Kategori</th>
              <th>Minggu / Tarikh</th>
              <th>Muat Naik Tugasan</th>
              <th>Jenis Fail</th>
              <th>Nama Fail</th>
              <th>Tarikh Hantar</th>
              <th>Status</th>
              <th>Tindakan</th>
              <th>Semakan Pentadbir</th>
              <th>Pengesahan Pengetua</th>
            </tr>
          </thead>
          <tbody id="tableBody"></tbody>
        </table>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="loginModal">
    <div class="modal">
      <div class="modal-header">
        <h3><i class="fas fa-shield-alt"></i> Log Masuk Pentadbir</h3>
        <button class="modal-close" type="button" onclick="closeModal('loginModal')"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body">
        <div style="display:flex;gap:8px;margin-bottom:18px">
          <button class="btn-sm btn-primary" type="button" style="flex:1" onclick="setLoginRole('pengetua')" id="btnRolePengetua">Pengetua</button>
          <button class="btn-sm btn-secondary" type="button" style="flex:1" onclick="setLoginRole('admin')" id="btnRoleAdmin">Admin</button>
        </div>

        <div class="form-input" style="margin-bottom:12px;background:#f8fafc">
          Login ini hanya untuk Admin / Pengetua.
        </div>

        <div style="margin-bottom:14px">
          <label style="display:block;font-size:12.5px;font-weight:600;color:var(--navy);margin-bottom:5px">Kata Laluan</label>
          <input type="password" class="form-input" id="loginPass" placeholder="Masukkan kata laluan..." onkeydown="if(event.key==='Enter') doLogin()">
        </div>

        <p id="loginError" style="display:none;color:var(--crimson);font-size:12.5px">
          <i class="fas fa-exclamation-circle"></i> Kata laluan tidak sah.
        </p>
      </div>
      <div class="modal-footer">
        <button class="btn-sm btn-secondary" type="button" onclick="closeModal('loginModal')">Batal</button>
        <button class="btn-sm btn-primary" type="button" onclick="doLogin()"><i class="fas fa-sign-in-alt"></i> Log Masuk</button>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="confirmModal">
    <div class="modal" style="max-width:380px">
      <div class="modal-header">
        <h3><i class="fas fa-exclamation-triangle"></i> Pengesahan Pembatalan</h3>
        <button class="modal-close" type="button" onclick="closeModal('confirmModal')"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body">
        <p style="text-align:center;font-size:14px;line-height:1.6">
          Adakah anda pasti ingin <strong>membatalkan penghantaran</strong> ini?
        </p>
      </div>
      <div class="modal-footer">
        <button class="btn-sm btn-secondary" type="button" onclick="closeModal('confirmModal')">Tidak</button>
        <button class="btn-sm btn-danger" type="button" onclick="confirmCancelSubmission()"><i class="fas fa-trash"></i> Ya, Batalkan</button>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="previewModal">
    <div class="modal" style="max-width:700px">
      <div class="modal-header">
        <h3><i class="fas fa-eye"></i> Pratonton Fail</h3>
        <button class="modal-close" type="button" onclick="closeModal('previewModal')"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body" style="padding:16px">
        <p id="previewFileName" style="font-size:13px;font-weight:600;margin-bottom:10px;color:var(--navy)"></p>
        <div class="preview-container" id="previewContainer"></div>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="reportModal">
    <div class="modal" style="max-width:720px">
      <div class="modal-header">
        <h3><i class="fas fa-file-alt"></i> Laporan Penghantaran Mingguan</h3>
        <button class="modal-close" type="button" onclick="closeModal('reportModal')"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body" id="reportBody"></div>
      <div class="modal-footer">
        <button class="btn-sm btn-secondary" type="button" onclick="closeModal('reportModal')">Tutup</button>
        <button class="btn-sm btn-primary" type="button" onclick="window.print()"><i class="fas fa-print"></i> Cetak</button>
      </div>
    </div>
  </div>

  <div class="modal-overlay" id="pengesahanModal">
    <div class="modal" style="max-width:420px">
      <div class="modal-header">
        <h3><i class="fas fa-stamp"></i> Pengesahan Pengetua</h3>
        <button class="modal-close" type="button" onclick="closeModal('pengesahanModal')"><i class="fas fa-times"></i></button>
      </div>
      <div class="modal-body">
        <p style="font-size:13px;margin-bottom:12px;color:var(--slate)">
          Pengesahan bagi staf: <strong id="pengesahanStaffName"></strong>
        </p>
        <div>
          <label style="display:block;font-size:12.5px;font-weight:600;color:var(--navy);margin-bottom:5px">Catatan / Ulasan</label>
          <textarea class="form-input" id="pengesahanCatatan" placeholder="Masukkan catatan (jika ada)..." style="min-height:80px;resize:vertical"></textarea>
        </div>
        <div id="pengesahanError" style="display:none;color:var(--crimson);font-size:12.5px;margin-top:6px">
          <i class="fas fa-lock"></i> Hanya Pengetua yang boleh mengesahkan.
        </div>
      </div>
      <div class="modal-footer">
        <button class="btn-sm btn-secondary" type="button" onclick="closeModal('pengesahanModal')">Batal</button>
        <button class="btn-sm btn-success" type="button" onclick="submitPengesahan()"><i class="fas fa-check"></i> Sahkan</button>
      </div>
    </div>
  </div>

  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-app.js";
    import { getAuth, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-auth.js";
    import {
      getFirestore, doc, setDoc, getDoc, deleteDoc, onSnapshot,
      serverTimestamp
    } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-firestore.js";
    import {
      getStorage, ref, uploadBytes, getDownloadURL, deleteObject
    } from "https://www.gstatic.com/firebasejs/10.14.1/firebase-storage.js";

    const STAFF_LIST = [
      { id:1,  nama:"'Afifah Binti Abdul Aziz",         kat:1 },
      { id:2,  nama:"Ida Zarina Binti Idris",           kat:1 },
      { id:3,  nama:"Azian Binti Mohamad",              kat:1 },
      { id:4,  nama:"Fatimah Binti Latiff",             kat:1 },
      { id:5,  nama:"Zainun Binti Mohamed Ramthan",     kat:1 },
      { id:6,  nama:"Nor'aini Binti Md Yusoff",         kat:1 },
      { id:7,  nama:"Fakarullah Amer Bin Zainal Abidin",kat:1 },
      { id:8,  nama:"Abdul Azam Bin Mohamed",           kat:1 },
      { id:9,  nama:"Nor Faiza Binti Mustaffa Kamal",   kat:2 },
      { id:10, nama:"Wan Azlena Binti Wan Deraman",     kat:2 },
      { id:11, nama:"Mohd Faizal Bin Zainal",           kat:2 },
      { id:12, nama:"Juhaida Binti Abd Rasid",          kat:3 },
      { id:13, nama:"Junainah Binti Hassan",            kat:3 },
      { id:14, nama:"Rafidah Binti Sidek",              kat:3 },
      { id:15, nama:"Muhammad Fahmi Bin Hamidin",       kat:4 },
      { id:16, nama:"Nursyaza Aina Binti Mohd Adaha",   kat:4 }
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

    const app = initializeApp(firebaseConfig);
    const auth = getAuth(app);
    const db = getFirestore(app);
    const storage = getStorage(app);

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
      bannerData: null,
      logoData: null
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
      const startOfYear = new Date(mon.getFullYear(), 0, 1);
      const dayOfYear = Math.floor((mon - startOfYear) / 86400000);
      return Math.ceil((dayOfYear + startOfYear.getDay() + 1) / 7);
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

    async function initFirebase(){
      try{
        await signInAnonymously(auth);
      }catch(err){
        console.error(err);
        setFirebaseStatus("Gagal sambung Firebase");
        showToast("Gagal sambung Firebase. Semak config.", "error");
      }

      onAuthStateChanged(auth, user => {
        if(user){
          firebaseUid = user.uid;
          firebaseReady = true;
          setFirebaseStatus("Tersambung");
          subscribeSettings();
          subscribeWeekData();
        }
      });
    }

    function subscribeSettings(){
      if(unsettings) unsettings();

      const settingsRef = doc(db, "systemSettings", "branding");
      unsettings = onSnapshot(settingsRef, snap => {
        settingsData = snap.exists() ? snap.data() : { bannerData:null, logoData:null };

        if(settingsData.bannerData){
          const img = document.getElementById("bannerImg");
          img.src = settingsData.bannerData;
          img.style.display = "block";
        }

        if(settingsData.logoData){
          document.getElementById("logoText").style.display = "none";
          const img = document.getElementById("logoImg");
          img.src = settingsData.logoData;
          img.style.display = "block";
        }
      }, err => {
        console.error(err);
      });
    }

    function subscribeWeekData(){
      if(!firebaseReady) return;

      const weekKey = getWeekKey();

      if(unsubmissions) unsubmissions();
      if(unweeksig) unweeksig();

      const submissionsRef = doc(db, "weeklySubmissions", weekKey);
      unsubmissions = onSnapshot(submissionsRef, snap => {
        const data = snap.exists() ? snap.data() : { records:{} };
        submissions[weekKey] = data.records || {};
        renderTable();
      });

      const sigRef = doc(db, "weeklySignatures", weekKey);
      unweeksig = onSnapshot(sigRef, snap => {
        weekSignatures[weekKey] = snap.exists() ? snap.data() : {};
        updatePrincipalSection();
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
        bannerData: settingsData.bannerData || null,
        logoData: settingsData.logoData || null,
        updatedAt: serverTimestamp()
      }, { merge:true });
      triggerAutosave();
    }

    function applyFilters(){
      renderTable();
    }
    window.applyFilters = applyFilters;

    function renderTable(){
      const search = (document.getElementById("searchInput").value || "").toLowerCase();
      const filterKat = document.getElementById("filterKat").value;
      const filterStatus = document.getElementById("filterStatus").value;

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

        let ftBadge = '<span class="empty-cell">–</span>';
        if(sub){
          const ext = (sub.fileType || "").toLowerCase();
          const cls = ext === "pdf" ? "ft-pdf" : (ext === "doc" || ext === "docx") ? "ft-doc" : "ft-img";
          ftBadge = `<span class="file-type-badge ${cls}">${escapeHtml(ext.toUpperCase())}</span>`;
        }

        const isOwnRow = currentStaffId === staff.id;

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
            : (semakanVal ? `<span style="font-size:12px;white-space:normal;line-height:1.45">${escapeHtml(semakanVal)}</span>` : '<span class="empty-cell">–</span>');

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
        if(!firebaseReady){
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
        const storagePath = `submissions/${weekKey}/${staffId}/${Date.now()}_${file.name}`;
        const storageRef = ref(storage, storagePath);

        showToast("Sedang upload fail...", "warning");
        await uploadBytes(storageRef, file);
        const fileUrl = await getDownloadURL(storageRef);

        if(!submissions[weekKey]) submissions[weekKey] = {};

        submissions[weekKey][staffId] = {
          staffId,
          fileName: file.name,
          fileType: ext,
          fileUrl,
          storagePath,
          tarikhHantar: formatDateShort(now),
          status: isLate(currentWeekOffset) ? "Lewat" : "Disahkan",
          semakan: "",
          pengesahan: null,
          uploadedByName: STAFF_LIST.find(s => s.id === staffId)?.nama || "",
          updatedAtMs: Date.now()
        };

        await saveWeekSubmissions(weekKey);
        showToast("Fail berjaya dimuat naik!", "success");
      }catch(err){
        console.error(err);
        showToast("Upload gagal. Semak Storage Rules / config.", "error");
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
            <i class="fas fa-file-alt"></i>
            <p>Pratonton tidak tersedia untuk jenis fail ini.<br><strong>${escapeHtml(sub.fileName || "")}</strong></p>
            <p style="margin-top:10px"><a href="${sub.fileUrl}" target="_blank" rel="noopener">Buka fail</a></p>
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
      const size = Math.min(canvas.clientWidth || 180, 180);
      const ratio = window.devicePixelRatio || 1;

      canvas.width = size * ratio;
      canvas.height = size * ratio;
      ctx.setTransform(ratio,0,0,ratio,0,0);
      ctx.clearRect(0,0,size,size);

      const cx = size / 2;
      const cy = size / 2;
      const r = Math.max(50, size / 2 - 10);

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

      let angle = -Math.PI/2;
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

    window.changeBanner = function(event){
      if(currentRole !== "admin") return;
      const file = event.target.files?.[0];
      if(!file) return;

      const reader = new FileReader();
      reader.onload = async function(e){
        settingsData.bannerData = e.target.result;
        const img = document.getElementById("bannerImg");
        img.src = settingsData.bannerData;
        img.style.display = "block";
        try{
          await saveBranding();
          showToast("Banner berjaya diubah!", "success");
        }catch(err){
          console.error(err);
          showToast("Gagal simpan banner.", "error");
        }
      };
      reader.readAsDataURL(file);
    };

    window.changeLogo = function(event){
      if(currentRole !== "admin") return;
      const file = event.target.files?.[0];
      if(!file) return;

      const reader = new FileReader();
      reader.onload = async function(e){
        settingsData.logoData = e.target.result;
        document.getElementById("logoText").style.display = "none";
        const img = document.getElementById("logoImg");
        img.src = settingsData.logoData;
        img.style.display = "block";
        try{
          await saveBranding();
          showToast("Logo berjaya diubah!", "success");
        }catch(err){
          console.error(err);
          showToast("Gagal simpan logo.", "error");
        }
      };
      reader.readAsDataURL(file);
    };

    window.addEventListener("resize", updateStats);

    populateStaffSelect();
    updateWeekDisplay();
    renderTable();
    updateStats();
    updatePrincipalSection();
    initFirebase();
  </script>
</body>
</html>