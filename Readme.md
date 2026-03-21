<!DOCTYPE html>

<html lang="ms">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sistem Penghantaran Mingguan – SMK Mentakab</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />
  <style>
    /* ── CSS Variables ── */
    :root {
      --navy:        #0f172a;
      --navy-mid:    #1e293b;
      --navy-soft:   #334155;
      --slate:       #64748b;
      --slate-light: #94a3b8;
      --border:      #e2e8f0;
      --border-soft: #f1f5f9;
      --bg:          #f8fafc;
      --white:       #ffffff;

```
  --emerald:     #059669;
  --emerald-pale:#d1fae5;
  --emerald-mid: #065f46;

  --amber:       #d97706;
  --amber-pale:  #fef3c7;
  --amber-mid:   #92400e;

  --crimson:     #dc2626;
  --crimson-pale:#fee2e2;
  --crimson-mid: #991b1b;

  --gold:        #b8860b;
  --gold-pale:   #fffbeb;

  --blue:        #2563eb;
  --blue-pale:   #dbeafe;

  --radius:      12px;
  --radius-sm:   8px;
  --radius-xs:   5px;
  --shadow-sm:   0 1px 3px rgba(0,0,0,.08), 0 1px 2px rgba(0,0,0,.05);
  --shadow:      0 4px 16px rgba(0,0,0,.08), 0 2px 4px rgba(0,0,0,.04);
  --shadow-lg:   0 20px 60px rgba(0,0,0,.12), 0 8px 24px rgba(0,0,0,.06);

  --font: "Plus Jakarta Sans", sans-serif;
}

/* ── Reset ── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body {
  font-family: var(--font);
  background: var(--bg);
  color: var(--navy);
  min-height: 100vh;
  line-height: 1.55;
  font-size: 14px;
}

/* ── Autosave indicator ── */
#autosaveIndicator {
  position: fixed; bottom: 24px; right: 24px; z-index: 9999;
  background: var(--navy); color: #fff;
  padding: 8px 16px; border-radius: 20px;
  font-size: 12px; font-weight: 600;
  display: flex; align-items: center; gap: 6px;
  opacity: 0; transform: translateY(8px);
  transition: opacity .3s, transform .3s;
  pointer-events: none;
  box-shadow: var(--shadow);
}
#autosaveIndicator.visible { opacity: 1; transform: translateY(0); }
#autosaveIndicator i { color: var(--emerald); font-size: 10px; }

/* ── Toast ── */
#toastContainer {
  position: fixed; top: 20px; right: 20px; z-index: 10000;
  display: flex; flex-direction: column; gap: 8px;
  pointer-events: none;
}
.toast {
  display: flex; align-items: center; gap: 10px;
  padding: 12px 18px; border-radius: var(--radius-sm);
  background: var(--navy-mid); color: #fff;
  font-size: 13px; font-weight: 500;
  box-shadow: var(--shadow-lg);
  animation: toastIn .25s ease;
  max-width: 340px;
}
.toast.success { background: var(--emerald-mid); }
.toast.error   { background: var(--crimson-mid); }
.toast.warning { background: var(--amber-mid); }
@keyframes toastIn { from { opacity:0; transform:translateX(20px); } to { opacity:1; transform:none; } }

/* ── Header / Banner ── */
.banner-wrap {
  background: var(--navy);
  position: relative;
  overflow: hidden;
}
.banner-wrap::before {
  content: "";
  position: absolute; inset: 0;
  background: linear-gradient(135deg, #0f172a 0%, #1e3a5f 50%, #0f172a 100%);
  opacity: .9;
}
#bannerImg {
  position: absolute; inset: 0;
  width: 100%; height: 100%; object-fit: cover;
  opacity: .18; display: none;
}
.banner-inner {
  position: relative; z-index: 1;
  max-width: 1320px; margin: 0 auto;
  padding: 20px 24px;
  display: flex; align-items: center; gap: 18px;
}
.logo-wrap {
  width: 56px; height: 56px; flex-shrink: 0;
  border-radius: 50%; overflow: hidden;
  background: rgba(255,255,255,.12);
  display: flex; align-items: center; justify-content: center;
  border: 2px solid rgba(255,255,255,.25);
}
#logoImg { width: 100%; height: 100%; object-fit: cover; display: none; }
#logoText {
  font-family: "Instrument Serif", serif;
  font-size: 22px; color: #fff; font-weight: 400;
  font-style: italic;
}
.banner-titles { flex: 1; min-width: 0; }
.banner-titles h1 {
  font-size: 16px; font-weight: 700; color: #fff;
  letter-spacing: .01em; white-space: nowrap;
  overflow: hidden; text-overflow: ellipsis;
}
.banner-titles p {
  font-size: 12px; color: rgba(255,255,255,.55);
  font-weight: 400; margin-top: 2px;
}
.banner-right {
  display: flex; align-items: center; gap: 10px; flex-shrink: 0;
}

/* ── Firebase status chip ── */
.fb-status {
  display: flex; align-items: center; gap: 6px;
  background: rgba(255,255,255,.08); border: 1px solid rgba(255,255,255,.12);
  border-radius: 20px; padding: 5px 12px;
  font-size: 11.5px; color: rgba(255,255,255,.7); font-weight: 500;
}
.fb-dot {
  width: 7px; height: 7px; border-radius: 50%;
  background: #4ade80;
  box-shadow: 0 0 6px #4ade80;
  animation: pulse 2s infinite;
}
@keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.4} }

/* ── Notification ── */
.notif-wrapper { position: relative; }
.notif-btn {
  width: 38px; height: 38px; border-radius: 50%;
  background: rgba(255,255,255,.1); border: 1px solid rgba(255,255,255,.18);
  color: #fff; cursor: pointer; display: flex; align-items: center; justify-content: center;
  font-size: 15px; position: relative; transition: background .2s;
}
.notif-btn:hover { background: rgba(255,255,255,.18); }
#notifBadge {
  position: absolute; top: -4px; right: -4px;
  background: var(--crimson); color: #fff;
  font-size: 9.5px; font-weight: 700;
  min-width: 17px; height: 17px; border-radius: 9px;
  display: flex; align-items: center; justify-content: center;
  padding: 0 3px; border: 2px solid var(--navy);
}
#notifPanel {
  position: absolute; top: calc(100% + 10px); right: 0;
  width: 280px; background: var(--white);
  border-radius: var(--radius); box-shadow: var(--shadow-lg);
  border: 1px solid var(--border);
  overflow: hidden; z-index: 500;
  opacity: 0; transform: translateY(-6px) scale(.97);
  pointer-events: none; transition: opacity .2s, transform .2s;
}
#notifPanel.open { opacity: 1; transform: none; pointer-events: all; }
.notif-header {
  padding: 12px 16px; background: var(--navy); color: #fff;
  font-size: 12px; font-weight: 600; letter-spacing: .04em;
  text-transform: uppercase;
}
.notif-item {
  display: flex; align-items: center; gap: 10px;
  padding: 10px 16px; font-size: 12.5px; color: var(--navy-mid);
  border-bottom: 1px solid var(--border-soft);
}
.notif-item:last-child { border-bottom: none; }
.notif-dot {
  width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0;
}
.notif-dot.amber { background: var(--amber); }
.notif-dot.red   { background: var(--crimson); }
.notif-dot.green { background: var(--emerald); }

/* ── Buttons general ── */
button { font-family: var(--font); cursor: pointer; }
.btn {
  display: inline-flex; align-items: center; gap: 7px;
  padding: 9px 20px; border-radius: var(--radius-sm);
  font-size: 13.5px; font-weight: 600; border: none;
  transition: opacity .15s, box-shadow .15s, transform .1s;
  white-space: nowrap;
}
.btn:hover { opacity: .88; }
.btn:active { transform: scale(.97); }
.btn-primary { background: var(--blue); color: #fff; box-shadow: 0 2px 8px rgba(37,99,235,.25); }
.btn-secondary { background: var(--border-soft); color: var(--navy-mid); border: 1px solid var(--border); }
.btn-gold { background: var(--gold); color: #fff; box-shadow: 0 2px 8px rgba(184,134,11,.25); }
.btn-danger { background: var(--crimson); color: #fff; box-shadow: 0 2px 8px rgba(220,38,38,.2); }
.btn-sm {
  padding: 5px 12px; font-size: 12px; border-radius: var(--radius-xs);
  display: inline-flex; align-items: center; gap: 5px;
}

.admin-btn {
  display: flex; align-items: center; gap: 8px;
  padding: 8px 18px; border-radius: var(--radius-sm);
  background: rgba(255,255,255,.1); border: 1px solid rgba(255,255,255,.18);
  color: #fff; font-size: 13px; font-weight: 600;
  cursor: pointer; transition: background .2s; white-space: nowrap;
}
.admin-btn:hover { background: rgba(255,255,255,.2); }
.admin-btn.logged-in { background: rgba(5,150,105,.3); border-color: rgba(5,150,105,.5); }

/* ── Admin bar ── */
#adminBar {
  background: var(--navy-mid); border-bottom: 1px solid rgba(255,255,255,.08);
  display: none; padding: 0;
}
#adminBar.visible { display: block; }
.admin-bar-inner {
  max-width: 1320px; margin: 0 auto;
  padding: 10px 24px;
  display: flex; align-items: center; gap: 24px; flex-wrap: wrap;
}
.admin-bar-inner span {
  font-size: 11.5px; color: rgba(255,255,255,.45);
  font-weight: 600; text-transform: uppercase; letter-spacing: .06em;
}
.upload-label-admin {
  display: inline-flex; align-items: center; gap: 6px;
  padding: 6px 14px; border-radius: var(--radius-xs);
  background: rgba(255,255,255,.08); border: 1px solid rgba(255,255,255,.15);
  color: rgba(255,255,255,.7); font-size: 12px; font-weight: 500;
  cursor: pointer; transition: background .2s;
}
.upload-label-admin:hover { background: rgba(255,255,255,.14); color: #fff; }
.upload-label-admin input { display: none; }

/* ── Main layout ── */
.main-wrap {
  max-width: 1320px; margin: 0 auto;
  padding: 24px 24px;
  display: grid;
  grid-template-columns: 1fr 300px;
  gap: 24px;
  align-items: start;
}
@media (max-width: 1024px) {
  .main-wrap { grid-template-columns: 1fr; }
}

/* ── Cards ── */
.card {
  background: var(--white);
  border-radius: var(--radius);
  border: 1px solid var(--border);
  box-shadow: var(--shadow-sm);
  overflow: hidden;
}
.card-header {
  padding: 16px 20px;
  display: flex; align-items: center; justify-content: space-between;
  border-bottom: 1px solid var(--border-soft);
}
.card-title {
  font-size: 14px; font-weight: 700; color: var(--navy);
  display: flex; align-items: center; gap: 8px;
}
.card-title i { color: var(--slate); font-size: 13px; }
.card-body { padding: 20px; }

/* ── Week nav ── */
.week-nav {
  display: flex; align-items: center; gap: 12px;
  flex-wrap: wrap;
}
.week-btn {
  width: 34px; height: 34px; border-radius: var(--radius-xs);
  border: 1px solid var(--border); background: var(--white);
  color: var(--navy-soft); font-size: 13px;
  display: flex; align-items: center; justify-content: center;
  cursor: pointer; transition: background .15s, color .15s;
}
.week-btn:hover { background: var(--navy); color: #fff; border-color: var(--navy); }
.week-info { text-align: center; }
#weekLabel { font-size: 15px; font-weight: 700; color: var(--navy); display: block; }
#weekDates { font-size: 11.5px; color: var(--slate); display: block; margin-top: 1px; }

/* ── Stat cards ── */
.stats-row {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 12px;
  margin-bottom: 20px;
}
@media (max-width: 640px) { .stats-row { grid-template-columns: repeat(2,1fr); } }
.stat-card {
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  padding: 14px 16px;
  display: flex; align-items: center; gap: 12px;
  box-shadow: var(--shadow-sm);
  transition: box-shadow .2s;
}
.stat-card:hover { box-shadow: var(--shadow); }
.stat-icon {
  width: 40px; height: 40px; border-radius: var(--radius-xs);
  display: flex; align-items: center; justify-content: center;
  font-size: 16px; flex-shrink: 0;
}
.stat-icon.navy   { background: #e8edf5; color: var(--navy); }
.stat-icon.green  { background: var(--emerald-pale); color: var(--emerald); }
.stat-icon.amber  { background: var(--amber-pale); color: var(--amber); }
.stat-icon.red    { background: var(--crimson-pale); color: var(--crimson); }
.stat-num { font-size: 22px; font-weight: 800; color: var(--navy); line-height: 1; }
.stat-label { font-size: 11px; color: var(--slate); font-weight: 500; margin-top: 2px; }

/* ── Filters toolbar ── */
.toolbar {
  display: flex; align-items: center; gap: 10px; flex-wrap: wrap;
  padding: 14px 20px; border-bottom: 1px solid var(--border-soft);
  background: var(--bg);
}
.toolbar-search {
  position: relative; flex: 1; min-width: 180px;
}
.toolbar-search i {
  position: absolute; left: 11px; top: 50%; transform: translateY(-50%);
  color: var(--slate-light); font-size: 13px; pointer-events: none;
}
.toolbar-search input {
  width: 100%; padding: 8px 12px 8px 32px;
  border: 1px solid var(--border); border-radius: var(--radius-xs);
  font-family: var(--font); font-size: 13px; color: var(--navy);
  background: var(--white); outline: none; transition: border-color .15s;
}
.toolbar-search input:focus { border-color: var(--blue); }
.toolbar select {
  padding: 8px 12px; border: 1px solid var(--border);
  border-radius: var(--radius-xs);
  font-family: var(--font); font-size: 13px; color: var(--navy);
  background: var(--white); outline: none; cursor: pointer;
  transition: border-color .15s;
}
.toolbar select:focus { border-color: var(--blue); }
#filterCount { font-size: 12px; color: var(--slate); font-weight: 500; margin-left: auto; }

/* ── Staff selector ── */
.staff-selector-row {
  display: flex; align-items: center; gap: 10px; flex-wrap: wrap;
  padding: 12px 20px; background: var(--amber-pale);
  border-bottom: 1px solid #fde68a;
}
.staff-selector-row label { font-size: 12.5px; font-weight: 600; color: var(--amber-mid); }
.staff-selector-row select {
  flex: 1; min-width: 200px; max-width: 400px;
  padding: 7px 12px; border: 1px solid #fde68a;
  border-radius: var(--radius-xs); font-family: var(--font);
  font-size: 13px; background: var(--white); color: var(--navy);
  outline: none;
}

/* ── Table ── */
.table-wrap { overflow-x: auto; }
table { width: 100%; border-collapse: collapse; min-width: 900px; }
thead tr { background: var(--navy); }
thead th {
  padding: 11px 14px; text-align: left;
  font-size: 11px; font-weight: 700; color: rgba(255,255,255,.75);
  letter-spacing: .06em; text-transform: uppercase;
  white-space: nowrap; border: none;
}
tbody tr {
  border-bottom: 1px solid var(--border-soft);
  transition: background .12s;
}
tbody tr:hover { background: #f8fafc; }
tbody td {
  padding: 10px 14px; font-size: 13px; color: var(--navy-mid);
  vertical-align: middle;
}
.bil-cell {
  font-size: 11.5px; color: var(--slate); font-weight: 600;
  width: 36px; text-align: center;
}
.nama-cell { font-weight: 600; font-size: 13px; min-width: 160px; }
.td-wrap { white-space: normal; word-break: break-word; }
.empty-cell { color: var(--slate-light); font-size: 12px; }

/* ── Badges ── */
.kat-badge {
  display: inline-flex; align-items: center;
  padding: 3px 10px; border-radius: 20px;
  font-size: 11px; font-weight: 600; white-space: nowrap;
}
.kat-1 { background: #dbeafe; color: #1e40af; }
.kat-2 { background: #f3e8ff; color: #6b21a8; }
.kat-3 { background: #dcfce7; color: #15803d; }
.kat-4 { background: #ffe4e6; color: #9f1239; }

.status-badge {
  display: inline-flex; align-items: center; gap: 5px;
  padding: 4px 10px; border-radius: 20px;
  font-size: 11.5px; font-weight: 600; white-space: nowrap;
}
.status-disahkan { background: var(--emerald-pale); color: var(--emerald-mid); }
.status-belum    { background: var(--amber-pale); color: var(--amber-mid); }
.status-lewat    { background: var(--crimson-pale); color: var(--crimson-mid); }

.file-type-badge {
  display: inline-block; padding: 2px 8px; border-radius: 4px;
  font-size: 10.5px; font-weight: 700; letter-spacing: .04em;
}
.ft-pdf { background: #fee2e2; color: #991b1b; }
.ft-doc { background: #dbeafe; color: #1e40af; }
.ft-img { background: #dcfce7; color: #14532d; }

/* ── Upload label ── */
.upload-label {
  display: inline-flex; align-items: center; gap: 6px;
  padding: 5px 12px; border-radius: var(--radius-xs);
  background: var(--blue-pale); color: var(--blue);
  font-size: 12px; font-weight: 600; cursor: pointer;
  border: 1px dashed #93c5fd; transition: background .15s;
}
.upload-label:hover { background: #bfdbfe; }
input[type="file"] { display: none; }

/* ── Semakan textarea ── */
.semakan-input {
  width: 100%; min-width: 120px; max-width: 200px;
  padding: 6px 10px; border: 1px solid var(--border);
  border-radius: var(--radius-xs); font-family: var(--font);
  font-size: 12px; color: var(--navy); resize: vertical;
  outline: none; transition: border-color .15s;
  background: var(--white);
}
.semakan-input:focus { border-color: var(--blue); }

/* ── Pengesahan cell ── */
.pengesahan-cell { display: flex; flex-direction: column; gap: 3px; }
.pengesahan-badge {
  display: inline-flex; align-items: center; gap: 5px;
  padding: 3px 9px; border-radius: 20px;
  font-size: 11px; font-weight: 600;
}
.pengesahan-disahkan { background: var(--emerald-pale); color: var(--emerald-mid); }
.pengesahan-pending  { background: var(--amber-pale); color: var(--amber-mid); }
.catatan-text { font-size: 11px; color: var(--slate); }

/* ── Action group ── */
.action-group { display: flex; align-items: center; gap: 5px; flex-wrap: wrap; }

/* ── Sidebar ── */
.sidebar { display: flex; flex-direction: column; gap: 20px; }

/* ── Pie chart ── */
.pie-wrap {
  display: flex; flex-direction: column; align-items: center; gap: 14px;
}
#pieChart { display: block; }
.legend { width: 100%; display: flex; flex-direction: column; gap: 6px; }
.legend-item {
  display: flex; align-items: center; justify-content: space-between;
  font-size: 12.5px;
}
.legend-dot {
  width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0;
}
.legend-label { display: flex; align-items: center; gap: 7px; color: var(--navy-mid); }
.legend-val { font-weight: 700; color: var(--navy); }

/* ── Principal section ── */
.principal-note {
  padding: 12px 16px; border-radius: var(--radius-xs);
  background: var(--border-soft); font-size: 12px; color: var(--slate);
  border-left: 3px solid var(--border);
}
.principal-stamp {
  border: 2px dashed var(--border); border-radius: var(--radius-sm);
  padding: 20px; text-align: center; transition: border-color .2s;
  display: flex; flex-direction: column; align-items: center; gap: 6px;
}
.principal-stamp.signed {
  border: 2px solid var(--emerald);
  background: var(--emerald-pale);
}
.stamp-sign { font-size: 32px; color: var(--emerald); font-weight: 700; }
.stamp-name { font-size: 13px; font-weight: 700; color: var(--emerald-mid); }
.stamp-date { font-size: 11px; color: var(--slate); }
.principal-form { display: grid; gap: 10px; margin-top: 12px; }
.principal-form label { font-size: 12px; font-weight: 600; color: var(--navy-soft); }
.principal-form input,
.principal-form textarea {
  width: 100%; padding: 8px 12px;
  border: 1px solid var(--border); border-radius: var(--radius-xs);
  font-family: var(--font); font-size: 13px; color: var(--navy);
  outline: none; resize: vertical; transition: border-color .15s;
}
.principal-form input:focus,
.principal-form textarea:focus { border-color: var(--blue); }

/* ── Subtitle under week nav ── */
#tableSubtitle { font-size: 11.5px; color: var(--slate); margin-bottom: 14px; padding: 0 20px; }

/* ── Modal ── */
.modal-overlay {
  position: fixed; inset: 0;
  background: rgba(15,23,42,.55);
  backdrop-filter: blur(4px);
  z-index: 800;
  display: flex; align-items: center; justify-content: center; padding: 20px;
  opacity: 0; pointer-events: none; transition: opacity .2s;
}
.modal-overlay.open { opacity: 1; pointer-events: all; }
.modal {
  background: var(--white); border-radius: var(--radius);
  box-shadow: var(--shadow-lg);
  width: 100%; max-width: 560px;
  max-height: 90vh; overflow-y: auto;
  transform: translateY(12px) scale(.98);
  transition: transform .2s;
}
.modal-overlay.open .modal { transform: none; }
.modal-header {
  padding: 18px 22px; border-bottom: 1px solid var(--border);
  display: flex; align-items: center; justify-content: space-between;
}
.modal-header h2 { font-size: 16px; font-weight: 700; }
.modal-close {
  width: 30px; height: 30px; border-radius: 50%;
  background: var(--border-soft); border: none; cursor: pointer;
  display: flex; align-items: center; justify-content: center;
  font-size: 14px; color: var(--slate); transition: background .15s;
}
.modal-close:hover { background: var(--border); }
.modal-body { padding: 20px 22px; }
.modal-footer {
  padding: 14px 22px; border-top: 1px solid var(--border);
  display: flex; justify-content: flex-end; gap: 10px;
}
.form-group { margin-bottom: 14px; }
.form-group label { display: block; font-size: 12.5px; font-weight: 600; color: var(--navy-soft); margin-bottom: 5px; }
.form-group input,
.form-group textarea,
.form-group select {
  width: 100%; padding: 9px 12px;
  border: 1px solid var(--border); border-radius: var(--radius-xs);
  font-family: var(--font); font-size: 13px; color: var(--navy);
  outline: none; resize: vertical; transition: border-color .15s;
}
.form-group input:focus,
.form-group textarea:focus,
.form-group select:focus { border-color: var(--blue); }
.error-msg {
  display: none; padding: 8px 12px;
  background: var(--crimson-pale); color: var(--crimson-mid);
  border-radius: var(--radius-xs); font-size: 12.5px; font-weight: 500;
  margin-bottom: 10px;
}

/* ── Preview modal ── */
#previewModal .modal { max-width: 780px; }
#previewContainer img {
  max-width: 100%; border-radius: var(--radius-xs);
  display: block; margin: 0 auto;
}
#previewContainer iframe {
  width: 100%; height: 520px; border: none;
  border-radius: var(--radius-xs);
}
.preview-placeholder {
  text-align: center; padding: 40px 20px; color: var(--slate);
}
.preview-placeholder a {
  color: var(--blue); font-weight: 600; text-decoration: none;
}
.preview-placeholder a:hover { text-decoration: underline; }

/* ── Report modal ── */
#reportModal .modal { max-width: 820px; }
.report-table {
  width: 100%; border-collapse: collapse; font-size: 12.5px;
}
.report-table th {
  background: var(--navy); color: rgba(255,255,255,.8);
  padding: 9px 12px; text-align: left; font-size: 11px;
  font-weight: 700; letter-spacing: .05em; text-transform: uppercase;
}
.report-table td {
  padding: 8px 12px; border-bottom: 1px solid var(--border-soft);
  color: var(--navy-mid);
}
.report-table tr:hover td { background: var(--bg); }

/* ── Login modal ── */
.role-tabs { display: flex; gap: 8px; margin-bottom: 18px; }

/* ── Principal signed info ── */
#principalSignedInfo {
  display: none; margin-top: 10px;
  padding: 10px 14px; background: var(--emerald-pale);
  border-radius: var(--radius-xs); border-left: 3px solid var(--emerald);
}
#principalSignedDetails { font-size: 12px; color: var(--emerald-mid); font-weight: 500; }

/* ── Responsive tweaks ── */
@media (max-width: 768px) {
  .banner-inner { padding: 14px 16px; flex-wrap: wrap; }
  .banner-titles h1 { font-size: 13px; }
  .main-wrap { padding: 16px; }
  .stats-row { grid-template-columns: repeat(2, 1fr); gap: 8px; }
  .toolbar { padding: 10px 14px; }
}
@media (max-width: 480px) {
  .banner-right { gap: 6px; }
  .admin-btn span { display: none; }
}

/* ── Section divider ── */
.section-label {
  font-size: 10.5px; font-weight: 700; color: var(--slate);
  text-transform: uppercase; letter-spacing: .08em;
  margin-bottom: 10px; display: flex; align-items: center; gap: 8px;
}
.section-label::after {
  content: ""; flex: 1; height: 1px; background: var(--border);
}
```

  </style>
</head>
<body>

<div id="toastContainer"></div>
<div id="autosaveIndicator"><i class="fas fa-circle"></i> Autosimpan…</div>

<!-- ══ BANNER ══ -->

<div class="banner-wrap">
  <img id="bannerImg" alt="Banner" />
  <div class="banner-inner">
    <div class="logo-wrap">
      <img id="logoImg" alt="Logo" />
      <span id="logoText">S</span>
    </div>

```
<div class="banner-titles">
  <h1>Sekolah Menengah Kebangsaan Mentakab</h1>
  <p>Sistem Penghantaran Rekod Mingguan Bukan Guru</p>
</div>

<div class="banner-right">
  <div class="fb-status">
    <div class="fb-dot"></div>
    <span id="firebaseStatusText">Memuat…</span>
  </div>

  <div class="notif-wrapper">
    <button class="notif-btn" onclick="toggleNotif()" title="Notifikasi">
      <i class="fas fa-bell"></i>
      <span id="notifBadge">0</span>
    </button>
    <div id="notifPanel">
      <div class="notif-header"><i class="fas fa-bell"></i> &nbsp;Notifikasi</div>
      <div id="notifList"></div>
    </div>
  </div>

  <button class="admin-btn" id="adminBtn" onclick="openLogin()">
    <i class="fas fa-user-shield"></i>
    <span id="adminBtnText">Log Masuk</span>
  </button>
</div>
```

  </div>
</div>

<!-- ══ ADMIN BAR ══ -->

<div id="adminBar">
  <div class="admin-bar-inner">
    <span><i class="fas fa-sliders"></i> &nbsp;Admin</span>
    <label class="upload-label-admin">
      <i class="fas fa-image"></i> Tukar Banner
      <input type="file" accept="image/*" onchange="changeBanner(event)" />
    </label>
    <label class="upload-label-admin">
      <i class="fas fa-circle"></i> Tukar Logo
      <input type="file" accept="image/*" onchange="changeLogo(event)" />
    </label>
  </div>
</div>

<!-- ══ MAIN ══ -->

<div class="main-wrap">

  <!-- LEFT COLUMN -->

  <div>

```
<!-- WEEK NAV + STATS -->
<div class="card" style="margin-bottom:20px">
  <div class="card-header">
    <div class="week-nav">
      <button class="week-btn" onclick="prevWeek()" title="Minggu lepas"><i class="fas fa-chevron-left"></i></button>
      <div class="week-info">
        <span id="weekLabel">Minggu –</span>
        <span id="weekDates">–</span>
      </div>
      <button class="week-btn" onclick="nextWeek()" title="Minggu depan"><i class="fas fa-chevron-right"></i></button>
      <button class="btn btn-secondary btn-sm" onclick="goToCurrentWeek()" style="margin-left:4px">
        <i class="fas fa-rotate-left"></i> Semasa
      </button>
    </div>
    <div style="display:flex;gap:8px">
      <button class="btn btn-gold btn-sm" onclick="openReport()">
        <i class="fas fa-file-alt"></i> Laporan
      </button>
    </div>
  </div>

  <div style="padding:14px 20px 0">
    <div class="stats-row">
      <div class="stat-card">
        <div class="stat-icon navy"><i class="fas fa-users"></i></div>
        <div>
          <div class="stat-num" id="statTotal">–</div>
          <div class="stat-label">Jumlah Staf</div>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-icon green"><i class="fas fa-check-circle"></i></div>
        <div>
          <div class="stat-num" id="statDisahkan">–</div>
          <div class="stat-label">Disahkan</div>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-icon amber"><i class="fas fa-clock"></i></div>
        <div>
          <div class="stat-num" id="statBelum">–</div>
          <div class="stat-label">Belum Hantar</div>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-icon red"><i class="fas fa-exclamation-circle"></i></div>
        <div>
          <div class="stat-num" id="statLewat">–</div>
          <div class="stat-label">Lewat</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- TABLE CARD -->
<div class="card">
  <!-- Staff selector -->
  <div class="staff-selector-row">
    <label><i class="fas fa-user"></i> &nbsp;Staf Aktif:</label>
    <select id="staffSelect" onchange="selectStaffLogin(this.value)">
      <option value="">Pilih nama staf untuk upload</option>
    </select>
  </div>

  <!-- Filters -->
  <div class="toolbar">
    <div class="toolbar-search">
      <i class="fas fa-search"></i>
      <input type="text" id="searchInput" placeholder="Cari nama staf…" oninput="applyFilters()" />
    </div>
    <select id="filterKat" onchange="applyFilters()">
      <option value="">Semua Kategori</option>
      <option value="1">Pembantu Makmal</option>
      <option value="2">Pembantu Pengurusan Murid</option>
      <option value="3">Pembantu Tadbir</option>
      <option value="4">Pembantu Khidmat Am</option>
    </select>
    <select id="filterStatus" onchange="applyFilters()">
      <option value="">Semua Status</option>
      <option value="Disahkan">Disahkan</option>
      <option value="Belum Hantar">Belum Hantar</option>
      <option value="Lewat">Lewat</option>
    </select>
    <span id="filterCount"></span>
  </div>

  <p id="tableSubtitle"></p>

  <div class="table-wrap">
    <table>
      <thead>
        <tr>
          <th style="width:36px">#</th>
          <th>Nama Staf</th>
          <th>Kategori</th>
          <th>Minggu</th>
          <th>Muat Naik</th>
          <th>Jenis</th>
          <th>Nama Fail</th>
          <th>Tarikh Hantar</th>
          <th>Status</th>
          <th>Tindakan</th>
          <th>Semakan</th>
          <th>Pengesahan PK</th>
        </tr>
      </thead>
      <tbody id="tableBody"></tbody>
    </table>
  </div>
</div>
```

  </div><!-- /LEFT -->

  <!-- SIDEBAR -->

  <div class="sidebar">

```
<!-- CHART CARD -->
<div class="card">
  <div class="card-header">
    <div class="card-title"><i class="fas fa-chart-pie"></i> Carta Status</div>
  </div>
  <div class="card-body">
    <div class="pie-wrap">
      <canvas id="pieChart" width="180" height="180"></canvas>
      <div class="legend">
        <div class="legend-item">
          <div class="legend-label"><div class="legend-dot" style="background:#059669"></div>Disahkan</div>
          <div class="legend-val" id="leg1">–</div>
        </div>
        <div class="legend-item">
          <div class="legend-label"><div class="legend-dot" style="background:#d97706"></div>Belum Hantar</div>
          <div class="legend-val" id="leg2">–</div>
        </div>
        <div class="legend-item">
          <div class="legend-label"><div class="legend-dot" style="background:#dc2626"></div>Lewat</div>
          <div class="legend-val" id="leg3">–</div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- PRINCIPAL CARD -->
<div class="card">
  <div class="card-header">
    <div class="card-title"><i class="fas fa-stamp"></i> Pengesahan Pengetua</div>
  </div>
  <div class="card-body">
    <div class="section-label">Hajah Aniza Binti Baharuddin</div>

    <div id="principalAccessNote" class="principal-note" style="margin-bottom:12px">
      <i class="fas fa-lock"></i> Log masuk sebagai Pengetua untuk menandatangani rekod minggu ini.
    </div>

    <div id="principalStamp" class="principal-stamp">
      <i class="fas fa-pen-to-square" style="font-size:24px;color:var(--slate);opacity:.4"></i>
      <p style="font-size:12.5px;color:var(--slate)">Belum disahkan</p>
    </div>

    <div id="principalSignedInfo">
      <p id="principalSignedDetails"></p>
    </div>

    <div id="principalForm" class="principal-form" style="display:none">
      <div style="margin-top:12px">
        <div class="section-label">Tandatangani Rekod</div>
        <div class="form-group">
          <label>Tarikh Semakan</label>
          <input type="date" id="principalDate" />
        </div>
        <div class="form-group">
          <label>Catatan (pilihan)</label>
          <textarea id="principalNotes" rows="2" placeholder="Catatan semakan…"></textarea>
        </div>
        <button class="btn btn-gold" style="width:100%" onclick="signPrincipal()">
          <i class="fas fa-stamp"></i> Sahkan Minggu Ini
        </button>
      </div>
    </div>
  </div>
</div>
```

  </div><!-- /SIDEBAR -->

</div><!-- /MAIN WRAP -->

<!-- ══ MODALS ══ -->

<!-- Confirm cancel -->

<div class="modal-overlay" id="confirmModal">
  <div class="modal">
    <div class="modal-header">
      <h2><i class="fas fa-triangle-exclamation" style="color:var(--crimson)"></i> &nbsp;Batalkan Penghantaran</h2>
      <button class="modal-close" onclick="closeModal('confirmModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body">
      <p style="font-size:14px;color:var(--navy-soft)">Adakah anda pasti ingin membatalkan penghantaran ini? Fail yang dimuat naik juga akan dipadam.</p>
    </div>
    <div class="modal-footer">
      <button class="btn btn-secondary" onclick="closeModal('confirmModal')">Batal</button>
      <button class="btn btn-danger" onclick="confirmCancelSubmission()"><i class="fas fa-trash"></i> Ya, Batalkan</button>
    </div>
  </div>
</div>

<!-- Preview -->

<div class="modal-overlay" id="previewModal">
  <div class="modal">
    <div class="modal-header">
      <h2><i class="fas fa-eye" style="color:var(--blue)"></i> &nbsp;<span id="previewFileName"></span></h2>
      <button class="modal-close" onclick="closeModal('previewModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body">
      <div id="previewContainer"></div>
    </div>
  </div>
</div>

<!-- Pengesahan PK -->

<div class="modal-overlay" id="pengesahanModal">
  <div class="modal">
    <div class="modal-header">
      <h2><i class="fas fa-stamp" style="color:var(--gold)"></i> &nbsp;Pengesahan Penketua</h2>
      <button class="modal-close" onclick="closeModal('pengesahanModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body">
      <p style="font-size:13px;color:var(--slate);margin-bottom:14px">Rekod untuk: <strong id="pengesahanStaffName"></strong></p>
      <div id="pengesahanError" class="error-msg"><i class="fas fa-times-circle"></i> Hanya Pengetua yang boleh mengesahkan.</div>
      <div class="form-group">
        <label>Catatan Pengesahan (pilihan)</label>
        <textarea id="pengesahanCatatan" rows="3" placeholder="Masukkan catatan jika ada…"></textarea>
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-secondary" onclick="closeModal('pengesahanModal')">Batal</button>
      <button class="btn btn-gold" onclick="submitPengesahan()"><i class="fas fa-stamp"></i> Sahkan</button>
    </div>
  </div>
</div>

<!-- Report -->

<div class="modal-overlay" id="reportModal">
  <div class="modal">
    <div class="modal-header">
      <h2><i class="fas fa-file-alt" style="color:var(--gold)"></i> &nbsp;Laporan Mingguan</h2>
      <button class="modal-close" onclick="closeModal('reportModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body" id="reportBody"></div>
    <div class="modal-footer">
      <button class="btn btn-secondary" onclick="closeModal('reportModal')">Tutup</button>
    </div>
  </div>
</div>

<!-- Login -->

<div class="modal-overlay" id="loginModal">
  <div class="modal">
    <div class="modal-header">
      <h2><i class="fas fa-user-shield" style="color:var(--blue)"></i> &nbsp;Log Masuk</h2>
      <button class="modal-close" onclick="closeModal('loginModal')"><i class="fas fa-times"></i></button>
    </div>
    <div class="modal-body">
      <div class="role-tabs">
        <button class="btn btn-sm btn-primary" id="btnRolePengetua" onclick="setLoginRole('pengetua')">
          <i class="fas fa-user-tie"></i> Pengetua
        </button>
        <button class="btn btn-sm btn-secondary" id="btnRoleAdmin" onclick="setLoginRole('admin')">
          <i class="fas fa-user-cog"></i> Admin
        </button>
      </div>
      <div id="loginError" class="error-msg"><i class="fas fa-times-circle"></i> Kata laluan tidak sah.</div>
      <div class="form-group">
        <label>Kata Laluan</label>
        <input type="password" id="loginPass" placeholder="Masukkan kata laluan…"
          onkeydown="if(event.key==='Enter') doLogin()" />
      </div>
    </div>
    <div class="modal-footer">
      <button class="btn btn-secondary" onclick="closeModal('loginModal')">Batal</button>
      <button class="btn btn-primary" onclick="doLogin()"><i class="fas fa-right-to-bracket"></i> Log Masuk</button>
    </div>
  </div>
</div>

<!-- ══ SCRIPT ══ -->

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

  let app=null, auth=null, db=null, storage=null;
  let firebaseReady=false, firebaseUid=null;
  let currentWeekOffset=0, currentRole=null, currentLoginTab="pengetua", currentStaffId=null;
  let pendingCancelId=null, pendingPengesahanId=null;
  let submissions={}, weekSignatures={}, settingsData={ bannerUrl:null,bannerPath:null,logoUrl:null,logoPath:null };
  let autosaveTimer=null, unsubmissions=null, unweeksig=null, unsettings=null;

  function escapeHtml(str){
    return String(str??"")
      .replace(/&/g,"&amp;").replace(/</g,"&lt;")
      .replace(/>/g,"&gt;").replace(/"/g,"&quot;").replace(/'/g,"&#039;");
  }

  function showToast(msg, type=""){
    const container=document.getElementById("toastContainer");
    const toast=document.createElement("div");
    toast.className=`toast ${type}`;
    const icons={success:"fa-check-circle",error:"fa-times-circle",warning:"fa-exclamation-triangle",default:"fa-info-circle"};
    toast.innerHTML=`<i class="fas ${icons[type]||icons.default}"></i> ${escapeHtml(msg)}`;
    container.appendChild(toast);
    setTimeout(()=>{ toast.style.opacity="0"; toast.style.transition="opacity .4s"; setTimeout(()=>toast.remove(),400); },3000);
  }

  function triggerAutosave(){
    const ind=document.getElementById("autosaveIndicator");
    ind.classList.add("visible");
    clearTimeout(autosaveTimer);
    autosaveTimer=setTimeout(()=>ind.classList.remove("visible"),2200);
  }

  function openModal(id){ document.getElementById(id).classList.add("open"); document.body.style.overflow="hidden"; }
  function closeModal(id){
    document.getElementById(id).classList.remove("open");
    if(!document.querySelector(".modal-overlay.open")) document.body.style.overflow="";
  }
  window.closeModal=closeModal;

  document.querySelectorAll(".modal-overlay").forEach(o=>{
    o.addEventListener("click",e=>{ if(e.target===o){ o.classList.remove("open"); if(!document.querySelector(".modal-overlay.open")) document.body.style.overflow=""; } });
  });

  function getWeekStart(offset=0){
    const now=new Date(), day=now.getDay(), diff=day===0?-6:1-day;
    const mon=new Date(now); mon.setDate(now.getDate()+diff+offset*7); mon.setHours(0,0,0,0); return mon;
  }
  function getWeekEnd(offset=0){
    const mon=getWeekStart(offset), fri=new Date(mon);
    fri.setDate(mon.getDate()+4); fri.setHours(23,59,59,999); return fri;
  }
  function getWeekKey(offset=currentWeekOffset){
    const mon=getWeekStart(offset); return `week_${mon.getFullYear()}_${mon.getMonth()+1}_${mon.getDate()}`;
  }
  function getWeekNumber(offset=0){
    const mon=getWeekStart(offset), jan1=new Date(mon.getFullYear(),0,1);
    const days=Math.floor((mon-jan1)/86400000);
    return Math.ceil((days+jan1.getDay()+1)/7);
  }
  function formatDate(d){
    const days=["Ahad","Isnin","Selasa","Rabu","Khamis","Jumaat","Sabtu"];
    const months=["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];
    return `${days[d.getDay()]}, ${d.getDate()} ${months[d.getMonth()]} ${d.getFullYear()}`;
  }
  function formatDateShort(d){
    const months=["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];
    return `${d.getDate()} ${months[d.getMonth()]} ${d.getFullYear()}`;
  }

  function updateWeekDisplay(){
    const mon=getWeekStart(currentWeekOffset), fri=getWeekEnd(currentWeekOffset);
    const wn=getWeekNumber(currentWeekOffset);
    const months=["Jan","Feb","Mac","Apr","Mei","Jun","Jul","Ogo","Sep","Okt","Nov","Dis"];
    document.getElementById("weekLabel").textContent=`Minggu ${wn}`;
    document.getElementById("weekDates").textContent=`${formatDate(mon)} – ${formatDate(fri)}`;
    document.getElementById("tableSubtitle").textContent=
      `${mon.getDate()} ${months[mon.getMonth()]} – ${fri.getDate()} ${months[fri.getMonth()]} ${fri.getFullYear()}`;
  }

  function prevWeek(){ currentWeekOffset--; updateWeekDisplay(); subscribeWeekData(); }
  function nextWeek(){ currentWeekOffset++; updateWeekDisplay(); subscribeWeekData(); }
  function goToCurrentWeek(){ currentWeekOffset=0; updateWeekDisplay(); subscribeWeekData(); }
  window.prevWeek=prevWeek; window.nextWeek=nextWeek; window.goToCurrentWeek=goToCurrentWeek;

  function isLate(offset){ return new Date()>getWeekEnd(offset); }

  function computeStatus(staffId, weekOffset){
    const key=getWeekKey(weekOffset), sub=(submissions[key]||{})[staffId];
    if(!sub) return isLate(weekOffset)?"Lewat":"Belum Hantar";
    return sub.status||"Disahkan";
  }

  function populateStaffSelect(){
    const select=document.getElementById("staffSelect");
    select.innerHTML=`<option value="">Pilih nama staf untuk upload</option>`;
    STAFF_LIST.forEach(staff=>{
      const opt=document.createElement("option");
      opt.value=String(staff.id); opt.textContent=staff.nama;
      select.appendChild(opt);
    });
    const saved=localStorage.getItem("smkm_selected_staff");
    if(saved){ select.value=saved; currentStaffId=Number(saved); }
  }

  window.selectStaffLogin=function(staffId){
    currentStaffId=staffId?Number(staffId):null;
    if(currentStaffId){
      localStorage.setItem("smkm_selected_staff",String(currentStaffId));
      const staff=STAFF_LIST.find(s=>s.id===currentStaffId);
      showToast(`Staf aktif: ${staff?.nama||"Dipilih"}`,"success");
    } else {
      localStorage.removeItem("smkm_selected_staff");
      showToast("Pilihan staf dikosongkan.","warning");
    }
    renderTable();
  };

  function setFirebaseStatus(text){ document.getElementById("firebaseStatusText").textContent=text; }

  function applyBrandingToUI(){
    const bannerImg=document.getElementById("bannerImg");
    const logoImg=document.getElementById("logoImg");
    const logoText=document.getElementById("logoText");
    if(settingsData.bannerUrl){ bannerImg.src=settingsData.bannerUrl; bannerImg.style.display="block"; }
    else { bannerImg.removeAttribute("src"); bannerImg.style.display="none"; }
    if(settingsData.logoUrl){ logoImg.src=settingsData.logoUrl; logoImg.style.display="block"; logoText.style.display="none"; }
    else { logoImg.removeAttribute("src"); logoImg.style.display="none"; logoText.style.display="inline"; }
  }

  async function initFirebase(){
    if(hasPlaceholderConfig(firebaseConfig)){
      setFirebaseStatus("Sila lengkapkan config Firebase");
      showToast("Gantikan semua nilai PASTE_* dalam firebaseConfig dahulu.","error");
      renderTable(); updateStats(); updatePrincipalSection(); return;
    }
    try{
      app=initializeApp(firebaseConfig);
      auth=getAuth(app); db=getFirestore(app); storage=getStorage(app);
      await signInAnonymously(auth);
      onAuthStateChanged(auth, user=>{
        if(user){ firebaseUid=user.uid; firebaseReady=true; setFirebaseStatus("Tersambung"); subscribeSettings(); subscribeWeekData(); }
        else { firebaseReady=false; firebaseUid=null; setFirebaseStatus("Belum log masuk"); }
      });
    }catch(err){
      console.error(err); firebaseReady=false;
      setFirebaseStatus("Gagal sambung Firebase");
      showToast("Gagal sambung Firebase. Semak config dan rules.","error");
    }
  }

  function subscribeSettings(){
    if(!firebaseReady||!db) return;
    if(unsettings) unsettings();
    unsettings=onSnapshot(doc(db,"systemSettings","branding"), snap=>{
      settingsData=snap.exists()
        ?{ bannerUrl:snap.data().bannerUrl||null, bannerPath:snap.data().bannerPath||null, logoUrl:snap.data().logoUrl||null, logoPath:snap.data().logoPath||null }
        :{ bannerUrl:null, bannerPath:null, logoUrl:null, logoPath:null };
      applyBrandingToUI();
    }, err=>{ console.error(err); showToast("Gagal baca tetapan branding.","error"); });
  }

  function subscribeWeekData(){
    if(!firebaseReady||!db) return;
    const weekKey=getWeekKey();
    if(unsubmissions) unsubmissions();
    if(unweeksig) unweeksig();
    unsubmissions=onSnapshot(doc(db,"weeklySubmissions",weekKey), snap=>{
      const data=snap.exists()?snap.data():{records:{}};
      submissions[weekKey]=data.records||{};
      renderTable();
    }, err=>{ console.error(err); showToast("Gagal baca data penghantaran.","error"); });
    unweeksig=onSnapshot(doc(db,"weeklySignatures",weekKey), snap=>{
      weekSignatures[weekKey]=snap.exists()?snap.data():{};
      updatePrincipalSection();
    }, err=>{ console.error(err); showToast("Gagal baca pengesahan pengetua.","error"); });
  }

  async function saveWeekSubmissions(weekKey){
    await setDoc(doc(db,"weeklySubmissions",weekKey),{ records:submissions[weekKey]||{}, updatedAt:serverTimestamp() },{merge:true});
    triggerAutosave();
  }
  async function saveWeekSignature(weekKey){
    await setDoc(doc(db,"weeklySignatures",weekKey),{ ...weekSignatures[weekKey], updatedAt:serverTimestamp() },{merge:true});
    triggerAutosave();
  }
  async function saveBranding(){
    await setDoc(doc(db,"systemSettings","branding"),{ bannerUrl:settingsData.bannerUrl||null, bannerPath:settingsData.bannerPath||null, logoUrl:settingsData.logoUrl||null, logoPath:settingsData.logoPath||null, updatedAt:serverTimestamp() },{merge:true});
    triggerAutosave();
  }

  function applyFilters(){ renderTable(); }
  window.applyFilters=applyFilters;

  function renderTable(){
    const search=(document.getElementById("searchInput")?.value||"").toLowerCase();
    const filterKat=document.getElementById("filterKat")?.value||"";
    const filterStatus=document.getElementById("filterStatus")?.value||"";
    const key=getWeekKey();
    const mon=getWeekStart(currentWeekOffset), fri=getWeekEnd(currentWeekOffset);
    const weekRange=`${formatDateShort(mon)} – ${formatDateShort(fri)}`;

    const filtered=STAFF_LIST.filter(s=>{
      if(search&&!s.nama.toLowerCase().includes(search)) return false;
      if(filterKat&&String(s.kat)!==filterKat) return false;
      const st=computeStatus(s.id,currentWeekOffset);
      if(filterStatus&&st!==filterStatus) return false;
      return true;
    });

    document.getElementById("filterCount").textContent=`Paparan: ${filtered.length} / ${STAFF_LIST.length} rekod`;

    const tbody=document.getElementById("tableBody");
    tbody.innerHTML="";

    filtered.forEach((staff,idx)=>{
      const sub=(submissions[key]||{})[staff.id];
      const status=computeStatus(staff.id,currentWeekOffset);
      const statusClass=status==="Disahkan"?"status-disahkan":status==="Lewat"?"status-lewat":"status-belum";
      const isOwnRow=currentStaffId===staff.id;

      let ftBadge='<span class="empty-cell">–</span>';
      if(sub){
        const ext=(sub.fileType||"").toLowerCase();
        const cls=ext==="pdf"?"ft-pdf":(ext==="doc"||ext==="docx")?"ft-doc":"ft-img";
        ftBadge=`<span class="file-type-badge ${cls}">${escapeHtml(ext.toUpperCase())}</span>`;
      }

      const uploadCell=sub
        ?`<span style="font-size:12px;color:var(--emerald)"><i class="fas fa-check-circle"></i> Dimuat naik</span>`
        :isOwnRow
          ?`<label class="upload-label" for="fileInput_${staff.id}"><i class="fas fa-upload"></i> Muat Naik</label>
             <input type="file" id="fileInput_${staff.id}" accept=".pdf,.jpg,.jpeg,.png,.doc,.docx" onchange="handleUpload(event,${staff.id})">`
          :`<span class="empty-cell">–</span>`;

      let actions="";
      if(sub){
        actions+=`<button class="btn-sm btn-secondary" type="button" onclick="previewFile(${staff.id})"><i class="fas fa-eye"></i> Lihat</button>`;
        if(isOwnRow||currentRole==="admin"||currentRole==="pengetua"){
          actions+=`<button class="btn-sm btn-danger" type="button" onclick="openCancelConfirm(${staff.id})"><i class="fas fa-times"></i> Batal</button>`;
        }
      } else { actions='<span class="empty-cell">–</span>'; }

      const semakanVal=sub?(sub.semakan||""):"";
      const semakanCell=(currentRole==="admin"||currentRole==="pengetua")
        ?`<textarea class="semakan-input" rows="2" placeholder="Catatan semakan..." onchange="saveSemakan(${staff.id},this.value)">${escapeHtml(semakanVal)}</textarea>`

```
    :(semakanVal?`<span style="font-size:12px;white-space:normal;line-height:1.45">${escapeHtml(semakanVal)}</span>`:'<span class="empty-cell">–</span>');

  const pengesahan=sub?sub.pengesahan:null;
  let pengesahanCell="";
  if(pengesahan){
    pengesahanCell=`<div class="pengesahan-cell">
      <span class="pengesahan-badge pengesahan-disahkan"><i class="fas fa-check-circle"></i> Disahkan</span>
      <span class="catatan-text">${escapeHtml(pengesahan.catatan||"")}</span>
      <span style="font-size:10.5px;color:var(--slate)">${escapeHtml(pengesahan.tarikh||"")}</span>
    </div>`;
  } else if(sub&&currentRole==="pengetua"){
    pengesahanCell=`<button class="btn-sm btn-gold" type="button" onclick="openPengesahan(${staff.id})"><i class="fas fa-stamp"></i> Sahkan</button>`;
  } else if(sub){
    pengesahanCell=`<span class="pengesahan-badge pengesahan-pending"><i class="fas fa-hourglass-half"></i> Menunggu</span>`;
  } else {
    pengesahanCell='<span class="empty-cell">–</span>';
  }

  const tr=document.createElement("tr");
  tr.innerHTML=`
    <td class="bil-cell">${idx+1}</td>
    <td class="nama-cell td-wrap">${escapeHtml(staff.nama)}${isOwnRow?' <span style="font-size:11px;color:var(--amber)">(Anda)</span>':''}</td>
    <td><span class="kat-badge ${KAT_CSS[staff.kat]}">${escapeHtml(KAT_NAMES[staff.kat])}</span></td>
    <td style="font-size:12px">${escapeHtml(weekRange)}</td>
    <td>${uploadCell}</td>
    <td>${ftBadge}</td>
    <td style="max-width:160px;overflow:hidden;text-overflow:ellipsis;font-size:12px">${sub?escapeHtml(sub.fileName):'<span class="empty-cell">–</span>'}</td>
    <td style="font-size:12px">${sub?escapeHtml(sub.tarikhHantar):'<span class="empty-cell">–</span>'}</td>
    <td><span class="status-badge ${statusClass}"><i class="fas ${status==='Disahkan'?'fa-check-circle':status==='Lewat'?'fa-exclamation-circle':'fa-clock'}"></i> ${escapeHtml(status)}</span></td>
    <td><div class="action-group">${actions}</div></td>
    <td class="semakan-cell">${semakanCell}</td>
    <td>${pengesahanCell}</td>
  `;
  tbody.appendChild(tr);
});

updateStats(); updateNotifications(); updatePrincipalSection();
```

}

window.handleUpload=async function(event, staffId){
try{
if(!firebaseReady||!storage||!db){ showToast(“Firebase belum sedia.”,“error”); return; }
if(currentStaffId!==staffId){ showToast(“Hanya staf terpilih boleh upload fail sendiri.”,“error”); event.target.value=””; return; }
const file=event.target.files?.[0]; if(!file) return;
const allowed=[“pdf”,“jpg”,“jpeg”,“png”,“doc”,“docx”];
const ext=file.name.split(”.”).pop().toLowerCase();
if(!allowed.includes(ext)){ showToast(“Jenis fail tidak dibenarkan.”,“error”); event.target.value=””; return; }
const weekKey=getWeekKey(), now=new Date();
const safeName=file.name.replace(/[^\w.-]+/g,”_”);
const storagePath=`submissions/${weekKey}/${staffId}/${Date.now()}_${safeName}`;
const storageRef=ref(storage,storagePath);
showToast(“Sedang upload fail…”,“warning”);
await uploadBytes(storageRef,file);
const fileUrl=await getDownloadURL(storageRef);
if(!submissions[weekKey]) submissions[weekKey]={};
const oldRecord=submissions[weekKey][staffId];
if(oldRecord?.storagePath){ try{ await deleteObject(ref(storage,oldRecord.storagePath)); }catch(e){ console.warn(e); } }
submissions[weekKey][staffId]={
staffId, fileName:file.name, fileType:ext, fileUrl, storagePath,
tarikhHantar:formatDateShort(now),
status:isLate(currentWeekOffset)?“Lewat”:“Disahkan”,
semakan:oldRecord?.semakan||””,
pengesahan:oldRecord?.pengesahan||null,
uploadedByName:STAFF_LIST.find(s=>s.id===staffId)?.nama||””,
updatedAtMs:Date.now()
};
await saveWeekSubmissions(weekKey);
showToast(“Fail berjaya dimuat naik!”,“success”);
renderTable();
}catch(err){ console.error(err); showToast(“Upload gagal. Semak Storage Rules dan config.”,“error”); }
finally{ event.target.value=””; }
};

window.openCancelConfirm=function(staffId){ pendingCancelId=staffId; openModal(“confirmModal”); };

window.confirmCancelSubmission=async function(){
try{
const weekKey=getWeekKey(), row=submissions[weekKey]?.[pendingCancelId];
if(!row) return;
const canDelete=currentStaffId===pendingCancelId||currentRole===“admin”||currentRole===“pengetua”;
if(!canDelete){ showToast(“Anda tidak dibenarkan membatalkan rekod ini.”,“error”); return; }
if(row.storagePath){ try{ await deleteObject(ref(storage,row.storagePath)); }catch(e){ console.warn(e); } }
delete submissions[weekKey][pendingCancelId];
await saveWeekSubmissions(weekKey);
renderTable(); showToast(“Penghantaran berjaya dibatalkan.”,“warning”);
}catch(err){ console.error(err); showToast(“Gagal batalkan penghantaran.”,“error”); }
finally{ closeModal(“confirmModal”); pendingCancelId=null; }
};

window.previewFile=function(staffId){
const weekKey=getWeekKey(), sub=submissions[weekKey]?.[staffId]; if(!sub) return;
document.getElementById(“previewFileName”).textContent=sub.fileName||””;
const container=document.getElementById(“previewContainer”); container.innerHTML=””;
const ext=(sub.fileType||””).toLowerCase();
if([“jpg”,“jpeg”,“png”].includes(ext)){
const img=document.createElement(“img”); img.src=sub.fileUrl; img.alt=sub.fileName||“Preview”; container.appendChild(img);
} else if(ext===“pdf”){
const iframe=document.createElement(“iframe”); iframe.src=sub.fileUrl; iframe.title=sub.fileName||“PDF Preview”; container.appendChild(iframe);
} else {
container.innerHTML=`<div class="preview-placeholder"><i class="fas fa-file-alt" style="font-size:28px;margin-bottom:8px"></i><p>Pratonton tidak tersedia untuk jenis fail ini.<br><strong>${escapeHtml(sub.fileName||"")}</strong></p><p style="margin-top:10px"><a href="${sub.fileUrl}" target="_blank" rel="noopener">Buka fail</a></p></div>`;
}
openModal(“previewModal”);
};

window.saveSemakan=async function(staffId,value){
try{
if(currentRole!==“admin”&&currentRole!==“pengetua”) return;
const weekKey=getWeekKey();
if(!submissions[weekKey]?.[staffId]) return;
submissions[weekKey][staffId].semakan=value;
await saveWeekSubmissions(weekKey);
}catch(err){ console.error(err); showToast(“Gagal simpan semakan.”,“error”); }
};

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
submissions[weekKey][pendingPengesahanId].pengesahan={
tarikh:formatDateShort(new Date()),
catatan:document.getElementById(“pengesahanCatatan”).value||””
};
submissions[weekKey][pendingPengesahanId].status=“Disahkan”;
await saveWeekSubmissions(weekKey);
closeModal(“pengesahanModal”); renderTable();
showToast(“Pengesahan berjaya disimpan!”,“success”);
}catch(err){ console.error(err); showToast(“Gagal simpan pengesahan.”,“error”); }
};

function updatePrincipalSection(){
const key=getWeekKey(), sig=weekSignatures[key]||{};
const isPrincipal=currentRole===“pengetua”;
document.getElementById(“principalAccessNote”).style.display=isPrincipal?“none”:“block”;
document.getElementById(“principalForm”).style.display=isPrincipal&&!sig.signed?“grid”:“none”;
const stamp=document.getElementById(“principalStamp”);
const signedInfo=document.getElementById(“principalSignedInfo”);
if(sig.signed){
stamp.className=“principal-stamp signed”;
stamp.innerHTML=`<div class="stamp-sign">&#10003;</div><div class="stamp-name">Hajah Aniza Binti Baharuddin</div><div class="stamp-date">Tarikh Semakan: ${escapeHtml(sig.date||"")}</div>`;
signedInfo.style.display=“block”;
document.getElementById(“principalSignedDetails”).textContent=`Catatan: ${sig.notes||"Tiada catatan"} | Tarikh: ${sig.date||""}`;
} else {
stamp.className=“principal-stamp”;
stamp.innerHTML=`<i class="fas fa-pen-to-square" style="font-size:24px;color:var(--slate);opacity:.4"></i><p style="font-size:12.5px;color:var(--slate)">Belum disahkan</p>`;
signedInfo.style.display=“none”;
}
if(isPrincipal){
const today=new Date();
document.getElementById(“principalDate”).value=`${today.getFullYear()}-${String(today.getMonth()+1).padStart(2,"0")}-${String(today.getDate()).padStart(2,"0")}`;
}
}

window.signPrincipal=async function(){
try{
if(currentRole!==“pengetua”){ showToast(“Hanya Pengetua boleh menandatangani.”,“error”); return; }
const key=getWeekKey();
const dateVal=document.getElementById(“principalDate”).value;
const notesVal=document.getElementById(“principalNotes”).value;
weekSignatures[key]={ signed:true, date:dateVal?formatDateShort(new Date(dateVal)):formatDateShort(new Date()), notes:notesVal||”” };
await saveWeekSignature(key);
updatePrincipalSection();
showToast(“Pengesahan pengetua berjaya disimpan!”,“success”);
}catch(err){ console.error(err); showToast(“Gagal simpan tandatangan pengetua.”,“error”); }
};

function updateStats(){
let d=0,b=0,l=0;
STAFF_LIST.forEach(s=>{ const st=computeStatus(s.id,currentWeekOffset); if(st===“Disahkan”) d++; else if(st===“Lewat”) l++; else b++; });
document.getElementById(“statTotal”).textContent=STAFF_LIST.length;
document.getElementById(“statDisahkan”).textContent=d;
document.getElementById(“statBelum”).textContent=b;
document.getElementById(“statLewat”).textContent=l;
document.getElementById(“leg1”).textContent=d;
document.getElementById(“leg2”).textContent=b;
document.getElementById(“leg3”).textContent=l;
drawPie(d,b,l);
}

function drawPie(d,b,l){
const canvas=document.getElementById(“pieChart”);
const ctx=canvas.getContext(“2d”);
const total=d+b+l;
const cssSize=Math.min(canvas.clientWidth||180,180);
const ratio=window.devicePixelRatio||1;
canvas.width=cssSize*ratio; canvas.height=cssSize*ratio;
canvas.style.width=`${cssSize}px`; canvas.style.height=`${cssSize}px`;
ctx.setTransform(ratio,0,0,ratio,0,0);
ctx.clearRect(0,0,cssSize,cssSize);
const cx=cssSize/2, cy=cssSize/2, r=Math.max(50,cssSize/2-10);
const data=[{val:d,color:”#059669”},{val:b,color:”#d97706”},{val:l,color:”#dc2626”}];
if(total===0){
ctx.beginPath(); ctx.arc(cx,cy,r,0,Math.PI*2); ctx.fillStyle=”#e2e8f0”; ctx.fill(); return;
}
let angle=-Math.PI/2;
data.forEach(seg=>{
if(!seg.val) return;
const slice=(seg.val/total)*Math.PI*2;
ctx.beginPath(); ctx.moveTo(cx,cy); ctx.arc(cx,cy,r,angle,angle+slice); ctx.closePath();
ctx.fillStyle=seg.color; ctx.fill();
ctx.strokeStyle=”#fff”; ctx.lineWidth=2; ctx.stroke();
angle+=slice;
});
ctx.beginPath(); ctx.arc(cx,cy,Math.max(28,r*.45),0,Math.PI*2); ctx.fillStyle=”#fff”; ctx.fill();
ctx.fillStyle=”#1e293b”; ctx.font=`bold 13px "Plus Jakarta Sans"`; ctx.textAlign=“center”; ctx.textBaseline=“middle”;
ctx.fillText(String(total),cx,cy-6);
ctx.fillStyle=”#64748b”; ctx.font=`10px "Plus Jakarta Sans"`; ctx.fillText(“staf”,cx,cy+10);
}

function updateNotifications(){
const key=getWeekKey(), items=[];
STAFF_LIST.forEach(s=>{
const sub=submissions[key]?.[s.id];
if(!sub) items.push({type:“amber”,msg:`${s.nama.split(" ")[0]} belum hantar`});
else if(sub.status===“Lewat”) items.push({type:“red”,msg:`${s.nama.split(" ")[0]} lewat`});
});
const shortList=items.slice(0,5);
document.getElementById(“notifBadge”).textContent=shortList.length;
const list=document.getElementById(“notifList”); list.innerHTML=””;
if(shortList.length===0){
list.innerHTML=`<div class="notif-item"><div class="notif-dot green"></div><span>Semua rekod terkini terkawal.</span></div>`; return;
}
shortList.forEach(it=>{
const div=document.createElement(“div”); div.className=“notif-item”;
div.innerHTML=`<div class="notif-dot ${it.type}"></div><span>${escapeHtml(it.msg)}</span>`;
list.appendChild(div);
});
}

window.toggleNotif=function(){ document.getElementById(“notifPanel”).classList.toggle(“open”); };

document.addEventListener(“click”,function(e){
const w=document.querySelector(”.notif-wrapper”);
if(w&&!w.contains(e.target)) document.getElementById(“notifPanel”).classList.remove(“open”);
});

window.openReport=function(){
const key=getWeekKey(), mon=getWeekStart(currentWeekOffset), fri=getWeekEnd(currentWeekOffset);
const wn=getWeekNumber(currentWeekOffset);
const months=[“Jan”,“Feb”,“Mac”,“Apr”,“Mei”,“Jun”,“Jul”,“Ogo”,“Sep”,“Okt”,“Nov”,“Dis”];
const weekStr=`${mon.getDate()} ${months[mon.getMonth()]} – ${fri.getDate()} ${months[fri.getMonth()]} ${fri.getFullYear()}`;
let d=0,b=0,l=0;
STAFF_LIST.forEach(s=>{ const st=computeStatus(s.id,currentWeekOffset); if(st===“Disahkan”) d++; else if(st===“Lewat”) l++; else b++; });
const sig=weekSignatures[key]||{};
let rows=””;
STAFF_LIST.forEach((s,i)=>{
const sub=submissions[key]?.[s.id];
const st=computeStatus(s.id,currentWeekOffset);
const stColor=st===“Disahkan”?”#059669”:st===“Lewat”?”#dc2626”:”#d97706”;
const peng=sub?.pengesahan?`✓ ${sub.pengesahan.tarikh}`:”–”;
rows+=`<tr><td>${i+1}</td><td>${escapeHtml(s.nama)}</td><td>${escapeHtml(KAT_NAMES[s.kat])}</td><td>${sub?escapeHtml(sub.fileName):"–"}</td><td>${sub?escapeHtml(sub.tarikhHantar):"–"}</td><td style="font-weight:700;color:${stColor}">${escapeHtml(st)}</td><td>${escapeHtml(peng)}</td></tr>`;
});
document.getElementById(“reportBody”).innerHTML=` <div style="background:var(--gold-pale);border:1px solid #fde68a;border-radius:var(--radius-sm);padding:14px 16px;margin-bottom:16px"> <p><strong>Sekolah:</strong> Sekolah Menengah Kebangsaan Mentakab</p> <p><strong>Pengetua:</strong> Hajah Aniza Binti Baharuddin</p> <p><strong>Minggu:</strong> Minggu ${wn} (${weekStr})</p> <p><strong>Tarikh Laporan:</strong> ${formatDateShort(new Date())}</p> <p style="margin-top:8px"> <span style="color:var(--emerald);font-weight:700">✓ Disahkan: ${d}</span> &nbsp;|&nbsp; <span style="color:var(--amber);font-weight:700">Belum Hantar: ${b}</span> &nbsp;|&nbsp; <span style="color:var(--crimson);font-weight:700">Lewat: ${l}</span> </p> <p style="margin-top:6px;font-size:12px"><strong>Status Pengesahan Pengetua:</strong> ${sig.signed?`<span style="color:var(--emerald);font-weight:700">✓ Disahkan pada ${escapeHtml(sig.date||””)}</span>`:'<span style="color:var(--slate)">Belum Disahkan</span>'}</p> </div> <div style="overflow-x:auto"> <table class="report-table"> <thead><tr><th>Bil</th><th>Nama Staf</th><th>Kategori</th><th>Nama Fail</th><th>Tarikh Hantar</th><th>Status</th><th>Pengesahan Pengetua</th></tr></thead> <tbody>${rows}</tbody> </table> </div> ${sig.notes?`<p style="margin-top:14px;font-size:12.5px;color:var(--navy)"><strong>Catatan Pengetua:</strong> ${escapeHtml(sig.notes)}</p>`:""} `;
openModal(“reportModal”);
};

window.setLoginRole=function(role){
currentLoginTab=role;
document.getElementById(“btnRolePengetua”).className=role===“pengetua”?“btn btn-sm btn-primary”:“btn btn-sm btn-secondary”;
document.getElementById(“btnRoleAdmin”).className=role===“admin”?“btn btn-sm btn-primary”:“btn btn-sm btn-secondary”;
};

window.openLogin=function(){
if(currentRole){ logout(); return; }
document.getElementById(“loginPass”).value=””;
document.getElementById(“loginError”).style.display=“none”;
setLoginRole(“pengetua”);
openModal(“loginModal”);
};

window.doLogin=function(){
const pass=document.getElementById(“loginPass”).value;
const correct=currentLoginTab===“pengetua”?“1234”:“0000”;
if(pass!==correct){ document.getElementById(“loginError”).style.display=“block”; return; }
currentRole=currentLoginTab;
closeModal(“loginModal”);
const roleLabel=currentRole===“pengetua”?“Pengetua”:“Admin”;
document.getElementById(“adminBtnText”).textContent=`Log Keluar (${roleLabel})`;
document.getElementById(“adminBtn”).classList.add(“logged-in”);
if(currentRole===“admin”) document.getElementById(“adminBar”).classList.add(“visible”);
else document.getElementById(“adminBar”).classList.remove(“visible”);
showToast(`Selamat datang, ${roleLabel}!`,“success”);
renderTable();
};

function logout(){
currentRole=null;
document.getElementById(“adminBtnText”).textContent=“Log Masuk”;
document.getElementById(“adminBtn”).classList.remove(“logged-in”);
document.getElementById(“adminBar”).classList.remove(“visible”);
renderTable();
showToast(“Anda telah log keluar.”,“warning”);
}
window.logout=logout;

async function uploadBrandingFile(file,type){
const safeName=file.name.replace(/[^\w.-]+/g,”_”);
const filePath=`branding/${type}/${Date.now()}_${safeName}`;
const fileRef=ref(storage,filePath);
await uploadBytes(fileRef,file);
const url=await getDownloadURL(fileRef);
return { url, path:filePath };
}

window.changeBanner=async function(event){
try{
if(currentRole!==“admin”){ showToast(“Hanya admin boleh tukar banner.”,“error”); return; }
if(!firebaseReady||!storage){ showToast(“Firebase belum sedia.”,“error”); return; }
const file=event.target.files?.[0]; if(!file) return;
showToast(“Sedang memuat naik banner…”,“warning”);
const result=await uploadBrandingFile(file,“banner”);
if(settingsData.bannerPath){ try{ await deleteObject(ref(storage,settingsData.bannerPath)); }catch(e){ console.warn(e); } }
settingsData.bannerUrl=result.url; settingsData.bannerPath=result.path;
applyBrandingToUI(); await saveBranding();
showToast(“Banner berjaya diubah!”,“success”);
}catch(err){ console.error(err); showToast(“Gagal simpan banner.”,“error”); }
finally{ event.target.value=””; }
};

window.changeLogo=async function(event){
try{
if(currentRole!==“admin”){ showToast(“Hanya admin boleh tukar logo.”,“error”); return; }
if(!firebaseReady||!storage){ showToast(“Firebase belum sedia.”,“error”); return; }
const file=event.target.files?.[0]; if(!file) return;
showToast(“Sedang memuat naik logo…”,“warning”);
const result=await uploadBrandingFile(file,“logo”);
if(settingsData.logoPath){ try{ await deleteObject(ref(storage,settingsData.logoPath)); }catch(e){ console.warn(e); } }
settingsData.logoUrl=result.url; settingsData.logoPath=result.path;
applyBrandingToUI(); await saveBranding();
showToast(“Logo berjaya diubah!”,“success”);
}catch(err){ console.error(err); showToast(“Gagal simpan logo.”,“error”); }
finally{ event.target.value=””; }
};

window.addEventListener(“resize”, updateStats);

populateStaffSelect();
updateWeekDisplay();
renderTable();
updateStats();
updatePrincipalSection();
initFirebase();
</script>

</body>
</html>