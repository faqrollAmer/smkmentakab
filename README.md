<html lang="ms">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Senarai Penghantaran Tugasan Harian &ndash; SMK Mentakab</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Merriweather:wght@400;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<style>
:root {
  --navy: #0f2444;
  --navy-mid: #1a3a6e;
  --navy-light: #2a5298;
  --gold: #c9a84c;
  --gold-light: #f0c96a;
  --gold-pale: #fdf6e3;
  --emerald: #1a7a4a;
  --emerald-light: #e6f7ef;
  --crimson: #c0392b;
  --crimson-light: #fdecea;
  --amber: #d4820a;
  --amber-light: #fff3e0;
  --slate: #64748b;
  --slate-light: #f1f5f9;
  --white: #ffffff;
  --bg: #f0f4f8;
  --border: #dbe4ef;
  --shadow-sm: 0 2px 8px rgba(15,36,68,0.08);
  --shadow-md: 0 4px 20px rgba(15,36,68,0.12);
  --shadow-lg: 0 8px 40px rgba(15,36,68,0.16);
  --radius: 12px;
  --radius-sm: 8px;
  --transition: all 0.2s ease;
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
font-family: ‘Plus Jakarta Sans’, sans-serif;
background: var(–bg);
color: #1e293b;
min-height: 100vh;
font-size: 14px;
}

/* – HEADER – */
.site-header {
background: linear-gradient(135deg, var(–navy) 0%, var(–navy-mid) 60%, var(–navy-light) 100%);
color: white;
padding: 0;
position: sticky;
top: 0;
z-index: 100;
box-shadow: var(–shadow-lg);
}

.header-banner {
width: 100%;
height: 60px;
object-fit: cover;
display: block;
opacity: 0.35;
position: absolute;
top: 0; left: 0;
pointer-events: none;
}

.header-inner {
position: relative;
display: flex;
align-items: center;
justify-content: space-between;
padding: 14px 24px;
gap: 16px;
flex-wrap: wrap;
}

.header-left {
display: flex;
align-items: center;
gap: 14px;
}

.school-logo {
width: 56px;
height: 56px;
border-radius: 50%;
border: 2.5px solid var(–gold);
object-fit: cover;
background: white;
cursor: pointer;
flex-shrink: 0;
display: flex;
align-items: center;
justify-content: center;
font-size: 22px;
font-weight: 800;
color: var(–navy);
overflow: hidden;
}

.school-logo img { width: 100%; height: 100%; object-fit: cover; border-radius: 50%; }

.school-info h1 {
font-family: ‘Merriweather’, serif;
font-size: 15px;
font-weight: 700;
letter-spacing: 0.3px;
line-height: 1.3;
}

.school-info p {
font-size: 11.5px;
opacity: 0.82;
margin-top: 2px;
}

.header-right {
display: flex;
align-items: center;
gap: 10px;
}

.btn-icon {
width: 38px; height: 38px;
border-radius: 50%;
background: rgba(255,255,255,0.15);
border: 1px solid rgba(255,255,255,0.25);
color: white;
cursor: pointer;
display: flex; align-items: center; justify-content: center;
font-size: 15px;
transition: var(–transition);
position: relative;
}
.btn-icon:hover { background: rgba(255,255,255,0.28); }

.notif-badge {
position: absolute;
top: -3px; right: -3px;
background: #ef4444;
color: white;
border-radius: 50%;
width: 17px; height: 17px;
font-size: 9px;
display: flex; align-items: center; justify-content: center;
font-weight: 700;
border: 1.5px solid var(–navy);
}

.btn-admin {
padding: 7px 15px;
background: rgba(255,255,255,0.15);
border: 1px solid rgba(255,255,255,0.3);
color: white;
border-radius: 20px;
font-size: 12px;
font-weight: 600;
cursor: pointer;
display: flex; align-items: center; gap: 6px;
transition: var(–transition);
}
.btn-admin:hover { background: rgba(255,255,255,0.28); }
.btn-admin.logged-in { background: rgba(201,168,76,0.35); border-color: var(–gold); }

/* – SUBHEADER / WEEK NAV – */
.week-bar {
background: white;
border-bottom: 2px solid var(–border);
padding: 10px 24px;
display: flex;
align-items: center;
justify-content: space-between;
flex-wrap: wrap;
gap: 10px;
box-shadow: var(–shadow-sm);
}

.week-nav {
display: flex;
align-items: center;
gap: 10px;
}

.week-nav button {
width: 32px; height: 32px;
border-radius: var(–radius-sm);
background: var(–slate-light);
border: 1px solid var(–border);
color: var(–navy);
cursor: pointer;
display: flex; align-items: center; justify-content: center;
font-size: 13px;
transition: var(–transition);
}
.week-nav button:hover { background: var(–navy); color: white; }

.week-label {
font-size: 13.5px;
font-weight: 700;
color: var(–navy);
padding: 4px 14px;
background: var(–gold-pale);
border: 1px solid var(–gold);
border-radius: 20px;
}

.week-dates {
font-size: 12px;
color: var(–slate);
font-weight: 500;
}

.week-bar-right {
display: flex;
gap: 8px;
align-items: center;
flex-wrap: wrap;
}

/* – MAIN LAYOUT – */
.main-wrap {
max-width: 1400px;
margin: 0 auto;
padding: 20px 16px 40px;
}

/* – STATS CARDS – */
.stats-grid {
display: grid;
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
gap: 14px;
margin-bottom: 20px;
}

.stat-card {
background: white;
border-radius: var(–radius);
padding: 18px 20px;
box-shadow: var(–shadow-sm);
border: 1px solid var(–border);
display: flex;
align-items: center;
gap: 14px;
transition: var(–transition);
cursor: default;
}
.stat-card:hover { box-shadow: var(–shadow-md); transform: translateY(-1px); }

.stat-icon {
width: 46px; height: 46px;
border-radius: var(–radius-sm);
display: flex; align-items: center; justify-content: center;
font-size: 20px;
flex-shrink: 0;
}

