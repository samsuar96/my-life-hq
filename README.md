# my-life-hq
Personal life dashboard — weight, workouts, schedule, chores &amp; groceries
<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>My Life HQ</title>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:wght@400;600;700;900&family=Plus+Jakarta+Sans:wght@300;400;500;600&display=swap" rel="stylesheet"/>
<style>
:root{
  --bg:#fdf8f3;
  --surface:#ffffff;
  --surface2:#fef3e8;
  --border:#e8ddd2;
  --border2:#d4c5b5;
  --coral:#f4845f;
  --coral2:#e86a42;
  --sage:#4caf87;
  --sage2:#3d9470;
  --sky:#5ba4cf;
  --amber:#f5a623;
  --lavender:#9b7fc8;
  --text:#2c1f0e;
  --text2:#5a4230;
  --muted:#9e8572;
  --radius:14px;
  --shadow:0 2px 12px rgba(44,31,14,.08);
  --shadow-lg:0 6px 24px rgba(44,31,14,.12);
}
*{box-sizing:border-box;margin:0;padding:0;}
body{background:var(--bg);color:var(--text);font-family:'Plus Jakarta Sans',sans-serif;min-height:100vh;font-size:14px;}

/* ── NAV ── */
.topbar{
background:var(–surface);border-bottom:2px solid var(–border);
padding:0 20px;display:flex;align-items:center;gap:6px;
position:sticky;top:0;z-index:100;box-shadow:var(–shadow);
}
.topbar-title{
font-family:‘Fraunces’,serif;font-size:20px;color:var(–coral);font-weight:900;
padding:14px 0;margin-right:14px;white-space:nowrap;letter-spacing:-.02em;
}
.sync-dot{width:8px;height:8px;border-radius:50%;background:#ccc;flex-shrink:0;transition:background .3s;title:attr(data-tip);}
.sync-dot.synced{background:var(–sage);}
.sync-dot.syncing{background:var(–amber);animation:pulse 1s infinite;}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.4}}
.nav-tabs{display:flex;gap:2px;overflow-x:auto;flex:1;scrollbar-width:none;}
.nav-tabs::-webkit-scrollbar{display:none;}
.nav-tab{
padding:8px 15px;border-radius:9px;cursor:pointer;font-size:13px;font-weight:600;
color:var(–muted);border:none;background:none;white-space:nowrap;transition:all .2s;
font-family:‘Plus Jakarta Sans’,sans-serif;
}
.nav-tab:hover{color:var(–text);background:var(–surface2);}
.nav-tab.active{color:var(–coral);background:rgba(244,132,95,.1);}

/* ── LAYOUT ── */
.main{padding:20px;max-width:1160px;margin:0 auto;}
.page{display:none;} .page.active{display:block;animation:fadeUp .22s ease;}
@keyframes fadeUp{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
.grid-2{display:grid;grid-template-columns:1fr 1fr;gap:14px;}
.grid-3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;}
.grid-4{display:grid;grid-template-columns:repeat(4,1fr);gap:10px;}
@media(max-width:760px){.grid-3,.grid-4{grid-template-columns:1fr 1fr;}}
@media(max-width:520px){.grid-2,.grid-3,.grid-4{grid-template-columns:1fr;}}

