<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>NTL/BSCS Parking</title>
<link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0f1117; --bg2: #161820; --bg3: #1e2030; --bg4: #252840;
  --accent: #4f9cf9; --accent2: #7c6af7; --green: #3ecf8e;
  --amber: #f5a623; --red: #f06060;
  --border: rgba(255,255,255,0.07); --border2: rgba(255,255,255,0.12);
  --text: #e8eaf0; --muted: #7c8096;
  --font: 'Sarabun', sans-serif; --mono: 'IBM Plex Mono', monospace;
  --sidebar-w: 220px; --topbar-h: 56px; --bottom-nav-h: 64px;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html,body{height:100%;background:var(--bg);color:var(--text);font-family:var(--font);font-size:14px;overflow:hidden;}

/* ═══ SHELL ═══ */
.shell{display:flex;height:100vh;overflow:hidden;}

/* ═══ SIDEBAR (desktop only) ═══ */
.sidebar{
  width:var(--sidebar-w);background:var(--bg2);border-right:1px solid var(--border);
  display:flex;flex-direction:column;flex-shrink:0;overflow-y:auto;
  transition:transform .25s ease;
}
.logo{padding:20px 18px 16px;border-bottom:1px solid var(--border);}
.logo-mark{font-family:var(--mono);font-size:10px;color:var(--accent);letter-spacing:2px;}
.logo-title{font-size:15px;font-weight:600;margin-top:3px;}
.logo-sub{font-size:11px;color:var(--muted);margin-top:1px;}
.nav{padding:12px 10px;flex:1;}
.nav-label{font-size:10px;letter-spacing:1.5px;color:var(--muted);padding:0 8px;margin:8px 0 4px;text-transform:uppercase;}
.nav-item{display:flex;align-items:center;gap:10px;padding:9px 10px;border-radius:8px;cursor:pointer;font-size:13.5px;color:var(--muted);transition:all .15s;margin-bottom:1px;}
.nav-item:hover,.nav-item.active{background:rgba(79,156,249,.12);color:var(--accent);}
.nav-item svg{width:15px;height:15px;flex-shrink:0;}
.quota-box{margin:0 10px 16px;background:var(--bg3);border:1px solid var(--border);border-radius:10px;padding:12px;}
.quota-label{font-size:11px;color:var(--muted);margin-bottom:5px;}
.quota-nums{font-family:var(--mono);font-size:20px;font-weight:500;color:var(--accent);}
.quota-nums span{font-size:12px;color:var(--muted);font-family:var(--font);}
.quota-bar-bg{background:var(--bg4);border-radius:4px;height:5px;margin-top:7px;}
.quota-bar-fill{background:linear-gradient(90deg,var(--accent),var(--accent2));height:5px;border-radius:4px;width:68%;}

/* ═══ MAIN ═══ */
.main{flex:1;display:flex;flex-direction:column;overflow:hidden;}