.stat-card.total .stat-icon { background: #e8f0fe; color: var(–navy-light); }
.stat-card.disahkan .stat-icon { background: var(–emerald-light); color: var(–emerald); }
.stat-card.belum .stat-icon { background: var(–amber-light); color: var(–amber); }
.stat-card.lewat .stat-icon { background: var(–crimson-light); color: var(–crimson); }

.stat-info p { font-size: 11px; color: var(–slate); font-weight: 500; text-transform: uppercase; letter-spacing: 0.5px; }
.stat-info h3 { font-size: 28px; font-weight: 800; margin-top: 2px; }
.stat-card.total .stat-info h3 { color: var(–navy-light); }
.stat-card.disahkan .stat-info h3 { color: var(–emerald); }
.stat-card.belum .stat-info h3 { color: var(–amber); }
.stat-card.lewat .stat-info h3 { color: var(–crimson); }

/* – PANEL – */
.panel {
background: white;
border-radius: var(–radius);
box-shadow: var(–shadow-sm);
border: 1px solid var(–border);
overflow: hidden;
margin-bottom: 18px;
}

.panel-header {
padding: 14px 20px;
border-bottom: 1px solid var(–border);
display: flex;
align-items: center;
justify-content: space-between;
gap: 10px;
background: linear-gradient(90deg, #f8fafd, white);
flex-wrap: wrap;
}

.panel-title {
font-size: 14px;
font-weight: 700;
color: var(–navy);
display: flex;
align-items: center;
gap: 8px;
}

.panel-title i { color: var(–navy-light); }

/* – CHARTS ROW – */
.charts-row {
display: grid;
grid-template-columns: 260px 1fr;
gap: 16px;
margin-bottom: 18px;
}

@media (max-width: 768px) {
.charts-row { grid-template-columns: 1fr; }
}

.pie-container {
display: flex;
flex-direction: column;
align-items: center;
padding: 20px;
}

canvas#pieChart {
max-width: 180px;
max-height: 180px;
}

.pie-legend {
margin-top: 14px;
width: 100%;
}

.pie-legend-item {
display: flex;
align-items: center;
gap: 8px;
padding: 5px 0;
font-size: 12.5px;
}

.pie-dot {
width: 11px; height: 11px;
border-radius: 50%;
flex-shrink: 0;
}

.pie-legend-item span:last-child {
margin-left: auto;
font-weight: 700;
}

/* – FILTERS – */
.filters-row {
display: flex;
gap: 8px;
flex-wrap: wrap;
align-items: center;
padding: 12px 16px;
}

.filter-input, .filter-select {
padding: 7px 12px;
border: 1px solid var(–border);
border-radius: var(–radius-sm);
font-family: inherit;
font-size: 13px;
color: #1e293b;
background: var(–slate-light);
outline: none;
transition: var(–transition);
}
.filter-input:focus, .filter-select:focus { border-color: var(–navy-light); background: white; }
.filter-input { min-width: 200px; }
.filter-select { cursor: pointer; }

/* – TABLE – */
.table-wrap {
overflow-x: auto;
}

table {
width: 100%;
border-collapse: collapse;
font-size: 13px;
}

thead th {
background: linear-gradient(180deg, var(–navy) 0%, var(–navy-mid) 100%);
color: white;
padding: 11px 12px;
text-align: left;
font-weight: 600;
font-size: 11.5px;
letter-spacing: 0.3px;
white-space: nowrap;
border-right: 1px solid rgba(255,255,255,0.1);
}
thead th:last-child { border-right: none; }

tbody tr {
border-bottom: 1px solid var(–border);
transition: background 0.15s;
}
tbody tr:hover { background: #f7f9fc; }
tbody tr:last-child { border-bottom: none; }

tbody td {
padding: 10px 12px;
vertical-align: middle;
white-space: nowrap;
}

.td-wrap { white-space: normal; min-width: 120px; }

.bil-cell {
font-weight: 700;
color: var(–slate);
font-size: 12px;
}

.nama-cell {
font-weight: 600;
color: var(–navy);
}

.kat-badge {
display: inline-block;
padding: 3px 9px;
border-radius: 20px;
font-size: 10.5px;
font-weight: 600;
white-space: nowrap;
}

.kat-1 { background: #e8f0fe; color: #1a56db; }
.kat-2 { background: #fce8f3; color: #9b1c7b; }
.kat-3 { background: #fef3c7; color: #92400e; }
.kat-4 { background: #d1fae5; color: #065f46; }

/* STATUS BADGE */
.status-badge {
display: inline-flex;
align-items: center;
gap: 5px;
padding: 4px 10px;
border-radius: 20px;
font-size: 11.5px;
font-weight: 600;
white-space: nowrap;
}
.status-disahkan { background: var(–emerald-light); color: var(–emerald); }
.status-belum { background: var(–amber-light); color: var(–amber); }
.status-lewat { background: var(–crimson-light); color: var(–crimson); }

/* FILE TYPE BADGE */
.file-type-badge {
display: inline-block;
padding: 2px 8px;
border-radius: 4px;
font-size: 10.5px;
font-weight: 700;
letter-spacing: 0.5px;
text-transform: uppercase;
}
.ft-pdf { background: #fee2e2; color: #b91c1c; }
.ft-img { background: #dbeafe; color: #1d4ed8; }
.ft-doc { background: #e0f2fe; color: #0369a1; }

/* ACTION BUTTONS */
.action-group {
display: flex;
gap: 5px;
align-items: center;
flex-wrap: nowrap;
}

.btn-sm {
padding: 5px 10px;
border-radius: var(–radius-sm);
font-size: 11.5px;
font-weight: 600;
cursor: pointer;
border: none;
display: inline-flex;
align-items: center;
gap: 4px;
transition: var(–transition);
white-space: nowrap;
}
.btn-primary { background: var(–navy-light); color: white; }
.btn-primary:hover { background: var(–navy); }
.btn-success { background: var(–emerald); color: white; }
.btn-success:hover { background: #155d38; }
.btn-danger { background: var(–crimson); color: white; }
.btn-danger:hover { background: #a93226; }
.btn-secondary { background: var(–slate-light); color: var(–navy); border: 1px solid var(–border); }
.btn-secondary:hover { background: var(–border); }
.btn-warning { background: var(–amber); color: white; }
.btn-warning:hover { background: #b06c08; }
.btn-gold { background: var(–gold); color: var(–navy); }
.btn-gold:hover { background: var(–gold-light); }

.upload-label {
padding: 5px 10px;
border-radius: var(–radius-sm);
font-size: 11.5px;
font-weight: 600;
cursor: pointer;
background: var(–navy-light);
color: white;
display: inline-flex;
align-items: center;
gap: 4px;
transition: var(–transition);
white-space: nowrap;
}
.upload-label:hover { background: var(–navy); }

input[type=“file”] { display: none; }

/* PENGESAHAN PENGETUA CELL */
.pengesahan-cell {
display: flex;
flex-direction: column;
gap: 4px;
min-width: 160px;
}
.pengesahan-badge {
display: inline-flex;
align-items: center;
gap: 5px;
padding: 3px 9px;
border-radius: 20px;
font-size: 11px;
font-weight: 600;
}
.pengesahan-disahkan { background: var(–emerald-light); color: var(–emerald); }
.pengesahan-pending { background: var(–slate-light); color: var(–slate); }
.catatan-text {
font-size: 11px;
color: var(–slate);
font-style: italic;
max-width: 150px;
white-space: normal;
}

/* – PRINCIPAL SECTION – */
.principal-section {
background: linear-gradient(135deg, #f0f7ff 0%, #fff9e6 100%);
border: 1.5px solid var(–gold);
border-radius: var(–radius);
padding: 20px;
margin-bottom: 18px;
}

.principal-header {
display: flex;
align-items: center;
gap: 14px;
margin-bottom: 16px;
}

.principal-avatar {
width: 52px; height: 52px;
border-radius: 50%;
background: linear-gradient(135deg, var(–navy), var(–navy-light));
display: flex; align-items: center; justify-content: center;
color: white;
font-size: 20px;
flex-shrink: 0;
border: 2px solid var(–gold);
}

.principal-info h3 { font-size: 15px; font-weight: 700; color: var(–navy); }
.principal-info p { font-size: 12px; color: var(–slate); }

.principal-stamp {
border: 2px dashed var(–gold);
border-radius: var(–radius);
padding: 16px 20px;
text-align: center;
background: rgba(255,255,255,0.7);
min-height: 80px;
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
gap: 6px;
}

.principal-stamp.signed {
border-style: solid;
border-color: var(–emerald);
background: var(–emerald-light);
}

.stamp-date { font-size: 11.5px; color: var(–slate); }
.stamp-name { font-size: 13px; font-weight: 700; color: var(–navy); }
.stamp-sign { font-size: 22px; font-weight: 800; color: var(–emerald); font-family: ‘Merriweather’, serif; }

.principal-form {
display: grid;
grid-template-columns: 1fr 1fr;
gap: 12px;
margin-top: 14px;
}

@media (max-width: 600px) { .principal-form { grid-template-columns: 1fr; } }

textarea.principal-notes {
width: 100%;
padding: 10px 12px;
border: 1px solid var(–border);
border-radius: var(–radius-sm);
font-family: inherit;
font-size: 13px;
resize: vertical;
min-height: 72px;
grid-column: 1 / -1;
outline: none;
transition: var(–transition);
}
textarea.principal-notes:focus { border-color: var(–navy-light); }

/* – MODALS – */
.modal-overlay {
display: none;
position: fixed;
inset: 0;
background: rgba(10,20,40,0.65);
z-index: 1000;
align-items: center;
justify-content: center;
padding: 16px;
backdrop-filter: blur(4px);
}
.modal-overlay.open { display: flex; }

.modal {
background: white;
border-radius: 16px;
box-shadow: var(–shadow-lg);
width: 100%;
max-width: 440px;
animation: modalIn 0.25s ease;
overflow: hidden;
}

@keyframes modalIn {
from { opacity: 0; transform: scale(0.94) translateY(16px); }
to { opacity: 1; transform: scale(1) translateY(0); }
}

.modal-header {
background: linear-gradient(135deg, var(–navy), var(–navy-mid));
color: white;
padding: 18px 22px;
display: flex;
align-items: center;
justify-content: space-between;
}
.modal-header h3 { font-size: 15px; font-weight: 700; display: flex; align-items: center; gap: 8px; }

.modal-close {
background: rgba(255,255,255,0.15);
border: none;
color: white;
width: 28px; height: 28px;
border-radius: 50%;
cursor: pointer;
display: flex; align-items: center; justify-content: center;
font-size: 13px;
transition: var(–transition);
}
.modal-close:hover { background: rgba(255,255,255,0.28); }

.modal-body { padding: 22px; }
.modal-footer { padding: 14px 22px; border-top: 1px solid var(–border); display: flex; gap: 10px; justify-content: flex-end; }

.form-group { margin-bottom: 14px; }
.form-group label { display: block; font-size: 12.5px; font-weight: 600; color: var(–navy); margin-bottom: 5px; }
.form-input {
width: 100%;
padding: 9px 12px;
border: 1.5px solid var(–border);
border-radius: var(–radius-sm);
font-family: inherit;
font-size: 13.5px;
outline: none;
transition: var(–transition);
}
.form-input:focus { border-color: var(–navy-light); box-shadow: 0 0 0 3px rgba(42,82,152,0.1); }

.btn-full { width: 100%; padding: 11px; font-size: 14px; border-radius: var(–radius-sm); }

/* LOGIN TABS */
.login-tabs { display: flex; gap: 0; margin-bottom: 18px; border: 1px solid var(–border); border-radius: var(–radius-sm); overflow: hidden; }
.login-tab { flex: 1; padding: 9px; text-align: center; cursor: pointer; font-size: 13px; font-weight: 600; background: var(–slate-light); color: var(–slate); border: none; transition: var(–transition); }
.login-tab.active { background: var(–navy); color: white; }

/* – NOTIFICATION PANEL – */
.notif-panel {
display: none;
position: absolute;
top: 50px; right: 0;
width: 300px;
background: white;
border-radius: var(–radius);
box-shadow: var(–shadow-lg);
border: 1px solid var(–border);
z-index: 200;
overflow: hidden;
}
.notif-panel.open { display: block; }
.notif-panel-header { padding: 12px 14px; background: var(–navy); color: white; font-size: 13px; font-weight: 700; }
.notif-list { max-height: 280px; overflow-y: auto; }
.notif-item { padding: 10px 14px; border-bottom: 1px solid var(–border); font-size: 12.5px; display: flex; align-items: flex-start; gap: 8px; }
.notif-item:last-child { border-bottom: none; }
.notif-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; margin-top: 4px; }
.notif-dot.red { background: var(–crimson); }
.notif-dot.amber { background: var(–amber); }
.notif-dot.green { background: var(–emerald); }

.notif-wrapper { position: relative; }

/* – LAPORAN MODAL – */
.report-modal { max-width: 680px; }
.report-header-info { background: var(–gold-pale); border: 1px solid var(–gold); border-radius: var(–radius-sm); padding: 14px 16px; margin-bottom: 16px; }
.report-header-info p { font-size: 13px; margin: 2px 0; }
.report-table { width: 100%; border-collapse: collapse; font-size: 12.5px; margin-top: 10px; }
.report-table th { background: var(–navy); color: white; padding: 8px 10px; text-align: left; }
.report-table td { padding: 7px 10px; border-bottom: 1px solid var(–border); }
.report-table tr:hover td { background: #f8fafc; }

/* – PREVIEW MODAL – */
.preview-modal { max-width: 700px; }
.preview-container { width: 100%; min-height: 300px; display: flex; align-items: center; justify-content: center; background: #f0f4f8; border-radius: var(–radius-sm); overflow: hidden; }
.preview-container img { max-width: 100%; max-height: 400px; object-fit: contain; }
.preview-container iframe { width: 100%; height: 400px; border: none; }
.preview-placeholder { text-align: center; color: var(–slate); padding: 40px; }
.preview-placeholder i { font-size: 40px; display: block; margin-bottom: 12px; }

/* – CONFIRM MODAL – */
.confirm-modal { max-width: 380px; }
.confirm-icon { text-align: center; font-size: 40px; margin-bottom: 12px; }
.confirm-msg { text-align: center; font-size: 14px; color: #1e293b; line-height: 1.5; }

/* – BANNER SECTION – */
.banner-section {
width: 100%;
height: 90px;
background: linear-gradient(135deg, var(–navy-mid) 0%, #1e4d8c 50%, var(–navy-light) 100%);
position: relative;
overflow: hidden;
display: flex;
align-items: center;
justify-content: center;
margin-bottom: 0;
}
.banner-section img { width: 100%; height: 100%; object-fit: cover; position: absolute; opacity: 0.4; }
.banner-text {
position: relative;
z-index: 1;
text-align: center;
color: white;
}
.banner-text h2 { font-family: ‘Merriweather’, serif; font-size: 17px; font-weight: 700; letter-spacing: 1px; }
.banner-text p { font-size: 12px; opacity: 0.85; margin-top: 3px; }

.banner-edit-btn {
position: absolute;
bottom: 8px; right: 12px;
padding: 4px 10px;
background: rgba(255,255,255,0.2);
border: 1px solid rgba(255,255,255,0.4);
color: white;
border-radius: 20px;
font-size: 11px;
cursor: pointer;
display: none;
align-items: center;
gap: 5px;
z-index: 2;
transition: var(–transition);
}
.banner-edit-btn:hover { background: rgba(255,255,255,0.35); }
.banner-edit-btn.visible { display: flex; }

/* – SEMAKAN CELL – */
.semakan-cell { min-width: 120px; }
.semakan-input {
width: 100%;
padding: 4px 8px;
border: 1px solid var(–border);
border-radius: 6px;
font-family: inherit;
font-size: 12px;
outline: none;
resize: none;
transition: var(–transition);
}
.semakan-input:focus { border-color: var(–navy-light); }

/* – TOAST – */
.toast-container {
position: fixed;
bottom: 24px; right: 24px;
z-index: 9999;
display: flex;
flex-direction: column;
gap: 8px;
}

.toast {
background: var(–navy);
color: white;
padding: 10px 16px;
border-radius: var(–radius-sm);
font-size: 13px;
font-weight: 500;
box-shadow: var(–shadow-md);
display: flex;
align-items: center;
gap: 8px;
animation: toastIn 0.3s ease;
min-width: 220px;
}
.toast.success { background: var(–emerald); }
.toast.error { background: var(–crimson); }
.toast.warning { background: var(–amber); }

@keyframes toastIn { from { opacity: 0; transform: translateX(30px); } to { opacity: 1; transform: translateX(0); } }

/* – RESPONSIVE – */
@media (max-width: 900px) {
.header-inner { padding: 10px 14px; }
.school-info h1 { font-size: 13px; }
.week-bar { padding: 8px 14px; }
.main-wrap { padding: 14px 10px 30px; }
.filters-row { padding: 10px; }
thead th, tbody td { padding: 8px 8px; font-size: 12px; }
}

@media (max-width: 600px) {
.school-info p { display: none; }
.btn-admin span { display: none; }
.stats-grid { grid-template-columns: 1fr 1fr; }
.stat-card { padding: 12px 14px; }
.stat-info h3 { font-size: 22px; }
}

/* – ADMIN CONTROLS – */
.admin-bar {
display: none;
background: #fff8e6;
border-bottom: 2px solid var(–gold);
padding: 8px 24px;
align-items: center;
gap: 12px;
flex-wrap: wrap;
}
.admin-bar.visible { display: flex; }
.admin-bar-label { font-size: 12px; font-weight: 700; color: var(–amber); display: flex; align-items: center; gap: 6px; }

.empty-cell { color: var(–slate); font-style: italic; font-size: 12px; }

/* Auto-save indicator */
.autosave-indicator {
position: fixed;
bottom: 80px; right: 24px;
background: var(–emerald);
color: white;
padding: 6px 12px;
border-radius: 20px;
font-size: 11.5px;
font-weight: 600;
display: none;
align-items: center;
gap: 5px;
z-index: 500;
box-shadow: var(–shadow-sm);
}
.autosave-indicator.visible { display: flex; }
</style>

</head>
<body>

<!-- TOAST CONTAINER -->

<div class="toast-container" id="toastContainer"></div>

<!-- AUTOSAVE INDICATOR -->

<div class="autosave-indicator" id="autosaveIndicator">
  <i class="fas fa-check-circle"></i> Data disimpan
</div>

<!-- ====== SITE HEADER ====== -->

<header class="site-header">
  <div class="header-inner">
    <div class="header-left">
      <div class="school-logo" id="logoContainer">
        <span id="logoText">SMK</span>
        <img id="logoImg" style="display:none" src="" alt="Logo Sekolah">
      </div>
      <div class="school-info">
        <h1>Sekolah Menengah Kebangsaan Mentakab</h1>
        <p><i class="fas fa-user-tie" style="font-size:10px"></i>&nbsp; Pengetua: Hajah Aniza Binti Baharuddin</p>
      </div>
    </div>
    <div class="header-right">
      <div class="notif-wrapper">
        <button class="btn-icon" id="notifBtn" title="Notifikasi" onclick="toggleNotif()">
          <i class="fas fa-bell"></i>
          <span class="notif-badge" id="notifBadge">0</span>
        </button>
        <div class="notif-panel" id="notifPanel">
          <div class="notif-panel-header"><i class="fas fa-bell"></i>&nbsp; Notifikasi</div>
          <div class="notif-list" id="notifList"></div>
        </div>
      </div>
      <button class="btn-icon" title="Laporan" onclick="openReport()">
        <i class="fas fa-chart-bar"></i>
      </button>
      <button class="btn-admin" id="adminBtn" onclick="openLogin()">
        <i class="fas fa-shield-alt"></i>
        <span id="adminBtnText">Log Masuk</span>
      </button>
    </div>
  </div>
</header>

<!-- ADMIN BAR -->

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
  <button class="btn-sm btn-danger" onclick="logout()"><i class="fas fa-sign-out-alt"></i> Log Keluar</button>
</div>

<!-- BANNER -->

<div class="banner-section" id="bannerSection">
  <img id="bannerImg" src="" alt="" style="display:none">
  <div class="banner-text">
    <h2>SENARAI PENGHANTARAN TUGASAN HARIAN</h2>
    <p>Sistem Pengurusan Rekod Mingguan &ndash; Staf Sokongan</p>
  </div>
</div>

<!-- ====== WEEK NAV ====== -->

<div class="week-bar">
  <div class="week-nav">
    <button onclick="prevWeek()" title="Minggu Lepas"><i class="fas fa-chevron-left"></i></button>
    <span class="week-label" id="weekLabel">Minggu 1</span>
    <button onclick="nextWeek()" title="Minggu Akan Datang"><i class="fas fa-chevron-right"></i></button>
  </div>
  <div class="week-dates" id="weekDates">Isnin, 17 Mac &ndash; Jumaat, 21 Mac 2025</div>
  <div class="week-bar-right">
    <button class="btn-sm btn-primary" onclick="goToCurrentWeek()"><i class="fas fa-calendar-check"></i> Minggu Semasa</button>
    <button class="btn-sm btn-secondary" onclick="openReport()"><i class="fas fa-print"></i> Laporan</button>
  </div>
</div>

<!-- ====== MAIN ====== -->

<div class="main-wrap">

  <!-- STATS -->

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

  <!-- CHARTS + PENGESAHAN -->

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

```
<!-- PENGESAHAN PENGETUA -->
<div class="panel">
  <div class="panel-header">
    <span class="panel-title"><i class="fas fa-stamp"></i> Pengesahan Pengetua</span>
    <span id="principalAccessNote" style="font-size:11.5px;color:var(--slate)"><i class="fas fa-lock"></i> Log masuk sebagai Pengetua untuk mengesahkan</span>
  </div>
  <div style="padding:18px">
    <div class="principal-header">
      <div class="principal-avatar"><i class="fas fa-user-tie"></i></div>
      <div class="principal-info">
        <h3>Hajah Aniza Binti Baharuddin</h3>
        <p>Pengetua &ndash; SMK Mentakab</p>
      </div>
    </div>
    <div class="principal-stamp" id="principalStamp">
      <i class="fas fa-pen-to-square" style="font-size:24px;color:var(--slate);opacity:0.4"></i>
      <p style="font-size:12.5px;color:var(--slate)">Belum disahkan</p>
    </div>
    <div class="principal-form" id="principalForm" style="display:none">
      <div>
        <label class="form-group" style="font-size:12px;font-weight:600;color:var(--navy);display:block;margin-bottom:5px">Tarikh Semakan</label>
        <input type="date" class="form-input" id="principalDate" style="width:100%">
      </div>
      <div style="display:flex;align-items:flex-end">
        <button class="btn-sm btn-success btn-full" onclick="signPrincipal()">
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
```

  </div>

  <!-- JADUAL UTAMA -->

  <div class="panel">
    <div class="panel-header">
      <span class="panel-title"><i class="fas fa-table"></i> Jadual Penghantaran Tugasan</span>
      <span style="font-size:12px;color:var(--slate)" id="tableSubtitle"></span>
    </div>
    <!-- FILTERS -->
    <div class="filters-row">
      <input type="text" class="filter-input" id="searchInput" placeholder="&#xf002;  Cari nama staf..." oninput="applyFilters()" style="font-family:inherit">
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
    <!-- TABLE -->
    <div class="table-wrap">
      <table id="mainTable">
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

</div><!-- end main-wrap -->

<!-- ========================== MODALS ========================== -->

<!-- LOGIN MODAL -->

<div class="modal-overlay" id="loginModal">
  <div class="modal">
    <div class="modal-header">
      <h3><i class="fas fa-shield-alt"></i> Log Masuk Pentadbir</h3>
      <button class="modal-close" onclick="closeModal('loginModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body">
      <div class="login-tabs">
        <button class="login-tab active" id="tabPengetua" onclick="switchTab('pengetua')">
          <i class="fas fa-user-tie"></i> Pengetua
        </button>
        <button class="login-tab" id="tabAdmin" onclick="switchTab('admin')">
          <i class="fas fa-cog"></i> Admin
        </button>
      </div>
      <div id="loginInfo" style="font-size:12.5px;color:var(--slate);margin-bottom:14px;padding:10px;background:var(--slate-light);border-radius:var(--radius-sm)">
        <i class="fas fa-info-circle"></i> <span id="loginInfoText">Log masuk sebagai Pengetua untuk menyemak dan mengesahkan penghantaran.</span>
      </div>
      <div class="form-group">
        <label>Kata Laluan</label>
        <input type="password" class="form-input" id="loginPass" placeholder="Masukkan kata laluan..." onkeydown="if(event.key==='Enter') doLogin()">
      </div>
      <p id="loginError" style="color:var(--crimson);font-size:12.5px;display:none"><i class="fas fa-exclamation-circle"></i> Kata laluan tidak sah.</p>
    </div>
    <div class="modal-footer">
      <button class="btn-sm btn-secondary" onclick="closeModal('loginModal')">Batal</button>
      <button class="btn-sm btn-primary" onclick="doLogin()"><i class="fas fa-sign-in-alt"></i> Log Masuk</button>
    </div>
  </div>
</div>

<!-- CONFIRM CANCEL MODAL -->

<div class="modal-overlay" id="confirmModal">
  <div class="modal confirm-modal">
    <div class="modal-header">
      <h3><i class="fas fa-exclamation-triangle"></i> Pengesahan Pembatalan</h3>
      <button class="modal-close" onclick="closeModal('confirmModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body">
      <div class="confirm-icon"></div>
      <p class="confirm-msg">Adakah anda pasti ingin <strong>membatalkan penghantaran</strong> ini?<br><span style="font-size:12.5px;color:var(--slate)">Data fail dan status akan dikemaskini serta-merta.</span></p>
    </div>
    <div class="modal-footer">
      <button class="btn-sm btn-secondary" onclick="closeModal('confirmModal')">Tidak</button>
      <button class="btn-sm btn-danger" id="confirmCancelBtn" onclick="confirmCancelSubmission()"><i class="fas fa-trash"></i> Ya, Batalkan</button>
    </div>
  </div>
</div>

<!-- PREVIEW MODAL -->

<div class="modal-overlay" id="previewModal">
  <div class="modal preview-modal" style="max-width:700px">
    <div class="modal-header">
      <h3><i class="fas fa-eye"></i> Pratonton Fail</h3>
      <button class="modal-close" onclick="closeModal('previewModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body" style="padding:16px">
      <p id="previewFileName" style="font-size:13px;font-weight:600;margin-bottom:10px;color:var(--navy)"></p>
      <div class="preview-container" id="previewContainer"></div>
    </div>
  </div>
</div>

<!-- REPORT MODAL -->

<div class="modal-overlay" id="reportModal">
  <div class="modal report-modal" style="max-width:720px;max-height:90vh;overflow-y:auto">
    <div class="modal-header">
      <h3><i class="fas fa-file-alt"></i> Laporan Penghantaran Mingguan</h3>
      <button class="modal-close" onclick="closeModal('reportModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body" id="reportBody"></div>
    <div class="modal-footer">
      <button class="btn-sm btn-secondary" onclick="closeModal('reportModal')">Tutup</button>
      <button class="btn-sm btn-primary" onclick="window.print()"><i class="fas fa-print"></i> Cetak</button>
    </div>
  </div>
</div>

<!-- PENGESAHAN PENGETUA (inline) MODAL -->

<div class="modal-overlay" id="pengesahanModal">
  <div class="modal" style="max-width:420px">
    <div class="modal-header">
      <h3><i class="fas fa-stamp"></i> Pengesahan Pengetua</h3>
      <button class="modal-close" onclick="closeModal('pengesahanModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body">
      <p style="font-size:13px;margin-bottom:12px;color:var(--slate)">Pengesahan bagi staf: <strong id="pengesahanStaffName"></strong></p>
      <div class="form-group">
        <label>Catatan / Ulasan</label>
        <textarea class="form-input" id="pengesahanCatatan" placeholder="Masukkan catatan (jika ada)..." style="min-height:80px;resize:vertical"></textarea>
      </div>
      <div id="pengesahanError" style="color:var(--crimson);font-size:12.5px;display:none;margin-top:6px"><i class="fas fa-lock"></i> Hanya Pengetua yang boleh mengesahkan.</div>
    </div>
    <div class="modal-footer">
      <button class="btn-sm btn-secondary" onclick="closeModal('pengesahanModal')">Batal</button>
      <button class="btn-sm btn-success" onclick="submitPengesahan()"><i class="fas fa-check"></i> Sahkan</button>
    </div>
  </div>
</div>

<!-- ========================== SCRIPT ========================== -->

<script>
// -- DATA ------------------------------------------------------

const STAFF_LIST = [
  { id:1,  nama:"'Afifah Binti Abdul Aziz",        kat:1 },
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
  1: "Pembantu Makmal",
  2: "Pembantu Pengurusan Murid",
  3: "Pembantu Tadbir",
  4: "Pembantu Khidmat Am"
};

const KAT_CSS = { 1:"kat-1", 2:"kat-2", 3:"kat-3", 4:"kat-4" };

// -- STATE -----------------------------------------------------

let currentWeekOffset = 0;
let currentRole = null; // 'pengetua' | 'admin' | null
let pendingCancelId = null;
let pendingPengesahanId = null;
let currentLoginTab = 'pengetua';

// submissions[weekKey][staffId] = { fileName, fileType, fileData, tarikhHantar, status, semakan, pengesahan, catatan }
let submissions = {};
let weekSignatures = {}; // weekKey => { signed, date, notes }
let bannerData = null;
let logoData = null;

// -- WEEK UTILITIES --------------------------------------------

function getWeekStart(offset=0) {
  const now = new Date();
  const day = now.getDay(); // 0=Sun
  const diff = (day === 0) ? -6 : 1 - day; // Monday
  const monday = new Date(now);
  monday.setDate(now.getDate() + diff + offset * 7);
  monday.setHours(0,0,0,0);
  return monday;
}

function getWeekEnd(offset=0) {
  const mon = getWeekStart(offset);
  const fri = new Date(mon);
  fri.setDate(mon.getDate() + 4);
  return fri;
}

function formatDate(d) {
  const days = ["Ahad","Isnin","Selasa","Rabu","Khamis","Jumaat","Sabtu"];
  const months = ["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];
  return `${days[d.getDay()]}, ${d.getDate()} ${months[d.getMonth()]} ${d.getFullYear()}`;
}

function formatDateShort(d) {
  const months = ["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];
  return `${d.getDate()} ${months[d.getMonth()]} ${d.getFullYear()}`;
}

function getWeekKey(offset=currentWeekOffset) {
  const mon = getWeekStart(offset);
  return `week_${mon.getFullYear()}_${mon.getMonth()}_${mon.getDate()}`;
}

function getWeekNumber(offset=0) {
  const mon = getWeekStart(offset);
  const startOfYear = new Date(mon.getFullYear(), 0, 1);
  const dayOfYear = Math.floor((mon - startOfYear) / 86400000);
  return Math.ceil((dayOfYear + startOfYear.getDay() + 1) / 7);
}

function updateWeekDisplay() {
  const mon = getWeekStart(currentWeekOffset);
  const fri = getWeekEnd(currentWeekOffset);
  const wn = getWeekNumber(currentWeekOffset);
  document.getElementById('weekLabel').textContent = `Minggu ${wn}`;
  document.getElementById('weekDates').textContent = `${formatDate(mon)} &ndash; ${formatDate(fri)}`;
  const key = getWeekKey();
  const months = ["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];
  document.getElementById('tableSubtitle').textContent =
    `${mon.getDate()} ${months[mon.getMonth()]} &ndash; ${fri.getDate()} ${months[fri.getMonth()]} ${fri.getFullYear()}`;
}

function prevWeek() { currentWeekOffset--; updateWeekDisplay(); renderTable(); updateStats(); updatePrincipalSection(); }
function nextWeek() { currentWeekOffset++; updateWeekDisplay(); renderTable(); updateStats(); updatePrincipalSection(); }
function goToCurrentWeek() { currentWeekOffset = 0; updateWeekDisplay(); renderTable(); updateStats(); updatePrincipalSection(); }

// -- IS LATE? --------------------------------------------------

function isLate(offset) {
  const fri = getWeekEnd(offset);
  const now = new Date();
  now.setHours(0,0,0,0);
  const frid = new Date(fri); frid.setHours(23,59,59,999);
  return now > frid;
}

function computeStatus(staffId, weekOffset) {
  const key = getWeekKey(weekOffset);
  const sub = (submissions[key] || {})[staffId];
  if (!sub) return isLate(weekOffset) ? 'Lewat' : 'Belum Hantar';
  return sub.status || 'Disahkan';
}

// -- TABLE RENDER ----------------------------------------------

function applyFilters() { renderTable(); }

function renderTable() {
  const search = (document.getElementById('searchInput').value || '').toLowerCase();
  const filterKat = document.getElementById('filterKat').value;
  const filterStatus = document.getElementById('filterStatus').value;

  const key = getWeekKey();
  const mon = getWeekStart(currentWeekOffset);
  const fri = getWeekEnd(currentWeekOffset);
  const weekRange = `${formatDateShort(mon)} &ndash; ${formatDateShort(fri)}`;
  const weekSig = weekSignatures[key] || {};

  let filtered = STAFF_LIST.filter(s => {
    if (search && !s.nama.toLowerCase().includes(search)) return false;
    if (filterKat && String(s.kat) !== filterKat) return false;
    const st = computeStatus(s.id, currentWeekOffset);
    if (filterStatus && st !== filterStatus) return false;
    return true;
  });

  document.getElementById('filterCount').textContent = `Paparan: ${filtered.length} / ${STAFF_LIST.length} rekod`;

  const tbody = document.getElementById('tableBody');
  tbody.innerHTML = '';

  filtered.forEach((staff, idx) => {
    const sub = (submissions[key] || {})[staff.id];
    const status = computeStatus(staff.id, currentWeekOffset);
    const statusClass = status === 'Disahkan' ? 'status-disahkan' : status === 'Lewat' ? 'status-lewat' : 'status-belum';

    // File type badge
    let ftBadge = '<span class="empty-cell">&ndash;</span>';
    if (sub) {
      const ext = sub.fileType.toLowerCase();
      let cls = ext === 'pdf' ? 'ft-pdf' : (ext === 'doc' || ext === 'docx') ? 'ft-doc' : 'ft-img';
      ftBadge = `<span class="file-type-badge ${cls}">${ext.toUpperCase()}</span>`;
    }

    // Upload cell
    const uploadCell = sub
      ? `<span style="font-size:12px;color:var(--emerald)"><i class="fas fa-check-circle"></i> Dimuat naik</span>`
      : `<label class="upload-label" for="fileInput_${staff.id}">
           <i class="fas fa-upload"></i> Muat Naik
         </label>
         <input type="file" id="fileInput_${staff.id}" accept=".pdf,.jpg,.jpeg,.png,.doc,.docx" onchange="handleUpload(event,${staff.id})">`;

    // Actions
    let actions = '';
    if (sub) {
      actions += `<button class="btn-sm btn-secondary" onclick="previewFile(${staff.id})"><i class="fas fa-eye"></i> Lihat</button>`;
      actions += `<button class="btn-sm btn-danger" onclick="openCancelConfirm(${staff.id})"><i class="fas fa-times"></i> Batal</button>`;
    } else {
      actions = '<span class="empty-cell">&ndash;</span>';
    }

    // Admin semakan
    const semakanVal = sub ? (sub.semakan || '') : '';
    const semakanCell = (currentRole === 'admin' || currentRole === 'pengetua')
      ? `<textarea class="semakan-input" rows="2" placeholder="Catatan semakan..." onchange="saveSemakan(${staff.id},this.value)">${semakanVal}</textarea>`

```
  : (semakanVal ? `<span style="font-size:12px">${semakanVal}</span>` : '<span class="empty-cell">&ndash;</span>');

// Pengesahan pengetua
let pengesahanCell = '';
const pengesahan = sub ? sub.pengesahan : null;
if (pengesahan) {
  pengesahanCell = `<div class="pengesahan-cell">
    <span class="pengesahan-badge pengesahan-disahkan"><i class="fas fa-check-circle"></i> Disahkan</span>
    <span class="catatan-text">${pengesahan.catatan || ''}</span>
    <span style="font-size:10.5px;color:var(--slate)">${pengesahan.tarikh}</span>
  </div>`;
} else if (sub && currentRole === 'pengetua') {
  pengesahanCell = `<button class="btn-sm btn-gold" onclick="openPengesahan(${staff.id})"><i class="fas fa-stamp"></i> Sahkan</button>`;
} else if (sub) {
  pengesahanCell = `<span class="pengesahan-badge pengesahan-pending"><i class="fas fa-hourglass-half"></i> Menunggu</span>`;
} else {
  pengesahanCell = '<span class="empty-cell">&ndash;</span>';
}

const tr = document.createElement('tr');
tr.innerHTML = `
  <td class="bil-cell">${idx + 1}</td>
  <td class="nama-cell td-wrap">${staff.nama}</td>
  <td><span class="kat-badge ${KAT_CSS[staff.kat]}">${KAT_NAMES[staff.kat]}</span></td>
  <td style="font-size:12px">${weekRange}</td>
  <td>${uploadCell}</td>
  <td>${ftBadge}</td>
  <td style="max-width:140px;overflow:hidden;text-overflow:ellipsis;font-size:12px">${sub ? sub.fileName : '<span class="empty-cell">&ndash;</span>'}</td>
  <td style="font-size:12px">${sub ? sub.tarikhHantar : '<span class="empty-cell">&ndash;</span>'}</td>
  <td><span class="status-badge ${statusClass}">
    <i class="fas ${status==='Disahkan'?'fa-check-circle':status==='Lewat'?'fa-exclamation-circle':'fa-clock'}"></i> ${status}
  </span></td>
  <td><div class="action-group">${actions}</div></td>
  <td class="semakan-cell">${semakanCell}</td>
  <td>${pengesahanCell}</td>
`;
tbody.appendChild(tr);
```

});

updateStats();
updateNotifications();
updatePrincipalSection();
}

// – UPLOAD ––––––––––––––––––––––––––

function handleUpload(event, staffId) {
const file = event.target.files[0];
if (!file) return;
const allowed = [‘pdf’,‘jpg’,‘jpeg’,‘png’,‘doc’,‘docx’];
const ext = file.name.split(’.’).pop().toLowerCase();
if (!allowed.includes(ext)) { showToast(‘Jenis fail tidak dibenarkan.’, ‘error’); return; }

const reader = new FileReader();
reader.onload = function(e) {
const key = getWeekKey();
if (!submissions[key]) submissions[key] = {};
const now = new Date();
const status = isLate(currentWeekOffset) ? ‘Lewat’ : ‘Disahkan’;
submissions[key][staffId] = {
fileName: file.name,
fileType: ext,
fileData: e.target.result,
tarikhHantar: formatDateShort(now),
status: status,
semakan: ‘’,
pengesahan: null
};
saveData();
renderTable();
showToast(‘Fail berjaya dimuat naik!’, ‘success’);
triggerAutosave();
};
reader.readAsDataURL(file);
}

// – CANCEL ––––––––––––––––––––––––––

function openCancelConfirm(staffId) {
pendingCancelId = staffId;
openModal(‘confirmModal’);
}

function confirmCancelSubmission() {
const key = getWeekKey();
if (submissions[key] && submissions[key][pendingCancelId]) {
delete submissions[key][pendingCancelId];
saveData();
renderTable();
showToast(‘Penghantaran berjaya dibatalkan.’, ‘warning’);
triggerAutosave();
}
closeModal(‘confirmModal’);
pendingCancelId = null;
}

// – PREVIEW —————————————————

function previewFile(staffId) {
const key = getWeekKey();
const sub = (submissions[key] || {})[staffId];
if (!sub) return;
document.getElementById(‘previewFileName’).textContent = ` ${sub.fileName}`;
const container = document.getElementById(‘previewContainer’);
container.innerHTML = ‘’;
const ext = sub.fileType.toLowerCase();
if ([‘jpg’,‘jpeg’,‘png’].includes(ext)) {
const img = document.createElement(‘img’);
img.src = sub.fileData;
container.appendChild(img);
} else if (ext === ‘pdf’) {
const iframe = document.createElement(‘iframe’);
iframe.src = sub.fileData;
container.appendChild(iframe);
} else {
container.innerHTML = `<div class="preview-placeholder"><i class="fas fa-file-alt"></i><p>Pratonton tidak tersedia untuk jenis fail ini.<br><strong>${sub.fileName}</strong></p></div>`;
}
openModal(‘previewModal’);
}

// – SEMAKAN —————————————————

function saveSemakan(staffId, val) {
const key = getWeekKey();
if (!submissions[key] || !submissions[key][staffId]) return;
submissions[key][staffId].semakan = val;
saveData();
triggerAutosave();
}

// – PENGESAHAN ————————————————

function openPengesahan(staffId) {
pendingPengesahanId = staffId;
const staff = STAFF_LIST.find(s => s.id === staffId);
document.getElementById(‘pengesahanStaffName’).textContent = staff ? staff.nama : ‘’;
document.getElementById(‘pengesahanCatatan’).value = ‘’;
document.getElementById(‘pengesahanError’).style.display = ‘none’;
openModal(‘pengesahanModal’);
}

function submitPengesahan() {
if (currentRole !== ‘pengetua’) {
document.getElementById(‘pengesahanError’).style.display = ‘block’;
return;
}
const key = getWeekKey();
if (!submissions[key] || !submissions[key][pendingPengesahanId]) return;
submissions[key][pendingPengesahanId].pengesahan = {
tarikh: formatDateShort(new Date()),
catatan: document.getElementById(‘pengesahanCatatan’).value
};
submissions[key][pendingPengesahanId].status = ‘Disahkan’;
saveData();
renderTable();
closeModal(‘pengesahanModal’);
showToast(‘Pengesahan berjaya disimpan!’, ‘success’);
triggerAutosave();
}

// – PRINCIPAL SECTION —————————————–

function updatePrincipalSection() {
const key = getWeekKey();
const sig = weekSignatures[key] || {};
const isPrincipal = currentRole === ‘pengetua’;

document.getElementById(‘principalAccessNote’).style.display = isPrincipal ? ‘none’ : ‘block’;
document.getElementById(‘principalForm’).style.display = isPrincipal && !sig.signed ? ‘grid’ : ‘none’;

const stamp = document.getElementById(‘principalStamp’);
const signedInfo = document.getElementById(‘principalSignedInfo’);

if (sig.signed) {
stamp.className = ‘principal-stamp signed’;
stamp.innerHTML = `<div class="stamp-sign">&#10003;</div> <div class="stamp-name">Hajah Aniza Binti Baharuddin</div> <div class="stamp-date">Tarikh Semakan: ${sig.date}</div>`;
signedInfo.style.display = ‘block’;
document.getElementById(‘principalSignedDetails’).textContent = `Catatan: ${sig.notes || 'Tiada catatan'} | Tarikh: ${sig.date}`;
document.getElementById(‘principalForm’).style.display = ‘none’;
} else {
stamp.className = ‘principal-stamp’;
stamp.innerHTML = `<i class="fas fa-pen-to-square" style="font-size:24px;color:var(--slate);opacity:0.4"></i> <p style="font-size:12.5px;color:var(--slate)">Belum disahkan</p>`;
signedInfo.style.display = ‘none’;
}

// Set date default
if (isPrincipal) {
const today = new Date();
const yyyy = today.getFullYear();
const mm = String(today.getMonth()+1).padStart(2,‘0’);
const dd = String(today.getDate()).padStart(2,‘0’);
document.getElementById(‘principalDate’).value = `${yyyy}-${mm}-${dd}`;
}
}

function signPrincipal() {
if (currentRole !== ‘pengetua’) return;
const key = getWeekKey();
const dateVal = document.getElementById(‘principalDate’).value;
const notesVal = document.getElementById(‘principalNotes’).value;
weekSignatures[key] = {
signed: true,
date: dateVal ? formatDateShort(new Date(dateVal)) : formatDateShort(new Date()),
notes: notesVal
};
saveData();
updatePrincipalSection();
showToast(‘Pengesahan pengetua berjaya disimpan!’, ‘success’);
triggerAutosave();
}

// – STATS —————————————————–

function updateStats() {
let disahkan=0, belum=0, lewat=0;
STAFF_LIST.forEach(s => {
const st = computeStatus(s.id, currentWeekOffset);
if (st === ‘Disahkan’) disahkan++;
else if (st === ‘Lewat’) lewat++;
else belum++;
});
document.getElementById(‘statDisahkan’).textContent = disahkan;
document.getElementById(‘statBelum’).textContent = belum;
document.getElementById(‘statLewat’).textContent = lewat;
document.getElementById(‘leg1’).textContent = disahkan;
document.getElementById(‘leg2’).textContent = belum;
document.getElementById(‘leg3’).textContent = lewat;
drawPie(disahkan, belum, lewat);
}

// – PIE CHART ———————————————––

function drawPie(d, b, l) {
const canvas = document.getElementById(‘pieChart’);
const ctx = canvas.getContext(‘2d’);
const total = d + b + l;
ctx.clearRect(0,0,180,180);
const cx=90, cy=90, r=80;
const data = [
{ val:d, color:’#1a7a4a’ },
{ val:b, color:’#d4820a’ },
{ val:l, color:’#c0392b’ }
];
if (total === 0) {
ctx.beginPath(); ctx.arc(cx,cy,r,0,Math.PI*2);
ctx.strokeStyle=’#ddd’; ctx.lineWidth=2; ctx.stroke();
ctx.fillStyle=’#ddd’; ctx.fill();
return;
}
let angle = -Math.PI/2;
data.forEach(seg => {
if (!seg.val) return;
const slice = (seg.val / total) * Math.PI * 2;
ctx.beginPath();
ctx.moveTo(cx, cy);
ctx.arc(cx, cy, r, angle, angle+slice);
ctx.closePath();
ctx.fillStyle = seg.color;
ctx.fill();
ctx.strokeStyle = ‘white’;
ctx.lineWidth = 2;
ctx.stroke();
angle += slice;
});
// Center donut hole
ctx.beginPath(); ctx.arc(cx,cy,38,0,Math.PI*2);
ctx.fillStyle=‘white’; ctx.fill();
ctx.fillStyle=’#1e293b’; ctx.font=‘bold 13px Plus Jakarta Sans’;
ctx.textAlign=‘center’; ctx.textBaseline=‘middle’;
ctx.fillText(total, cx, cy-6);
ctx.fillStyle=’#64748b’; ctx.font=‘10px Plus Jakarta Sans’;
ctx.fillText(‘staf’, cx, cy+9);
}

// – NOTIFICATIONS ———————————————

function updateNotifications() {
const key = getWeekKey();
const items = [];
const late = isLate(currentWeekOffset);

STAFF_LIST.forEach(s => {
const sub = (submissions[key] || {})[s.id];
if (sub) {
items.push({ type:‘green’, msg:`${s.nama} &ndash; baru dihantar (${sub.tarikhHantar})` });
} else if (late) {
items.push({ type:‘red’, msg:`${s.nama} &ndash; LEWAT hantar tugasan` });
} else {
items.push({ type:‘amber’, msg:`${s.nama} &ndash; belum menghantar tugasan` });
}
});

const important = items.filter(i => i.type !== ‘green’);
document.getElementById(‘notifBadge’).textContent = important.length > 99 ? ‘99+’ : important.length;

const list = document.getElementById(‘notifList’);
list.innerHTML = ‘’;
items.forEach(it => {
const div = document.createElement(‘div’);
div.className = ‘notif-item’;
div.innerHTML = `<div class="notif-dot ${it.type}"></div><span>${it.msg}</span>`;
list.appendChild(div);
});
}

function toggleNotif() {
const panel = document.getElementById(‘notifPanel’);
panel.classList.toggle(‘open’);
}

document.addEventListener(‘click’, function(e) {
const wrapper = document.querySelector(’.notif-wrapper’);
if (wrapper && !wrapper.contains(e.target)) {
document.getElementById(‘notifPanel’).classList.remove(‘open’);
}
});

// – REPORT ––––––––––––––––––––––––––

function openReport() {
const key = getWeekKey();
const mon = getWeekStart(currentWeekOffset);
const fri = getWeekEnd(currentWeekOffset);
const wn = getWeekNumber(currentWeekOffset);
const months = [“Jan”,“Feb”,“Mac”,“Apr”,“Mei”,“Jun”,“Jul”,“Ogo”,“Sep”,“Okt”,“Nov”,“Dis”];
const weekStr = `${mon.getDate()} ${months[mon.getMonth()]} &ndash; ${fri.getDate()} ${months[fri.getMonth()]} ${fri.getFullYear()}`;

let d=0,b=0,l=0;
STAFF_LIST.forEach(s => {
const st = computeStatus(s.id, currentWeekOffset);
if (st===‘Disahkan’) d++; else if (st===‘Lewat’) l++; else b++;
});

const sig = weekSignatures[key] || {};

let rows = ‘’;
STAFF_LIST.forEach((s,i) => {
const sub = (submissions[key] || {})[s.id];
const st = computeStatus(s.id, currentWeekOffset);
const stColor = st===‘Disahkan’?’#1a7a4a’:st===‘Lewat’?’#c0392b’:’#d4820a’;
const peng = sub && sub.pengesahan ? `&#10003; ${sub.pengesahan.tarikh}` : ‘–’;
rows += `<tr> <td>${i+1}</td> <td>${s.nama}</td> <td>${KAT_NAMES[s.kat]}</td> <td>${sub ? sub.fileName : '&ndash;'}</td> <td>${sub ? sub.tarikhHantar : '&ndash;'}</td> <td style="font-weight:700;color:${stColor}">${st}</td> <td>${peng}</td> </tr>`;
});

document.getElementById(‘reportBody’).innerHTML = `<div class="report-header-info"> <p><strong>Sekolah:</strong> Sekolah Menengah Kebangsaan Mentakab</p> <p><strong>Pengetua:</strong> Hajah Aniza Binti Baharuddin</p> <p><strong>Minggu:</strong> Minggu ${wn} (${weekStr})</p> <p><strong>Tarikh Laporan:</strong> ${formatDateShort(new Date())}</p> <p style="margin-top:8px"> <span style="color:var(--emerald);font-weight:700">&#10003; Disahkan: ${d}</span> &nbsp;|&nbsp; <span style="color:var(--amber);font-weight:700"> Belum Hantar: ${b}</span> &nbsp;|&nbsp; <span style="color:var(--crimson);font-weight:700">! Lewat: ${l}</span> </p> <p style="margin-top:6px;font-size:12px"> <strong>Status Pengesahan Pengetua:</strong>  ${sig.signed ?`<span style="color:var(--emerald);font-weight:700">✓ Disahkan pada ${sig.date}</span>`: '<span style="color:var(--slate)">Belum Disahkan</span>'} </p> </div> <table class="report-table"> <thead><tr> <th>Bil</th><th>Nama Staf</th><th>Kategori</th> <th>Nama Fail</th><th>Tarikh Hantar</th><th>Status</th><th>Pengesahan Pengetua</th> </tr></thead> <tbody>${rows}</tbody> </table> ${sig.notes ?`<p style="margin-top:14px;font-size:12.5px;color:var(--navy)"><strong>Catatan Pengetua:</strong> ${sig.notes}</p>`: ''} <div style="margin-top:24px;display:flex;justify-content:flex-end"> <div style="text-align:center;border-top:1px solid #333;padding-top:6px;min-width:200px;font-size:12.5px"> <p style="font-weight:700">Hajah Aniza Binti Baharuddin</p> <p style="color:var(--slate)">Pengetua, SMK Mentakab</p> </div> </div>`;
openModal(‘reportModal’);
}

// – LOGIN —————————————————–

function openLogin() {
if (currentRole) { logout(); return; }
document.getElementById(‘loginPass’).value = ‘’;
document.getElementById(‘loginError’).style.display = ‘none’;
openModal(‘loginModal’);
}

function switchTab(tab) {
currentLoginTab = tab;
document.getElementById(‘tabPengetua’).className = ‘login-tab’ + (tab===‘pengetua’?’ active’:’’);
document.getElementById(‘tabAdmin’).className = ‘login-tab’ + (tab===‘admin’?’ active’:’’);
document.getElementById(‘loginInfoText’).textContent = tab === ‘pengetua’
? ‘Log masuk sebagai Pengetua untuk menyemak dan mengesahkan penghantaran.’
: ‘Log masuk sebagai Admin untuk mengurus paparan dan tetapan sistem.’;
document.getElementById(‘loginError’).style.display = ‘none’;
}

function doLogin() {
const pass = document.getElementById(‘loginPass’).value;
const correct = currentLoginTab === ‘pengetua’ ? ‘1234’ : ‘0000’;
if (pass !== correct) {
document.getElementById(‘loginError’).style.display = ‘block’;
return;
}
currentRole = currentLoginTab;
closeModal(‘loginModal’);
const roleLabel = currentRole === ‘pengetua’ ? ‘Pengetua’ : ‘Admin’;
document.getElementById(‘adminBtnText’).textContent = `Log Keluar (${roleLabel})`;
document.getElementById(‘adminBtn’).classList.add(‘logged-in’);
if (currentRole === ‘admin’) {
document.getElementById(‘adminBar’).classList.add(‘visible’);
}
document.getElementById(‘principalAccessNote’).style.display = ‘none’;
showToast(`Selamat datang, ${roleLabel}!`, ‘success’);
renderTable();
updatePrincipalSection();
}

function logout() {
currentRole = null;
document.getElementById(‘adminBtnText’).textContent = ‘Log Masuk’;
document.getElementById(‘adminBtn’).classList.remove(‘logged-in’);
document.getElementById(‘adminBar’).classList.remove(‘visible’);
showToast(‘Anda telah log keluar.’, ‘warning’);
renderTable();
updatePrincipalSection();
}

// – BANNER & LOGO (ADMIN) ———————————––

function changeBanner(event) {
if (currentRole !== ‘admin’) return;
const file = event.target.files[0];
if (!file) return;
const reader = new FileReader();
reader.onload = function(e) {
bannerData = e.target.result;
const img = document.getElementById(‘bannerImg’);
img.src = bannerData;
img.style.display = ‘block’;
saveData();
showToast(‘Banner berjaya diubah!’, ‘success’);
triggerAutosave();
};
reader.readAsDataURL(file);
}

function changeLogo(event) {
if (currentRole !== ‘admin’) return;
const file = event.target.files[0];
if (!file) return;
const reader = new FileReader();
reader.onload = function(e) {
logoData = e.target.result;
document.getElementById(‘logoText’).style.display = ‘none’;
const img = document.getElementById(‘logoImg’);
img.src = logoData;
img.style.display = ‘block’;
saveData();
showToast(‘Logo berjaya diubah!’, ‘success’);
triggerAutosave();
};
reader.readAsDataURL(file);
}

// – MODAL HELPERS ———————————————

function openModal(id) { document.getElementById(id).classList.add(‘open’); }
function closeModal(id) { document.getElementById(id).classList.remove(‘open’); }

// Close modal on overlay click
document.querySelectorAll(’.modal-overlay’).forEach(overlay => {
overlay.addEventListener(‘click’, function(e) {
if (e.target === overlay) overlay.classList.remove(‘open’);
});
});

// – TOAST —————————————————–

function showToast(msg, type=’’) {
const container = document.getElementById(‘toastContainer’);
const toast = document.createElement(‘div’);
toast.className = `toast ${type}`;
const icons = { success:‘fa-check-circle’, error:‘fa-times-circle’, warning:‘fa-exclamation-triangle’, ‘’:‘fa-info-circle’ };
toast.innerHTML = `<i class="fas ${icons[type]||icons['']}"></i> ${msg}`;
container.appendChild(toast);
setTimeout(() => { toast.style.opacity=‘0’; toast.style.transition=‘opacity 0.4s’; setTimeout(()=>toast.remove(),400); }, 3000);
}

// – AUTOSAVE –––––––––––––––––––––––––

let autosaveTimer = null;
function triggerAutosave() {
const ind = document.getElementById(‘autosaveIndicator’);
ind.classList.add(‘visible’);
clearTimeout(autosaveTimer);
autosaveTimer = setTimeout(() => { ind.classList.remove(‘visible’); }, 2200);
}

// – PERSIST —————————————————

function saveData() {
try {
localStorage.setItem(‘smkm_submissions’, JSON.stringify(submissions));
localStorage.setItem(‘smkm_weekSig’, JSON.stringify(weekSignatures));
if (bannerData) localStorage.setItem(‘smkm_banner’, bannerData);
if (logoData) localStorage.setItem(‘smkm_logo’, logoData);
} catch(e) { console.warn(‘LocalStorage penuh atau tidak tersedia.’); }
}

function loadData() {
try {
const s = localStorage.getItem(‘smkm_submissions’);
if (s) submissions = JSON.parse(s);
const w = localStorage.getItem(‘smkm_weekSig’);
if (w) weekSignatures = JSON.parse(w);
const b = localStorage.getItem(‘smkm_banner’);
if (b) { bannerData = b; const img = document.getElementById(‘bannerImg’); img.src=b; img.style.display=‘block’; }
const l = localStorage.getItem(‘smkm_logo’);
if (l) { logoData = l; document.getElementById(‘logoText’).style.display=‘none’; const img=document.getElementById(‘logoImg’); img.src=l; img.style.display=‘block’; }
} catch(e) {}
}

// – INIT ——————————————————

loadData();
updateWeekDisplay();
renderTable();
updateStats();
updatePrincipalSection();

</script>
</body>
</html>