/* ── CARDS ── */
.card{
background:var(–surface);border:1.5px solid var(–border);border-radius:var(–radius);
padding:18px;margin-bottom:12px;box-shadow:var(–shadow);
}
.card.coral{border-color:rgba(244,132,95,.35);background:linear-gradient(135deg,#fff,rgba(244,132,95,.04));}
.card.sage{border-color:rgba(76,175,135,.35);background:linear-gradient(135deg,#fff,rgba(76,175,135,.04));}
.card.sky{border-color:rgba(91,164,207,.35);background:linear-gradient(135deg,#fff,rgba(91,164,207,.04));}
.card-title{font-family:‘Fraunces’,serif;font-size:15px;color:var(–text);font-weight:700;margin-bottom:12px;display:flex;align-items:center;gap:7px;}
.section-head{font-family:‘Fraunces’,serif;font-size:24px;font-weight:900;color:var(–text);margin-bottom:2px;letter-spacing:-.03em;}
.section-sub{font-size:13px;color:var(–muted);margin-bottom:18px;}

/* ── STAT BOXES ── */
.stat-box{background:var(–surface2);border-radius:12px;padding:14px;text-align:center;border:1.5px solid var(–border);}
.stat-num{font-family:‘Fraunces’,serif;font-size:28px;font-weight:700;letter-spacing:-.02em;}
.stat-label{font-size:10px;color:var(–muted);margin-top:2px;text-transform:uppercase;letter-spacing:.08em;font-weight:600;}

/* ── PROGRESS ── */
.prog-wrap{background:var(–border);border-radius:100px;height:9px;overflow:hidden;margin:5px 0;}
.prog-fill{height:100%;border-radius:100px;transition:width .5s ease;}

/* ── BUTTONS ── */
.btn{padding:9px 18px;border-radius:10px;border:none;cursor:pointer;font-size:13px;font-weight:600;font-family:‘Plus Jakarta Sans’,sans-serif;transition:all .15s;}
.btn-coral{background:var(–coral);color:#fff;} .btn-coral:hover{background:var(–coral2);}
.btn-sage{background:rgba(76,175,135,.15);color:var(–sage);border:1.5px solid rgba(76,175,135,.3);}
.btn-sage:hover{background:rgba(76,175,135,.25);}
.btn-ghost{background:transparent;color:var(–text2);border:1.5px solid var(–border);}
.btn-ghost:hover{border-color:var(–coral);color:var(–coral);}
.btn-sky{background:rgba(91,164,207,.15);color:var(–sky);border:1.5px solid rgba(91,164,207,.3);}
.btn-sm{padding:5px 11px;font-size:12px;}

/* ── INPUTS ── */
.field{display:flex;flex-direction:column;gap:4px;flex:1;min-width:85px;}
.field label{font-size:10px;color:var(–muted);text-transform:uppercase;letter-spacing:.07em;font-weight:600;}
.field input,.field select,.field textarea{
background:var(–bg);border:1.5px solid var(–border);color:var(–text);
border-radius:9px;padding:8px 11px;font-size:13px;font-family:‘Plus Jakarta Sans’,sans-serif;
outline:none;transition:border .2s;
}
.field input:focus,.field select:focus,.field textarea:focus{border-color:var(–coral);}
.field textarea{min-height:60px;resize:vertical;}
.field-row{display:flex;gap:8px;flex-wrap:wrap;align-items:flex-end;margin-bottom:10px;}
.inline-input{
background:transparent;border:none;border-bottom:1.5px solid transparent;
color:var(–text);font-family:‘Plus Jakarta Sans’,sans-serif;font-size:13px;
outline:none;transition:border .2s;padding:2px 4px;flex:1;
}
.inline-input:hover{border-bottom-color:var(–border2);}
.inline-input:focus{border-bottom-color:var(–coral);}
.time-input{
background:var(–surface2);border:1.5px solid transparent;border-radius:7px;
color:var(–coral);font-size:12px;font-weight:700;font-family:‘Plus Jakarta Sans’,sans-serif;
outline:none;padding:3px 7px;width:64px;text-align:center;transition:border .2s;
}
.time-input:hover{border-color:var(–border2);}
.time-input:focus{border-color:var(–coral);}

/* ── LOG ITEMS ── */
.log-item{
display:flex;align-items:center;gap:8px;padding:9px 12px;
background:var(–bg);border-radius:9px;margin-bottom:6px;
border-left:3px solid var(–border);font-size:13px;
border:1.5px solid var(–border);border-left:3px solid var(–border);
}
.log-main{flex:1;}
.tag{display:inline-block;padding:2px 8px;border-radius:100px;font-size:11px;font-weight:700;}
.tag-coral{background:rgba(244,132,95,.15);color:var(–coral);}
.tag-sage{background:rgba(76,175,135,.15);color:var(–sage);}
.tag-sky{background:rgba(91,164,207,.15);color:var(–sky);}
.tag-amber{background:rgba(245,166,35,.15);color:var(–amber);}
.tag-lav{background:rgba(155,127,200,.15);color:var(–lavender);}
.tag-muted{background:var(–surface2);color:var(–muted);}

/* ── CHECKLIST ── */
.check-item{
display:flex;align-items:flex-start;gap:10px;padding:10px 13px;
background:var(–bg);border-radius:10px;margin-bottom:6px;cursor:pointer;
border:1.5px solid var(–border);transition:all .18s;
}
.check-item:hover{border-color:var(–coral);background:rgba(244,132,95,.04);}
.check-item.done{opacity:.55;}
.check-item.done .check-label{text-decoration:line-through;color:var(–muted);}
.check-item.done .ck-box{background:var(–sage);border-color:var(–sage);color:#fff;}
.ck-box{
width:20px;height:20px;border-radius:6px;border:2px solid var(–border2);
display:flex;align-items:center;justify-content:center;flex-shrink:0;
font-size:11px;font-weight:800;transition:all .2s;margin-top:1px;
}
.check-label{font-size:13px;flex:1;font-weight:500;}
.check-sub{font-size:11px;color:var(–muted);margin-top:2px;}

/* ── TIMELINE ── */
.tl-item{display:flex;gap:10px;padding:8px 0;border-bottom:1.5px solid var(–border);}
.tl-item:last-child{border-bottom:none;}
.tl-time{color:var(–coral);font-weight:700;font-size:11px;width:54px;flex-shrink:0;padding-top:3px;}
.tl-body{flex:1;font-size:13px;line-height:1.5;}
.tl-sub{font-size:11px;color:var(–muted);margin-top:1px;}

/* ── DEL BTN ── */
.del-btn{background:none;border:none;color:var(–muted);cursor:pointer;font-size:14px;padding:2px 6px;border-radius:5px;flex-shrink:0;}
.del-btn:hover{color:#e05252;background:rgba(224,82,82,.1);}

/* ── TIMERS ── */
.big-timer{font-family:‘Fraunces’,serif;font-size:54px;font-weight:900;text-align:center;letter-spacing:-.02em;line-height:1;}
.med-timer{font-family:‘Fraunces’,serif;font-size:38px;font-weight:700;text-align:center;line-height:1;}
.timer-row{display:flex;gap:8px;justify-content:center;margin-top:12px;flex-wrap:wrap;}
.timer-bg{background:var(–surface2);border-radius:14px;padding:18px;text-align:center;}

/* ── CAL RING ── */
.ring-wrap{display:flex;align-items:center;gap:18px;flex-wrap:wrap;}
.ring-svg{width:100px;height:100px;flex-shrink:0;}

/* ── CHORE TABS ── */
.day-tabs{display:flex;gap:4px;margin-bottom:14px;flex-wrap:wrap;}
.day-tab{
padding:7px 13px;border-radius:9px;cursor:pointer;font-size:12px;font-weight:700;
color:var(–muted);border:1.5px solid var(–border);background:var(–surface);transition:all .15s;
}
.day-tab:hover{border-color:var(–coral);color:var(–coral);}
.day-tab.active{background:var(–coral);border-color:var(–coral);color:#fff;}
.day-tab.today-tab{border-color:var(–sage);color:var(–sage);}
.day-tab.today-tab.active{background:var(–sage);border-color:var(–sage);color:#fff;}

/* ── GROCERY ── */
.grocery-item{
display:flex;align-items:center;gap:8px;padding:9px 12px;
border-radius:9px;margin-bottom:5px;border:1.5px solid var(–border);background:var(–surface);
}
.grocery-item.got{opacity:.5;}
.grocery-item.got .groc-text{text-decoration:line-through;color:var(–muted);}
.groc-text{flex:1;font-size:13px;}

/* ── SCHEDULE EDIT ── */
.sched-row{display:flex;align-items:center;gap:8px;padding:7px 0;border-bottom:1.5px solid var(–border);}
.sched-row:last-child{border-bottom:none;}
.sched-icon{font-size:16px;width:24px;flex-shrink:0;}

/* ── MACHINE GRID ── */
.mach-grid{display:grid;grid-template-columns:repeat(11,1fr);gap:5px;margin-bottom:10px;}
.mach-dot{
aspect-ratio:1;border-radius:7px;display:flex;align-items:center;justify-content:center;
font-size:10px;font-weight:700;cursor:pointer;transition:all .18s;
border:1.5px solid var(–border);background:var(–bg);color:var(–muted);
}
.mach-dot:hover{border-color:var(–coral);}
.mach-dot.inprog{background:#fef3e8;border-color:var(–amber);color:var(–amber);}
.mach-dot.done{background:rgba(76,175,135,.15);border-color:var(–sage);color:var(–sage);}

.empty-state{text-align:center;color:var(–muted);font-size:13px;padding:24px 0;}
.cal-big{
background:var(–bg);border:2px solid var(–border);color:var(–text);border-radius:12px;
padding:12px 16px;font-size:28px;font-family:‘Fraunces’,serif;font-weight:700;
text-align:center;width:130px;outline:none;transition:border .2s;
}
.cal-big:focus{border-color:var(–coral);}

/* workout category */
.wo-grid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-bottom:12px;}
.wo-btn{
padding:14px 8px;border-radius:12px;border:2px solid var(–border);background:var(–bg);
cursor:pointer;text-align:center;transition:all .18s;color:var(–muted);
font-family:‘Plus Jakarta Sans’,sans-serif;font-size:13px;font-weight:700;
}
.wo-btn:hover{border-color:var(–coral);}
.wo-btn.sel-pickleball{background:rgba(76,175,135,.12);border-color:var(–sage);color:var(–sage);}
.wo-btn.sel-strength{background:rgba(244,132,95,.12);border-color:var(–coral);color:var(–coral);}
.wo-btn.sel-cardio{background:rgba(91,164,207,.12);border-color:var(–sky);color:var(–sky);}
</style>

</head>
<body>

<div class="topbar">
  <div class="topbar-title">✦ My Life HQ</div>
  <div class="sync-dot" id="sync-dot" title="Sync status"></div>
  <div class="nav-tabs">
    <button class="nav-tab active" onclick="showPage('today')">Today</button>
    <button class="nav-tab" onclick="showPage('schedule')">Schedule</button>
    <button class="nav-tab" onclick="showPage('work')">Work</button>
    <button class="nav-tab" onclick="showPage('body')">Body</button>
    <button class="nav-tab" onclick="showPage('fitness')">Fitness</button>
    <button class="nav-tab" onclick="showPage('chores')">Chores & Groceries</button>
  </div>
</div>

<div class="main">

<!-- ══════════════════════════════════ TODAY -->

<div class="page active" id="page-today">
  <div class="section-head" id="today-greeting">Good morning! ✦</div>
  <div class="section-sub" id="today-datestr"> </div>

  <div class="grid-4" style="margin-bottom:14px">
    <div class="stat-box"><div class="stat-num" id="td-lbs" style="color:var(--coral)">—</div><div class="stat-label">lbs to 160</div></div>
    <div class="stat-box"><div class="stat-num" id="td-days" style="color:var(--sky)">—</div><div class="stat-label">days to May 30</div></div>
    <div class="stat-box"><div class="stat-num" id="td-cal" style="color:var(--lavender)">—</div><div class="stat-label">cal today</div></div>
    <div class="stat-box"><div class="stat-num" id="td-wo" style="color:var(--sage)">—</div><div class="stat-label">workouts logged</div></div>
  </div>

  <div class="grid-2">
    <div>
      <div class="card coral">
        <div class="card-title">⚖️ Weight Progress — 180 → 160 by May 30</div>
        <div style="display:flex;justify-content:space-between;font-size:11px;color:var(--muted);margin-bottom:4px"><span>180</span><span id="td-wpct">Log your weight</span><span>160</span></div>
        <div class="prog-wrap"><div class="prog-fill" id="td-wbar" style="background:linear-gradient(90deg,var(--coral),var(--amber));width:0%"></div></div>
        <div style="font-size:12px;color:var(--muted);margin-top:5px" id="td-wsub"> </div>
      </div>
      <div class="card sage">
        <div class="card-title">🍽️ Calories Today — target 1,700</div>
        <div style="display:flex;justify-content:space-between;font-size:11px;color:var(--muted);margin-bottom:4px"><span>0</span><span id="td-clbl">Log in Body tab</span><span>1,700</span></div>
        <div class="prog-wrap"><div class="prog-fill" id="td-cbar" style="background:linear-gradient(90deg,var(--sage),var(--sky));width:0%"></div></div>
        <div style="font-size:12px;color:var(--muted);margin-top:5px" id="td-csub">Skipping breakfast → more room for lunch + dinner 👍</div>
      </div>
    </div>
    <div>
      <div class="card">
        <div class="card-title">✅ Today's Checklist</div>
        <div id="today-checklist"></div>
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════ SCHEDULE -->

<div class="page" id="page-schedule">
  <div class="section-head">Schedule</div>
  <div class="section-sub">Click any time or text to edit — changes save automatically</div>

  <div style="display:flex;gap:6px;margin-bottom:16px;flex-wrap:wrap" id="sched-day-btns"></div>

  <div class="grid-2" id="sched-cols">
    <div class="card" id="sched-card-am">
      <div class="card-title" id="sched-am-title">🌅 Morning</div>
      <div id="sched-am-rows"></div>
      <button class="btn btn-ghost btn-sm" style="margin-top:10px" onclick="addSchedRow('am')">+ Add row</button>
    </div>
    <div class="card" id="sched-card-pm">
      <div class="card-title" id="sched-pm-title">🌆 Evening</div>
      <div id="sched-pm-rows"></div>
      <button class="btn btn-ghost btn-sm" style="margin-top:10px" onclick="addSchedRow('pm')">+ Add row</button>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════ WORK -->

<div class="page" id="page-work">
  <div class="section-head">Work Day 💻</div>
  <div class="section-sub">Mon–Fri · Timer + break tracker · log your day</div>

  <div class="grid-2" style="margin-bottom:12px">
    <div class="card coral">
      <div class="card-title">⏱ Work Session Timer</div>
      <div class="timer-bg">
        <div style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.07em;margin-bottom:6px" id="wt-status">Not started</div>
        <div class="big-timer" id="wt-display" style="color:var(--coral)">0:00:00</div>
        <div style="font-size:11px;color:var(--muted);margin-top:4px" id="wt-start-lbl"> </div>
        <div class="timer-row">
          <button class="btn btn-coral btn-sm" id="wt-btn" onclick="toggleWT()">▶ Start Day</button>
          <button class="btn btn-ghost btn-sm" onclick="resetWT()">Reset</button>
        </div>
      </div>
    </div>
    <div class="card sky">
      <div class="card-title">🚶 Break Timer</div>
      <div class="timer-bg">
        <div style="font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:.07em;margin-bottom:6px" id="bt-status">Step away every ~90 min</div>
        <div class="med-timer" id="bt-display" style="color:var(--sky)">5:00</div>
        <div class="timer-row">
          <button class="btn btn-sky btn-sm" id="bt-btn" onclick="toggleBT()">▶ Start Break</button>
          <button class="btn btn-ghost btn-sm" onclick="resetBT()">Reset</button>
        </div>
        <div style="display:flex;gap:6px;justify-content:center;margin-top:10px">
          <button class="btn btn-ghost btn-sm" onclick="setBT(5)">5 min</button>
          <button class="btn btn-ghost btn-sm" onclick="setBT(10)">10 min</button>
          <button class="btn btn-ghost btn-sm" onclick="setBT(15)">15 min</button>
        </div>
      </div>
    </div>
  </div>

  <div class="card">
    <div class="card-title">📋 Log a Work Day</div>
    <div class="field-row">
      <div class="field"><label>Date</label><input type="date" id="wl-date"/></div>
      <div class="field"><label>Hours</label><input type="number" id="wl-hrs" step=".25" min="1" max="12" placeholder="8"/></div>
      <div class="field"><label>Breaks taken</label><input type="number" id="wl-breaks" min="0" max="10" placeholder="3"/></div>
      <div class="field"><label>Note</label><input type="text" id="wl-note" placeholder="Good focus day"/></div>
    </div>
    <button class="btn btn-coral" onclick="logWork()">Save Day</button>
  </div>

  <div class="card">
    <div class="card-title">📊 This Week</div>
    <div class="grid-3" style="margin-bottom:10px">
      <div class="stat-box"><div class="stat-num" id="wl-whrs" style="color:var(--sage)">0</div><div class="stat-label">hrs this week</div></div>
      <div class="stat-box"><div class="stat-num" id="wl-wbrk" style="color:var(--sky)">0</div><div class="stat-label">breaks taken</div></div>
      <div class="stat-box"><div class="stat-num" id="wl-wdays" style="color:var(--coral)">0</div><div class="stat-label">days logged</div></div>
    </div>
    <div id="wl-hist"></div>
  </div>
</div>

<!-- ══════════════════════════════════ BODY -->

<div class="page" id="page-body">
  <div class="section-head">Body 🌿</div>
  <div class="section-sub">Calories + weight in one place</div>

  <div class="grid-2">
    <!-- CALORIES -->
    <div>
      <div class="card coral">
        <div class="card-title">🍽️ Daily Calories — target 1,700</div>
        <div class="ring-wrap" style="margin-bottom:14px">
          <svg class="ring-svg" viewBox="0 0 100 100">
            <circle cx="50" cy="50" r="40" fill="none" stroke="#fef3e8" stroke-width="10"/>
            <circle cx="50" cy="50" r="40" fill="none" stroke="url(#cg)" stroke-width="10"
              stroke-dasharray="251.2" id="cal-ring" stroke-dashoffset="251.2"
              stroke-linecap="round" transform="rotate(-90 50 50)"/>
            <defs><linearGradient id="cg" x1="0%" y1="0%" x2="100%" y2="0%">
              <stop offset="0%" stop-color="#f4845f"/><stop offset="100%" stop-color="#f5a623"/>
            </linearGradient></defs>
            <text x="50" y="47" text-anchor="middle" fill="#2c1f0e" font-size="13" font-family="Fraunces" font-weight="700" id="ring-num">—</text>
            <text x="50" y="58" text-anchor="middle" fill="#9e8572" font-size="8" font-family="Plus Jakarta Sans">cal today</text>
          </svg>
          <div style="flex:1">
            <div id="cal-verdict" style="font-size:15px;font-weight:700;margin-bottom:4px"> </div>
            <div style="font-size:12px;color:var(--muted)">vs 1,700 target</div>
            <div style="font-size:12px;color:var(--muted);margin-top:8px;line-height:1.8">
              ☕ Breakfast: 0 (skip)<br>
              🥗 Lunch: ~600<br>
              🍎 Snacks: ~200<br>
              🍽️ Dinner: ~600
            </div>
          </div>
        </div>
        <div class="field-row">
          <div style="display:flex;flex-direction:column;align-items:center;gap:5px">
            <label style="font-size:10px;color:var(--muted);text-transform:uppercase;letter-spacing:.07em;font-weight:600">Total Cal</label>
            <input class="cal-big" type="number" id="cal-in" placeholder="1600"/>
          </div>
          <div style="flex:1;display:flex;flex-direction:column;gap:8px">
            <div class="field-row" style="margin-bottom:0">
              <div class="field"><label>Date</label><input type="date" id="cal-date"/></div>
              <div class="field"><label>Note</label><input type="text" id="cal-note" placeholder="e.g. Ate out"/></div>
            </div>
            <button class="btn btn-coral" onclick="logCal()">Save</button>
          </div>
        </div>
      </div>
      <div class="card">
        <div class="card-title">📋 Calorie History <span id="cal-avg-lbl" style="font-size:12px;color:var(--muted);font-weight:400;margin-left:6px"></span></div>
        <div id="cal-hist"></div>
      </div>
    </div>

```
<!-- WEIGHT -->
<div>
  <div class="card sage">
    <div class="card-title">⚖️ Weight — 180 → 160 by May 30</div>
    <div class="grid-3" style="margin-bottom:12px">
      <div class="stat-box"><div class="stat-num" id="w-cur" style="color:var(--coral)">—</div><div class="stat-label">current</div></div>
      <div class="stat-box"><div class="stat-num" id="w-lost" style="color:var(--sage)">0</div><div class="stat-label">lost</div></div>
      <div class="stat-box"><div class="stat-num" id="w-rem" style="color:var(--sky)">20</div><div class="stat-label">to go</div></div>
    </div>
    <div style="display:flex;justify-content:space-between;font-size:11px;color:var(--muted);margin-bottom:4px"><span>180</span><span id="w-pct">0%</span><span>160</span></div>
    <div class="prog-wrap" style="height:12px"><div class="prog-fill" id="w-bar" style="background:linear-gradient(90deg,var(--coral),var(--sage));width:0%"></div></div>
    <div style="font-size:12px;color:var(--muted);margin-top:6px" id="w-pace"> </div>
    <div class="field-row" style="margin-top:14px">
      <div class="field"><label>Date</label><input type="date" id="w-date"/></div>
      <div class="field"><label>Weight (lbs)</label><input type="number" id="w-lbs" step=".1" placeholder="178.5"/></div>
      <div class="field"><label>Note</label><input type="text" id="w-note" placeholder="Morning"/></div>
    </div>
    <button class="btn btn-coral" onclick="logWeight()">Save Weigh-in</button>
  </div>
  <div class="card">
    <div class="card-title">📋 Weight Log</div>
    <div id="w-hist"></div>
  </div>
</div>
```

  </div>
</div>

<!-- ══════════════════════════════════ FITNESS -->

<div class="page" id="page-fitness">
  <div class="section-head">Fitness 🏃</div>
  <div class="section-sub">Workouts + Apple Watch & Oura Ring data</div>

  <div class="grid-2">
    <div>
      <div class="card">
        <div class="card-title">➕ Log a Workout</div>
        <div class="wo-grid">
          <div class="wo-btn" id="wo-pkl" onclick="selWo('pickleball',this)">🏓<br>Pickleball</div>
          <div class="wo-btn" id="wo-str" onclick="selWo('strength',this)">🏋️<br>Strength</div>
          <div class="wo-btn" id="wo-crd" onclick="selWo('cardio',this)">🚴<br>Cardio</div>
        </div>
        <div class="field-row">
          <div class="field"><label>Date</label><input type="date" id="wo-date"/></div>
          <div class="field"><label>Duration (min)</label><input type="number" id="wo-mins" placeholder="45"/></div>
          <div class="field"><label>Notes</label><input type="text" id="wo-notes" placeholder="Full court, felt great"/></div>
        </div>
        <button class="btn btn-coral" onclick="logWo()">Log It</button>
        <span id="wo-err" style="font-size:12px;color:#e05252;margin-left:10px"></span>
      </div>

```
  <div class="card">
    <div class="card-title">📊 Overview</div>
    <div class="grid-3">
      <div class="stat-box"><div class="stat-num" style="color:var(--sage)" id="wo-pkl-ct">0</div><div class="stat-label">🏓 Pickleball</div></div>
      <div class="stat-box"><div class="stat-num" style="color:var(--coral)" id="wo-str-ct">0</div><div class="stat-label">🏋️ Strength</div></div>
      <div class="stat-box"><div class="stat-num" style="color:var(--sky)" id="wo-crd-ct">0</div><div class="stat-label">🚴 Cardio</div></div>
    </div>
    <div style="font-size:13px;color:var(--muted);margin-top:10px" id="wo-month-stats">Log some workouts to see monthly stats.</div>
  </div>

  <div class="card">
    <div class="card-title">📋 History</div>
    <div id="wo-hist"></div>
  </div>
</div>

<div>
  <div class="card sky" style="background:linear-gradient(135deg,rgba(91,164,207,.06),rgba(155,127,200,.06));border-color:rgba(91,164,207,.3)">
    <div class="card-title">📲 Log Health Metrics</div>
    <div style="font-size:12px;color:var(--muted);margin-bottom:12px;line-height:1.8">
      <strong style="color:var(--sky)">Apple Watch:</strong> Fitness app → Summary<br>
      <strong style="color:var(--lavender)">Oura:</strong> App → Today tab → Readiness/Sleep
    </div>
    <div class="field-row"><div class="field"><label>Date</label><input type="date" id="hr-date"/></div></div>
    <div style="font-size:10px;color:var(--muted);text-transform:uppercase;letter-spacing:.07em;font-weight:600;margin-bottom:7px">🍎 Apple Watch</div>
    <div class="field-row">
      <div class="field"><label>Move (cal)</label><input type="number" id="hr-move" placeholder="420"/></div>
      <div class="field"><label>Exercise (min)</label><input type="number" id="hr-ex" placeholder="38"/></div>
      <div class="field"><label>Steps</label><input type="number" id="hr-steps" placeholder="8500"/></div>
    </div>
    <div style="font-size:10px;color:var(--muted);text-transform:uppercase;letter-spacing:.07em;font-weight:600;margin-bottom:7px;margin-top:4px">💍 Oura Ring</div>
    <div class="field-row">
      <div class="field"><label>Readiness</label><input type="number" id="hr-ready" placeholder="82"/></div>
      <div class="field"><label>Sleep score</label><input type="number" id="hr-sleep" placeholder="78"/></div>
      <div class="field"><label>HRV (ms)</label><input type="number" id="hr-hrv" placeholder="45"/></div>
      <div class="field"><label>Resting HR</label><input type="number" id="hr-rhr" placeholder="58"/></div>
    </div>
    <button class="btn btn-coral" onclick="logHealth()">Save Metrics</button>
  </div>

  <div class="card">
    <div class="card-title">📈 Latest Health Data</div>
    <div id="hr-latest"><div class="empty-state">No data yet.</div></div>
  </div>
  <div class="card">
    <div class="card-title">📋 Health History</div>
    <div id="hr-hist"></div>
  </div>
</div>
```

  </div>
</div>

<!-- ══════════════════════════════════ CHORES & GROCERIES -->

<div class="page" id="page-chores">
  <div class="section-head">Chores & Groceries 🏠</div>
  <div class="section-sub">Daily task lists that refresh each week + your grocery list</div>

  <div class="grid-2">
    <!-- CHORES -->
    <div>
      <div class="card">
        <div class="card-title">📅 Weekly Chore Lists</div>
        <div class="day-tabs" id="chore-day-tabs"></div>
        <div id="chore-active-day" style="display:none">
          <div style="display:flex;gap:8px;margin-bottom:10px">
            <input type="text" id="chore-new-task" placeholder="Add a task..." style="flex:1;background:var(--bg);border:1.5px solid var(--border);border-radius:9px;padding:8px 11px;font-size:13px;font-family:'Plus Jakarta Sans',sans-serif;outline:none;" onkeydown="if(event.key==='Enter')addChoreTask()"/>
            <button class="btn btn-coral btn-sm" onclick="addChoreTask()">Add</button>
          </div>
          <div id="chore-task-list"></div>
          <div style="font-size:11px;color:var(--muted);margin-top:8px">✅ = done this week · resets every Monday</div>
        </div>
        <div id="chore-no-day" style="text-align:center;padding:20px;color:var(--muted);font-size:13px">Select a day above to manage tasks</div>
      </div>

```
  <div class="card" style="background:linear-gradient(135deg,rgba(245,166,35,.05),rgba(244,132,95,.05));border-color:rgba(244,132,95,.25)">
    <div style="font-size:10px;color:var(--coral);text-transform:uppercase;font-weight:700;letter-spacing:.1em;margin-bottom:8px">☀️ Sunday — Reset Day</div>
    <div class="tl-item"><div class="tl-time">6:00a</div><div class="tl-body">Wake up, take your time, coffee ☕</div></div>
    <div class="tl-item"><div class="tl-time">~9:00a</div><div class="tl-body" style="color:var(--amber);font-weight:600">⛪ Watch church<div class="tl-sub" style="color:var(--muted);font-weight:400">Morning service</div></div></div>
    <div class="tl-item"><div class="tl-time">~10:30a</div><div class="tl-body">🛒 Grocery run — bring the list!</div></div>
    <div class="tl-item"><div class="tl-time">12:00p</div><div class="tl-body">Home, put away groceries, light lunch</div></div>
    <div class="tl-item"><div class="tl-time">1:00–4p</div><div class="tl-body" style="color:var(--sage);font-weight:600">🏠 Whole-house catch-up + meal prep<div class="tl-sub" style="color:var(--muted);font-weight:400">Deep clean, laundry, basement, prep meals</div></div></div>
    <div class="tl-item"><div class="tl-time">5:00p</div><div class="tl-body" style="color:var(--coral);font-weight:700">🛑 Hard stop — no more chores after 5 PM</div></div>
    <div class="tl-item"><div class="tl-time">5:30–6p</div><div class="tl-body">Cook dinner 🍳</div></div>
    <div class="tl-item"><div class="tl-time">6:00p+</div><div class="tl-body" style="color:var(--lavender);font-weight:600">📺 Relax, TV, read — you earned it</div></div>
  </div>
</div>

<!-- GROCERIES -->
<div>
  <div class="card">
    <div class="card-title">🛒 Grocery List</div>
    <div style="display:flex;gap:8px;margin-bottom:12px">
      <input type="text" id="groc-input" placeholder="Add item..." style="flex:1;background:var(--bg);border:1.5px solid var(--border);border-radius:9px;padding:8px 11px;font-size:13px;font-family:'Plus Jakarta Sans',sans-serif;outline:none;" onkeydown="if(event.key==='Enter')addGroc()"/>
      <button class="btn btn-coral btn-sm" onclick="addGroc()">Add</button>
    </div>
    <div style="display:flex;gap:6px;margin-bottom:10px">
      <button class="btn btn-ghost btn-sm" onclick="clearGotGroc()">Clear got items</button>
      <button class="btn btn-ghost btn-sm" onclick="clearAllGroc()" style="color:var(--muted)">Clear all</button>
    </div>
    <div id="groc-list"></div>
    <div id="groc-empty" class="empty-state" style="display:none">List is empty — add your groceries!</div>
  </div>
</div>
```

  </div>
</div>

</div><!-- /main -->

<script>
// ═══════════════════════════ SYNC / STORAGE
let SYNC_AVAILABLE = typeof window.storage !== 'undefined';
const syncDot = document.getElementById('sync-dot');

async function dbGet(key, def) {
  if (SYNC_AVAILABLE) {
    try {
      const r = await window.storage.get(key);
      return r ? JSON.parse(r.value) : def;
    } catch { return def; }
  }
  try { const v = localStorage.getItem(key); return v !== null ? JSON.parse(v) : def; } catch { return def; }
}
async function dbSet(key, val) {
  syncDot.className = 'sync-dot syncing';
  if (SYNC_AVAILABLE) {
    try {
      await window.storage.set(key, JSON.stringify(val));
      syncDot.className = 'sync-dot synced';
    } catch { syncDot.className = 'sync-dot'; }
  } else {
    try { localStorage.setItem(key, JSON.stringify(val)); syncDot.className = 'sync-dot synced'; } catch { syncDot.className = 'sync-dot'; }
  }
  setTimeout(() => { if(syncDot.className.includes('synced')) syncDot.className='sync-dot synced'; }, 2000);
}
async function dbDel(key) {
  if (SYNC_AVAILABLE) { try { await window.storage.delete(key); } catch {} }
  else { localStorage.removeItem(key); }
}

// ═══════════════════════════ STATE
let weightLog=[], calLog=[], workLog=[], woLog=[], hrLog=[];
let choreTasks={mon:[],tue:[],wed:[],thu:[],fri:[],sat:[],sun:[]};
let choreChecked={};
let groceries=[];
let schedData={};
let todayChecks={};
let selWoCat='';
let currentChoreDay='';

const DAYS_ORDER=['mon','tue','wed','thu','fri','sat','sun'];
const DAY_LABELS={mon:'Mon',tue:'Tue',wed:'Wed',thu:'Thu',fri:'Fri',sat:'Sat',sun:'Sun'};

// ═══════════════════════════ INIT LOAD
async function initLoad() {
  weightLog = await dbGet('wl4', []);
  calLog = await dbGet('cl4', []);
  workLog = await dbGet('wkl4', []);
  woLog = await dbGet('wol4', []);
  hrLog = await dbGet('hrl4', []);
  choreTasks = await dbGet('cht4', {mon:[],tue:[],wed:[],thu:[],fri:[],sat:[],sun:[]});
  choreChecked = await dbGet('chk4', {});
  groceries = await dbGet('groc4', []);
  schedData = await dbGet('sched4', {});
  todayChecks = await dbGet('tdc4', {});
  syncDot.className = 'sync-dot synced';
  setDefaults();
  loadSchedDay(currentSchedDay());
  renderChoreDayTabs();
  renderGroceries();
  refreshAll();
}

// ═══════════════════════════ UTILS
function todayStr(){return new Date().toISOString().split('T')[0];}
function fmtD(d){return new Date(d+'T12:00:00').toLocaleDateString('en-US',{weekday:'short',month:'short',day:'numeric'});}
function isoWeek(){const d=new Date();d.setHours(0,0,0,0);d.setDate(d.getDate()+3-(d.getDay()+6)%7);const w1=new Date(d.getFullYear(),0,4);return 1+Math.round(((d-w1)/86400000-3+(w1.getDay()+6)%7)/7);}
function weekKey(){return new Date().getFullYear()+'-W'+isoWeek();}
function currentDayKey(){return ['sun','mon','tue','wed','thu','fri','sat'][new Date().getDay()];}
function setDefaults(){const t=todayStr();['wl-date','cal-date','w-date','wo-date','hr-date'].forEach(id=>{const el=document.getElementById(id);if(el)el.value=t;});}

// ═══════════════════════════ NAV
function showPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(b=>b.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  document.querySelectorAll('.nav-tab').forEach(b=>{if(b.getAttribute('onclick')?.includes("'"+id+"'"))b.classList.add('active');});
  refreshAll();
  if(id==='schedule')loadSchedDay(currentSchedDay());
}

// ═══════════════════════════ SCHEDULE
const defaultSchedules = {
  weekday: {
    label:'Mon–Fri',
    am:[
      {time:'6:00a',icon:'😴',text:'Wake up'},
      {time:'6:05a',icon:'🚿',text:'Shower — you + Paige takes turns'},
      {time:'6:25a',icon:'🐾',text:'Feed dogs, let them outside'},
      {time:'6:40a',icon:'👗',text:'Get ready for work'},
      {time:'7:10a',icon:'☕',text:'Coffee — out the door soon'},
      {time:'7:30a',icon:'🚗',text:'Leave for work (aim for 7:30–7:45)'},
      {time:'7:45a',icon:'💻',text:'At desk — engineering work starts'},
      {time:'9:30a',icon:'🚶',text:'5-min walk break'},
      {time:'11:00a',icon:'🚶',text:'5-min walk break'},
      {time:'12:00p',icon:'🏃',text:'Lunch workout'},
      {time:'1:00p',icon:'🥗',text:'Lunch — ~600 cal'},
      {time:'2:30p',icon:'🚶',text:'5-min walk break'},
      {time:'4:00p',icon:'🏁',text:'Wrap up, head home'},
    ],
    pm:[
      {time:'4:30p',icon:'🐾',text:'Home — dogs first'},
      {time:'4:35p',icon:'🚫',text:'No snacking — go straight to chores'},
      {time:'4:35p',icon:'🧺',text:'Start laundry before you sit down'},
      {time:'5:00p',icon:'🏠',text:'30-min chore blitz with Paige'},
      {time:'5:30p',icon:'🔪',text:'Prep & start cooking dinner'},
      {time:'6:00p',icon:'🍽️',text:'Dinner on the table'},
      {time:'6:30p',icon:'🍳',text:'Dishes + log calories'},
      {time:'7:00p',icon:'📺',text:'TV, reading, relax — your time'},
      {time:'8:30p',icon:'🚫',text:'Stop eating — kitchen closed'},
      {time:'10:30p',icon:'😴',text:'Lights out'},
    ]
  },
  saturday: {
    label:'Saturday',
    am:[
      {time:'7:00a',icon:'☀️',text:'Sleep in — no rush Saturday'},
      {time:'8:00a',icon:'☕',text:'Coffee, ease into the morning'},
      {time:'9:00a',icon:'🐾',text:'Dogs — longer walk'},
      {time:'10:00a',icon:'🏋️',text:'1-hour workout — gym, pickleball, run'},
      {time:'11:30a',icon:'🚿',text:'Shower, clean up'},
    ],
    pm:[
      {time:'12:00p',icon:'🍽️',text:'Lunch — enjoy it'},
      {time:'1:00p',icon:'🏡',text:'Free time — errands, fun, whatever'},
      {time:'5:30p',icon:'🔪',text:'Start cooking dinner'},
      {time:'6:00p',icon:'🍽️',text:'Dinner'},
      {time:'8:30p',icon:'🚫',text:'Stop eating'},
      {time:'11:00p',icon:'😴',text:'Wind down'},
    ]
  },
  sunday: {
    label:'Sunday',
    am:[
      {time:'6:30a',icon:'☀️',text:'Wake up — take your time'},
      {time:'7:00a',icon:'☕',text:'Coffee, ease into Sunday'},
      {time:'~9:00a',icon:'⛪',text:'Watch church service'},
      {time:'10:30a',icon:'🛒',text:'Grocery shopping — TJ\'s + Metro Market'},
      {time:'12:00p',icon:'🏠',text:'Home — groceries away, light lunch'},
    ],
    pm:[
      {time:'1:00p',icon:'🏡',text:'Whole-house chore catch-up'},
      {time:'3:00p',icon:'🍳',text:'Meal prep for the week'},
      {time:'5:00p',icon:'🛑',text:'HARD STOP — no more chores after 5 PM'},
      {time:'5:30p',icon:'🔪',text:'Start cooking dinner'},
      {time:'6:00p',icon:'🍽️',text:'Dinner on the table'},
      {time:'7:00p',icon:'📺',text:'Relax, TV, read — prep mentally for week'},
      {time:'8:30p',icon:'🚫',text:'Stop eating'},
      {time:'10:30p',icon:'😴',text:'Lights out — good week ahead!'},
    ]
  }
};

let activeSchedKey='weekday';
function currentSchedDay(){
  const d=new Date().getDay();
  return d===6?'saturday':d===0?'sunday':'weekday';
}
function loadSchedDay(key){
  activeSchedKey=key;
  // highlight buttons
  document.querySelectorAll('[data-sched-btn]').forEach(b=>{
    b.className='btn btn-ghost btn-sm'+(b.dataset.schedBtn===key?' btn-coral':'');
  });
  const saved=schedData[key]||{};
  const def=defaultSchedules[key];
  const am=saved.am||def.am;
  const pm=saved.pm||def.pm;
  document.getElementById('sched-am-title').textContent='🌅 Morning — '+def.label;
  document.getElementById('sched-pm-title').textContent='🌆 Evening — '+def.label;
  renderSchedRows('sched-am-rows',am,key,'am');
  renderSchedRows('sched-pm-rows',pm,key,'pm');
}
function renderSchedRows(containerId,rows,key,part){
  const c=document.getElementById(containerId);
  c.innerHTML=rows.map((r,i)=>`
    <div class="sched-row">
      <input class="time-input" value="${r.time}" onchange="saveSchedField('${key}','${part}',${i},'time',this.value)"/>
      <span class="sched-icon">${r.icon}</span>
      <input class="inline-input" value="${r.text}" onchange="saveSchedField('${key}','${part}',${i},'text',this.value)"/>
      <button class="del-btn" onclick="deleteSchedRow('${key}','${part}',${i})">✕</button>
    </div>`).join('');
}
async function saveSchedField(key,part,idx,field,val){
  if(!schedData[key]){
    const def=defaultSchedules[key];
    schedData[key]={am:[...def.am.map(r=>({...r}))],pm:[...def.pm.map(r=>({...r}))]};
  }
  if(schedData[key][part][idx])schedData[key][part][idx][field]=val;
  await dbSet('sched4',schedData);
}
async function addSchedRow(part){
  if(!schedData[activeSchedKey]){const def=defaultSchedules[activeSchedKey];schedData[activeSchedKey]={am:[...def.am.map(r=>({...r}))],pm:[...def.pm.map(r=>({...r}))]};}
  schedData[activeSchedKey][part].push({time:'—',icon:'📌',text:'New item'});
  await dbSet('sched4',schedData);
  loadSchedDay(activeSchedKey);
}
async function deleteSchedRow(key,part,idx){
  if(!schedData[key]){const def=defaultSchedules[key];schedData[key]={am:[...def.am.map(r=>({...r}))],pm:[...def.pm.map(r=>({...r}))]};}
  schedData[key][part].splice(idx,1);
  await dbSet('sched4',schedData);
  loadSchedDay(activeSchedKey);
}
function buildSchedButtons(){
  const container=document.getElementById('sched-day-btns');
  const cur=currentSchedDay();
  container.innerHTML=['weekday','saturday','sunday'].map(k=>`
    <button class="btn btn-ghost btn-sm${k===cur?' btn-coral':''}" data-sched-btn="${k}" onclick="loadSchedDay('${k}')">${defaultSchedules[k].label}</button>
  `).join('')+`<span style="font-size:11px;color:var(--muted);align-self:center;margin-left:6px">Click any time or text to edit</span>`;
}

// ═══════════════════════════ WORK TIMERS
let wtInt=null,wtRun=false,wtSec=0,wtStart=null;
function toggleWT(){
  if(wtRun){clearInterval(wtInt);wtRun=false;document.getElementById('wt-btn').textContent='▶ Resume';document.getElementById('wt-status').textContent='Paused';}
  else{
    wtRun=true;if(!wtStart)wtStart=new Date().toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit'});
    document.getElementById('wt-btn').textContent='⏸ Pause';document.getElementById('wt-status').textContent='Running';
    document.getElementById('wt-start-lbl').textContent='Started at '+wtStart;
    wtInt=setInterval(()=>{wtSec++;updateWTDisplay();},1000);
  }
}
function updateWTDisplay(){
  const h=Math.floor(wtSec/3600),m=Math.floor((wtSec%3600)/60),s=wtSec%60;
  document.getElementById('wt-display').textContent=`${h}:${String(m).padStart(2,'0')}:${String(s).padStart(2,'0')}`;
  document.getElementById('wl-hrs').value=(wtSec/3600).toFixed(2);
}
function resetWT(){clearInterval(wtInt);wtRun=false;wtSec=0;wtStart=null;document.getElementById('wt-display').textContent='0:00:00';document.getElementById('wt-btn').textContent='▶ Start Day';document.getElementById('wt-status').textContent='Not started';document.getElementById('wt-start-lbl').textContent=' ';}
let btInt=null,btRun=false,btSec=300;
function toggleBT(){
  if(btRun){clearInterval(btInt);btRun=false;document.getElementById('bt-btn').textContent='▶ Start Break';document.getElementById('bt-status').textContent='Paused';}
  else{
    btRun=true;document.getElementById('bt-btn').textContent='⏸ Pause';document.getElementById('bt-status').textContent='Step away — go! 🚶';
    btInt=setInterval(()=>{btSec--;const m=Math.floor(btSec/60),s=btSec%60;document.getElementById('bt-display').textContent=`${m}:${String(s).padStart(2,'0')}`;if(btSec<=0){clearInterval(btInt);btRun=false;document.getElementById('bt-display').textContent='✓ Done!';document.getElementById('bt-btn').textContent='▶ Start Break';document.getElementById('bt-status').textContent='Nice break! Back to it 💪';}},1000);
  }
}
function resetBT(){clearInterval(btInt);btRun=false;btSec=300;document.getElementById('bt-display').textContent='5:00';document.getElementById('bt-btn').textContent='▶ Start Break';document.getElementById('bt-status').textContent='Step away every ~90 min';}
function setBT(m){resetBT();btSec=m*60;document.getElementById('bt-display').textContent=m+':00';}

// ═══════════════════════════ LOG WORK
async function logWork(){
  const date=document.getElementById('wl-date').value;
  const hrs=parseFloat(document.getElementById('wl-hrs').value)||0;
  const breaks=parseInt(document.getElementById('wl-breaks').value)||0;
  const note=document.getElementById('wl-note').value;
  if(!date||!hrs)return alert('Enter date and hours.');
  workLog=workLog.filter(w=>w.date!==date);
  workLog.unshift({id:Date.now(),date,hrs,breaks,note});
  await dbSet('wkl4',workLog);
  document.getElementById('wl-hrs').value='';document.getElementById('wl-breaks').value='';document.getElementById('wl-note').value='';
  renderWork();
}
async function delWork(id){workLog=workLog.filter(w=>w.id!==id);await dbSet('wkl4',workLog);renderWork();}
function renderWork(){
  const wa=new Date();wa.setDate(wa.getDate()-wa.getDay()+1);wa.setHours(0,0,0,0);
  const wk=workLog.filter(w=>new Date(w.date+'T12:00:00')>=wa);
  document.getElementById('wl-whrs').textContent=wk.reduce((a,w)=>a+w.hrs,0).toFixed(1);
  document.getElementById('wl-wbrk').textContent=wk.reduce((a,w)=>a+w.breaks,0);
  document.getElementById('wl-wdays').textContent=wk.length;
  const h=document.getElementById('wl-hist');
  if(!workLog.length){h.innerHTML='<div class="empty-state">No days logged yet.</div>';return;}
  h.innerHTML=workLog.slice(0,7).map(w=>`
    <div class="log-item" style="border-left-color:var(--sage)">
      <div class="log-main"><strong>${fmtD(w.date)}</strong> · ${w.hrs} hrs · ${w.breaks} breaks${w.note?' · '+w.note:''}</div>
      <button class="del-btn" onclick="delWork(${w.id})">✕</button>
    </div>`).join('');
}

// ═══════════════════════════ CALORIES
async function logCal(){
  const date=document.getElementById('cal-date').value;
  const cal=parseInt(document.getElementById('cal-in').value);
  const note=document.getElementById('cal-note').value;
  if(!date||!cal)return alert('Enter date and calories.');
  calLog=calLog.filter(c=>c.date!==date);
  calLog.unshift({id:Date.now(),date,cal,note});
  await dbSet('cl4',calLog);
  document.getElementById('cal-in').value='';document.getElementById('cal-note').value='';
  renderCals();updateToday();
}
async function delCal(id){calLog=calLog.filter(c=>c.id!==id);await dbSet('cl4',calLog);renderCals();updateToday();}
function renderCals(){
  const s=[...calLog].sort((a,b)=>new Date(b.date)-new Date(a.date));
  const te=s.find(c=>c.date===todayStr());
  const pct=te?Math.min(100,(te.cal/1700)*100):0;
  const offset=251.2*(1-pct/100);
  document.getElementById('cal-ring').style.strokeDashoffset=offset;
  document.getElementById('ring-num').textContent=te?te.cal.toLocaleString():'—';
  if(te){
    const ov=te.cal>1700;
    document.getElementById('cal-verdict').textContent=ov?`${te.cal-1700} over ⚠️`:`${1700-te.cal} left ✅`;
    document.getElementById('cal-verdict').style.color=ov?'#e05252':'var(--sage)';
  } else {document.getElementById('cal-verdict').textContent='Log today →';}
  const h=document.getElementById('cal-hist');
  if(!s.length){h.innerHTML='<div class="empty-state">No entries yet.</div>';return;}
  h.innerHTML=s.map(c=>{
    const ov=c.cal>1700;
    return `<div class="log-item" style="border-left-color:${ov?'#e05252':'var(--sage)'}">
      <div class="log-main"><strong>${fmtD(c.date)}</strong>${c.note?' — '+c.note:''}</div>
      <span class="tag ${ov?'tag-coral':'tag-sage'}">${c.cal.toLocaleString()}</span>
      <span class="tag ${ov?'tag-coral':'tag-sage'}">${ov?'over':'under'}</span>
      <button class="del-btn" onclick="delCal(${c.id})">✕</button>
    </div>`;
  }).join('');
  if(s.length){const avg=Math.round(s.slice(0,7).reduce((a,c)=>a+c.cal,0)/Math.min(7,s.length));document.getElementById('cal-avg-lbl').textContent='7-day avg: '+avg.toLocaleString();}
}

// ═══════════════════════════ WEIGHT
async function logWeight(){
  const date=document.getElementById('w-date').value;
  const lbs=parseFloat(document.getElementById('w-lbs').value);
  const note=document.getElementById('w-note').value;
  if(!date||!lbs)return alert('Enter date and weight.');
  weightLog=weightLog.filter(w=>w.date!==date);
  weightLog.unshift({id:Date.now(),date,lbs,note});
  await dbSet('wl4',weightLog);
  document.getElementById('w-lbs').value='';document.getElementById('w-note').value='';
  renderWeight();updateToday();
}
async function delWeight(id){weightLog=weightLog.filter(w=>w.id!==id);await dbSet('wl4',weightLog);renderWeight();updateToday();}
function renderWeight(){
  const s=[...weightLog].sort((a,b)=>new Date(b.date)-new Date(a.date));
  const h=document.getElementById('w-hist');
  if(!s.length){h.innerHTML='<div class="empty-state">Weigh in tomorrow morning!</div>';document.getElementById('w-cur').textContent='—';return;}
  h.innerHTML=s.map(w=>`
    <div class="log-item" style="border-left-color:var(--coral)">
      <div class="log-main"><strong>${fmtD(w.date)}</strong>${w.note?' — '+w.note:''}</div>
      <span class="tag tag-amber">${w.lbs} lbs</span>
      ${180-w.lbs>0?`<span class="tag tag-sage">-${(180-w.lbs).toFixed(1)}</span>`:''}
      <button class="del-btn" onclick="delWeight(${w.id})">✕</button>
    </div>`).join('');
  const lat=s[0].lbs,lost=Math.max(0,180-lat),rem=Math.max(0,lat-160),pct=Math.min(100,(lost/20)*100);
  document.getElementById('w-cur').textContent=lat;
  document.getElementById('w-lost').textContent=lost.toFixed(1);
  document.getElementById('w-rem').textContent=rem.toFixed(1);
  document.getElementById('w-pct').textContent=Math.round(pct)+'%';
  document.getElementById('w-bar').style.width=pct+'%';
  const dl=Math.ceil((new Date('2026-05-30')-new Date())/86400000);
  document.getElementById('w-pace').textContent=rem>0?`Need ~${((rem/dl)*7).toFixed(1)} lbs/week · ${dl} days left`:'🎉 Goal reached!';
}

// ═══════════════════════════ WORKOUTS
let selWoStr='';
function selWo(cat,el){
  selWoStr=cat;
  document.querySelectorAll('.wo-btn').forEach(b=>{b.className='wo-btn';});
  el.className='wo-btn sel-'+cat;
  document.getElementById('wo-err').textContent='';
}
async function logWo(){
  if(!selWoStr)return(document.getElementById('wo-err').textContent='Pick a category first');
  const date=document.getElementById('wo-date').value;
  const mins=parseInt(document.getElementById('wo-mins').value)||0;
  const notes=document.getElementById('wo-notes').value;
  if(!date||!mins)return alert('Enter date and duration.');
  const cal=Math.round(mins*(selWoStr==='pickleball'?5:4.5));
  woLog.unshift({id:Date.now(),date,cat:selWoStr,mins,cal,notes});
  await dbSet('wol4',woLog);
  document.getElementById('wo-mins').value='';document.getElementById('wo-notes').value='';
  renderWo();
}
async function delWo(id){woLog=woLog.filter(w=>w.id!==id);await dbSet('wol4',woLog);renderWo();}
function renderWo(){
  document.getElementById('wo-pkl-ct').textContent=woLog.filter(w=>w.cat==='pickleball').length;
  document.getElementById('wo-str-ct').textContent=woLog.filter(w=>w.cat==='strength').length;
  document.getElementById('wo-crd-ct').textContent=woLog.filter(w=>w.cat==='cardio').length;
  const h=document.getElementById('wo-hist');
  if(!woLog.length){h.innerHTML='<div class="empty-state">Log your first workout!</div>';}
  else{
    const cc={pickleball:'var(--sage)',strength:'var(--coral)',cardio:'var(--sky)'};
    const cl={pickleball:'🏓 Pickleball',strength:'🏋️ Strength',cardio:'🚴 Cardio'};
    h.innerHTML=woLog.slice(0,8).map(w=>`
      <div class="log-item" style="border-left-color:${cc[w.cat]}">
        <div class="log-main"><strong>${fmtD(w.date)}</strong> · ${cl[w.cat]} · ${w.mins}min${w.notes?' · '+w.notes:''}</div>
        <span class="tag" style="background:${cc[w.cat]}22;color:${cc[w.cat]}">~${w.cal} cal</span>
        <button class="del-btn" onclick="delWo(${w.id})">✕</button>
      </div>`).join('');
  }
  const now=new Date(),mo=now.getMonth(),yr=now.getFullYear();
  const tm=woLog.filter(w=>{const d=new Date(w.date+'T12:00:00');return d.getMonth()===mo&&d.getFullYear()===yr;});
  document.getElementById('wo-month-stats').innerHTML=tm.length?`This month: ${tm.length} sessions · ${tm.reduce((a,w)=>a+w.mins,0)} min · ~${tm.reduce((a,w)=>a+w.cal,0)} cal burned`:'Log some workouts to see monthly stats.';
  document.getElementById('td-wo').textContent=woLog.length;
}

// ═══════════════════════════ HEALTH
async function logHealth(){
  const date=document.getElementById('hr-date').value;
  if(!date)return alert('Pick a date.');
  const e={id:Date.now(),date,
    move:parseInt(document.getElementById('hr-move').value)||null,
    ex:parseInt(document.getElementById('hr-ex').value)||null,
    steps:parseInt(document.getElementById('hr-steps').value)||null,
    ready:parseInt(document.getElementById('hr-ready').value)||null,
    sleep:parseInt(document.getElementById('hr-sleep').value)||null,
    hrv:parseInt(document.getElementById('hr-hrv').value)||null,
    rhr:parseInt(document.getElementById('hr-rhr').value)||null};
  hrLog=hrLog.filter(h=>h.date!==date);hrLog.unshift(e);
  await dbSet('hrl4',hrLog);
  ['hr-move','hr-ex','hr-steps','hr-ready','hr-sleep','hr-hrv','hr-rhr'].forEach(id=>document.getElementById(id).value='');
  renderHealth();
}
async function delHealth(id){hrLog=hrLog.filter(h=>h.id!==id);await dbSet('hrl4',hrLog);renderHealth();}
function renderHealth(){
  const s=[...hrLog].sort((a,b)=>new Date(b.date)-new Date(a.date));
  const lat=document.getElementById('hr-latest');
  const hist=document.getElementById('hr-hist');
  if(!s.length){lat.innerHTML='<div class="empty-state">No data yet.</div>';hist.innerHTML='';return;}
  const l=s[0];
  lat.innerHTML=`<div style="display:flex;flex-wrap:wrap;gap:8px">
    ${l.move!=null?`<div class="stat-box" style="min-width:80px"><div class="stat-num" style="font-size:20px;color:#e05252">${l.move}</div><div class="stat-label">Move cal</div></div>`:``}
    ${l.ex!=null?`<div class="stat-box" style="min-width:80px"><div class="stat-num" style="font-size:20px;color:var(--sage)">${l.ex}m</div><div class="stat-label">Exercise</div></div>`:``}
    ${l.steps!=null?`<div class="stat-box" style="min-width:80px"><div class="stat-num" style="font-size:20px;color:var(--sky)">${l.steps.toLocaleString()}</div><div class="stat-label">Steps</div></div>`:``}
    ${l.ready!=null?`<div class="stat-box" style="min-width:80px"><div class="stat-num" style="font-size:20px;color:var(--lavender)">${l.ready}</div><div class="stat-label">Readiness</div></div>`:``}
    ${l.sleep!=null?`<div class="stat-box" style="min-width:80px"><div class="stat-num" style="font-size:20px;color:var(--amber)">${l.sleep}</div><div class="stat-label">Sleep</div></div>`:``}
    ${l.hrv!=null?`<div class="stat-box" style="min-width:80px"><div class="stat-num" style="font-size:20px;color:var(--coral)">${l.hrv}</div><div class="stat-label">HRV</div></div>`:``}
  </div><div style="font-size:11px;color:var(--muted);margin-top:8px">${fmtD(l.date)}</div>`;
  hist.innerHTML=s.slice(0,5).map(h=>`
    <div class="log-item" style="border-left-color:var(--lavender)">
      <div class="log-main"><strong>${fmtD(h.date)}</strong>
        ${h.steps!=null?` · ${h.steps.toLocaleString()} steps`:''}
        ${h.ready!=null?` · Ready: ${h.ready}`:''}
        ${h.sleep!=null?` · Sleep: ${h.sleep}`:''}
        ${h.hrv!=null?` · HRV: ${h.hrv}`:''}
      </div>
      <button class="del-btn" onclick="delHealth(${h.id})">✕</button>
    </div>`).join('');
}

// ═══════════════════════════ CHORES
function renderChoreDayTabs(){
  const container=document.getElementById('chore-day-tabs');
  const today=currentDayKey();
  container.innerHTML=DAYS_ORDER.map(d=>`
    <div class="day-tab${d===today?' today-tab':''} ${d===currentChoreDay?' active':''}" onclick="selectChoreDay('${d}')">${DAY_LABELS[d]}${d===today?' ← today':''}</div>
  `).join('');
}
function selectChoreDay(day){
  currentChoreDay=day;
  renderChoreDayTabs();
  document.getElementById('chore-active-day').style.display='block';
  document.getElementById('chore-no-day').style.display='none';
  renderChoreTaskList();
}
function renderChoreTaskList(){
  if(!currentChoreDay)return;
  const tasks=choreTasks[currentChoreDay]||[];
  const wk=weekKey();
  const container=document.getElementById('chore-task-list');
  if(!tasks.length){container.innerHTML='<div class="empty-state" style="padding:16px 0">No tasks yet — add some above!</div>';return;}
  container.innerHTML=tasks.map((t,i)=>{
    const key=wk+'_'+currentChoreDay+'_'+t.id;
    const done=choreChecked[key];
    return `<div class="check-item ${done?'done':''}" onclick="toggleChoreTask('${t.id}')">
      <div class="ck-box">${done?'✓':''}</div>
      <span class="check-label">${t.text}</span>
      <button class="del-btn" onclick="event.stopPropagation();deleteChoreTask('${t.id}')">✕</button>
    </div>`;
  }).join('');
}
async function addChoreTask(){
  const input=document.getElementById('chore-new-task');
  const text=input.value.trim();
  if(!text)return;
  if(!choreTasks[currentChoreDay])choreTasks[currentChoreDay]=[];
  choreTasks[currentChoreDay].push({id:Date.now().toString(),text});
  await dbSet('cht4',choreTasks);
  input.value='';
  renderChoreTaskList();
}
async function deleteChoreTask(id){
  choreTasks[currentChoreDay]=choreTasks[currentChoreDay].filter(t=>t.id!==id);
  await dbSet('cht4',choreTasks);
  renderChoreTaskList();
}
async function toggleChoreTask(id){
  const key=weekKey()+'_'+currentChoreDay+'_'+id;
  choreChecked[key]=!choreChecked[key];
  await dbSet('chk4',choreChecked);
  renderChoreTaskList();
}

// ═══════════════════════════ GROCERIES
async function addGroc(){
  const inp=document.getElementById('groc-input');
  const text=inp.value.trim();
  if(!text)return;
  groceries.push({id:Date.now().toString(),text,got:false});
  await dbSet('groc4',groceries);
  inp.value='';
  renderGroceries();
}
async function toggleGroc(id){
  const item=groceries.find(g=>g.id===id);
  if(item)item.got=!item.got;
  await dbSet('groc4',groceries);
  renderGroceries();
}
async function delGroc(id){
  groceries=groceries.filter(g=>g.id!==id);
  await dbSet('groc4',groceries);
  renderGroceries();
}
async function clearGotGroc(){
  groceries=groceries.filter(g=>!g.got);
  await dbSet('groc4',groceries);
  renderGroceries();
}
async function clearAllGroc(){
  if(!confirm('Clear entire grocery list?'))return;
  groceries=[];
  await dbSet('groc4',groceries);
  renderGroceries();
}
function renderGroceries(){
  const container=document.getElementById('groc-list');
  const empty=document.getElementById('groc-empty');
  if(!groceries.length){container.innerHTML='';empty.style.display='block';return;}
  empty.style.display='none';
  const pending=groceries.filter(g=>!g.got);
  const got=groceries.filter(g=>g.got);
  const renderItem=g=>`
    <div class="grocery-item${g.got?' got':''}">
      <div class="ck-box" onclick="toggleGroc('${g.id}')" style="cursor:pointer;border-color:${g.got?'var(--sage)':'var(--border2)'};background:${g.got?'var(--sage)':'transparent'};color:${g.got?'#fff':'transparent'};flex-shrink:0">✓</div>
      <span class="groc-text">${g.text}</span>
      <button class="del-btn" onclick="delGroc('${g.id}')">✕</button>
    </div>`;
  container.innerHTML=[...pending.map(renderItem),...got.map(renderItem)].join('');
}

// ═══════════════════════════ TODAY DASHBOARD
const WEEKDAY_CHECKS=[
  {key:'weight',label:'Morning weigh-in',sub:'Before eating → Body tab'},
  {key:'calories',label:'Log calories today',sub:'Body tab — one number'},
  {key:'workout',label:'Lunch workout',sub:'Fitness tab'},
  {key:'breaks',label:'3 walk breaks at work',sub:'Work tab timer'},
  {key:'nosnack',label:'No snacking when home 🚫',sub:'Go straight to chores!'},
  {key:'dinner',label:'Dinner by 6 PM 🍽️',sub:'Anti-inflammatory'},
  {key:'chore',label:'30-min chore blitz with Paige 🏠',sub:'Chores tab'},
];
const SATURDAY_CHECKS=[
  {key:'wo-sat',label:'1-hour workout 🏋️',sub:'Gym, pickleball, run — your choice'},
  {key:'relax-sat',label:'Rest of the day is yours 😌',sub:'No pressure'},
];
const SUNDAY_CHECKS=[
  {key:'church',label:'Watch church ⛪',sub:'Morning service'},
  {key:'grocery',label:'Grocery run 🛒',sub:'Bring your list!'},
  {key:'clean',label:'Whole-house clean 🏠',sub:'Done by 5 PM'},
  {key:'mealprep',label:'Meal prep 🍳',sub:'Chop, marinate, plan week'},
  {key:'relax-su',label:'Relax after 5 PM 📺',sub:'You earned it — hard stop on chores'},
];
async function toggleTodayCheck(key,el){
  const done=!el.classList.contains('done');
  done?el.classList.add('done'):el.classList.remove('done');
  el.querySelector('.ck-box').textContent=done?'✓':'';
  todayChecks[todayStr()+'_'+key]=done;
  await dbSet('tdc4',todayChecks);
}
function renderTodayChecklist(){
  const dow=new Date().getDay();
  const items=dow===6?SATURDAY_CHECKS:dow===0?SUNDAY_CHECKS:WEEKDAY_CHECKS;
  document.getElementById('today-checklist').innerHTML=items.map(item=>{
    const done=todayChecks[todayStr()+'_'+item.key];
    return `<div class="check-item${done?' done':''}" onclick="toggleTodayCheck('${item.key}',this)">
      <div class="ck-box">${done?'✓':''}</div>
      <div><div class="check-label">${item.label}</div><div class="check-sub">${item.sub}</div></div>
    </div>`;
  }).join('');
}
function updateToday(){
  const h=new Date().getHours();
  document.getElementById('today-greeting').textContent=`Good ${h<12?'morning':h<17?'afternoon':'evening'}! ✦`;
  document.getElementById('today-datestr').textContent=new Date().toLocaleDateString('en-US',{weekday:'long',year:'numeric',month:'long',day:'numeric'});
  document.getElementById('td-days').textContent=Math.ceil((new Date('2026-05-30')-new Date())/86400000);
  const ws=[...weightLog].sort((a,b)=>new Date(b.date)-new Date(a.date));
  if(ws.length){
    const lat=ws[0].lbs,pct=Math.min(100,Math.max(0,((180-lat)/20)*100));
    document.getElementById('td-lbs').textContent=Math.max(0,lat-160).toFixed(1);
    document.getElementById('td-wbar').style.width=pct+'%';
    document.getElementById('td-wpct').textContent=Math.round(pct)+'% complete';
    document.getElementById('td-wsub').textContent=lat+' lbs · lost '+(180-lat).toFixed(1)+' lbs';
  } else {document.getElementById('td-lbs').textContent='20';}
  const tc=calLog.find(c=>c.date===todayStr());
  if(tc){
    const ov=tc.cal>1700,pct=Math.min(100,(tc.cal/1700)*100);
    document.getElementById('td-cal').textContent=tc.cal.toLocaleString();
    document.getElementById('td-cbar').style.width=pct+'%';
    document.getElementById('td-clbl').textContent=ov?`${tc.cal-1700} over`:`${1700-tc.cal} left`;
    document.getElementById('td-csub').textContent=ov?'⚠️ Over 1,700 today':'✅ Under target!';
  } else {document.getElementById('td-cal').textContent='—';}
}

// ═══════════════════════════ REFRESH ALL
function refreshAll(){
  renderWork();renderCals();renderWeight();renderWo();renderHealth();
  updateToday();renderTodayChecklist();
  if(document.getElementById('page-chores').classList.contains('active')){renderChoreDayTabs();if(currentChoreDay)renderChoreTaskList();renderGroceries();}
}

// ═══════════════════════════ KICK OFF
setDefaults();
buildSchedButtons();
initLoad();
</script>

</body>
</html>