/* ═══ TOPBAR ═══ */
.topbar{
  height:var(--topbar-h);background:var(--bg2);border-bottom:1px solid var(--border);
  display:flex;align-items:center;padding:0 16px;gap:10px;flex-shrink:0;
}
.menu-btn{display:none;background:none;border:none;color:var(--muted);cursor:pointer;padding:6px;}
.topbar-title{font-size:15px;font-weight:500;flex:1;}
.view-tabs{display:flex;background:var(--bg3);border-radius:8px;padding:3px;gap:2px;}
.tab{padding:5px 12px;border-radius:6px;font-size:13px;cursor:pointer;color:var(--muted);transition:all .15s;white-space:nowrap;}
.tab.active{background:var(--bg4);color:var(--text);}
.date-nav{display:flex;align-items:center;gap:8px;}
.date-nav button{background:var(--bg3);border:1px solid var(--border);color:var(--muted);width:28px;height:28px;border-radius:6px;cursor:pointer;font-size:14px;display:flex;align-items:center;justify-content:center;transition:all .15s;}
.date-nav button:hover{border-color:var(--accent);color:var(--accent);}
.date-label{font-family:var(--mono);font-size:12px;color:var(--text);min-width:130px;text-align:center;}
.btn-add{background:var(--accent);color:#fff;border:none;padding:7px 14px;border-radius:8px;font-size:13px;font-family:var(--font);cursor:pointer;font-weight:500;white-space:nowrap;transition:opacity .15s;}
.btn-add:hover{opacity:.85;}
.btn-add:active{transform:scale(.97);}

/* ═══ CONTENT AREA ═══ */
.content{flex:1;overflow-y:auto;padding:20px 20px;-webkit-overflow-scrolling:touch;}

/* ═══ STATS ═══ */
.stats{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:20px;}
.stat-card{background:var(--bg2);border:1px solid var(--border);border-radius:12px;padding:14px 16px;}
.stat-top{display:flex;align-items:center;justify-content:space-between;margin-bottom:7px;}
.stat-icon{width:30px;height:30px;border-radius:8px;display:flex;align-items:center;justify-content:center;}
.stat-icon.blue{background:rgba(79,156,249,.15);}
.stat-icon.green{background:rgba(62,207,142,.15);}
.stat-icon.amber{background:rgba(245,166,35,.15);}
.stat-icon.red{background:rgba(240,96,96,.15);}
.stat-badge{font-size:10px;padding:2px 7px;border-radius:20px;font-family:var(--mono);}
.stat-badge.up{background:rgba(62,207,142,.15);color:var(--green);}
.stat-badge.warn{background:rgba(245,166,35,.15);color:var(--amber);}
.stat-val{font-family:var(--mono);font-size:24px;font-weight:500;}
.stat-label{font-size:11px;color:var(--muted);margin-top:2px;}

/* ═══ PANELS ═══ */
.panels{display:grid;grid-template-columns:1fr 300px;gap:16px;}
.panel{background:var(--bg2);border:1px solid var(--border);border-radius:12px;overflow:hidden;}
.panel-head{padding:13px 16px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;}
.panel-title{font-size:13.5px;font-weight:500;}
.panel-meta{font-size:12px;color:var(--muted);}

/* ═══ TABLE ═══ */
.tbl-wrap{overflow-x:auto;}
table{width:100%;border-collapse:collapse;min-width:520px;}
thead th{font-size:11px;color:var(--muted);padding:9px 14px;text-align:left;border-bottom:1px solid var(--border);font-weight:400;letter-spacing:.4px;}
tbody tr{border-bottom:1px solid var(--border);transition:background .1s;}
tbody tr:last-child{border-bottom:none;}
tbody tr:hover{background:var(--bg3);}
tbody td{padding:10px 14px;font-size:13px;}
.plate{font-family:var(--mono);font-size:12px;background:var(--bg3);padding:2px 7px;border-radius:4px;border:1px solid var(--border);letter-spacing:1px;}
.badge{display:inline-block;font-size:11px;padding:2px 8px;border-radius:20px;font-weight:500;}
.badge.rotate{background:rgba(79,156,249,.15);color:var(--accent);}
.badge.replace{background:rgba(124,106,247,.15);color:var(--accent2);}
.badge.night{background:rgba(245,166,35,.15);color:var(--amber);}
.badge.normal{background:rgba(62,207,142,.12);color:var(--green);}

/* ═══ MINI CAL ═══ */
.cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:3px;padding:12px;}
.cal-day-name{font-size:10px;color:var(--muted);text-align:center;padding-bottom:3px;}
.cal-cell{aspect-ratio:1;border-radius:6px;display:flex;flex-direction:column;align-items:center;justify-content:center;cursor:pointer;transition:all .15s;border:1px solid transparent;}
.cal-cell:hover{border-color:var(--accent);}
.cal-cell.empty{opacity:0;pointer-events:none;}
.cal-cell.today{border-color:var(--accent);background:rgba(79,156,249,.08);}
.cal-cell.selected{background:var(--accent);}
.cal-date{font-size:11px;font-family:var(--mono);}
.cal-dot{width:4px;height:4px;border-radius:50%;margin-top:1px;}
.cal-cell.full .cal-dot{background:var(--red);}
.cal-cell.busy .cal-dot{background:var(--amber);}
.cal-cell.free .cal-dot{background:var(--green);}
.cal-cell.selected .cal-date{color:#fff;}
.cal-cell.selected .cal-dot{background:rgba(255,255,255,.7);}
.cal-legend{display:flex;gap:10px;padding:0 12px 12px;}
.dot{width:6px;height:6px;border-radius:50%;flex-shrink:0;}
.cal-legend-item{display:flex;align-items:center;gap:5px;font-size:11px;color:var(--muted);}

/* ═══ MONTH VIEW ═══ */
.month-bar-row{display:flex;align-items:center;padding:7px 16px;gap:10px;border-bottom:1px solid var(--border);}
.month-bar-row:last-child{border-bottom:none;}
.month-day{font-family:var(--mono);font-size:12px;color:var(--muted);width:26px;flex-shrink:0;}
.month-bar-bg{flex:1;background:var(--bg3);border-radius:4px;height:7px;}
.month-bar-fill{height:7px;border-radius:4px;}
.month-count{font-family:var(--mono);font-size:12px;color:var(--muted);width:20px;text-align:right;flex-shrink:0;}

/* ═══ BIG CAL ═══ */
.big-cal-grid{display:grid;grid-template-columns:repeat(7,1fr);gap:6px;padding:14px;}
.big-cal-cell{border:1px solid var(--border);border-radius:8px;padding:8px;min-height:62px;cursor:pointer;transition:border .15s;}
.big-cal-cell:hover{border-color:var(--accent);}
.big-cal-cell.today{border-color:var(--accent);background:rgba(79,156,249,.08);}

/* ═══ VIEW TOGGLE ═══ */
.view-section{display:none;}
.view-section.active{display:block;}

/* ═══ MOBILE BOTTOM NAV ═══ */
.bottom-nav{
  display:none;height:var(--bottom-nav-h);background:var(--bg2);
  border-top:1px solid var(--border);flex-shrink:0;
}
.bottom-nav-inner{display:flex;height:100%;}
.bnav-item{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:3px;cursor:pointer;color:var(--muted);transition:color .15s;font-size:10px;}
.bnav-item.active{color:var(--accent);}
.bnav-item svg{width:20px;height:20px;}

/* ═══ MOBILE OVERLAY SIDEBAR ═══ */
.sidebar-overlay{display:none;position:fixed;inset:0;background:rgba(0,0,0,.6);z-index:40;}
.sidebar-overlay.open{display:block;}

/* ═══ MODAL / FORM ═══ */
.modal-bg{display:none;position:fixed;inset:0;background:rgba(0,0,0,.7);z-index:50;align-items:flex-end;justify-content:center;}
.modal-bg.open{display:flex;}
.modal{background:var(--bg2);border-radius:20px 20px 0 0;padding:20px 20px 32px;width:100%;max-width:520px;max-height:90vh;overflow-y:auto;animation:slideUp .25s ease;}
@keyframes slideUp{from{transform:translateY(30px);opacity:0;}to{transform:translateY(0);opacity:1;}}
.modal-handle{width:40px;height:4px;background:var(--border2);border-radius:4px;margin:0 auto 18px;}
.modal-title{font-size:16px;font-weight:500;margin-bottom:18px;}
.form-group{margin-bottom:14px;}
.form-label{font-size:12px;color:var(--muted);margin-bottom:5px;display:block;}
.form-control{width:100%;background:var(--bg3);border:1px solid var(--border);color:var(--text);border-radius:8px;padding:10px 12px;font-size:14px;font-family:var(--font);transition:border .15s;outline:none;}
.form-control:focus{border-color:var(--accent);}
select.form-control{cursor:pointer;}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.form-hint{font-size:11px;color:var(--muted);margin-top:5px;display:none;}
.form-hint.show{display:block;}
.voice-row{display:flex;gap:10px;align-items:flex-end;margin-bottom:18px;}
.voice-box{flex:1;background:var(--bg3);border:1px solid var(--border);border-radius:8px;padding:10px 12px;min-height:44px;font-size:13px;color:var(--muted);display:flex;align-items:center;}
.voice-box.listening{border-color:var(--red);color:var(--text);}
.voice-box.heard{border-color:var(--accent);color:var(--text);}
.mic-btn{width:44px;height:44px;border-radius:50%;background:var(--bg3);border:1px solid var(--border);cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .15s;flex-shrink:0;}
.mic-btn:hover{border-color:var(--accent);}
.mic-btn.recording{background:var(--red);border-color:var(--red);animation:pulse 1s infinite;}
@keyframes pulse{0%,100%{box-shadow:0 0 0 0 rgba(240,96,96,.4);}50%{box-shadow:0 0 0 8px rgba(240,96,96,0);}}
.mic-btn svg{width:18px;height:18px;}
.btn-submit{width:100%;background:var(--accent);color:#fff;border:none;padding:13px;border-radius:10px;font-size:15px;font-family:var(--font);font-weight:500;cursor:pointer;transition:opacity .15s;margin-top:4px;}
.btn-submit:hover{opacity:.85;}
.btn-submit:active{transform:scale(.98);}
.close-btn{position:absolute;top:20px;right:20px;background:var(--bg3);border:1px solid var(--border);color:var(--muted);width:30px;height:30px;border-radius:8px;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:16px;}
.modal{position:relative;}
.voice-tip{background:rgba(79,156,249,.08);border:1px solid rgba(79,156,249,.2);border-radius:8px;padding:10px 12px;margin-bottom:14px;font-size:12px;color:var(--accent);line-height:1.6;}
.voice-tip strong{color:var(--accent);}

/* ═══ TOAST ═══ */
.toast{position:fixed;top:20px;right:20px;background:var(--bg3);border:1px solid var(--border);border-radius:10px;padding:12px 16px;font-size:13px;z-index:99;display:none;animation:fadeIn .2s ease;}
.toast.show{display:block;}
.toast.success{border-color:rgba(62,207,142,.4);color:var(--green);}
@keyframes fadeIn{from{opacity:0;transform:translateY(-6px);}to{opacity:1;transform:translateY(0);}}

/* ═══ RESPONSIVE BREAKPOINTS ═══ */
@media(max-width:1024px){
  .stats{grid-template-columns:repeat(2,1fr);}
  .panels{grid-template-columns:1fr;}
}

@media(max-width:768px){
  /* hide sidebar, show mobile nav */
  .sidebar{
    position:fixed;left:0;top:0;bottom:0;z-index:45;
    transform:translateX(-100%);width:260px;
  }
  .sidebar.open{transform:translateX(0);}
  .menu-btn{display:flex;}
  .bottom-nav{display:flex;}
  .content{padding:14px 12px 14px;}
  /* hide desktop view tabs from topbar */
  .view-tabs,.date-nav,.btn-add{display:none;}
  .topbar-title{font-size:14px;}
  .stats{grid-template-columns:repeat(2,1fr);gap:8px;margin-bottom:14px;}
  .stat-card{padding:12px;}
  .stat-val{font-size:20px;}
  .panels{grid-template-columns:1fr;}
  /* show fab */
  .fab{display:flex;}
  .big-cal-cell{min-height:52px;padding:6px;}
}

@media(max-width:480px){
  .stats{grid-template-columns:repeat(2,1fr);}
  .stat-label{font-size:10px;}
}

/* ═══ FAB (mobile add button) ═══ */
.fab{
  display:none;position:fixed;bottom:calc(var(--bottom-nav-h) + 16px);right:18px;
  width:52px;height:52px;background:var(--accent);border:none;border-radius:50%;
  cursor:pointer;align-items:center;justify-content:center;z-index:30;
  box-shadow:0 4px 16px rgba(79,156,249,.4);transition:transform .15s;
}
.fab:active{transform:scale(.93);}
.fab svg{width:22px;height:22px;color:#fff;}
</style>
</head>
<body>

<div class="shell">
  <!-- Sidebar overlay (mobile) -->
  <div class="sidebar-overlay" id="overlay" onclick="closeSidebar()"></div>

  <!-- SIDEBAR -->
  <aside class="sidebar" id="sidebar">
    <div class="logo">
      <div class="logo-mark">NTL · BSCS</div>
      <div class="logo-title">ที่จอดรถ</div>
      <div class="logo-sub">ระบบจัดการ</div>
    </div>
    <div class="nav">
      <div class="nav-label">เมนูหลัก</div>
      <div class="nav-item active">
        <svg viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="1" y="1" width="6" height="6" rx="1"/><rect x="9" y="1" width="6" height="6" rx="1"/><rect x="1" y="9" width="6" height="6" rx="1"/><rect x="9" y="9" width="6" height="6" rx="1"/></svg>
        Dashboard
      </div>
      <div class="nav-item" onclick="switchView('day');closeSidebar()">
        <svg viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M2 4h12M2 8h8M2 12h5"/></svg>
        รายการวันนี้
      </div>
      <div class="nav-item" onclick="switchView('month');closeSidebar()">
        <svg viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="1" y="3" width="14" height="11" rx="1.5"/><path d="M5 3V1M11 3V1M1 7h14"/></svg>
        รายเดือน
      </div>
      <div class="nav-item" onclick="switchView('cal');closeSidebar()">
        <svg viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="1" y="3" width="14" height="11" rx="1.5"/><path d="M5 3V1M11 3V1M1 7h14M5 11h2M9 11h2"/></svg>
        ปฏิทิน
      </div>
    </div>
    <div class="quota-box">
      <div class="quota-label">โควตาวันนี้ (หมุนเวียน)</div>
      <div class="quota-nums">19 <span>/ 28 ที่</span></div>
      <div class="quota-bar-bg"><div class="quota-bar-fill"></div></div>
    </div>
  </aside>

  <!-- MAIN -->
  <div class="main">
    <!-- TOPBAR -->
    <div class="topbar">
      <button class="menu-btn" onclick="openSidebar()">
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M3 5h14M3 10h14M3 15h14"/></svg>
      </button>
      <div class="topbar-title">ที่จอดรถ NTL/BSCS</div>
      <div class="view-tabs">
        <div class="tab active" onclick="switchView('day',this)">รายวัน</div>
        <div class="tab" onclick="switchView('month',this)">รายเดือน</div>
        <div class="tab" onclick="switchView('cal',this)">ปฏิทิน</div>
      </div>
      <div class="date-nav">
        <button onclick="changeDate(-1)">‹</button>
        <div class="date-label" id="dateLabel">จ.ที่ 23 มี.ค. 2026</div>
        <button onclick="changeDate(1)">›</button>
      </div>
      <button class="btn-add" onclick="openModal()">+ แจ้งจอง</button>
    </div>

    <!-- CONTENT -->
    <div class="content">
      <!-- STATS -->
      <div class="stats">
        <div class="stat-card">
          <div class="stat-top">
            <div class="stat-icon blue"><svg width="15" height="15" viewBox="0 0 16 16" fill="none" stroke="var(--accent)" stroke-width="1.5"><rect x="1" y="1" width="14" height="14" rx="2"/><path d="M5 8h6M8 5v6"/></svg></div>
            <span class="stat-badge up">+2</span>
          </div>
          <div class="stat-val">19</div>
          <div class="stat-label">จองวันนี้</div>
        </div>
        <div class="stat-card">
          <div class="stat-top">
            <div class="stat-icon green"><svg width="15" height="15" viewBox="0 0 16 16" fill="none" stroke="var(--green)" stroke-width="1.5"><path d="M13 4L6 11 3 8"/></svg></div>
            <span class="stat-badge up">ว่าง</span>
          </div>
          <div class="stat-val">9</div>
          <div class="stat-label">ที่จอดเหลือ</div>
        </div>
        <div class="stat-card">
          <div class="stat-top">
            <div class="stat-icon amber"><svg width="15" height="15" viewBox="0 0 16 16" fill="none" stroke="var(--amber)" stroke-width="1.5"><circle cx="8" cy="8" r="6"/><path d="M8 5v3.5l2 2"/></svg></div>
            <span class="stat-badge warn">คืนนี้</span>
          </div>
          <div class="stat-val">3</div>
          <div class="stat-label">ค้างคืน</div>
        </div>
        <div class="stat-card">
          <div class="stat-top">
            <div class="stat-icon red"><svg width="15" height="15" viewBox="0 0 16 16" fill="none" stroke="var(--red)" stroke-width="1.5"><path d="M8 2v7M8 13h.01"/></svg></div>
            <span class="stat-badge up">ปกติ</span>
          </div>
          <div class="stat-val">0</div>
          <div class="stat-label">ผิดพลาด</div>
        </div>
      </div>

      <!-- DAY VIEW -->
      <div id="view-day" class="view-section active">
        <div class="panels">
          <div class="panel">
            <div class="panel-head">
              <div class="panel-title">รายการจองวันนี้</div>
              <div class="panel-meta" id="dayMeta">19 รายการ</div>
            </div>
            <div class="tbl-wrap">
              <table>
                <thead><tr><th>#</th><th>ชื่อ</th><th>ทะเบียน</th><th>ประเภท</th><th>เวลา</th><th>ถึงวันที่</th></tr></thead>
                <tbody id="tableBody"></tbody>
              </table>
            </div>
          </div>
          <div class="panel">
            <div class="panel-head"><div class="panel-title">มีนาคม 2026</div><div class="panel-meta">ภาพรวมเดือน</div></div>
            <div class="cal-grid" id="miniCal"></div>
            <div class="cal-legend">
              <div class="cal-legend-item"><div class="dot" style="background:var(--red)"></div>เต็ม</div>
              <div class="cal-legend-item"><div class="dot" style="background:var(--amber)"></div>>80%</div>
              <div class="cal-legend-item"><div class="dot" style="background:var(--green)"></div>ว่าง</div>
            </div>
          </div>
        </div>
      </div>

      <!-- MONTH VIEW -->
      <div id="view-month" class="view-section">
        <div class="panels">
          <div class="panel">
            <div class="panel-head"><div class="panel-title">มีนาคม 2026 — รายวัน</div></div>
            <div id="monthBars"></div>
          </div>
          <div class="panel">
            <div class="panel-head"><div class="panel-title">สถิติเดือน</div></div>
            <div style="padding:14px 16px;display:flex;flex-direction:column;gap:12px;">
              <div style="display:flex;justify-content:space-between;"><span style="color:var(--muted);font-size:13px;">จองทั้งหมด</span><span style="font-family:var(--mono);">342</span></div>
              <div style="display:flex;justify-content:space-between;"><span style="color:var(--muted);font-size:13px;">เฉลี่ย/วัน</span><span style="font-family:var(--mono);">15.5</span></div>
              <div style="display:flex;justify-content:space-between;"><span style="color:var(--muted);font-size:13px;">วันใช้มากสุด</span><span style="font-family:var(--mono);">10 มี.ค.</span></div>
              <div style="display:flex;justify-content:space-between;"><span style="color:var(--muted);font-size:13px;">ค้างคืน</span><span style="font-family:var(--mono);">48</span></div>
              <div style="display:flex;justify-content:space-between;"><span style="color:var(--muted);font-size:13px;">หมุนเวียน</span><span style="font-family:var(--mono);">241</span></div>
              <div style="display:flex;justify-content:space-between;"><span style="color:var(--muted);font-size:13px;">จอดแทน</span><span style="font-family:var(--mono);">101</span></div>
            </div>
          </div>
        </div>
      </div>

      <!-- CAL VIEW -->
      <div id="view-cal" class="view-section">
        <div class="panel">
          <div class="panel-head">
            <div class="panel-title">ปฏิทิน — มีนาคม 2026</div>
            <div class="cal-legend" style="padding:0">
              <div class="cal-legend-item"><div class="dot" style="background:var(--red)"></div>เต็ม</div>
              <div class="cal-legend-item"><div class="dot" style="background:var(--amber)"></div>>80%</div>
              <div class="cal-legend-item"><div class="dot" style="background:var(--green)"></div>ว่าง</div>
            </div>
          </div>
          <div class="big-cal-grid" id="bigCal"></div>
        </div>
      </div>
    </div><!-- /content -->

    <!-- MOBILE BOTTOM NAV -->
    <nav class="bottom-nav">
      <div class="bottom-nav-inner">
        <div class="bnav-item active" id="bnav-day" onclick="switchView('day');setActiveNav('day')">
          <svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M3 5h14M3 10h8M3 15h5"/></svg>
          รายวัน
        </div>
        <div class="bnav-item" id="bnav-month" onclick="switchView('month');setActiveNav('month')">
          <svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="2" y="4" width="16" height="13" rx="2"/><path d="M6 4V2M14 4V2M2 9h16"/></svg>
          รายเดือน
        </div>
        <div class="bnav-item" id="bnav-cal" onclick="switchView('cal');setActiveNav('cal')">
          <svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="2" y="4" width="16" height="13" rx="2"/><path d="M6 4V2M14 4V2M2 9h16M6 13h2M12 13h2"/></svg>
          ปฏิทิน
        </div>
        <div class="bnav-item" id="bnav-add" onclick="openModal()">
          <svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5"><circle cx="10" cy="10" r="7"/><path d="M7 10h6M10 7v6"/></svg>
          แจ้งจอง
        </div>
      </div>
    </nav>
  </div><!-- /main -->
</div><!-- /shell -->

<!-- FAB (mobile) -->
<button class="fab" onclick="openModal()">
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 5v14M5 12h14"/></svg>
</button>

<!-- BOOKING MODAL -->
<div class="modal-bg" id="modalBg" onclick="handleModalBgClick(event)">
  <div class="modal" id="modal">
    <div class="modal-handle"></div>
    <button class="close-btn" onclick="closeModal()">✕</button>
    <div class="modal-title">แจ้งจองที่จอดรถ</div>

    <!-- Voice tip -->
    <div class="voice-tip">
      💬 พูดเพื่อกรอกข้อมูลอัตโนมัติ เช่น<br>
      <strong>"จองหมุนเวียน ทะเบียน กข 1234 ชื่อสมศักดิ์ วันที่ 25 มีนาคม จอดปกติ"</strong>
    </div>

    <!-- Voice input -->
    <div class="voice-row">
      <div class="voice-box" id="voiceBox">กดไมค์แล้วพูด...</div>
      <button class="mic-btn" id="micBtn" onclick="toggleVoice()">
        <svg id="micIcon" viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.5">
          <rect x="7" y="1" width="6" height="10" rx="3"/>
          <path d="M4 10a6 6 0 0012 0M10 17v2M7 19h6"/>
        </svg>
      </button>
    </div>

    <!-- Form -->
    <div class="form-group">
      <label class="form-label">ประเภทการจอด</label>
      <select class="form-control" id="fType" onchange="toggleReplace()">
        <option value="หมุนเวียน">จอดหมุนเวียน (โควตา 28 ที่)</option>
        <option value="จอดแทน">จอดแทนพนักงานประจำ</option>
      </select>
    </div>

    <div class="form-group" id="replaceGroup" style="display:none">
      <label class="form-label">ชื่อเจ้าของสิทธิ์ / เลขช่อง</label>
      <input class="form-control" id="fReplaceInfo" placeholder="เช่น คุณนุกูล ช่อง 02">
    </div>

    <div class="form-row">
      <div class="form-group">
        <label class="form-label">จากวันที่</label>
        <input type="date" class="form-control" id="fStart">
      </div>
      <div class="form-group">
        <label class="form-label">ถึงวันที่</label>
        <input type="date" class="form-control" id="fEnd">
      </div>
    </div>

    <div class="form-group">
      <label class="form-label">ช่วงเวลา</label>
      <select class="form-control" id="fTime">
        <option value="ปกติ">จอดปกติ (08.00 – 23.00 น.)</option>
        <option value="ค้างคืน">จอดค้างคืน (เกิน 23.00 น.)</option>
      </select>
    </div>

    <div class="form-group">
      <label class="form-label">ทะเบียนรถ</label>
      <input class="form-control" id="fPlate" placeholder="เช่น 5ธฌ 7777">
    </div>

    <div class="form-group">
      <label class="form-label">ชื่อผู้แจ้งจอง</label>
      <input class="form-control" id="fName" placeholder="ชื่อ-นามสกุล">
    </div>

    <button class="btn-submit" onclick="submitForm()">บันทึกการจอง</button>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<script>
// ─── DATA ───
const mockData = [
  {name:'สมศักดิ์ วงษ์ใหญ่',plate:'กข 1234',type:'rotate',period:'normal',start:'23/03',end:'23/03'},
  {name:'นุกูล ชัยมงคล',plate:'5ธฌ 7777',type:'replace',period:'normal',start:'23/03',end:'25/03'},
  {name:'ปิยะ สมบูรณ์ดี',plate:'กง 5544',type:'rotate',period:'night',start:'23/03',end:'24/03'},
  {name:'วารี แสนสุข',plate:'ขข 9900',type:'rotate',period:'normal',start:'23/03',end:'23/03'},
  {name:'ธนกร ศิริวงศ์',plate:'3ผว 1122',type:'replace',period:'night',start:'23/03',end:'24/03'},
  {name:'อรุณี พงษ์ศักดิ์',plate:'กต 3312',type:'rotate',period:'normal',start:'23/03',end:'23/03'},
  {name:'มานพ เจริญสุข',plate:'ชง 4488',type:'rotate',period:'normal',start:'23/03',end:'23/03'},
  {name:'สุภาพ รักดี',plate:'กค 7766',type:'replace',period:'normal',start:'23/03',end:'26/03'},
];
const dayVals=[0,0,0,0,12,18,22,15,8,0,0,25,19,28,17,14,11,0,0,20,16,23,18,9,0,0,15,19,28,21,17];

// ─── RENDER TABLE ───
function renderTable(){
  document.getElementById('tableBody').innerHTML=mockData.map((r,i)=>`
    <tr>
      <td style="color:var(--muted);font-family:var(--mono);font-size:11px;">${String(i+1).padStart(2,'0')}</td>
      <td>${r.name}</td>
      <td><span class="plate">${r.plate}</span></td>
      <td><span class="badge ${r.type}">${r.type==='rotate'?'หมุนเวียน':'จอดแทน'}</span></td>
      <td><span class="badge ${r.period}">${r.period==='normal'?'ปกติ':'ค้างคืน'}</span></td>
      <td style="color:var(--muted);font-size:12px;">${r.end}</td>
    </tr>`).join('');
}

// ─── MINI CAL ───
function renderMiniCal(){
  const days=['อา','จ','อ','พ','พฤ','ศ','ส'];
  const st=[null,'free','free','busy','free','full','free','free','free','busy','full','free','free','busy','free','free','busy','free','free','full','free','busy','free','today','free','free','free','busy','free','free','full'];
  let h=days.map(d=>`<div class="cal-day-name">${d}</div>`).join('');
  for(let i=0;i<4;i++)h+='<div class="cal-cell empty"></div>';
  for(let d=1;d<=31;d++){
    const s=d===23?'today selected':st[d]||'free';
    const dc=s.includes('full')?'var(--red)':s.includes('busy')?'var(--amber)':'var(--green)';
    h+=`<div class="cal-cell ${s}"><span class="cal-date">${d}</span><div class="cal-dot" style="background:${s.includes('selected')?'rgba(255,255,255,.7)':dc}"></div></div>`;
  }
  document.getElementById('miniCal').innerHTML=h;
}

// ─── MONTH BARS ───
function renderMonthBars(){
  document.getElementById('monthBars').innerHTML=dayVals.slice(0,23).map((v,i)=>{
    if(!v)return'';
    const p=Math.round(v/28*100);
    const c=p>=100?'var(--red)':p>=80?'var(--amber)':'var(--accent)';
    return`<div class="month-bar-row"><div class="month-day">${i+1}</div><div class="month-bar-bg"><div class="month-bar-fill" style="width:${p}%;background:${c}"></div></div><div class="month-count">${v}</div></div>`;
  }).join('');
}

// ─── BIG CAL ───
function renderBigCal(){
  const days=['อาทิตย์','จันทร์','อังคาร','พุธ','พฤหัส','ศุกร์','เสาร์'];
  let h=days.map(d=>`<div style="text-align:center;font-size:10px;color:var(--muted);padding-bottom:4px;">${d}</div>`).join('');
  for(let i=0;i<4;i++)h+=`<div></div>`;
  for(let d=1;d<=31;d++){
    const v=dayVals[d-1]||0;const p=Math.round(v/28*100);
    const dc=p>=100?'var(--red)':p>=80?'var(--amber)':'var(--green)';
    const isTod=d===23;
    h+=`<div class="big-cal-cell${isTod?' today':''}" onclick="">
      <div style="font-family:var(--mono);font-size:12px;color:${isTod?'var(--accent)':'var(--text)'};">${d}</div>
      ${v>0?`<div style="margin-top:4px;"><div style="background:var(--bg4);border-radius:3px;height:3px;"><div style="width:${p}%;background:${dc};height:3px;border-radius:3px;"></div></div><div style="font-size:10px;color:var(--muted);margin-top:3px;">${v}/28</div></div>`:'<div style="font-size:10px;color:var(--border);margin-top:3px;">—</div>'}
    </div>`;
  }
  document.getElementById('bigCal').innerHTML=h;
}

// ─── VIEW SWITCH ───
let curView='day';
function switchView(v,tabEl){
  curView=v;
  document.querySelectorAll('.view-section').forEach(s=>s.classList.remove('active'));
  document.getElementById('view-'+v).classList.add('active');
  if(tabEl){document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));tabEl.classList.add('active');}
}
function setActiveNav(v){
  document.querySelectorAll('.bnav-item').forEach(i=>i.classList.remove('active'));
  document.getElementById('bnav-'+v)?.classList.add('active');
}

// ─── DATE NAV ───
const thDays=['อา.','จ.','อ.','พ.','พฤ.','ศ.','ส.'];
const thMonths=['ม.ค.','ก.พ.','มี.ค.','เม.ย.','พ.ค.','มิ.ย.','ก.ค.','ส.ค.','ก.ย.','ต.ค.','พ.ย.','ธ.ค.'];
let cur=new Date(2026,2,23);
function updateDateLabel(){
  const d=cur;
  document.getElementById('dateLabel').textContent=`${thDays[d.getDay()]}ที่ ${d.getDate()} ${thMonths[d.getMonth()]} ${d.getFullYear()}`;
}
function changeDate(n){cur.setDate(cur.getDate()+n);updateDateLabel();}

// ─── SIDEBAR ───
function openSidebar(){document.getElementById('sidebar').classList.add('open');document.getElementById('overlay').classList.add('open');}
function closeSidebar(){document.getElementById('sidebar').classList.remove('open');document.getElementById('overlay').classList.remove('open');}

// ─── MODAL ───
function openModal(){
  const today=new Date().toISOString().split('T')[0];
  document.getElementById('fStart').value='2026-03-23';
  document.getElementById('fEnd').value='2026-03-23';
  document.getElementById('modalBg').classList.add('open');
}
function closeModal(){document.getElementById('modalBg').classList.remove('open');stopVoice();}
function handleModalBgClick(e){if(e.target===document.getElementById('modalBg'))closeModal();}
function toggleReplace(){document.getElementById('replaceGroup').style.display=document.getElementById('fType').value==='จอดแทน'?'block':'none';}

// ─── FORM SUBMIT ───
function submitForm(){
  const name=document.getElementById('fName').value.trim();
  const plate=document.getElementById('fPlate').value.trim();
  if(!name||!plate){showToast('กรุณากรอก ชื่อ และ ทะเบียน','warn');return;}
  closeModal();
  showToast('✓ บันทึกการจองสำเร็จ','success');
  // reset
  document.getElementById('fName').value='';
  document.getElementById('fPlate').value='';
}

// ─── TOAST ───
function showToast(msg,type='success'){
  const t=document.getElementById('toast');
  t.textContent=msg;t.className='toast show '+(type==='success'?'success':'');
  setTimeout(()=>t.classList.remove('show'),3000);
}

// ─── VOICE INPUT ───
let recognition=null,isRecording=false;

function toggleVoice(){
  if(isRecording){stopVoice();return;}
  if(!('webkitSpeechRecognition' in window||'SpeechRecognition' in window)){
    showToast('เบราว์เซอร์นี้ไม่รองรับ กรุณาใช้ Chrome','warn');return;
  }
  const SR=window.SpeechRecognition||window.webkitSpeechRecognition;
  recognition=new SR();
  recognition.lang='th-TH';
  recognition.interimResults=true;
  recognition.continuous=false;

  recognition.onstart=()=>{
    isRecording=true;
    document.getElementById('micBtn').classList.add('recording');
    document.getElementById('voiceBox').className='voice-box listening';
    document.getElementById('voiceBox').textContent='กำลังฟัง... พูดได้เลยครับ';
  };
  recognition.onresult=e=>{
    const t=Array.from(e.results).map(r=>r[0].transcript).join('');
    document.getElementById('voiceBox').textContent=t;
    if(e.results[e.results.length-1].isFinal){
      document.getElementById('voiceBox').className='voice-box heard';
      parseVoice(t);
    }
  };
  recognition.onerror=()=>{stopVoice();showToast('ไม่ได้ยินเสียง ลองใหม่อีกครั้ง','warn');};
  recognition.onend=()=>stopVoice();
  recognition.start();
}

function stopVoice(){
  isRecording=false;
  document.getElementById('micBtn').classList.remove('recording');
  if(recognition)try{recognition.stop();}catch(e){}
}

function parseVoice(text){
  const t=text.toLowerCase();

  // ประเภท
  if(t.includes('แทน')||t.includes('แทนพนักงาน')){
    document.getElementById('fType').value='จอดแทน';toggleReplace();
  } else {
    document.getElementById('fType').value='หมุนเวียน';toggleReplace();
  }

  // ค้างคืน
  if(t.includes('ค้างคืน')||t.includes('เกินสี่ทุ่ม')||t.includes('เกิน23')){
    document.getElementById('fTime').value='ค้างคืน';
  } else {
    document.getElementById('fTime').value='ปกติ';
  }

  // ทะเบียน — จับหลัง "ทะเบียน"
  const plateMatch=text.match(/ทะเบียน\s*([ก-ฮa-zA-Z0-9\s]{2,12}?)(?:\s|$|ชื่อ|วันที่|จอด)/);
  if(plateMatch){document.getElementById('fPlate').value=plateMatch[1].trim();}

  // ชื่อ — จับหลัง "ชื่อ"
  const nameMatch=text.match(/ชื่อ\s*([ก-ฮa-zA-Z\s]{2,20})(?:\s|$|วันที่|ทะเบียน|จอด)/);
  if(nameMatch){document.getElementById('fName').value=nameMatch[1].trim();}

  // วันที่ — จับเดือนไทย
  const months={มกราคม:1,กุมภาพันธ์:2,มีนาคม:3,เมษายน:4,พฤษภาคม:5,มิถุนายน:6,กรกฎาคม:7,สิงหาคม:8,กันยายน:9,ตุลาคม:10,พฤศจิกายน:11,ธันวาคม:12};
  const dateMatch=text.match(/(\d{1,2})\s*(มกราคม|กุมภาพันธ์|มีนาคม|เมษายน|พฤษภาคม|มิถุนายน|กรกฎาคม|สิงหาคม|กันยายน|ตุลาคม|พฤศจิกายน|ธันวาคม)/);
  if(dateMatch){
    const m=String(months[dateMatch[2]]).padStart(2,'0');
    const d=String(dateMatch[1]).padStart(2,'0');
    document.getElementById('fStart').value=`2026-${m}-${d}`;
    document.getElementById('fEnd').value=`2026-${m}-${d}`;
  }

  showToast('✓ กรอกข้อมูลจากเสียงแล้ว ตรวจสอบอีกครั้งก่อนบันทึก');
}

// ─── INIT ───
renderTable();renderMiniCal();renderMonthBars();renderBigCal();updateDateLabel();
</script>
</body>
</html>
