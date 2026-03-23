# simulator-latest[pro_football_simulator_v5 (2).html](https://github.com/user-attachments/files/26182424/pro_football_simulator_v5.2.html)
<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>⚽ Pro Football Simulator v5</title>
<link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@400;600;700;900&family=Noto+Sans+KR:wght@400;500;700&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{
  --bg:#04080f;--surface:#080e1a;--surface2:#0c1422;
  --border:#1a2a40;--border2:#243550;
  --accent:#00e5ff;--accent2:#0078ff;
  --home:#00c4ff;--away:#ff7b00;
  --green:#00ff88;--red:#ff3366;--yellow:#ffd700;
  --text:#e8f4ff;--muted:#4a6a8a;
}
body{background:var(--bg);color:var(--text);font-family:'Noto Sans KR',sans-serif;height:100vh;overflow:hidden;display:flex;flex-direction:column}

header{display:flex;align-items:center;justify-content:space-between;padding:6px 20px;background:linear-gradient(90deg,#000812,#05122a,#000812);border-bottom:1px solid #0a2a50;flex-shrink:0;min-height:46px}
.logo{display:flex;align-items:center;gap:10px}
.logo-icon{font-size:1.5rem}
.logo-text{font-family:'Barlow Condensed',sans-serif;font-weight:900;font-size:1.3rem;color:var(--accent);letter-spacing:1px}
.logo-sub{font-size:0.6rem;color:var(--muted);letter-spacing:2px}
.hstats{display:flex;gap:8px;align-items:center}
.hpill{background:#0a1a2e;border:1px solid #1a3a5a;border-radius:5px;padding:3px 9px;font-size:0.68rem;color:var(--muted)}
.hpill strong{color:var(--accent);font-family:'Barlow Condensed',sans-serif}
.hbtn{padding:4px 10px;background:#0a1628;border:1px solid #1e3050;border-radius:4px;font-size:0.68rem;cursor:pointer;font-family:'Barlow Condensed',sans-serif;letter-spacing:1px;transition:all 0.15s;color:#7aa}
.hbtn:hover{background:#1a2638}
.hbtn.connected{color:#4ade80;border-color:#166534}

/* API KEY SETUP SCREEN */
.setup-screen{position:fixed;inset:0;background:var(--bg);z-index:9999;display:flex;align-items:center;justify-content:center;flex-direction:column;gap:16px}
.setup-card{background:#0b1628;border:1px solid #1e3050;border-radius:12px;padding:28px;width:400px;max-width:92vw}
.setup-card h2{font-size:1rem;color:var(--accent);font-family:'Barlow Condensed',sans-serif;letter-spacing:2px;margin-bottom:6px}
.setup-card p{font-size:0.73rem;color:var(--muted);margin-bottom:18px;line-height:1.6}
.setup-field{margin-bottom:14px}
.setup-field label{font-size:0.70rem;color:#7aa;display:block;margin-bottom:5px;letter-spacing:1px}
.setup-field .sub{font-size:0.62rem;color:#444;margin-bottom:5px;display:block}
.setup-field input{width:100%;background:#060c18;border:1px solid #1e3050;border-radius:5px;color:var(--text);font-size:0.78rem;padding:8px 10px;outline:none}
.setup-field input:focus{border-color:var(--accent2)}
.setup-btn{width:100%;padding:10px;background:linear-gradient(135deg,#0044cc,#0099ff);border:none;border-radius:7px;color:#fff;font-size:0.9rem;font-weight:700;cursor:pointer;font-family:'Barlow Condensed',sans-serif;letter-spacing:1px;margin-top:6px}
.setup-skip{width:100%;padding:7px;background:transparent;border:1px solid #1e3050;border-radius:7px;color:#555;font-size:0.75rem;cursor:pointer;margin-top:8px}
.setup-status{font-size:0.68rem;text-align:center;min-height:16px;margin-top:6px}

/* LAYOUT */
.layout{display:grid;grid-template-columns:268px 1fr 268px;flex:1;overflow:hidden;min-height:0}

/* PANEL */
.panel{background:var(--surface);display:flex;flex-direction:column;overflow:hidden;border-right:1px solid var(--border)}
.panel.right{border-right:none;border-left:1px solid var(--border)}
.ph{padding:10px 12px 8px;border-bottom:1px solid var(--border);flex-shrink:0}
.tbadge{display:flex;align-items:center;gap:8px;margin-bottom:7px}
.bcircle{width:32px;height:32px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:1rem;flex-shrink:0}
.bcircle.home{background:linear-gradient(135deg,#002244,#0055aa);border:2px solid var(--home)}
.bcircle.away{background:linear-gradient(135deg,#2a0a00,#aa3300);border:2px solid var(--away)}
.tname{font-family:'Barlow Condensed',sans-serif;font-size:1.05rem;font-weight:700}
.tname.home{color:var(--home)}.tname.away{color:var(--away)}
.tleague{font-size:0.6rem;color:var(--muted);letter-spacing:1px}
.elo-badge{font-family:'Barlow Condensed',sans-serif;font-size:0.72rem;padding:1px 6px;border-radius:3px;border:1px solid;display:inline-block;margin-top:2px}
.elo-badge.home{color:var(--home);border-color:var(--home)44;background:#00c4ff11}
.elo-badge.away{color:var(--away);border-color:var(--away)44;background:#ff7b0011}
.form-badges{display:flex;gap:3px;margin-top:4px;flex-wrap:wrap;min-height:20px}

select,input[type=text]{background:#060c18;border:1px solid var(--border2);border-radius:5px;color:var(--text);padding:5px 8px;font-size:0.76rem;outline:none;width:100%;font-family:'Noto Sans KR',sans-serif;margin-bottom:4px}
select:focus,input:focus{border-color:var(--accent2)}
option{background:#060c18}
.frow{display:flex;gap:3px;margin-top:2px;flex-wrap:wrap}
.fbtn{padding:3px 6px;font-size:0.65rem;font-weight:700;border:1px solid var(--border2);border-radius:4px;background:transparent;color:var(--muted);cursor:pointer;font-family:'Barlow Condensed',sans-serif;transition:all 0.15s}
.fbtn.active.home{background:#001e44;border-color:var(--home);color:var(--home)}
.fbtn.active.away{background:#2a0e00;border-color:var(--away);color:var(--away)}

.tabs{display:flex;border-bottom:1px solid var(--border);flex-shrink:0}
.tab{flex:1;padding:7px 0;font-size:0.68rem;font-weight:700;text-align:center;cursor:pointer;color:var(--muted);border:none;background:transparent;font-family:'Barlow Condensed',sans-serif;transition:all 0.15s;border-bottom:2px solid transparent}
.tab.active{color:var(--accent);border-bottom-color:var(--accent)}
.sbox{padding:6px 10px;border-bottom:1px solid var(--border);flex-shrink:0}
.sbox input{margin-bottom:0;font-size:0.72rem}

/* LOADING STATE */
.loading-state{display:flex;flex-direction:column;align-items:center;justify-content:center;flex:1;gap:10px;color:var(--muted);font-size:0.78rem}
.spinner{width:28px;height:28px;border:2px solid #1e3050;border-top-color:var(--accent);border-radius:50%;animation:spin 0.8s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
.api-call-count{font-size:0.62rem;color:#555;text-align:center;padding:4px 8px;background:#0a1020;border-radius:4px}

/* PLAYER LIST */
.plist{flex:1;overflow-y:auto;min-height:0}
.plist::-webkit-scrollbar{width:3px}
.plist::-webkit-scrollbar-thumb{background:#1a3a5a;border-radius:2px}
.prow{display:flex;align-items:center;gap:7px;padding:6px 10px;border-bottom:1px solid #0a1420;cursor:pointer;transition:background 0.1s;user-select:none}
.prow:hover{background:#0c1e30}
.prow.starting{background:#091c14}
.ptag{width:26px;height:16px;border-radius:3px;display:flex;align-items:center;justify-content:center;font-size:0.6rem;font-weight:800;flex-shrink:0;font-family:'Barlow Condensed',sans-serif}
.pinfo{flex:1;min-width:0}
.pname{font-size:0.78rem;color:#ccddee;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.pstats{font-size:0.63rem;color:var(--muted)}
.pscore{font-family:'Barlow Condensed',sans-serif;font-size:0.85rem;font-weight:700;color:var(--muted);flex-shrink:0;width:24px;text-align:right}
.pscore.hi{color:var(--green)}
.pcheck{font-size:0.85rem;flex-shrink:0;width:16px;text-align:center}
.xg-mini{font-size:0.58rem;color:#4a6a8a}

.subs{border-top:1px solid var(--border);padding:6px 10px;flex-shrink:0;min-height:48px}
.subs-title{font-size:0.62rem;color:var(--muted);letter-spacing:2px;margin-bottom:4px;font-family:'Barlow Condensed',sans-serif}
.subs-list{display:flex;flex-wrap:wrap;gap:3px}
.schip{display:inline-flex;align-items:center;gap:3px;background:#0a1422;border:1px solid var(--border2);border-radius:3px;padding:2px 6px;font-size:0.65rem;color:#889aaa}

/* CENTER */
.center{display:flex;flex-direction:column;overflow:hidden}
.mbar{background:linear-gradient(90deg,#001122,#040c18,#001122);border-bottom:1px solid var(--border);padding:8px 16px;display:flex;align-items:center;justify-content:space-between;flex-shrink:0}
.mteam{font-family:'Barlow Condensed',sans-serif;font-size:1rem;font-weight:700}
.mteam.home{color:var(--home)}.mteam.away{color:var(--away)}
.mvsbox{text-align:center;min-width:200px}
.mvslbl{font-size:0.62rem;color:var(--muted);letter-spacing:2px;font-family:'Barlow Condensed',sans-serif}
.probbar{display:flex;height:5px;border-radius:3px;overflow:hidden;width:160px;margin:3px auto}
.prob-h{background:linear-gradient(90deg,#0044cc,#0099ff);transition:width 0.5s}
.prob-d{background:#1a3050;transition:width 0.5s}
.prob-a{background:linear-gradient(90deg,#cc4400,#ff8800);transition:width 0.5s}
.plabels{display:flex;justify-content:space-between;width:160px;margin:2px auto;font-size:0.64rem;font-family:'Barlow Condensed',sans-serif}
.predscore{font-size:0.62rem;color:var(--muted);text-align:center;margin-top:2px}

.pwrap{flex:1;display:flex;align-items:center;justify-content:center;padding:8px;overflow:hidden}
.pitch{position:relative;width:100%;max-width:380px;height:100%;max-height:500px;
  background:repeating-linear-gradient(180deg,#1a6b2f 0px,#1a6b2f 28px,#1d7534 28px,#1d7534 56px);
  border:2px solid #2a5a3a;border-radius:5px;overflow:hidden}
.pitch-svg{position:absolute;inset:0;width:100%;height:100%;pointer-events:none}
.pp{position:absolute;transform:translate(-50%,-50%);display:flex;flex-direction:column;align-items:center;cursor:pointer;z-index:10;transition:all 0.3s}
.pp:hover .pc{transform:scale(1.15)}
.pc{width:36px;height:36px;border-radius:50%;display:flex;align-items:center;justify-content:center;border:2.5px solid;transition:all 0.2s;font-family:'Barlow Condensed',sans-serif;position:relative;flex-shrink:0}
.pc.home{background:radial-gradient(circle at 35% 35%,#003080,#001040);border-color:var(--home);box-shadow:0 0 8px #00c4ff44}
.pc.away{background:radial-gradient(circle at 35% 35%,#802000,#400800);border-color:var(--away);box-shadow:0 0 8px #ff7b0044}
.pc-num{font-size:0.78rem;font-weight:900;color:#fff}
.pc-rating{position:absolute;bottom:-2px;right:-2px;width:14px;height:14px;border-radius:50%;font-size:0.48rem;font-weight:900;display:flex;align-items:center;justify-content:center;background:var(--yellow);color:#000;font-family:'Barlow Condensed',sans-serif}
.plbl{font-size:0.56rem;font-weight:600;color:#fff;white-space:nowrap;max-width:60px;overflow:hidden;text-overflow:ellipsis;background:rgba(0,0,0,0.8);padding:1px 4px;border-radius:2px;margin-top:2px;text-align:center}

.statsbar{background:#040a14;border-top:1px solid var(--border);padding:6px 16px;display:grid;grid-template-columns:1fr auto 1fr;gap:10px;align-items:center;flex-shrink:0}
.srow{display:flex;align-items:center;gap:6px;margin-bottom:3px}
.srow:last-child{margin-bottom:0}
.srow.r{flex-direction:row-reverse}
.sval{font-family:'Barlow Condensed',sans-serif;font-size:0.95rem;font-weight:900;flex-shrink:0;width:34px}
.sval.home{color:var(--home)}.sval.away{color:var(--away);text-align:right}
.sbar{flex:1;height:3px;border-radius:2px;background:var(--border);overflow:hidden}
.sfill{height:100%;border-radius:2px;transition:width 0.5s}
.sfill.home{background:var(--home)}.sfill.away{background:var(--away);float:right}
.scenter{text-align:center;display:flex;flex-direction:column;gap:4px;align-items:center}
.snm{font-size:0.6rem;color:var(--muted);letter-spacing:1px;font-family:'Barlow Condensed',sans-serif}
.simbtn{padding:7px 20px;background:linear-gradient(135deg,#0044cc,#0099ff);border:none;border-radius:7px;color:#fff;font-size:0.82rem;font-weight:700;cursor:pointer;font-family:'Barlow Condensed',sans-serif;letter-spacing:1px;box-shadow:0 3px 14px #0077ff33;transition:all 0.2s}
.simbtn:hover{transform:translateY(-1px)}
.simbtn:disabled{opacity:0.5;cursor:not-allowed;transform:none}

.wbox{background:var(--surface2);border-top:1px solid var(--border);padding:7px 14px;flex-shrink:0}
.wtitle{font-size:0.6rem;color:var(--muted);letter-spacing:2px;margin-bottom:5px;font-family:'Barlow Condensed',sans-serif}
.wgrid{display:grid;grid-template-columns:repeat(4,1fr);gap:8px}
.witem label{font-size:0.62rem;color:var(--muted);display:flex;justify-content:space-between;margin-bottom:2px}
.witem label span{font-family:'Barlow Condensed',sans-serif;font-size:0.78rem;font-weight:700;color:var(--accent)}
.witem input[type=range]{width:100%;height:3px;accent-color:var(--accent2);margin:0;cursor:pointer}

/* AUTO MENU */
.auto-menu{position:fixed;z-index:2000;background:#0a1628;border:1px solid #1e3050;border-radius:6px;min-width:200px;box-shadow:0 8px 24px #000a;display:none}
.auto-menu-item{display:flex;align-items:center;gap:8px;padding:8px 12px;cursor:pointer;transition:background 0.1s;border-bottom:1px solid #0f1e30}
.auto-menu-item:last-child{border-bottom:none}
.auto-menu-item:hover{background:#1a2a40}
.ami-icon{font-size:1rem;width:20px;text-align:center}
.ami-label{font-size:0.75rem;color:var(--text);display:block}
.ami-sub{font-size:0.62rem;color:var(--muted);display:block}

/* RESULT MODAL */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,5,0.88);z-index:1000;display:none;align-items:center;justify-content:center}
.modal-overlay.show{display:flex}
.modal{background:#0b1628;border:1px solid #1e3050;border-radius:10px;padding:18px;width:400px;max-width:94vw;max-height:88vh;overflow-y:auto}
.modal h2{font-size:0.85rem;color:#7aa;letter-spacing:2px;margin-bottom:10px;text-align:center}
.result-score-big{display:flex;justify-content:center;align-items:center;gap:12px;font-family:'Barlow Condensed',sans-serif;font-size:2.8rem;font-weight:900;margin:8px 0}
.result-bars{margin:10px 0}
.rbar-row{display:flex;align-items:center;justify-content:space-between;margin-bottom:5px;font-size:0.75rem}
.rbar{height:6px;background:var(--border);border-radius:3px;overflow:hidden;flex:1;margin:0 8px}
.rbar-fill{height:100%;border-radius:3px;transition:width 0.6s}
.top-players{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin:10px 0}
.top-box{background:#070d1a;border-radius:5px;padding:7px 9px;font-size:0.68rem}
.top-box .tb-title{color:var(--muted);letter-spacing:1px;margin-bottom:4px;font-size:0.62rem;font-family:'Barlow Condensed',sans-serif}
.top-box .tb-player{color:#aaccff;margin-bottom:2px}

.ev-section{background:#070d1a;border:1px solid #1e3050;border-radius:6px;padding:10px;margin:10px 0}
.ev-title{font-size:0.68rem;color:#7aa;font-weight:700;letter-spacing:1px;margin-bottom:8px}
.ev-grid{display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px;margin-bottom:6px}
.ev-item label{font-size:0.62rem;color:var(--muted);display:block;margin-bottom:2px}
.ev-item input{width:100%;background:#050a14;border:1px solid #1e3050;border-radius:3px;color:var(--text);font-size:0.75rem;padding:4px 6px;outline:none;text-align:center}
.ev-result{display:grid;grid-template-columns:1fr 1fr 1fr;gap:4px;font-size:0.68rem;text-align:center}
.ev-value{font-family:'Barlow Condensed',sans-serif;font-size:0.85rem;font-weight:700}
.ev-value.pos{color:var(--green)}.ev-value.neg{color:var(--red)}.ev-value.neu{color:var(--muted)}
.ev-rec{text-align:center;padding:6px;border-radius:4px;font-size:0.72rem;margin-top:6px}

.result-input{background:#070d1a;border:1px solid #1e3050;border-radius:6px;padding:9px;margin:8px 0}
.ri-title{font-size:0.68rem;color:#7aa;margin-bottom:7px;font-weight:700;letter-spacing:1px}
.result-btns{display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px}
.rbtn{padding:6px 4px;border-radius:4px;border:1px solid #1e3050;background:#0a1628;font-size:0.70rem;cursor:pointer;font-family:'Barlow Condensed',sans-serif;transition:all 0.15s}
.rbtn:hover{background:#1a2638}
.modal-close{width:100%;padding:9px;margin-top:12px;background:var(--border);border:none;border-radius:6px;color:var(--muted);font-size:0.82rem;cursor:pointer;font-family:'Barlow Condensed',sans-serif}

/* STATS PANEL */
.stats-panel{position:fixed;inset:0;background:#000b;z-index:2000;display:none;align-items:center;justify-content:center}
.stats-panel.show{display:flex}
.stats-box{background:#0b1628;border:1px solid #1e3050;border-radius:10px;padding:16px;width:520px;max-width:95vw;max-height:88vh;overflow-y:auto}
.summary-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:12px}
.summary-card{background:#0a1628;border-radius:6px;padding:9px;text-align:center}
.summary-card .sv{font-size:1.2rem;font-weight:700;font-family:'Barlow Condensed',sans-serif}
.summary-card .sl{font-size:0.62rem;color:var(--muted);margin-top:2px}
.rec-row{display:grid;grid-template-columns:1fr 1fr 0.6fr 0.5fr 0.6fr 0.7fr;gap:4px;padding:5px 4px;border-bottom:1px solid #0a1628;font-size:0.65rem;align-items:center}
.rec-row.header{color:var(--muted);font-weight:700;border-bottom:1px solid #1e3050}
.profit-pos{color:#4ade80;font-weight:700}
.profit-neg{color:#f87171;font-weight:700}

/* API 설정 모달 */
.api-modal{position:fixed;inset:0;background:#000a;z-index:3000;display:none;align-items:center;justify-content:center}
.api-modal.show{display:flex}
.api-box{background:#0b1628;border:1px solid #1e3050;border-radius:10px;padding:16px;width:360px;max-width:92vw}
.api-section{margin-bottom:12px;padding-bottom:12px;border-bottom:1px solid #1e3050}
.api-section:last-of-type{border-bottom:none;margin-bottom:4px}
.api-row{display:flex;gap:6px;margin-top:4px}
.api-row input{flex:1;background:#060c18;border:1px solid #1e3050;border-radius:4px;color:var(--text);font-size:0.75rem;padding:5px 8px;outline:none}
.api-row button{padding:5px 12px;background:#1a3050;border:none;border-radius:4px;color:#7aa;font-size:0.72rem;cursor:pointer}
.api-status{font-size:0.65rem;margin-top:3px;min-height:14px}
.api-callcount{font-size:0.65rem;color:#555;margin-top:6px;text-align:center}

#toast{position:fixed;bottom:20px;left:50%;transform:translateX(-50%);background:#0b1628;border:1px solid #1e3050;border-radius:6px;padding:8px 16px;font-size:0.75rem;z-index:5000;transition:opacity 0.3s;opacity:0;pointer-events:none;max-width:80vw;text-align:center}
#toast.show{opacity:1}
</style>
</head>
<body>

<!-- API 키 없을 때 첫 진입 화면 -->
<div class="setup-screen" id="setup-screen">
  <div style="font-size:2rem">⚽</div>
  <div class="setup-card">
    <h2>PRO FOOTBALL SIMULATOR</h2>
    <p>API-Football 키를 입력하면 실시간 선수 스탯, 폼, 라인업을 자동으로 불러옵니다.<br>
    The Odds API 키를 입력하면 실시간 배당률도 자동 입력됩니다.</p>
    <div class="setup-field">
      <label>🔴 API-FOOTBALL KEY</label>
      <span class="sub">dashboard.api-football.com · 무료 100콜/일</span>
      <input type="password" id="setup-apif" placeholder="API-Football 키 입력...">
    </div>
    <div class="setup-field">
      <label>💰 THE ODDS API KEY <span style="color:#555;font-weight:400">(선택)</span></label>
      <span class="sub">the-odds-api.com · 무료 500크레딧/월</span>
      <input type="password" id="setup-odds" placeholder="Odds API 키 입력... (선택)">
    </div>
    <button class="setup-btn" onclick="startWithKeys()">▶ 시작하기</button>
    <button class="setup-skip" onclick="startWithoutKeys()">API 없이 테스트 모드로 시작 (제한됨)</button>
    <div class="setup-status" id="setup-status"></div>
  </div>
</div>

<header>
  <div class="logo">
    <div class="logo-icon">⚽</div>
    <div>
      <div class="logo-text">PRO TACTICAL SIMULATOR <span style="font-size:0.65rem;color:#cc44ff;margin-left:6px">v5 LIVE</span></div>
      <div class="logo-sub">REAL-TIME API · ELO MODEL · MONTE CARLO · EV CALCULATOR</div>
    </div>
  </div>
  <div class="hstats">
    <button class="hbtn" onclick="openStats()">📈 통계</button>
    <button class="hbtn" id="api-btn" onclick="openApiModal()">🔑 API설정</button>
    <div class="hpill" id="call-count-pill">API: <strong id="call-count">0</strong>/100</div>
    <div class="hpill">시즌 <strong>2025</strong></div>
  </div>
</header>

<div class="layout">
  <!-- LEFT: HOME -->
  <div class="panel" id="home-panel">
    <div class="ph">
      <div class="tbadge">
        <div class="bcircle home">🏠</div>
        <div style="flex:1;min-width:0">
          <div class="tname home" id="home-name">팀 선택</div>
          <div class="tleague" id="home-league-lbl">HOME</div>
          <div class="elo-badge home" id="home-elo">ELO: —</div>
          <div class="form-badges" id="home-form"></div>
        </div>
      </div>
      <select id="home-league" onchange="onLeagueChange('home')"></select>
      <select id="home-team" onchange="onTeamChange('home')"><option value="">-- 팀 선택 --</option></select>
      <div class="frow" id="home-formations"></div>
    </div>
    <div class="tabs">
      <button class="tab active" onclick="switchTab('home','all',this)">선수 목록</button>
      <button class="tab" onclick="switchTab('home','starting',this)">선발(<span id="home-start-count">0</span>)</button>
      <button class="tab" onclick="showAutoMenu('home',this)">⚡자동▾</button>
    </div>
    <div class="sbox"><input type="text" id="home-search" placeholder="🔍 이름·포지션..." oninput="renderPlayerList('home')"></div>
    <div class="plist" id="home-plist">
      <div class="loading-state" id="home-loading" style="display:none">
        <div class="spinner"></div>
        <span id="home-loading-text">로딩 중...</span>
      </div>
      <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;flex:1;padding:20px;color:#334;font-size:0.75rem;text-align:center" id="home-empty">리그와 팀을 선택하면<br>실시간으로 선수 데이터를 불러옵니다</div>
    </div>
    <div class="subs">
      <div class="subs-title">선발 (<span id="home-sub-count">0</span>/11)</div>
      <div class="subs-list" id="home-subs"></div>
    </div>
  </div>

  <!-- CENTER -->
  <div class="center">
    <div class="mbar">
      <div>
        <div class="mteam home" id="m-home-name">홈팀</div>
        <div style="font-size:0.65rem;color:var(--muted)" id="m-home-form">-</div>
        <div style="font-size:0.60rem;color:#334" id="xg-h">xG —</div>
      </div>
      <div class="mvsbox">
        <div class="mvslbl">WIN PROBABILITY</div>
        <button onclick="swapTeams()" style="padding:3px 8px;background:#0a1628;border:1px solid #1e3050;border-radius:3px;color:#7aa;font-size:0.68rem;cursor:pointer;margin-bottom:3px">⇄ 교체</button>
        <div class="probbar">
          <div class="prob-h" id="pb-h" style="width:33%"></div>
          <div class="prob-d" id="pb-d" style="width:34%"></div>
          <div class="prob-a" id="pb-a" style="width:33%"></div>
        </div>
        <div class="plabels">
          <span style="color:var(--home)" id="pl-h">33%</span>
          <span style="color:var(--muted)" id="pl-d">34%</span>
          <span style="color:var(--away)" id="pl-a">33%</span>
        </div>
        <div class="predscore" id="pred-score">예상 스코어: — : —</div>
      </div>
      <div style="text-align:right">
        <div class="mteam away" id="m-away-name">원정팀</div>
        <div style="font-size:0.65rem;color:var(--muted);text-align:right" id="m-away-form">-</div>
        <div style="font-size:0.60rem;color:#334;text-align:right" id="xg-a">xG —</div>
      </div>
    </div>

    <div class="pwrap">
      <div class="pitch" id="pitch">
        <svg class="pitch-svg" viewBox="0 0 100 130" xmlns="http://www.w3.org/2000/svg">
          <rect x="2" y="2" width="96" height="126" fill="none" stroke="rgba(255,255,255,0.22)" stroke-width="0.5"/>
          <line x1="2" y1="65" x2="98" y2="65" stroke="rgba(255,255,255,0.22)" stroke-width="0.5"/>
          <circle cx="50" cy="65" r="11" fill="none" stroke="rgba(255,255,255,0.22)" stroke-width="0.5"/>
          <circle cx="50" cy="65" r="0.8" fill="rgba(255,255,255,0.4)"/>
          <rect x="20" y="98" width="60" height="26" fill="none" stroke="rgba(255,255,255,0.22)" stroke-width="0.5"/>
          <rect x="34" y="112" width="32" height="14" fill="none" stroke="rgba(255,255,255,0.22)" stroke-width="0.5"/>
          <circle cx="50" cy="107" r="4" fill="none" stroke="rgba(255,255,255,0.13)" stroke-width="0.5"/>
          <rect x="20" y="6" width="60" height="26" fill="none" stroke="rgba(255,255,255,0.22)" stroke-width="0.5"/>
          <rect x="34" y="6" width="32" height="14" fill="none" stroke="rgba(255,255,255,0.22)" stroke-width="0.5"/>
          <circle cx="50" cy="23" r="4" fill="none" stroke="rgba(255,255,255,0.13)" stroke-width="0.5"/>
          <rect x="40" y="124" width="20" height="4" fill="none" stroke="rgba(255,255,255,0.3)" stroke-width="0.4"/>
          <rect x="40" y="2" width="20" height="4" fill="none" stroke="rgba(255,255,255,0.3)" stroke-width="0.4"/>
        </svg>
        <div id="pitch-players"></div>
      </div>
    </div>

    <div class="statsbar">
      <div>
        <div class="srow"><div class="sval home" id="sv-att-h">—</div><div class="sbar"><div class="sfill home" id="sf-att" style="width:50%"></div></div><div class="sval away" id="sv-att-a">—</div></div>
        <div class="srow"><div class="sval home" id="sv-def-h">—</div><div class="sbar"><div class="sfill home" id="sf-def" style="width:50%"></div></div><div class="sval away" id="sv-def-a">—</div></div>
        <div class="srow"><div class="sval home" id="sv-ovr-h">—</div><div class="sbar"><div class="sfill home" id="sf-ovr" style="width:50%"></div></div><div class="sval away" id="sv-ovr-a">—</div></div>
      </div>
      <div class="scenter">
        <div class="snm">공격 | 수비 | 종합</div>
        <button class="simbtn" id="sim-btn" onclick="runSimulation()">▶ 시뮬레이션</button>
      </div>
      <div>
        <div class="srow r"><div class="sval away" id="sv-att-a2">—</div><div class="sbar"><div class="sfill away" id="sf-att2" style="width:50%"></div></div><div class="sval home" id="sv-att-h2">—</div></div>
        <div class="srow r"><div class="sval away" id="sv-def-a2">—</div><div class="sbar"><div class="sfill away" id="sf-def2" style="width:50%"></div></div><div class="sval home" id="sv-def-h2">—</div></div>
        <div class="srow r"><div class="sval away" id="sv-ovr-a2">—</div><div class="sbar"><div class="sfill away" id="sf-ovr2" style="width:50%"></div></div><div class="sval home" id="sv-ovr-h2">—</div></div>
      </div>
    </div>

    <div class="wbox">
      <div class="wtitle">⚙ 가중치 조정</div>
      <div class="wgrid">
        <div class="witem"><label>공격 FW <span id="wv-att">3.0</span></label><input type="range" min="0.5" max="5" step="0.1" value="3.0" oninput="onWeightChange('att',this.value)"></div>
        <div class="witem"><label>미드필더 <span id="wv-mid">2.5</span></label><input type="range" min="0.5" max="5" step="0.1" value="2.5" oninput="onWeightChange('mid',this.value)"></div>
        <div class="witem"><label>수비 DF <span id="wv-def">2.0</span></label><input type="range" min="0.5" max="5" step="0.1" value="2.0" oninput="onWeightChange('def',this.value)"></div>
        <div class="witem"><label>골키퍼 <span id="wv-gk">1.5</span></label><input type="range" min="0.5" max="5" step="0.1" value="1.5" oninput="onWeightChange('gk',this.value)"></div>
      </div>
    </div>
  </div>

  <!-- RIGHT: AWAY -->
  <div class="panel right" id="away-panel">
    <div class="ph">
      <div class="tbadge">
        <div class="bcircle away">✈️</div>
        <div style="flex:1;min-width:0">
          <div class="tname away" id="away-name">팀 선택</div>
          <div class="tleague" id="away-league-lbl">AWAY</div>
          <div class="elo-badge away" id="away-elo">ELO: —</div>
          <div class="form-badges" id="away-form"></div>
        </div>
      </div>
      <select id="away-league" onchange="onLeagueChange('away')"></select>
      <select id="away-team" onchange="onTeamChange('away')"><option value="">-- 팀 선택 --</option></select>
      <div class="frow" id="away-formations"></div>
    </div>
    <div class="tabs">
      <button class="tab active" onclick="switchTab('away','all',this)">선수 목록</button>
      <button class="tab" onclick="switchTab('away','starting',this)">선발(<span id="away-start-count">0</span>)</button>
      <button class="tab" onclick="showAutoMenu('away',this)">⚡자동▾</button>
    </div>
    <div class="sbox"><input type="text" id="away-search" placeholder="🔍 이름·포지션..." oninput="renderPlayerList('away')"></div>
    <div class="plist" id="away-plist">
      <div class="loading-state" id="away-loading" style="display:none">
        <div class="spinner"></div>
        <span id="away-loading-text">로딩 중...</span>
      </div>
      <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;flex:1;padding:20px;color:#334;font-size:0.75rem;text-align:center" id="away-empty">리그와 팀을 선택하면<br>실시간으로 선수 데이터를 불러옵니다</div>
    </div>
    <div class="subs">
      <div class="subs-title">선발 (<span id="away-sub-count">0</span>/11)</div>
      <div class="subs-list" id="away-subs"></div>
    </div>
  </div>
</div>

<!-- AUTO MENU -->
<div id="auto-menu" class="auto-menu">
  <div class="auto-menu-item" onclick="autoFillByScore()">
    <span class="ami-icon">⭐</span>
    <span><span class="ami-label">최고 점수 11인</span><span class="ami-sub">골+어시스트+출전 기반</span></span>
  </div>
  <div class="auto-menu-item" onclick="autoFillByStarts()">
    <span class="ami-icon">📋</span>
    <span><span class="ami-label">출전 빈도 기반</span><span class="ami-sub">이번 시즌 최다 선발</span></span>
  </div>
  <div style="border-top:1px solid #1e3050;margin:2px 0"></div>
  <div class="auto-menu-item" onclick="fetchAndApplyLineup()">
    <span class="ami-icon">🔴</span>
    <span><span class="ami-label">실제 라인업 불러오기</span><span class="ami-sub">API-Football 최근 경기 실제 선발</span></span>
  </div>
  <div class="auto-menu-item" onclick="fetchOddsAndFill()">
    <span class="ami-icon">💰</span>
    <span><span class="ami-label">배당률 자동 입력</span><span class="ami-sub">Odds API 실시간 배당</span></span>
  </div>
</div>

<!-- RESULT MODAL -->
<div class="modal-overlay" id="modal-overlay" onclick="if(event.target===this)closeModal()">
  <div class="modal">
    <h2>📊 시뮬레이션 결과 (6,000회)</h2>
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:4px">
      <div style="font-family:'Barlow Condensed',sans-serif;font-size:1rem;font-weight:700;color:var(--home)" id="modal-home-name"></div>
      <div style="font-family:'Barlow Condensed',sans-serif;font-size:1rem;font-weight:700;color:var(--away)" id="modal-away-name"></div>
    </div>
    <div class="result-score-big">
      <span style="color:var(--home)" id="modal-hg">—</span>
      <span style="color:var(--muted)">:</span>
      <span style="color:var(--away)" id="modal-ag">—</span>
    </div>
    <div id="modal-verdict" style="text-align:center;font-size:0.75rem;margin-bottom:10px;color:var(--muted)"></div>
    <div class="result-bars">
      <div class="rbar-row"><span style="color:var(--home);min-width:40px" id="modal-hw"></span><div class="rbar"><div class="rbar-fill" id="rbar-h" style="background:linear-gradient(90deg,#0044cc,#0099ff)"></div></div><span style="color:var(--muted);min-width:30px;text-align:right">홈</span></div>
      <div class="rbar-row"><span style="color:#fbbf24;min-width:40px" id="modal-dw"></span><div class="rbar"><div class="rbar-fill" id="rbar-d" style="background:#1a3050"></div></div><span style="color:var(--muted);min-width:30px;text-align:right">무</span></div>
      <div class="rbar-row"><span style="color:var(--away);min-width:40px" id="modal-aw"></span><div class="rbar"><div class="rbar-fill" id="rbar-a" style="background:linear-gradient(90deg,#cc4400,#ff8800)"></div></div><span style="color:var(--muted);min-width:30px;text-align:right">원정</span></div>
    </div>
    <div class="top-players">
      <div class="top-box"><div class="tb-title" style="color:var(--home)">🔵 홈 TOP3</div><div id="modal-home-top"></div></div>
      <div class="top-box"><div class="tb-title" style="color:var(--away)">🟠 원정 TOP3</div><div id="modal-away-top"></div></div>
    </div>
    <div style="font-size:0.65rem;color:#444;text-align:center;margin:4px 0" id="modal-meta"></div>

    <div class="ev-section">
      <div class="ev-title">💰 배당률 & EV 계산</div>
      <div class="ev-grid">
        <div class="ev-item"><label>홈 배당</label><input type="number" id="odds-home" placeholder="2.10" step="0.01" oninput="calcEV()"></div>
        <div class="ev-item"><label>무 배당</label><input type="number" id="odds-draw" placeholder="3.20" step="0.01" oninput="calcEV()"></div>
        <div class="ev-item"><label>원정 배당</label><input type="number" id="odds-away" placeholder="3.50" step="0.01" oninput="calcEV()"></div>
      </div>
      <div class="ev-result" id="ev-result" style="display:none">
        <div><div style="font-size:0.62rem;color:var(--muted)">홈 EV</div><div class="ev-value" id="ev-h">—</div></div>
        <div><div style="font-size:0.62rem;color:var(--muted)">무 EV</div><div class="ev-value" id="ev-d">—</div></div>
        <div><div style="font-size:0.62rem;color:var(--muted)">원정 EV</div><div class="ev-value" id="ev-a">—</div></div>
      </div>
      <div class="ev-rec" id="ev-rec" style="color:var(--muted);background:#0a1220">배당률을 입력하면 EV가 계산됩니다</div>
    </div>

    <div class="result-input">
      <div class="ri-title">📝 결과 입력 (통계 기록)</div>
      <div class="result-btns">
        <button class="rbtn" onclick="recordResult('home')" style="color:var(--home)">홈 승</button>
        <button class="rbtn" onclick="recordResult('draw')" style="color:#fbbf24">무승부</button>
        <button class="rbtn" onclick="recordResult('away')" style="color:var(--away)">원정 승</button>
      </div>
      <div id="record-status" style="font-size:0.65rem;color:#555;text-align:center;margin-top:5px"></div>
    </div>
    <button class="modal-close" onclick="closeModal()">✕ 닫기</button>
  </div>
</div>

<!-- STATS PANEL -->
<div class="stats-panel" id="stats-panel" onclick="if(event.target===this)closeStats()">
  <div class="stats-box">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px">
      <h2 style="font-size:0.9rem;color:#7aa;letter-spacing:2px;margin:0">📈 예측 통계</h2>
      <button onclick="closeStats()" style="background:none;border:none;color:#888;font-size:1.1rem;cursor:pointer">✕</button>
    </div>
    <div class="summary-grid">
      <div class="summary-card"><div class="sv" id="stat-total">0</div><div class="sl">총 예측</div></div>
      <div class="summary-card"><div class="sv" id="stat-correct" style="color:#4ade80">0</div><div class="sl">적중 / 적중률</div></div>
      <div class="summary-card"><div class="sv" id="stat-profit">0</div><div class="sl">누적 수익</div></div>
    </div>
    <div class="rec-row header"><span>홈</span><span>원정</span><span>예측</span><span>배당</span><span>결과</span><span>수익</span></div>
    <div id="stat-history" style="max-height:280px;overflow-y:auto"></div>
    <div id="stat-empty" style="text-align:center;color:#555;font-size:0.72rem;padding:20px">아직 기록이 없습니다</div>
    <div style="display:flex;gap:6px;margin-top:10px">
      <button onclick="clearStats()" style="flex:1;padding:7px;background:#1a0808;border:1px solid #7f1d1d;border-radius:5px;color:#f87171;font-size:0.72rem;cursor:pointer">🗑 초기화</button>
      <button onclick="closeStats()" style="flex:2;padding:7px;background:#1a2a3a;border:none;border-radius:5px;color:#888;font-size:0.72rem;cursor:pointer">닫기</button>
    </div>
  </div>
</div>

<!-- API 설정 모달 -->
<div class="api-modal" id="api-modal" onclick="if(event.target===this)closeApiModal()">
  <div class="api-box">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">
      <span style="font-size:0.82rem;color:#7aa;font-weight:700;letter-spacing:1px">🔑 API 키 설정</span>
      <button onclick="closeApiModal()" style="background:none;border:none;color:#888;cursor:pointer">✕</button>
    </div>
    <div class="api-section">
      <div style="font-size:0.70rem;color:#7aa;letter-spacing:1px">🔴 API-FOOTBALL</div>
      <div style="font-size:0.63rem;color:#555;margin:3px 0">dashboard.api-football.com · 무료 100콜/일</div>
      <div class="api-row">
        <input type="password" id="apif-input" placeholder="API 키...">
        <button onclick="saveKey('apif')">저장</button>
      </div>
      <div class="api-status" id="apif-status"></div>
    </div>
    <div class="api-section">
      <div style="font-size:0.70rem;color:#7aa;letter-spacing:1px">💰 THE ODDS API</div>
      <div style="font-size:0.63rem;color:#555;margin:3px 0">the-odds-api.com · 무료 500크레딧/월</div>
      <div class="api-row">
        <input type="password" id="odds-input" placeholder="API 키...">
        <button onclick="saveKey('odds')">저장</button>
      </div>
      <div class="api-status" id="odds-api-status"></div>
    </div>
    <div class="api-callcount">오늘 API 사용: <strong id="modal-call-count">0</strong>콜 / 남은 캐시: <strong id="cache-count">0</strong>팀</div>
    <button onclick="closeApiModal()" style="width:100%;padding:8px;background:#1a2a3a;border:none;border-radius:5px;color:#888;font-size:0.75rem;cursor:pointer;margin-top:10px">닫기</button>
  </div>
</div>

<div id="toast"></div>

<script>
// ═══════════════════════════════════
// CONSTANTS
// ═══════════════════════════════════
const SEASON = 2024; // API-Football 시즌 (2024-25 시즌)

const LEAGUES = {
  "EPL":      { id: 39,  name: "Premier League" },
  "라리가":   { id: 140, name: "La Liga" },
  "분데스리가":{ id: 78,  name: "Bundesliga" },
  "세리에A":  { id: 135, name: "Serie A" },
  "리그1":    { id: 61,  name: "Ligue 1" }
};

// ELO 기본값 (API 데이터 없을 때 폴백)
const ELO_BASE = {
  "Liverpool":1940,"Arsenal":1915,"Chelsea":1880,"Manchester City":1895,
  "Manchester United":1810,"Tottenham Hotspur":1820,"Aston Villa":1850,
  "Real Madrid":1950,"Barcelona":1935,"Atletico Madrid":1890,
  "Bayern Munich":1960,"Borussia Dortmund":1890,"Bayer Leverkusen":1920,
  "Inter":1900,"Juventus":1870,"Napoli":1860,
  "Paris Saint Germain":1930,"Marseille":1870,"Monaco":1860
};

const FORMATIONS = ["4-3-3","4-4-2","4-5-1","3-5-2","3-4-3","4-2-3-1","5-3-2","4-1-4-1"];

const FORM_POS = {
  "4-3-3":{home:[[50,92],[15,74],[38,76],[62,76],[85,74],[22,58],[50,54],[78,58],[15,40],[50,37],[85,40]],away:[[50,8],[85,26],[62,24],[38,24],[15,26],[78,42],[50,46],[22,42],[85,60],[50,63],[15,60]]},
  "4-4-2":{home:[[50,92],[15,74],[38,76],[62,76],[85,74],[15,57],[38,57],[62,57],[85,57],[34,38],[66,38]],away:[[50,8],[85,26],[62,24],[38,24],[15,26],[85,43],[62,43],[38,43],[15,43],[66,62],[34,62]]},
  "4-5-1":{home:[[50,92],[15,74],[38,76],[62,76],[85,74],[10,56],[30,55],[50,53],[70,55],[90,56],[50,37]],away:[[50,8],[85,26],[62,24],[38,24],[15,26],[90,44],[70,45],[50,47],[30,45],[10,44],[50,63]]},
  "3-5-2":{home:[[50,92],[25,76],[50,78],[75,76],[12,60],[32,57],[52,54],[72,57],[88,60],[34,38],[66,38]],away:[[50,8],[75,24],[50,22],[25,24],[88,40],[68,43],[48,46],[28,43],[12,40],[66,62],[34,62]]},
  "3-4-3":{home:[[50,92],[25,76],[50,78],[75,76],[15,60],[38,58],[62,58],[85,60],[20,40],[50,37],[80,40]],away:[[50,8],[75,24],[50,22],[25,24],[85,40],[62,42],[38,42],[15,40],[80,60],[50,63],[20,60]]},
  "4-2-3-1":{home:[[50,92],[15,74],[38,76],[62,76],[85,74],[34,62],[66,62],[22,48],[50,46],[78,48],[50,36]],away:[[50,8],[85,26],[62,24],[38,24],[15,26],[66,38],[34,38],[78,52],[50,54],[22,52],[50,64]]},
  "5-3-2":{home:[[50,92],[8,75],[28,76],[50,78],[72,76],[92,75],[22,60],[50,57],[78,60],[34,40],[66,40]],away:[[50,8],[92,25],[72,24],[50,22],[28,24],[8,25],[78,40],[50,43],[22,40],[66,60],[34,60]]},
  "4-1-4-1":{home:[[50,92],[15,74],[38,76],[62,76],[85,74],[50,64],[12,54],[35,52],[65,52],[88,54],[50,37]],away:[[50,8],[85,26],[62,24],[38,24],[15,26],[50,36],[88,46],[65,48],[35,48],[12,46],[50,63]]}
};

const FORM_GROUPS = {
  "4-3-3":["GK","DF","DF","DF","DF","MF","MF","MF","FW","FW","FW"],
  "4-4-2":["GK","DF","DF","DF","DF","MF","MF","MF","MF","FW","FW"],
  "4-5-1":["GK","DF","DF","DF","DF","MF","MF","MF","MF","MF","FW"],
  "3-5-2":["GK","DF","DF","DF","MF","MF","MF","MF","MF","FW","FW"],
  "3-4-3":["GK","DF","DF","DF","MF","MF","MF","MF","FW","FW","FW"],
  "4-2-3-1":["GK","DF","DF","DF","DF","MF","MF","MF","MF","MF","FW"],
  "5-3-2":["GK","DF","DF","DF","DF","DF","MF","MF","MF","FW","FW"],
  "4-1-4-1":["GK","DF","DF","DF","DF","MF","MF","MF","MF","MF","FW"]
};

// ═══════════════════════════════════
// STATE
// ═══════════════════════════════════
const state = {
  home: { league:"EPL", team:"", teamId:null, formation:"4-3-3", players:[], starting:[], tab:"all" },
  away: { league:"라리가", team:"", teamId:null, formation:"4-3-3", players:[], starting:[], tab:"all" },
  weights: { att:3.0, mid:2.5, def:2.0, gk:1.5 },
  lastSim: null
};

// 캐시 (선수 스탯, 팀 목록, 폼)
const cache = {
  squads: {},    // teamId → {players, ts}
  teams: {},     // leagueId → {teams, ts}
  forms: {},     // teamId → {form, ts}
};

let autoMenuSide = "home";
let apiCallCount = parseInt(localStorage.getItem("api_calls_today") || "0");
const todayKey = new Date().toDateString();
if (localStorage.getItem("api_call_date") !== todayKey) {
  apiCallCount = 0;
  localStorage.setItem("api_call_date", todayKey);
  localStorage.setItem("api_calls_today", "0");
}

// ═══════════════════════════════════
// API HELPER
// ═══════════════════════════════════
function getApifKey() { return localStorage.getItem("apif_key"); }
function getOddsKey() { return localStorage.getItem("odds_api_key"); }

async function apifCall(endpoint) {
  const key = getApifKey();
  if (!key) throw new Error("API-Football 키 없음 — 🔑 API설정 버튼을 눌러 키를 입력하세요");

  // file:// 프로토콜 체크
  if (location.protocol === "file:") {
    throw new Error("file:// 로 열면 API 차단됨. 파일을 서버에서 열어야 해요. 아래 방법 중 하나:\n1. VS Code Live Server 확장\n2. python -m http.server 8000\n3. Claude.ai 아티팩트로 실행");
  }

  apiCallCount++;
  localStorage.setItem("api_calls_today", apiCallCount);
  document.getElementById("call-count").textContent = apiCallCount;
  try { document.getElementById("modal-call-count").textContent = apiCallCount; } catch(e) {}

  const res = await fetch(`https://v3.football.api-sports.io${endpoint}`, {
    headers: { "x-apisports-key": key }
  });
  if (!res.ok) throw new Error(`API HTTP 오류 ${res.status}`);
  const data = await res.json();
  if (data.errors && Object.keys(data.errors).length) {
    throw new Error("API 에러: " + JSON.stringify(data.errors));
  }
  return data;
}

// ═══════════════════════════════════
// SETUP SCREEN
// ═══════════════════════════════════
function startWithKeys() {
  const apif = document.getElementById("setup-apif").value.trim();
  const odds = document.getElementById("setup-odds").value.trim();
  if (!apif) {
    document.getElementById("setup-status").textContent = "⚠ API-Football 키를 입력하세요";
    document.getElementById("setup-status").style.color = "#f87171";
    return;
  }
  localStorage.setItem("apif_key", apif);
  if (odds) localStorage.setItem("odds_api_key", odds);
  document.getElementById("setup-status").textContent = "✅ 저장 완료!";
  document.getElementById("setup-status").style.color = "#4ade80";
  setTimeout(() => {
    document.getElementById("setup-screen").style.display = "none";
    updateApiBtn();
    initApp();
  }, 600);
}
function startWithoutKeys() {
  document.getElementById("setup-screen").style.display = "none";
  showToast("⚠ API 키 없음 - 선수 데이터를 불러올 수 없습니다", "red");
  initApp();
}

// ═══════════════════════════════════
// TEAM LIST (API)
// ═══════════════════════════════════
async function fetchTeams(leagueName) {
  const league = LEAGUES[leagueName];
  if (!league) return [];

  // 캐시 확인 (1시간)
  const cached = cache.teams[league.id];
  if (cached && Date.now() - cached.ts < 3600000) return cached.teams;

  showToast(`📋 ${leagueName} 팀 목록 로딩 중...`, "blue");
  try {
    const data = await apifCall(`/teams?league=${league.id}&season=${SEASON}`);
    const teams = (data.response || []).map(t => ({
      id: t.team.id,
      name: t.team.name,
      logo: t.team.logo,
      venue: t.venue?.name
    })).sort((a,b) => a.name.localeCompare(b.name));

    cache.teams[league.id] = { teams, ts: Date.now() };
    return teams;
  } catch(e) {
    showToast("팀 목록 로딩 실패: " + e.message, "red");
    return [];
  }
}

// ═══════════════════════════════════
// SQUAD + STATS (API)
// ═══════════════════════════════════
async function fetchSquad(side, teamId, teamName) {
  // 캐시 확인 (6시간)
  const cached = cache.squads[teamId];
  if (cached && Date.now() - cached.ts < 21600000) {
    state[side].players = cached.players;
    renderPlayerList(side);
    return;
  }

  showLoading(side, `${teamName} 불러오는 중...`);

  try {
    // /players/squads - 무료 플랜 작동 확인된 엔드포인트
    const data = await apifCall(`/players/squads?team=${teamId}`);
    const rawPlayers = data.response?.[0]?.players || [];

    if (!rawPlayers.length) {
      throw new Error(`선수 없음 (팀ID: ${teamId})`);
    }

    const players = rawPlayers.map(p => ({
      id: p.id,
      name: p.name,
      no: p.number || 0,
      pos: normalizePos(p.position),
      mp: 0, starts: 0,
      gls: 0, ast: 0,
      xg: null, crdY: 0, crdR: 0,
      rating: null
    }));

    cache.squads[teamId] = { players, ts: Date.now() };
    state[side].players = players;
    hideLoading(side);
    renderPlayerList(side);
    showToast(`✅ ${teamName} ${players.length}명 로드. 스탯 업데이트 중...`, "green");

    // 백그라운드 스탯 로드
    loadPlayerStats(side, teamId, teamName);

  } catch(e) {
    console.error("fetchSquad error:", e);
    hideLoading(side);
    showToast("로딩 실패: " + e.message, "red");
  }
}

async function loadPlayerStats(side, teamId, teamName) {
  try {
    const leagueId = LEAGUES[state[side].league]?.id;
    if (!leagueId) return;

    // 선수 통계 페이지 1
    const page1 = await apifCall(`/players?team=${teamId}&season=${SEASON}&league=${leagueId}&page=1`);
    const items = page1.response || [];
    const totalPages = Math.min(page1.paging?.total || 1, 3); // 최대 3페이지

    let allItems = [...items];
    for (let pg = 2; pg <= totalPages; pg++) {
      const pageN = await apifCall(`/players?team=${teamId}&season=${SEASON}&league=${leagueId}&page=${pg}`);
      allItems = [...allItems, ...(pageN.response || [])];
    }

    if (!allItems.length) return;

    // 기존 선수 목록에 스탯 병합
    const current = cache.squads[teamId]?.players || [];
    const statsMap = {};
    allItems.forEach(item => {
      const p = item.player;
      const stats = item.statistics?.find(s => s.league?.id === leagueId) || item.statistics?.[0] || {};
      statsMap[p.id] = {
        mp: stats.games?.appearences || 0,
        starts: stats.games?.lineups || 0,
        gls: parseInt(stats.goals?.total) || 0,
        ast: parseInt(stats.goals?.assists) || 0,
        xg: stats.goals?.expected ? parseFloat(stats.goals.expected) : null,
        crdY: stats.cards?.yellow || 0,
        crdR: stats.cards?.red || 0,
        rating: parseFloat(stats.games?.rating) || null
      };
    });

    const merged = current.map(p => ({
      ...p,
      ...(statsMap[p.id] || {})
    }));

    cache.squads[teamId] = { players: merged, ts: Date.now() };
    // 아직 같은 팀이 선택되어 있으면 업데이트
    if (state[side].teamId === teamId) {
      state[side].players = merged;
      renderPlayerList(side);
      showToast(`✅ ${teamName} 스탯 업데이트 완료`, "green");
    }
  } catch(e) {
    // 스탯 로드 실패는 무시 (이미 기본 정보는 표시됨)
    console.warn("스탯 로드 실패:", e.message);
  }
}

function normalizePos(pos) {
  if (!pos) return "MF";
  const p = pos.toUpperCase();
  if (["G","GK","GOALKEEPER"].includes(p)) return "GK";
  if (["D","DF","DEFENDER"].includes(p)) return "DF";
  if (["F","FW","FORWARD","ATTACKER"].includes(p)) return "FW";
  if (["M","MF","MIDFIELDER","MIDFIELD"].includes(p)) return "MF";
  // 부분 매칭
  if (p.startsWith("GOAL")) return "GK";
  if (p.startsWith("DEF")) return "DF";
  if (p.startsWith("MID")) return "MF";
  if (p.startsWith("ATT") || p.startsWith("FOR")) return "FW";
  return "MF";
}

function showLoading(side, text) {
  const plist = document.getElementById(side+"-plist");
  if (plist) plist.innerHTML = `<div style="display:flex;flex-direction:column;align-items:center;justify-content:center;padding:30px;gap:10px;color:#4a6a8a;font-size:0.75rem"><div class="spinner"></div><span>${text}</span></div>`;
}
function hideLoading(side) {
  const plist = document.getElementById(side+"-plist");
  if (plist) plist.innerHTML = "";
}

// ═══════════════════════════════════
// FORM (API)
// ═══════════════════════════════════
async function fetchForm(side, teamId) {
  // 캐시 30분
  const cached = cache.forms[teamId];
  if (cached && Date.now() - cached.ts < 1800000) {
    renderFormBadges(side, cached.form);
    return;
  }
  try {
    const data = await apifCall(`/fixtures?team=${teamId}&last=5&status=FT`);
    const fixtures = (data.response || []).sort((a,b) =>
      new Date(a.fixture.date) - new Date(b.fixture.date)
    );
    const form = fixtures.map(f => {
      const isHome = f.teams.home.id === teamId;
      const hg = f.goals.home, ag = f.goals.away;
      if (hg === null || ag === null) return "?";
      return isHome ? (hg>ag?"W":hg===ag?"D":"L") : (ag>hg?"W":ag===hg?"D":"L");
    });
    cache.forms[teamId] = { form, ts: Date.now() };
    renderFormBadges(side, form);
  } catch(e) {
    // 폼 조회 실패는 무시 (중요하지 않음)
  }
}

function renderFormBadges(side, form) {
  const container = document.getElementById(side+"-form");
  container.innerHTML = "";
  form.forEach(r => {
    const span = document.createElement("span");
    const color = r==="W"?"#4ade80":r==="D"?"#fbbf24":r==="L"?"#f87171":"#555";
    span.style.cssText = `display:inline-block;width:18px;height:18px;border-radius:3px;background:${color}22;border:1px solid ${color}55;color:${color};font-size:0.65rem;font-weight:700;text-align:center;line-height:16px;font-family:'Barlow Condensed',sans-serif`;
    span.textContent = r;
    span.title = r==="W"?"승":r==="D"?"무":r==="L"?"패":"?";
    container.appendChild(span);
  });
}

// ═══════════════════════════════════
// LEAGUE/TEAM CHANGE
// ═══════════════════════════════════
function onLeagueChange(side) {
  const league = document.getElementById(side+"-league").value;
  state[side].league = league;
  state[side].team = "";
  state[side].teamId = null;
  state[side].players = [];
  state[side].starting = [];

  // 팀 목록 로드
  populateTeams(side);
  renderPlayerList(side);
  updateMatchupBar(side);
  updateLiveStats();
}

async function onTeamChange(side) {
  const sel = document.getElementById(side+"-team");
  const opt = sel.options[sel.selectedIndex];
  const dataId = opt ? opt.getAttribute("data-id") : null;
  const teamId = dataId ? parseInt(dataId) : null;
  const teamName = opt ? opt.value : "";

  if (!teamName) {
    state[side].team = ""; state[side].teamId = null;
    state[side].players = []; state[side].starting = [];
    updateMatchupBar(side); renderPlayerList(side); return;
  }

  state[side].team = teamName;
  state[side].teamId = teamId;
  state[side].players = [];
  state[side].starting = [];
  document.getElementById(side+"-form").innerHTML = "";
  updateMatchupBar(side);
  updateLiveStats();

  if (!getApifKey()) {
    const emptyEl = document.getElementById(side+"-empty");
    emptyEl.style.display = "flex";
    emptyEl.innerHTML = "API 키를 설정하면 선수 데이터를 불러올 수 있습니다";
    return;
  }

  // teamId 없으면 캐시에서 찾기
  let resolvedId = teamId;
  if (!resolvedId) {
    const leagueId = LEAGUES[state[side].league]?.id;
    const cachedTeams = cache.teams[leagueId]?.teams || [];
    const found = cachedTeams.find(t => t.name === teamName);
    if (found) {
      resolvedId = found.id;
      state[side].teamId = resolvedId;
    } else {
      // 팀 목록 다시 로드 후 재시도
      showToast("팀 목록 재로딩 중...", "blue");
      const teams = await fetchTeams(state[side].league);
      const t = teams.find(t => t.name === teamName);
      if (t) {
        resolvedId = t.id;
        state[side].teamId = resolvedId;
        // select option에 data-id 업데이트
        const sel = document.getElementById(side+"-team");
        Array.from(sel.options).forEach(opt => {
          if (opt.value === teamName) opt.setAttribute("data-id", t.id);
        });
      }
    }
  }

  if (!resolvedId) {
    showToast("팀 ID를 찾을 수 없습니다", "red");
    return;
  }

  // 선수 스탯 + 폼 동시에 당김
  fetchSquad(side, resolvedId, teamName);
  fetchForm(side, resolvedId);
}

async function populateTeams(side) {
  const sel = document.getElementById(side+"-team");
  sel.innerHTML = "<option value=''>-- 팀 선택 --</option>";

  const key = getApifKey();
  if (!key) return;

  const teams = await fetchTeams(state[side].league);
  teams.forEach(t => {
    const opt = document.createElement("option");
    opt.value = t.name;
    opt.setAttribute("data-id", t.id);
    opt.textContent = t.name;
    sel.appendChild(opt);
  });
}

// ═══════════════════════════════════
// PLAYER SCORE
// ═══════════════════════════════════
function posGroup(pos) {
  if (!pos) return "MF";
  if (pos==="GK") return "GK";
  if (pos==="DF") return "DF";
  if (pos==="FW") return "FW";
  return "MF";
}
function playerScore(p) {
  const W = {GK:{d:3.5,a:0.1},DF:{d:2.5,a:0.5},MF:{d:1.2,a:1.4},FW:{d:0.3,a:2.8}};
  const pg = posGroup(p.pos);
  const w = W[pg]||W.MF;
  // xG 있으면 우선 사용, 없으면 골수로 추정
  const goalContrib = p.xg != null ? p.xg * 3 + p.ast * 2 : p.gls * 3 + p.ast * 2;
  const att = goalContrib * w.a;
  const def = ((p.starts||p.mp)*0.3 - (p.crdY*0.5+p.crdR*2)) * w.d;
  // API rating 있으면 보너스
  const ratingBonus = p.rating ? (p.rating - 6.5) * 0.5 : 0;
  return Math.max(0.5, att + def + ratingBonus);
}
function teamPower(squad, weights) {
  return squad.reduce((sum,p) => {
    const pg = posGroup(p.pos);
    const wt = pg==="GK"?weights.gk:pg==="DF"?weights.def:pg==="FW"?weights.att:weights.mid;
    return sum + playerScore(p)*wt;
  }, 0);
}

// ═══════════════════════════════════
// SIMULATION
// ═══════════════════════════════════
function runSimulation() {
  const hs = state.home, as = state.away;
  if (hs.starting.length < 7 || as.starting.length < 7) {
    showToast("양팀 최소 7명 이상 선발하세요!", "red"); return;
  }

  const TACTIC = {
    "4-3-3":{beats:"4-4-2",weakTo:"4-5-1",b:1.08},
    "4-4-2":{beats:"4-5-1",weakTo:"4-3-3",b:1.05},
    "4-5-1":{beats:"4-3-3",weakTo:"4-4-2",b:1.06},
    "3-5-2":{beats:"4-4-2",weakTo:"4-3-3",b:1.10},
    "3-4-3":{beats:"4-5-1",weakTo:"3-5-2",b:1.12},
    "4-2-3-1":{beats:"4-4-2",weakTo:"4-3-3",b:1.05},
    "5-3-2":{beats:"4-3-3",weakTo:"3-5-2",b:1.07},
    "4-1-4-1":{beats:"3-4-3",weakTo:"4-3-3",b:1.06}
  };

  let hPow = teamPower(hs.starting, state.weights);
  let aPow = teamPower(as.starting, state.weights);

  // ELO (25%)
  const hElo = ELO_BASE[hs.team] || 1750;
  const aElo = ELO_BASE[as.team] || 1750;
  const eloF = Math.pow(10, (hElo-aElo)/400);
  hPow = hPow*0.75 + hPow*0.25*eloF;
  aPow = aPow*0.75 + aPow*0.25/eloF;

  // 홈 어드밴티지
  hPow *= 1.08;

  // 전술
  const hT = TACTIC[hs.formation], aT = TACTIC[as.formation];
  if (hT && hT.beats===as.formation) hPow *= hT.b;
  else if (hT && hT.weakTo===as.formation && aT) aPow *= aT.b;

  const total = hPow+aPow||1;
  const hR = hPow/total, aR = aPow/total;
  const hLambda = hR*2.6+0.2, aLambda = aR*2.6+0.2;

  function poisson(l) {
    let L=Math.exp(-l),k=0,p=1;
    do{k++;p*=Math.random();}while(p>L);
    return k-1;
  }

  const N=6000;
  let hw=0,d=0,aw=0,thg=0,tag=0;
  for(let i=0;i<N;i++){
    const hg=poisson(hLambda), ag=poisson(aLambda);
    thg+=hg; tag+=ag;
    if(hg>ag)hw++; else if(hg===ag)d++; else aw++;
  }

  const result = {
    homeWin:Math.round(hw/N*100), draw:Math.round(d/N*100), awayWin:Math.round(aw/N*100),
    homeGoals:(thg/N).toFixed(1), awayGoals:(tag/N).toFixed(1),
    hPow:Math.round(hPow), aPow:Math.round(aPow),
    hElo, aElo,
    homeTeam:hs.team, awayTeam:as.team,
    homeFormation:hs.formation, awayFormation:as.formation,
    homeLeague:hs.league, awayLeague:as.league,
    homeSquad:[...hs.starting], awaySquad:[...as.starting],
    ts:Date.now()
  };
  state.lastSim = result;

  updateProbBar(result.homeWin, result.draw, result.awayWin, result.homeGoals, result.awayGoals);
  showResultModal(result);
}

// ═══════════════════════════════════
// MODAL
// ═══════════════════════════════════
function showResultModal(r) {
  document.getElementById("modal-home-name").textContent = r.homeTeam;
  document.getElementById("modal-away-name").textContent = r.awayTeam;
  document.getElementById("modal-hg").textContent = r.homeGoals;
  document.getElementById("modal-ag").textContent = r.awayGoals;
  document.getElementById("modal-hw").textContent = r.homeWin+"%";
  document.getElementById("modal-dw").textContent = r.draw+"%";
  document.getElementById("modal-aw").textContent = r.awayWin+"%";
  document.getElementById("rbar-h").style.width = r.homeWin+"%";
  document.getElementById("rbar-d").style.width = r.draw+"%";
  document.getElementById("rbar-a").style.width = r.awayWin+"%";

  const verdict = r.homeWin>r.awayWin?`🎯 ${r.homeTeam} 승리 유력`:
                  r.awayWin>r.homeWin?`🎯 ${r.awayTeam} 승리 유력`:"🤝 무승부 유력";
  document.getElementById("modal-verdict").textContent = verdict;

  const hTop=[...r.homeSquad].sort((a,b)=>playerScore(b)-playerScore(a)).slice(0,3);
  const aTop=[...r.awaySquad].sort((a,b)=>playerScore(b)-playerScore(a)).slice(0,3);
  document.getElementById("modal-home-top").innerHTML=hTop.map(p=>
    `<div class="tb-player">⭐ ${p.name} <span style="color:#445">${p.gls}G ${p.ast}A${p.rating?" ⭐"+p.rating:""}</span></div>`).join("");
  document.getElementById("modal-away-top").innerHTML=aTop.map(p=>
    `<div class="tb-player">⭐ ${p.name} <span style="color:#445">${p.gls}G ${p.ast}A${p.rating?" ⭐"+p.rating:""}</span></div>`).join("");

  document.getElementById("modal-meta").textContent =
    `ELO: ${r.homeTeam} ${r.hElo} vs ${r.awayTeam} ${r.aElo} | 전력지수: ${r.hPow} vs ${r.aPow}`;

  // 배당 초기화
  ["odds-home","odds-draw","odds-away"].forEach(id=>document.getElementById(id).value="");
  document.getElementById("ev-result").style.display="none";
  document.getElementById("ev-rec").textContent="배당률을 입력하면 EV가 계산됩니다";
  document.getElementById("ev-rec").style.color="var(--muted)";
  document.getElementById("ev-rec").style.background="#0a1220";
  document.getElementById("record-status").textContent="";

  document.getElementById("modal-overlay").classList.add("show");
}
function closeModal(){ document.getElementById("modal-overlay").classList.remove("show"); }

// ═══════════════════════════════════
// EV
// ═══════════════════════════════════
function calcEV() {
  if (!state.lastSim) return;
  const r = state.lastSim;
  const oh=parseFloat(document.getElementById("odds-home").value);
  const od=parseFloat(document.getElementById("odds-draw").value);
  const oa=parseFloat(document.getElementById("odds-away").value);
  if (!oh&&!od&&!oa){document.getElementById("ev-result").style.display="none";return;}

  const pH=r.homeWin/100, pD=r.draw/100, pA=r.awayWin/100;
  const evH=oh?(pH*(oh-1)-(1-pH)).toFixed(3):null;
  const evD=od?(pD*(od-1)-(1-pD)).toFixed(3):null;
  const evA=oa?(pA*(oa-1)-(1-pA)).toFixed(3):null;

  document.getElementById("ev-result").style.display="grid";
  function setEV(id,v){
    const el=document.getElementById(id);
    el.textContent=v===null?"—":(parseFloat(v)>0?"+":"")+v;
    el.className="ev-value "+(v===null?"neu":parseFloat(v)>0?"pos":"neg");
  }
  setEV("ev-h",evH); setEV("ev-d",evD); setEV("ev-a",evA);

  const evs=[{l:"홈",v:evH,o:oh},{l:"무",v:evD,o:od},{l:"원정",v:evA,o:oa}]
    .filter(x=>x.v!==null).sort((a,b)=>parseFloat(b.v)-parseFloat(a.v));
  const rec=document.getElementById("ev-rec");
  if(evs.length&&parseFloat(evs[0].v)>0){
    rec.textContent=`✅ 추천: ${evs[0].l} 배당 ${evs[0].o} → EV +${evs[0].v}`;
    rec.style.color="#4ade80"; rec.style.background="#0a1a0a";
  } else {
    rec.textContent="❌ 모든 배당 EV 마이너스 — 베팅 비추천";
    rec.style.color="#f87171"; rec.style.background="#1a0808";
  }
}

// ═══════════════════════════════════
// STATS
// ═══════════════════════════════════
const STATS_KEY="sim_stats_v5";
function getStats(){try{return JSON.parse(localStorage.getItem(STATS_KEY)||"[]");}catch{return[];}}
function saveStats(a){localStorage.setItem(STATS_KEY,JSON.stringify(a));}

function recordResult(outcome) {
  if (!state.lastSim) return;
  const r = state.lastSim;
  const oh=parseFloat(document.getElementById("odds-home").value)||null;
  const od=parseFloat(document.getElementById("odds-draw").value)||null;
  const oa=parseFloat(document.getElementById("odds-away").value)||null;
  const predicted=r.homeWin>r.awayWin&&r.homeWin>r.draw?"home":r.awayWin>r.homeWin&&r.awayWin>r.draw?"away":"draw";
  const correct=predicted===outcome;
  const betOdds=outcome==="home"?oh:outcome==="draw"?od:oa;
  const profit=betOdds?(correct?betOdds-1:-1).toFixed(2):null;

  const arr=getStats();
  arr.unshift({id:r.ts,homeTeam:r.homeTeam,awayTeam:r.awayTeam,predicted,outcome,correct,
    oddsHome:oh,oddsDraw:od,oddsAway:oa,profit:profit?parseFloat(profit):null,
    date:new Date().toLocaleDateString("ko-KR")});
  saveStats(arr);

  const el=document.getElementById("record-status");
  el.textContent=correct?"✅ 적중! 기록됨":"❌ 미적중. 기록됨";
  el.style.color=correct?"#4ade80":"#f87171";
  showToast(correct?"✅ 적중!":"❌ 미적중","green");
}

function openStats(){renderStats();document.getElementById("stats-panel").classList.add("show");}
function closeStats(){document.getElementById("stats-panel").classList.remove("show");}
function renderStats(){
  const arr=getStats();
  const total=arr.length, correct=arr.filter(r=>r.correct).length;
  const profit=arr.reduce((s,r)=>s+(r.profit||0),0);
  document.getElementById("stat-total").textContent=total;
  document.getElementById("stat-correct").textContent=total?`${correct}(${Math.round(correct/total*100)}%)`:"0";
  document.getElementById("stat-profit").textContent=(profit>=0?"+":"")+profit.toFixed(2);
  document.getElementById("stat-profit").style.color=profit>=0?"#4ade80":"#f87171";
  const hist=document.getElementById("stat-history");
  const empty=document.getElementById("stat-empty");
  if(!arr.length){hist.innerHTML="";empty.style.display="block";return;}
  empty.style.display="none";
  hist.innerHTML=arr.slice(0,50).map(r=>{
    const bo=r.outcome==="home"?r.oddsHome:r.outcome==="draw"?r.oddsDraw:r.oddsAway;
    const pt=r.profit!=null?(r.profit>=0?"+":"")+r.profit.toFixed(2):"—";
    return `<div class="rec-row">
      <span style="color:#aac;font-size:0.63rem">${r.homeTeam||"?"}</span>
      <span style="color:#ca8;font-size:0.63rem">${r.awayTeam||"?"}</span>
      <span style="color:${r.predicted==="home"?"var(--home)":r.predicted==="away"?"var(--away)":"#fbbf24"}">${r.predicted==="home"?"홈":r.predicted==="away"?"원정":"무"}</span>
      <span style="color:#7aa">${bo||"—"}</span>
      <span style="color:${r.correct?"#4ade80":"#f87171"}">${r.correct?"✅":"❌"}</span>
      <span class="${r.profit!=null&&r.profit>=0?"profit-pos":r.profit!=null?"profit-neg":""}">${pt}</span>
    </div>`;
  }).join("");
}
function clearStats(){if(!confirm("초기화?"))return;saveStats([]);renderStats();}

// ═══════════════════════════════════
// PLAYER LIST
// ═══════════════════════════════════
function renderPlayerList(side) {
  const s = state[side];
  const search = (document.getElementById(side+"-search").value||"").toLowerCase();
  let players = s.tab==="starting" ? s.starting :
    s.players.filter(p => !search || p.name.toLowerCase().includes(search) || p.pos.toLowerCase().includes(search));

  const list = document.getElementById(side+"-plist");

  // 팀 미선택
  if (!s.team) {
    list.innerHTML = "";
    const empty = document.getElementById(side+"-empty");
    if (empty) { empty.style.display="flex"; empty.textContent="리그와 팀을 선택하면 실시간으로 선수 데이터를 불러옵니다"; list.appendChild(empty); }
    return;
  }

  // 로딩 중 (선수 없음)
  if (!s.players.length) {
    return;
  }

  // 선수 있으면 loading/empty 숨기기
  document.getElementById(side+"-loading").style.display = "none";
  document.getElementById(side+"-empty").style.display = "none";

  // 포지션 순서로 정렬
  const posOrder = {GK:0,DF:1,MF:2,FW:3};
  players = [...players].sort((a,b) => {
    const pd = (posOrder[posGroup(a.pos)]||2) - (posOrder[posGroup(b.pos)]||2);
    return pd !== 0 ? pd : playerScore(b) - playerScore(a);
  });

  list.innerHTML = "";
  players.forEach(p => {
    const isStart = s.starting.includes(p);
    const score = Math.round(playerScore(p));
    const row = document.createElement("div");
    row.className = "prow" + (isStart?" starting":"");
    const c = {GK:"#ffaa44",DF:"#44dd88",MF:"#66aaff",FW:"#ff6688"}[p.pos]||"#66aaff";
    const ratingBadge = p.rating ? `<span style="font-size:0.6rem;color:#ffd700;margin-left:3px">⭐${p.rating}</span>` : "";
    const xgBadge = p.xg != null ? `<span class="xg-mini">xG${p.xg}</span>` : "";
    row.innerHTML = `<div class="ptag" style="background:${c}22;color:${c};border:1px solid ${c}33">${p.pos}</div>
      <div class="pinfo">
        <div class="pname">${p.name}${ratingBadge}</div>
        <div class="pstats">${p.starts||p.mp}경기 · ${p.gls}G ${p.ast}A${xgBadge}${p.crdY?" · 🟨"+p.crdY:""}</div>
      </div>
      <div class="pscore${score>=80?" hi":""}">${score}</div>
      <div class="pcheck" style="color:${isStart?(side==="home"?"var(--home)":"var(--away)"):"#1a3a5a"}">${isStart?"✓":"+"}</div>`;
    row.addEventListener("click", () => togglePlayer(side, p));
    list.appendChild(row);
  });
  renderSubs(side);
  updateCounts(side);
}

function togglePlayer(side, p) {
  const s = state[side];
  const idx = s.starting.indexOf(p);
  if (idx>=0) s.starting.splice(idx,1);
  else s.starting.push(p);
  renderPlayerList(side);
  renderPitch();
  updateLiveStats();
}

function renderSubs(side) {
  const s = state[side];
  const el = document.getElementById(side+"-subs");
  el.innerHTML = "";
  s.starting.forEach(p => {
    const span = document.createElement("span");
    span.className = "schip";
    const c={GK:"#ffaa44",DF:"#44dd88",MF:"#66aaff",FW:"#ff6688"}[p.pos]||"#66aaff";
    span.innerHTML=`<span style="color:${c}">${p.pos}</span>${p.name.split(" ").pop()}`;
    span.onclick = () => togglePlayer(side, p);
    el.appendChild(span);
  });
}
function updateCounts(side) {
  document.getElementById(side+"-start-count").textContent = state[side].starting.slice(0,11).length;
  document.getElementById(side+"-sub-count").textContent = state[side].starting.length;
}
function switchTab(side, tab, btn) {
  state[side].tab = tab;
  document.getElementById(side+"-panel").querySelectorAll(".tab").forEach(t=>t.classList.remove("active"));
  if(btn) btn.classList.add("active");
  renderPlayerList(side);
}

// ═══════════════════════════════════
// AUTO FILL
// ═══════════════════════════════════
function showAutoMenu(side, btn) {
  autoMenuSide = side;
  const menu = document.getElementById("auto-menu");
  const rect = btn.getBoundingClientRect();
  menu.style.display = "block";
  menu.style.top = (rect.bottom+4)+"px";
  menu.style.left = rect.left+"px";
  document.addEventListener("click", hideAutoMenuOutside);
}
function hideAutoMenuOutside(e) {
  if (!document.getElementById("auto-menu").contains(e.target)) {
    document.getElementById("auto-menu").style.display="none";
    document.removeEventListener("click", hideAutoMenuOutside);
  }
}
function autoFillByScore() {
  document.getElementById("auto-menu").style.display="none";
  fillBySide(autoMenuSide, "score");
}
function autoFillByStarts() {
  document.getElementById("auto-menu").style.display="none";
  fillBySide(autoMenuSide, "starts");
}
function fillBySide(side, mode) {
  const s = state[side];
  if (!s.players.length) { showToast("선수 데이터를 먼저 로드하세요", "red"); return; }

  const formation = s.formation;
  const groups = FORM_GROUPS[formation] || FORM_GROUPS["4-3-3"];
  const needed = {GK:0,DF:0,MF:0,FW:0};
  groups.forEach(g => needed[g]++);

  const byPos = {GK:[],DF:[],MF:[],FW:[]};
  s.players.forEach(p => { const pg=posGroup(p.pos); if(byPos[pg]) byPos[pg].push(p); });

  const sortFn = mode==="score"
    ? (a,b) => playerScore(b)-playerScore(a)
    : (a,b) => (b.starts||b.mp)-(a.starts||a.mp);
  Object.keys(byPos).forEach(pg => byPos[pg].sort(sortFn));

  const selected = [];
  Object.entries(needed).forEach(([pg,cnt]) => byPos[pg].slice(0,cnt).forEach(p=>selected.push(p)));

  if (selected.length < 11) {
    const rem = s.players.filter(p=>!selected.includes(p)).sort((a,b)=>playerScore(b)-playerScore(a));
    while (selected.length<11 && rem.length) selected.push(rem.shift());
  }

  s.starting = selected;
  renderPlayerList(side);
  renderPitch();
  updateLiveStats();
  showToast(`⚡ ${side==="home"?"홈":"원정"} 자동선발 완료 (${formation})`, "green");
}

async function fetchAndApplyLineup() {
  document.getElementById("auto-menu").style.display="none";
  const side = autoMenuSide;
  const s = state[side];
  if (!s.teamId) { showToast("팀을 먼저 선택하세요", "red"); return; }
  if (!getApifKey()) { showToast("API-Football 키가 없습니다", "red"); return; }

  showToast("🔴 최근 경기 라인업 조회 중...", "blue");
  try {
    // 1. 최근 완료 경기 조회
    const fix = await apifCall(`/fixtures?team=${s.teamId}&last=5&status=FT`);
    if (!fix.response?.length) { showToast("최근 경기 없음", "red"); return; }

    const latest = fix.response[0];
    const fid = latest.fixture.id;
    const matchName = `${latest.teams.home.name} vs ${latest.teams.away.name}`;
    const matchDate = latest.fixture.date?.slice(0,10);

    // 2. 해당 경기 라인업
    const lu = await apifCall(`/fixtures/lineups?fixture=${fid}&team=${s.teamId}`);
    if (!lu.response?.length) { showToast("라인업 데이터 없음", "red"); return; }

    const startXI = lu.response[0].startXI || [];
    console.log("API 라인업:", startXI.map(x => x.player?.name));
    console.log("DB 선수 목록:", s.players.map(p => p.name));

    // 3. 강화된 이름 매칭
    const matched = [];
    const unmatched = [];

    startXI.forEach(xi => {
      const apiPlayer = xi.player;
      if (!apiPlayer?.name) return;

      const apiId = apiPlayer.id;
      const apiName = apiPlayer.name.toLowerCase().trim();
      const apiParts = apiName.split(/[\s.]+/).filter(Boolean);
      const apiLast = apiParts[apiParts.length - 1];
      const apiFirst = apiParts[0];

      // 1순위: player ID 직접 매칭
      let p = s.players.find(pl => pl.id === apiId);

      // 2순위: 성(last name) 완전 일치
      if (!p) p = s.players.find(pl => {
        const parts = pl.name.toLowerCase().split(/[\s.]+/).filter(Boolean);
        return parts[parts.length-1] === apiLast;
      });

      // 3순위: 이름 포함 (한쪽이 다른쪽을 포함)
      if (!p) p = s.players.find(pl => {
        const pn = pl.name.toLowerCase();
        return pn.includes(apiLast) || apiName.includes(pn.split(" ").pop());
      });

      // 4순위: 이름 첫글자 + 성 (B. Saka 형태 처리)
      if (!p && apiParts.length >= 2) {
        p = s.players.find(pl => {
          const parts = pl.name.toLowerCase().split(" ");
          const pFirst = parts[0][0]; // 첫글자
          const pLast = parts[parts.length-1];
          return pLast === apiLast && (apiFirst === pFirst || apiFirst.replace(".","") === pFirst);
        });
      }

      if (p && !matched.includes(p)) {
        matched.push(p);
      } else if (!p) {
        // DB에 없는 선수는 임시 객체로 추가 (이적생 등)
        const tempPlayer = {
          id: apiId,
          name: apiPlayer.name,
          no: xi.player.number || 0,
          pos: normalizePos(xi.player.pos || xi.player.grid?.split(":")[0]),
          mp: 0, starts: 0, gls: 0, ast: 0,
          xg: null, crdY: 0, crdR: 0, rating: null,
          _temp: true // 임시 선수 표시
        };
        matched.push(tempPlayer);
        unmatched.push(apiPlayer.name);
      }
    });

    if (matched.length < 4) {
      showToast(`매칭 실패 (${matched.length}명). 선수 목록이 로드됐는지 확인하세요.`, "red");
      return;
    }

    s.starting = matched;
    renderPlayerList(side);
    renderPitch();
    updateLiveStats();

    const unmatchedMsg = unmatched.length ? ` (DB없음: ${unmatched.join(", ")})` : "";
    showToast(`✅ ${matched.length}/11 로드 완료 (${matchName} · ${matchDate})${unmatchedMsg}`, "green");
    if (unmatched.length) console.warn("DB 미매칭 선수:", unmatched);
  } catch(e) {
    showToast("오류: "+e.message, "red");
  }
}

async function fetchOddsAndFill() {
  document.getElementById("auto-menu").style.display="none";
  const oddsKey = getOddsKey();
  if (!oddsKey) { showToast("Odds API 키가 없습니다", "red"); openApiModal(); return; }
  if (!state.home.team || !state.away.team) { showToast("양팀을 선택하세요", "red"); return; }

  const leagueKeys = {
    "EPL":"soccer_england_premier_league","라리가":"soccer_spain_la_liga",
    "분데스리가":"soccer_germany_bundesliga","세리에A":"soccer_italy_serie_a","리그1":"soccer_france_ligue_one"
  };
  const lk = leagueKeys[state.home.league] || leagueKeys[state.away.league];
  if (!lk) { showToast("지원하지 않는 리그", "red"); return; }

  showToast("💰 배당률 조회 중...", "blue");
  try {
    const res = await fetch(`https://api.the-odds-api.com/v4/sports/${lk}/odds/?apiKey=${oddsKey}&regions=eu&markets=h2h&oddsFormat=decimal`);
    const data = await res.json();
    if (!Array.isArray(data)) { showToast("배당 데이터 없음", "red"); return; }

    const ht = state.home.team.toLowerCase();
    const at = state.away.team.toLowerCase();
    const match = data.find(g => {
      const gh = g.home_team?.toLowerCase()||"";
      const ga = g.away_team?.toLowerCase()||"";
      return (gh.includes(ht.split(" ")[0])||ht.includes(gh.split(" ")[0])) &&
             (ga.includes(at.split(" ")[0])||at.includes(ga.split(" ")[0]));
    });
    if (!match) { showToast("해당 경기 배당 없음 (아직 일정 없거나 리그 불일치)", "red"); return; }

    const outcomes = match.bookmakers?.[0]?.markets?.[0]?.outcomes || [];
    const hO = outcomes.find(o=>o.name===match.home_team)?.price;
    const aO = outcomes.find(o=>o.name===match.away_team)?.price;
    const dO = outcomes.find(o=>o.name==="Draw")?.price;

    // 시뮬 결과 모달이 열려있으면 바로 입력
    if (document.getElementById("modal-overlay").classList.contains("show")) {
      if(hO) document.getElementById("odds-home").value = hO;
      if(dO) document.getElementById("odds-draw").value = dO;
      if(aO) document.getElementById("odds-away").value = aO;
      calcEV();
    }
    showToast(`✅ 배당: 홈 ${hO||"?"} / 무 ${dO||"?"} / 원정 ${aO||"?"}`, "green");
  } catch(e) {
    showToast("오류: "+e.message, "red");
  }
}

// ═══════════════════════════════════
// FORMATIONS
// ═══════════════════════════════════
function renderFormations(side) {
  const container = document.getElementById(side+"-formations");
  container.innerHTML = "";
  FORMATIONS.forEach(f => {
    const btn = document.createElement("button");
    btn.className = "fbtn"+(state[side].formation===f?" active "+side:"");
    btn.textContent = f;
    btn.onclick = () => {
      state[side].formation = f;
      renderFormations(side);
      renderPitch();
      updateMatchupBar(side);
      updateLiveStats();
    };
    container.appendChild(btn);
  });
}

// ═══════════════════════════════════
// PITCH
// ═══════════════════════════════════
function renderPitch() {
  const container = document.getElementById("pitch-players");
  container.innerHTML = "";
  const renderSide = (side, cls) => {
    const s = state[side];
    const positions = FORM_POS[s.formation]?.[side]||[];
    s.starting.slice(0,11).forEach((p,i) => {
      const pos = positions[i];
      if (!pos) return;
      const score = Math.round(playerScore(p));
      const div = document.createElement("div");
      div.className = "pp";
      div.style.left = pos[0]+"%"; div.style.top = pos[1]+"%";
      div.innerHTML = `<div class="pc ${cls}"><div class="pc-num">${p.no||i+1}</div><div class="pc-rating">${score}</div></div><div class="plbl">${p.name.split(" ").pop()}</div>`;
      div.title = `${p.name} | ${p.pos} | ${p.gls}G ${p.ast}A`;
      container.appendChild(div);
    });
  };
  renderSide("home","home");
  renderSide("away","away");
}

// ═══════════════════════════════════
// PROB BAR
// ═══════════════════════════════════
function updateProbBar(hw,d,aw,hg,ag) {
  document.getElementById("pb-h").style.width=hw+"%";
  document.getElementById("pb-d").style.width=d+"%";
  document.getElementById("pb-a").style.width=aw+"%";
  document.getElementById("pl-h").textContent=hw+"%";
  document.getElementById("pl-d").textContent=d+"%";
  document.getElementById("pl-a").textContent=aw+"%";
  document.getElementById("pred-score").innerHTML=`예상: <strong style="color:#ddd">${hg||"—"} : ${ag||"—"}</strong>`;
}
function updateLiveStats() {
  if (!state.home.starting.length && !state.away.starting.length) return;
  const hPow=teamPower(state.home.starting,state.weights);
  const aPow=teamPower(state.away.starting,state.weights);
  const tot=Math.max(1,hPow+aPow);
  const hR=hPow/tot, aR=aPow/tot;
  updateProbBar(Math.round(hR*100*0.8+10),Math.max(5,Math.min(30,100-Math.round(hR*100*0.8+10)-Math.round(aR*100*0.7+8))),Math.round(aR*100*0.7+8),(hR*2.6+0.2).toFixed(1),(aR*2.6+0.2).toFixed(1));

  function setS(h,a,s){const t=Math.max(1,h+a);
    document.getElementById(`sv-${s}-h`).textContent=h||"—";
    document.getElementById(`sv-${s}-a`).textContent=a||"—";
    document.getElementById(`sf-${s}`).style.width=Math.round(h/t*100)+"%";
    document.getElementById(`sv-${s}-h2`).textContent=h||"—";
    document.getElementById(`sv-${s}-a2`).textContent=a||"—";
    document.getElementById(`sf-${s}2`).style.width=Math.round(a/t*100)+"%";
  }
  const hAtt=Math.round(state.home.starting.filter(p=>posGroup(p.pos)==="FW").reduce((s,p)=>s+playerScore(p),0));
  const aDef=Math.round(state.away.starting.filter(p=>posGroup(p.pos)==="DF").reduce((s,p)=>s+playerScore(p),0));
  const aAtt=Math.round(state.away.starting.filter(p=>posGroup(p.pos)==="FW").reduce((s,p)=>s+playerScore(p),0));
  const hDef=Math.round(state.home.starting.filter(p=>posGroup(p.pos)==="DF").reduce((s,p)=>s+playerScore(p),0));
  setS(hAtt,aDef,"att"); setS(hDef,aAtt,"def"); setS(Math.round(hPow),Math.round(aPow),"ovr");

  const hxg=state.home.starting.reduce((s,p)=>s+(p.xg||p.gls*0.12),0).toFixed(2);
  const axg=state.away.starting.reduce((s,p)=>s+(p.xg||p.gls*0.12),0).toFixed(2);
  document.getElementById("xg-h").textContent="xG "+hxg;
  document.getElementById("xg-a").textContent="xG "+axg;
}

// ═══════════════════════════════════
// MATCHUP BAR
// ═══════════════════════════════════
function updateMatchupBar(side) {
  const s = state[side];
  const elo = ELO_BASE[s.team]||"—";
  if (side==="home") {
    document.getElementById("home-name").textContent = s.team||"팀 선택";
    document.getElementById("home-league-lbl").textContent = (s.league||"")+" · HOME";
    document.getElementById("m-home-name").textContent = s.team||"홈팀";
    document.getElementById("m-home-form").textContent = s.formation;
    document.getElementById("home-elo").textContent = "ELO "+elo;
  } else {
    document.getElementById("away-name").textContent = s.team||"팀 선택";
    document.getElementById("away-league-lbl").textContent = (s.league||"")+" · AWAY";
    document.getElementById("m-away-name").textContent = s.team||"원정팀";
    document.getElementById("m-away-form").textContent = s.formation;
    document.getElementById("away-elo").textContent = "ELO "+elo;
  }
}

function onWeightChange(key,val) {
  state.weights[key]=parseFloat(val);
  document.getElementById("wv-"+key).textContent=parseFloat(val).toFixed(1);
  updateLiveStats();
}

function swapTeams() {
  const tmp = {...state.home};
  state.home.league=state.away.league; state.home.team=state.away.team;
  state.home.teamId=state.away.teamId; state.home.players=[...state.away.players];
  state.home.starting=[...state.away.starting]; state.home.formation=state.away.formation;
  state.away.league=tmp.league; state.away.team=tmp.team;
  state.away.teamId=tmp.teamId; state.away.players=[...tmp.players];
  state.away.starting=[...tmp.starting]; state.away.formation=tmp.formation;

  ["home","away"].forEach(side => {
    const sel = document.getElementById(side+"-league");
    sel.value = state[side].league;
    populateTeams(side).then(() => {
      document.getElementById(side+"-team").value = state[side].team;
    });
    renderFormations(side);
    renderPlayerList(side);
    updateMatchupBar(side);
  });
  renderPitch();
  updateLiveStats();
  showToast("⇄ 홈/원정 교체", "green");
}

// ═══════════════════════════════════
// API 설정 모달
// ═══════════════════════════════════
function openApiModal() { loadApiStatus(); document.getElementById("api-modal").classList.add("show"); }
function closeApiModal() { document.getElementById("api-modal").classList.remove("show"); }
function loadApiStatus() {
  const apif = getApifKey(), odds = getOddsKey();
  if (apif) {
    document.getElementById("apif-input").placeholder = "저장됨 ("+apif.slice(0,6)+"...)";
    document.getElementById("apif-status").textContent = "✅ 연결됨"; document.getElementById("apif-status").style.color="#4ade80";
  }
  if (odds) {
    document.getElementById("odds-input").placeholder = "저장됨 ("+odds.slice(0,6)+"...)";
    document.getElementById("odds-api-status").textContent = "✅ 연결됨"; document.getElementById("odds-api-status").style.color="#4ade80";
  }
}
function saveKey(type) {
  const input = document.getElementById(type==="apif"?"apif-input":"odds-input").value.trim();
  if (!input) { showToast("키를 입력하세요","red"); return; }
  localStorage.setItem(type==="apif"?"apif_key":"odds_api_key", input);
  document.getElementById(type==="apif"?"apif-status":"odds-api-status").textContent="✅ 저장됨";
  updateApiBtn();
  showToast(`✅ ${type==="apif"?"API-Football":"Odds API"} 키 저장 완료`, "green");
}
function updateApiBtn() {
  const btn = document.getElementById("api-btn");
  if (getApifKey()) { btn.classList.add("connected"); btn.textContent="✅ API연결"; }
  else { btn.classList.remove("connected"); btn.textContent="🔑 API설정"; }
}

// ═══════════════════════════════════
// TOAST
// ═══════════════════════════════════
let toastTimer=null;
function showToast(msg,type) {
  const el=document.getElementById("toast");
  el.textContent=msg;
  el.style.color=type==="green"?"#4ade80":type==="red"?"#f87171":type==="blue"?"#60a5fa":"#ccc";
  el.style.borderColor=type==="green"?"#166534":type==="red"?"#7f1d1d":type==="blue"?"#1e3a5f":"#1e3050";
  el.classList.add("show");
  clearTimeout(toastTimer);
  toastTimer=setTimeout(()=>el.classList.remove("show"),3500);
}

// ═══════════════════════════════════
// INIT
// ═══════════════════════════════════
function initApp() {
  const leagues = Object.keys(LEAGUES);
  ["home","away"].forEach(side => {
    const sel = document.getElementById(side+"-league");
    sel.innerHTML = "";
    leagues.forEach(l => {
      const opt=document.createElement("option");
      opt.value=l; opt.textContent=l;
      if(l===state[side].league) opt.selected=true;
      sel.appendChild(opt);
    });
    if (getApifKey()) populateTeams(side);
    renderFormations(side);
    updateMatchupBar(side);
  });
  updateApiBtn();
  document.getElementById("call-count").textContent = apiCallCount;
}

// file:// 프로토콜 경고
if (location.protocol === "file:") {
  document.getElementById("setup-screen").style.display = "flex";
  document.getElementById("setup-status").style.color = "#f87171";
  document.getElementById("setup-status").innerHTML = `
    ⚠️ <strong>file:// 로 열면 API가 차단됩니다.</strong><br><br>
    해결 방법:<br>
    1. <strong>VS Code</strong> → Live Server 확장 설치 → Go Live 클릭<br>
    2. 터미널: <code>python -m http.server 8000</code> 후 localhost:8000 접속<br>
    3. 파일을 웹서버에 올리기
  `;
  document.getElementById("setup-btn").style.display = "none";
  document.getElementById("setup-skip").textContent = "그냥 계속 (API 안됨)";
} else if (getApifKey()) {
  document.getElementById("setup-screen").style.display = "none";
  initApp();
} else {
  document.getElementById("setup-apif").focus();
}
</script>
</body>
</html>
