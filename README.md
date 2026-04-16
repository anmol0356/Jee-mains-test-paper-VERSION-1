<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ΦSX — JEE Mains MCQ Arena</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;900&family=Share+Tech+Mono&family=Rajdhani:wght@300;400;500;600;700&family=IBM+Plex+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#020408;--bg2:#050910;--surface:#080d14;--surface2:#0c1220;
  --border:#0f1e35;--border2:#1a3050;
  --cyan:#00e5ff;--cyan2:#00b4d8;--pink:#ff2d78;--green:#00ff9d;
  --gold:#ffd700;--purple:#bd00ff;--orange:#ff6b35;
  --text:#cce8f4;--muted:#3a6080;
  --glow-c:rgba(0,229,255,0.18);--glow-p:rgba(255,45,120,0.18);
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{background:var(--bg);color:var(--text);font-family:'Rajdhani',sans-serif;min-height:100vh;overflow-x:hidden;cursor:none;}
#cursor{width:12px;height:12px;border:1.5px solid var(--cyan);border-radius:50%;position:fixed;top:0;left:0;pointer-events:none;z-index:9999;mix-blend-mode:screen;transition:border-color 0.15s;}
#cursor-trail{width:32px;height:32px;border:1px solid rgba(0,229,255,0.25);border-radius:50%;position:fixed;top:0;left:0;pointer-events:none;z-index:9998;}
#stars-canvas{position:fixed;inset:0;pointer-events:none;z-index:0;opacity:0.6;}
body::after{content:'';position:fixed;inset:0;background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,0,0,0.07) 2px,rgba(0,0,0,0.07) 4px);pointer-events:none;z-index:1;}
body::before{content:'';position:fixed;inset:0;background-image:linear-gradient(rgba(0,229,255,0.02) 1px,transparent 1px),linear-gradient(90deg,rgba(0,229,255,0.02) 1px,transparent 1px);background-size:50px 50px;pointer-events:none;z-index:0;}

/* HEADER */
header{position:sticky;top:0;z-index:200;background:rgba(2,4,8,0.95);backdrop-filter:blur(20px);border-bottom:1px solid var(--border2);height:60px;padding:0 2rem;display:flex;align-items:center;gap:1.5rem;box-shadow:0 0 40px rgba(0,229,255,0.05);}
header::after{content:'';position:absolute;bottom:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent 0%,var(--cyan) 30%,var(--purple) 60%,transparent 100%);animation:hdr-flow 6s linear infinite;background-size:200%;}
@keyframes hdr-flow{0%{background-position:200% 0;}100%{background-position:-200% 0;}}
.logo{font-family:'Orbitron',monospace;font-size:1.1rem;font-weight:900;color:var(--cyan);text-shadow:0 0 20px var(--cyan),0 0 40px rgba(0,229,255,0.3);letter-spacing:0.08em;animation:logopulse 3s ease-in-out infinite;}
.logo sub{font-size:0.5em;color:var(--pink);vertical-align:sub;}
@keyframes logopulse{0%,100%{text-shadow:0 0 20px var(--cyan),0 0 40px rgba(0,229,255,0.3);}50%{text-shadow:0 0 30px var(--cyan),0 0 60px rgba(0,229,255,0.5);}}
.hud-tag{font-family:'Share Tech Mono',monospace;font-size:0.58rem;color:var(--green);border:1px solid rgba(0,255,157,0.25);padding:3px 8px;border-radius:2px;letter-spacing:0.1em;text-shadow:0 0 8px var(--green);background:rgba(0,255,157,0.04);white-space:nowrap;}
.hud-tag::before{content:'● ';animation:blink 1.4s step-start infinite;}
@keyframes blink{50%{opacity:0;}}
.header-right{margin-left:auto;display:flex;align-items:center;gap:1rem;}
.progress-wrap{display:flex;align-items:center;gap:0.75rem;}
.progress-bar-outer{width:160px;height:6px;background:var(--surface2);border:1px solid var(--border2);border-radius:3px;overflow:hidden;}
.progress-bar-inner{height:100%;background:linear-gradient(90deg,var(--cyan),var(--purple));width:0%;transition:width 0.4s ease;border-radius:3px;}
.progress-text{font-family:'Share Tech Mono',monospace;font-size:0.6rem;color:var(--cyan);min-width:50px;text-align:right;}
.timer-box{font-family:'Share Tech Mono',monospace;font-size:0.72rem;color:var(--gold);border:1px solid rgba(255,215,0,0.3);padding:4px 10px;border-radius:2px;background:rgba(255,215,0,0.04);text-shadow:0 0 8px var(--gold);}

/* HUD corners */
.hc{position:fixed;width:18px;height:18px;border-color:var(--cyan);border-style:solid;opacity:0.18;pointer-events:none;z-index:2;}
.hc.tl{top:64px;left:0;border-width:1px 0 0 1px;}
.hc.tr{top:64px;right:0;border-width:1px 1px 0 0;}
.hc.bl{bottom:0;left:0;border-width:0 0 1px 1px;}
.hc.br{bottom:0;right:0;border-width:0 1px 1px 0;}

/* LAYOUT */
.layout{display:grid;grid-template-columns:230px 1fr;min-height:calc(100vh - 60px);position:relative;z-index:2;}

/* SIDEBAR */
nav.sidebar{border-right:1px solid var(--border2);background:rgba(5,9,16,0.8);backdrop-filter:blur(10px);padding:1rem 0;position:sticky;top:60px;height:calc(100vh - 60px);overflow-y:auto;display:flex;flex-direction:column;gap:0;}
nav.sidebar::-webkit-scrollbar{width:3px;}
nav.sidebar::-webkit-scrollbar-thumb{background:var(--border2);}
.nav-section-label{font-family:'Share Tech Mono',monospace;font-size:0.55rem;letter-spacing:0.18em;color:var(--muted);text-transform:uppercase;padding:0.6rem 1rem 0.4rem;display:flex;align-items:center;gap:0.5rem;}
.nav-section-label::after{content:'';flex:1;height:1px;background:linear-gradient(to right,var(--border2),transparent);}
.q-nav-grid{display:grid;grid-template-columns:repeat(5,1fr);gap:3px;padding:0 0.6rem 0.6rem;}
.q-nav-btn{width:100%;aspect-ratio:1;background:var(--surface);border:1px solid var(--border);border-radius:2px;color:var(--muted);font-family:'Share Tech Mono',monospace;font-size:0.56rem;cursor:none;transition:all 0.15s;display:flex;align-items:center;justify-content:center;}
.q-nav-btn:hover{border-color:var(--border2);color:var(--text);}
.q-nav-btn.active{border-color:var(--cyan);color:var(--cyan);background:rgba(0,229,255,0.08);box-shadow:0 0 6px rgba(0,229,255,0.15);}
.q-nav-btn.answered-correct{border-color:var(--green);color:var(--green);background:rgba(0,255,157,0.08);}
.q-nav-btn.answered-wrong{border-color:var(--pink);color:var(--pink);background:rgba(255,45,120,0.08);}
.q-nav-btn.skipped{border-color:var(--gold);color:var(--gold);background:rgba(255,215,0,0.06);}

/* SUBJECT FILTER */
.subject-filters{padding:0 0.6rem 0.8rem;display:flex;flex-direction:column;gap:4px;}
.sub-filter-btn{font-family:'Share Tech Mono',monospace;font-size:0.58rem;padding:5px 10px;border:1px solid var(--border2);border-radius:2px;background:var(--surface);color:var(--muted);cursor:none;text-align:left;letter-spacing:0.06em;transition:all 0.15s;}
.sub-filter-btn:hover{background:var(--surface2);color:var(--text);}
.sub-filter-btn.active-phy{border-color:var(--gold);color:var(--gold);background:rgba(255,215,0,0.06);}
.sub-filter-btn.active-chem{border-color:var(--green);color:var(--green);background:rgba(0,255,157,0.06);}
.sub-filter-btn.active-math{border-color:var(--purple);color:var(--purple);background:rgba(189,0,255,0.06);}

/* SIDEBAR SCORE */
.sidebar-score{margin:auto 0 0;padding:0.8rem 0.8rem;border-top:1px solid var(--border2);}
.score-mini{display:grid;grid-template-columns:1fr 1fr 1fr;gap:4px;}
.score-mini-item{background:var(--surface);border:1px solid var(--border);border-radius:2px;padding:5px 4px;text-align:center;}
.score-mini-val{font-family:'Orbitron',monospace;font-size:0.75rem;font-weight:700;line-height:1;}
.score-mini-label{font-family:'Share Tech Mono',monospace;font-size:0.45rem;color:var(--muted);margin-top:2px;letter-spacing:0.06em;}

/* MAIN */
main{padding:2rem 2.5rem;max-width:850px;}

/* QUESTION CARD */
.question-area{animation:fadeUp 0.35s ease both;}
@keyframes fadeUp{from{opacity:0;transform:translateY(14px);}to{opacity:1;transform:translateY(0);}}
.q-header{display:flex;align-items:center;gap:1rem;margin-bottom:1.5rem;}
.q-num{font-family:'Orbitron',monospace;font-size:0.6rem;color:var(--muted);background:var(--surface2);border:1px solid var(--border2);padding:4px 10px;border-radius:2px;letter-spacing:0.06em;}
.q-subject-tag{font-family:'Share Tech Mono',monospace;font-size:0.58rem;padding:3px 10px;border-radius:2px;letter-spacing:0.08em;}
.q-subject-tag.phy{border:1px solid rgba(255,215,0,0.4);color:var(--gold);background:rgba(255,215,0,0.05);}
.q-subject-tag.chem{border:1px solid rgba(0,255,157,0.4);color:var(--green);background:rgba(0,255,157,0.05);}
.q-subject-tag.math{border:1px solid rgba(189,0,255,0.4);color:var(--purple);background:rgba(189,0,255,0.05);}
.q-text{font-family:'Rajdhani',sans-serif;font-size:1.08rem;font-weight:500;line-height:1.7;color:var(--text);margin-bottom:1.5rem;padding:1.2rem 1.4rem;background:var(--surface);border:1px solid var(--border2);border-radius:3px;border-left:3px solid var(--cyan);clip-path:polygon(0 0,calc(100% - 10px) 0,100% 10px,100% 100%,0 100%);}

/* OPTIONS */
.options-grid{display:grid;grid-template-columns:1fr 1fr;gap:0.7rem;margin-bottom:1.5rem;}
.option-btn{background:var(--surface);border:1px solid var(--border2);border-radius:3px;padding:0.85rem 1.1rem;cursor:none;text-align:left;font-family:'Rajdhani',sans-serif;font-size:0.95rem;font-weight:500;color:var(--text);transition:all 0.2s;position:relative;clip-path:polygon(0 0,calc(100% - 8px) 0,100% 8px,100% 100%,0 100%);}
.option-btn::before{content:'';position:absolute;top:0;left:0;width:2px;height:0;background:var(--cyan);transition:height 0.25s;}
.option-btn:hover:not(.locked){border-color:rgba(0,229,255,0.3);background:var(--surface2);transform:translateX(3px);}
.option-btn:hover:not(.locked)::before{height:100%;}
.option-label{font-family:'Share Tech Mono',monospace;font-size:0.6rem;color:var(--muted);margin-right:0.6rem;}
.option-btn.selected-wrong{border-color:var(--pink)!important;background:rgba(255,45,120,0.09)!important;color:var(--pink)!important;animation:wrongFlash 0.4s ease;}
.option-btn.selected-wrong::before{height:100%;background:var(--pink)!important;}
@keyframes wrongFlash{0%,100%{background:rgba(255,45,120,0.09);}50%{background:rgba(255,45,120,0.2);}}
.option-btn.correct-glow{border-color:var(--green)!important;background:rgba(0,255,157,0.09)!important;color:var(--green)!important;box-shadow:0 0 18px rgba(0,255,157,0.25),inset 0 0 12px rgba(0,255,157,0.06);animation:correctPulse 1.2s ease infinite;}
.option-btn.correct-glow::before{height:100%;background:var(--green)!important;}
@keyframes correctPulse{0%,100%{box-shadow:0 0 18px rgba(0,255,157,0.25),inset 0 0 12px rgba(0,255,157,0.06);}50%{box-shadow:0 0 28px rgba(0,255,157,0.45),inset 0 0 20px rgba(0,255,157,0.1);}}
.option-btn.correct-plain{border-color:var(--green)!important;background:rgba(0,255,157,0.07)!important;color:var(--green)!important;}
.option-btn.locked{cursor:default!important;}

/* SOLUTION */
.solution-box{background:rgba(0,229,255,0.03);border:1px solid rgba(0,229,255,0.15);border-radius:3px;padding:1.1rem 1.3rem;margin-bottom:1.5rem;animation:fadeUp 0.3s ease;clip-path:polygon(0 0,calc(100% - 10px) 0,100% 10px,100% 100%,0 100%);}
.solution-box.hidden{display:none;}
.solution-label{font-family:'Share Tech Mono',monospace;font-size:0.6rem;color:var(--cyan);letter-spacing:0.12em;margin-bottom:0.6rem;display:flex;align-items:center;gap:0.5rem;}
.solution-label::before{content:'▶';font-size:0.45rem;color:var(--cyan);text-shadow:0 0 6px var(--cyan);}
.solution-text{font-family:'Rajdhani',sans-serif;font-size:0.96rem;color:var(--text);line-height:1.7;}

/* ACTION BUTTONS */
.action-row{display:flex;gap:0.75rem;align-items:center;flex-wrap:wrap;}
.btn{font-family:'Share Tech Mono',monospace;font-size:0.65rem;padding:9px 18px;border-radius:2px;cursor:none;letter-spacing:0.08em;transition:all 0.2s;border:1px solid;clip-path:polygon(0 0,calc(100% - 7px) 0,100% 7px,100% 100%,0 100%);}
.btn-show-sol{border-color:rgba(0,229,255,0.3);color:var(--cyan);background:rgba(0,229,255,0.05);}
.btn-show-sol:hover{background:rgba(0,229,255,0.12);box-shadow:0 0 14px rgba(0,229,255,0.15);}
.btn-show-sol.hidden{display:none;}
.btn-next{border-color:rgba(0,255,157,0.35);color:var(--green);background:rgba(0,255,157,0.05);}
.btn-next:hover{background:rgba(0,255,157,0.12);box-shadow:0 0 14px rgba(0,255,157,0.15);}
.btn-prev{border-color:var(--border2);color:var(--muted);background:var(--surface);}
.btn-prev:hover{color:var(--text);background:var(--surface2);}
.btn-skip{border-color:rgba(255,215,0,0.3);color:var(--gold);background:rgba(255,215,0,0.04);}
.btn-skip:hover{background:rgba(255,215,0,0.1);}
.btn-submit{border-color:rgba(255,45,120,0.4);color:var(--pink);background:rgba(255,45,120,0.06);}
.btn-submit:hover{background:rgba(255,45,120,0.14);box-shadow:0 0 16px rgba(255,45,120,0.2);}

/* RESULT SCREEN */
#result-screen{display:none;position:relative;z-index:2;padding:2.5rem 3rem;animation:fadeUp 0.5s ease;}
.result-hero{text-align:center;margin-bottom:3rem;padding-bottom:2.5rem;border-bottom:1px solid var(--border2);}
.result-title{font-family:'Orbitron',monospace;font-size:2.2rem;font-weight:900;color:transparent;background:linear-gradient(90deg,var(--cyan),var(--purple),var(--pink));-webkit-background-clip:text;background-clip:text;background-size:200%;animation:gshift 4s ease infinite;margin-bottom:0.5rem;letter-spacing:0.06em;}
@keyframes gshift{0%{background-position:0%;}50%{background-position:100%;}100%{background-position:0%;}}
.result-score-big{font-family:'Orbitron',monospace;font-size:4rem;font-weight:900;color:var(--cyan);text-shadow:0 0 40px rgba(0,229,255,0.5);line-height:1;margin:1rem 0;}
.result-out-of{font-family:'Share Tech Mono',monospace;font-size:0.75rem;color:var(--muted);letter-spacing:0.12em;}
.result-grade{font-family:'Orbitron',monospace;font-size:1.5rem;font-weight:700;margin-top:0.5rem;}
.result-stats{display:grid;grid-template-columns:repeat(4,1fr);gap:1rem;margin-bottom:2.5rem;}
.rs-card{background:var(--surface);border:1px solid var(--border2);border-radius:3px;padding:1rem 1.2rem;text-align:center;position:relative;clip-path:polygon(0 0,calc(100% - 8px) 0,100% 8px,100% 100%,0 100%);}
.rs-card::before{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:var(--accent-c,var(--cyan));box-shadow:0 0 6px var(--accent-c,var(--cyan));}
.rs-val{font-family:'Orbitron',monospace;font-size:1.8rem;font-weight:700;color:var(--accent-c,var(--cyan));line-height:1;}
.rs-label{font-family:'Share Tech Mono',monospace;font-size:0.54rem;color:var(--muted);margin-top:0.3rem;letter-spacing:0.1em;}
.subject-breakdown{margin-bottom:2.5rem;}
.sb-title{font-family:'Share Tech Mono',monospace;font-size:0.62rem;letter-spacing:0.18em;color:var(--green);text-transform:uppercase;margin-bottom:1rem;display:flex;align-items:center;gap:0.75rem;}
.sb-title::before{content:'▶';font-size:0.48rem;text-shadow:0 0 8px var(--green);}
.sb-title::after{content:'';flex:1;height:1px;background:linear-gradient(to right,rgba(0,255,157,0.3),transparent);}
.sb-row{display:flex;align-items:center;gap:1rem;margin-bottom:0.6rem;}
.sb-subject{font-family:'Share Tech Mono',monospace;font-size:0.62rem;color:var(--text);min-width:100px;letter-spacing:0.06em;}
.sb-bar-wrap{flex:1;height:8px;background:var(--surface2);border-radius:2px;overflow:hidden;border:1px solid var(--border);}
.sb-bar{height:100%;border-radius:2px;transition:width 1s ease;}
.sb-pct{font-family:'Share Tech Mono',monospace;font-size:0.62rem;min-width:50px;text-align:right;}
.btn-restart{font-family:'Share Tech Mono',monospace;font-size:0.7rem;padding:12px 28px;border:1px solid rgba(0,229,255,0.4);color:var(--cyan);background:rgba(0,229,255,0.06);border-radius:2px;cursor:none;letter-spacing:0.1em;transition:all 0.2s;clip-path:polygon(0 0,calc(100% - 10px) 0,100% 10px,100% 100%,0 100%);margin-top:1rem;}
.btn-restart:hover{background:rgba(0,229,255,0.14);box-shadow:0 0 24px rgba(0,229,255,0.2);}
.review-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(50px,1fr));gap:5px;margin-top:1rem;}
.review-pill{font-family:'Share Tech Mono',monospace;font-size:0.55rem;padding:4px;border-radius:2px;text-align:center;border:1px solid;}
.review-pill.correct{border-color:rgba(0,255,157,0.4);color:var(--green);background:rgba(0,255,157,0.07);}
.review-pill.wrong{border-color:rgba(255,45,120,0.4);color:var(--pink);background:rgba(255,45,120,0.07);}
.review-pill.skipped{border-color:rgba(255,215,0,0.3);color:var(--gold);background:rgba(255,215,0,0.05);}

/* WATERMARK */
#watermark{position:fixed;bottom:1.75rem;right:2rem;z-index:500;text-decoration:none;display:flex;align-items:center;gap:0.6rem;background:rgba(2,4,8,0.88);border:1px solid rgba(189,0,255,0.35);border-radius:3px;padding:0.5rem 0.85rem;backdrop-filter:blur(16px);transition:all 0.22s;clip-path:polygon(0 0,calc(100% - 8px) 0,100% 8px,100% 100%,0 100%);box-shadow:0 0 24px rgba(189,0,255,0.1);animation:wmpulse 4s ease-in-out infinite;}
@keyframes wmpulse{0%,100%{box-shadow:0 0 24px rgba(189,0,255,0.1);}50%{box-shadow:0 0 36px rgba(189,0,255,0.22),0 0 60px rgba(189,0,255,0.06);}}
#watermark::before{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,var(--purple),transparent);}
#watermark:hover{border-color:rgba(189,0,255,0.6);background:rgba(189,0,255,0.07);box-shadow:0 0 40px rgba(189,0,255,0.28);transform:translateY(-2px);}
.wm-avatar{width:30px;height:30px;border-radius:50%;background:linear-gradient(135deg,var(--purple),var(--pink));display:flex;align-items:center;justify-content:center;font-size:0.85rem;font-weight:700;color:#fff;font-family:'Orbitron',monospace;flex-shrink:0;box-shadow:0 0 12px rgba(189,0,255,0.45);}
.wm-info{display:flex;flex-direction:column;gap:1px;}
.wm-name{font-family:'Orbitron',monospace;font-size:0.64rem;font-weight:700;color:var(--text);letter-spacing:0.05em;}
.wm-handle{font-family:'Share Tech Mono',monospace;font-size:0.56rem;color:var(--purple);text-shadow:0 0 6px rgba(189,0,255,0.5);letter-spacing:0.03em;}

/* RESPONSIVE */
@media(max-width:820px){.layout{grid-template-columns:1fr;}nav.sidebar{display:none;}main{padding:1.5rem 1rem;}.options-grid{grid-template-columns:1fr;}.result-stats{grid-template-columns:repeat(2,1fr);}.result-score-big{font-size:2.8rem;}}

@keyframes glitch{0%{text-shadow:0 0 20px var(--cyan);}20%{text-shadow:-2px 0 var(--pink),2px 0 var(--cyan);}40%{text-shadow:2px 0 var(--purple),-2px 0 var(--pink);}60%{text-shadow:0 0 20px var(--cyan);}80%{text-shadow:-2px 0 var(--green),2px 0 var(--cyan);}100%{text-shadow:0 0 20px var(--cyan),0 0 40px rgba(0,229,255,0.3);}}
.logo:hover{animation:glitch 0.5s;}

/* Ripple */
@keyframes rip{to{transform:scale(80);opacity:0;}}

/* Answered correct no-glow variant */
.answered-correct-done{border-color:var(--green)!important;color:var(--green)!important;background:rgba(0,255,157,0.07)!important;}
</style>
</head>
<body>
<canvas id="stars-canvas"></canvas>
<div class="hc tl"></div><div class="hc tr"></div><div class="hc bl"></div><div class="hc br"></div>
<div id="cursor"></div>
<div id="cursor-trail"></div>

<header>
  <div class="logo">ΦSX<sub>jee</sub></div>
  <div class="hud-tag">MCQ-ARENA</div>
  <div class="progress-wrap">
    <div class="progress-bar-outer"><div class="progress-bar-inner" id="prog-bar"></div></div>
    <div class="progress-text" id="prog-text">0 / 100</div>
  </div>
  <div class="header-right">
    <div class="timer-box" id="timer-display">00:00:00</div>
    <div class="hud-tag">JEE MAIN</div>
  </div>
</header>

<div class="layout" id="quiz-layout">
<nav class="sidebar">
  <div class="nav-section-label">Subject Filter</div>
  <div class="subject-filters">
    <button class="sub-filter-btn" onclick="filterSubject('all',this)">ALL QUESTIONS</button>
    <button class="sub-filter-btn" onclick="filterSubject('Physics',this)">⬡ PHYSICS (1–35)</button>
    <button class="sub-filter-btn" onclick="filterSubject('Chemistry',this)">⬡ CHEMISTRY (36–68)</button>
    <button class="sub-filter-btn" onclick="filterSubject('Mathematics',this)">⬡ MATHEMATICS (69–100)</button>
  </div>
  <div class="nav-section-label">Question Map</div>
  <div class="q-nav-grid" id="q-nav-grid"></div>
  <div class="sidebar-score">
    <div class="score-mini">
      <div class="score-mini-item"><div class="score-mini-val" id="sm-correct" style="color:var(--green)">0</div><div class="score-mini-label">CORRECT</div></div>
      <div class="score-mini-item"><div class="score-mini-val" id="sm-wrong" style="color:var(--pink)">0</div><div class="score-mini-label">WRONG</div></div>
      <div class="score-mini-item"><div class="score-mini-val" id="sm-marks" style="color:var(--gold)">0</div><div class="score-mini-label">MARKS</div></div>
    </div>
  </div>
</nav>

<main id="quiz-main">
  <div class="question-area" id="question-area">
    <div class="q-header">
      <div class="q-num" id="q-num-display">Q — 01</div>
      <div class="q-subject-tag" id="q-subject-tag">PHYSICS</div>
      <div style="margin-left:auto;font-family:'Share Tech Mono',monospace;font-size:0.58rem;color:var(--muted);">MARKING: <span style="color:var(--green)">+4</span> / <span style="color:var(--pink)">-1</span></div>
    </div>
    <div class="q-text" id="q-text"></div>
    <div class="options-grid" id="options-grid"></div>
    <div class="solution-box hidden" id="solution-box">
      <div class="solution-label">SOLUTION DECODED</div>
      <div class="solution-text" id="solution-text"></div>
    </div>
    <div class="action-row">
      <button class="btn btn-prev" onclick="navigate(-1)">◀ PREV</button>
      <button class="btn btn-skip" onclick="skipQuestion()" id="btn-skip">SKIP ▷</button>
      <button class="btn btn-show-sol hidden" onclick="showSolution()" id="btn-show-sol">SHOW SOLUTION</button>
      <button class="btn btn-next" onclick="navigate(1)">NEXT ▶</button>
      <button class="btn btn-submit" onclick="submitQuiz()" style="margin-left:auto">SUBMIT TEST</button>
    </div>
  </div>
</main>
</div>

<!-- RESULT SCREEN -->
<div id="result-screen">
  <div style="max-width:860px;margin:0 auto;position:relative;z-index:2;">
    <div class="result-hero">
      <div class="result-title">MISSION COMPLETE</div>
      <div class="result-score-big" id="res-score">0</div>
      <div class="result-out-of">OUT OF 400 MARKS (JEE MAIN PATTERN)</div>
      <div class="result-grade" id="res-grade"></div>
    </div>
    <div class="result-stats">
      <div class="rs-card" style="--accent-c:var(--green)"><div class="rs-val" id="rs-correct">0</div><div class="rs-label">CORRECT</div></div>
      <div class="rs-card" style="--accent-c:var(--pink)"><div class="rs-val" id="rs-wrong">0</div><div class="rs-label">INCORRECT</div></div>
      <div class="rs-card" style="--accent-c:var(--gold)"><div class="rs-val" id="rs-skipped">0</div><div class="rs-label">SKIPPED</div></div>
      <div class="rs-card" style="--accent-c:var(--cyan)"><div class="rs-val" id="rs-accuracy">0%</div><div class="rs-label">ACCURACY</div></div>
    </div>
    <div class="subject-breakdown">
      <div class="sb-title">Subject-wise Performance</div>
      <div class="sb-row">
        <div class="sb-subject" style="color:var(--gold)">PHYSICS</div>
        <div class="sb-bar-wrap"><div class="sb-bar" id="bar-phy" style="background:var(--gold);width:0%"></div></div>
        <div class="sb-pct" id="pct-phy" style="color:var(--gold)">0%</div>
      </div>
      <div class="sb-row">
        <div class="sb-subject" style="color:var(--green)">CHEMISTRY</div>
        <div class="sb-bar-wrap"><div class="sb-bar" id="bar-chem" style="background:var(--green);width:0%"></div></div>
        <div class="sb-pct" id="pct-chem" style="color:var(--green)">0%</div>
      </div>
      <div class="sb-row">
        <div class="sb-subject" style="color:var(--purple)">MATHEMATICS</div>
        <div class="sb-bar-wrap"><div class="sb-bar" id="bar-math" style="background:var(--purple);width:0%"></div></div>
        <div class="sb-pct" id="pct-math" style="color:var(--purple)">0%</div>
      </div>
    </div>
    <div>
      <div class="sb-title">Question Review Map</div>
      <div class="review-grid" id="review-grid"></div>
    </div>
    <div style="text-align:center;margin-top:2rem;">
      <button class="btn-restart" onclick="restartQuiz()">↺ RESTART TEST</button>
    </div>
  </div>
</div>

<!-- WATERMARK -->
<a id="watermark" href="https://www.instagram.com/rajput_anmolsingh3" target="_blank" rel="noopener noreferrer" title="Visit @rajput_anmolsingh3 on Instagram">
  <div class="wm-avatar">A</div>
  <div class="wm-info">
    <div class="wm-name">ANMOL SINGH</div>
    <div class="wm-handle">@rajput_anmolsingh3</div>
  </div>
  <svg width="15" height="15" viewBox="0 0 24 24" fill="none" style="margin-left:4px;opacity:0.75;" xmlns="http://www.w3.org/2000/svg">
    <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z" fill="#bd00ff"/>
  </svg>
</a>

<script>
const questions=[
{id:1,subject:"Physics",q:"A ball is thrown vertically upward with initial velocity 20 m/s. Time taken to reach maximum height is (g = 10 m/s²):",opts:["1 s","2 s","3 s","4 s"],ans:1,sol:"At maximum height, v = 0. Using v = u − gt → 0 = 20 − 10t → t = 2 s."},
{id:2,subject:"Physics",q:"For a projectile, range is maximum when angle of projection θ equals:",opts:["30°","45°","60°","90°"],ans:1,sol:"Range R = u²sin2θ/g. For maximum R, sin2θ = 1 → 2θ = 90° → θ = 45°."},
{id:3,subject:"Physics",q:"A body of mass 2 kg moves with velocity 3 m/s. Its kinetic energy is:",opts:["3 J","6 J","9 J","18 J"],ans:2,sol:"KE = ½mv² = ½ × 2 × 9 = 9 J."},
{id:4,subject:"Physics",q:"Escape velocity from Earth's surface is (g = 10 m/s², R = 6.4 × 10⁶ m):",opts:["7.9 km/s","11.2 km/s","16 km/s","8.5 km/s"],ans:1,sol:"vₑ = √(2gR) = √(2 × 10 × 6.4×10⁶) ≈ 11.3 km/s ≈ 11.2 km/s."},
{id:5,subject:"Physics",q:"Time period of a simple pendulum of length 1 m (g = π² m/s²) is:",opts:["1 s","2 s","π s","2π s"],ans:1,sol:"T = 2π√(L/g) = 2π√(1/π²) = 2π/π = 2 s."},
{id:6,subject:"Physics",q:"Efficiency of a Carnot engine between 500 K and 300 K is:",opts:["30%","40%","50%","60%"],ans:1,sol:"η = 1 − TC/TH = 1 − 300/500 = 0.40 = 40%."},
{id:7,subject:"Physics",q:"Moment of inertia of a solid sphere about its diameter is:",opts:["MR²/2","2MR²/5","2MR²/3","MR²/3"],ans:1,sol:"Standard result: I = (2/5)MR² for solid sphere about any diameter axis."},
{id:8,subject:"Physics",q:"Energy stored in capacitor C charged to potential V is:",opts:["CV","CV²/2","C²V","2CV²"],ans:1,sol:"U = ½CV² (also = Q²/2C = QV/2). Three equivalent forms."},
{id:9,subject:"Physics",q:"A wire of resistance R is stretched to double its length. New resistance is:",opts:["R/2","2R","4R","8R"],ans:2,sol:"Volume = AL = const. L → 2L means A → A/2. R = ρL/A → ρ(2L)/(A/2) = 4R."},
{id:10,subject:"Physics",q:"Half-life of a radioactive substance is 20 years. Fraction remaining after 60 years:",opts:["1/4","1/6","1/8","1/16"],ans:2,sol:"n = 60/20 = 3 half-lives. Fraction = (1/2)³ = 1/8."},
{id:11,subject:"Physics",q:"In photoelectric effect, the stopping potential depends on:",opts:["Intensity of light","Frequency of light","Area of metal plate","Work function only"],ans:1,sol:"eV₀ = hf − φ. Stopping potential V₀ depends on frequency f, not intensity."},
{id:12,subject:"Physics",q:"Energy of electron in nth orbit of hydrogen atom is:",opts:["−13.6n eV","−13.6/n eV","−13.6/n² eV","−13.6n² eV"],ans:2,sol:"Eₙ = −13.6Z²/n² eV. For H (Z=1): Eₙ = −13.6/n² eV."},
{id:13,subject:"Physics",q:"Speed of sound in an ideal gas is proportional to:",opts:["T","T²","√T","1/√T"],ans:2,sol:"v = √(γRT/M). Since γ, R, M are constants → v ∝ √T."},
{id:14,subject:"Physics",q:"In YDSE, fringe width β = λD/d. If D is doubled, fringe width:",opts:["Remains same","Doubles","Halves","Quadruples"],ans:1,sol:"β = λD/d. D → 2D → β → 2β. Fringe width doubles."},
{id:15,subject:"Physics",q:"Magnetic force on a stationary charge in a magnetic field is:",opts:["qvB","qvB sinθ","Zero","qB"],ans:2,sol:"F = q(v × B). v = 0 → F = 0. Magnetic force only acts on moving charges."},
{id:16,subject:"Physics",q:"Velocity of the contact point of a body rolling without slipping on a surface is:",opts:["v_cm","2v_cm","Zero","ωR"],ans:2,sol:"For rolling: v_cm = ωR. Contact point velocity = v_cm − ωR = 0 (instantaneously at rest)."},
{id:17,subject:"Physics",q:"Dimension of Planck's constant h is same as:",opts:["Energy","Linear momentum","Angular momentum","Power"],ans:2,sol:"h = E/f → [ML²T⁻²]/[T⁻¹] = [ML²T⁻¹]. Angular momentum L = Iω = [ML²T⁻¹]. Same."},
{id:18,subject:"Physics",q:"For an adiabatic process with ideal gas, which relation holds?",opts:["PV = const","TV = const","PV^γ = const","P/V = const"],ans:2,sol:"Adiabatic process: PV^γ = constant, where γ = Cₚ/Cᵥ."},
{id:19,subject:"Physics",q:"Acceleration of a block on a frictionless inclined plane at angle θ is:",opts:["g","g cosθ","g sinθ","g tanθ"],ans:2,sol:"Net force along incline = mg sinθ → a = g sinθ."},
{id:20,subject:"Physics",q:"Two charges q each at distance r exert force F. If distance doubles and each charge doubles, new force is:",opts:["F","2F","F/2","4F"],ans:0,sol:"F' = k(2q)²/(2r)² = 4kq²/4r² = kq²/r² = F. Force remains unchanged."},
{id:21,subject:"Physics",q:"Angular momentum of a satellite in circular orbit is proportional to:",opts:["r","r²","√r","1/r"],ans:2,sol:"L = mvr, v = √(GM/r). L = m√(GM/r)·r = m√(GMr) ∝ √r."},
{id:22,subject:"Physics",q:"Natural frequency of oscillation in an LC circuit is:",opts:["1/(LC)","1/√(LC)","√(LC)","1/(2π√(LC))"],ans:3,sol:"f₀ = 1/(2π√(LC)). Angular frequency ω = 1/√(LC)."},
{id:23,subject:"Physics",q:"RMS speed of gas molecules at T is v. At temperature 4T it becomes:",opts:["v","2v","4v","v/2"],ans:1,sol:"v_rms ∝ √T. At 4T: v' = √(4T/T) × v = 2v."},
{id:24,subject:"Physics",q:"Critical angle for TIR in a medium of refractive index √2 is:",opts:["30°","45°","60°","90°"],ans:1,sol:"sin θ_c = 1/n = 1/√2 → θ_c = 45°."},
{id:25,subject:"Physics",q:"Power of a convex lens of focal length 25 cm is:",opts:["0.25 D","4 D","25 D","0.04 D"],ans:1,sol:"P = 1/f (in metres) = 1/0.25 = 4 D."},
{id:26,subject:"Physics",q:"For a proton and α-particle accelerated through same potential, ratio λ_p/λ_α is:",opts:["1:1","√2:1","2√2:1","2:1"],ans:2,sol:"λ = h/√(2mqV). λ_p/λ_α = √(m_α q_α/m_p q_p) = √(4×2/1×1) = 2√2."},
{id:27,subject:"Physics",q:"Kirchhoff's Current Law (KCL) is based on conservation of:",opts:["Energy","Charge","Momentum","Mass"],ans:1,sol:"KCL: ΣI_in = ΣI_out at junction. Based on conservation of electric charge."},
{id:28,subject:"Physics",q:"Magnetic field inside a long solenoid of n turns/metre carrying current I is:",opts:["μ₀I/n","μ₀nI","μ₀n²I","μ₀I"],ans:1,sol:"B = μ₀nI inside long solenoid, where n = N/L (turns per metre)."},
{id:29,subject:"Physics",q:"In elastic collision between equal masses (one at rest), after collision:",opts:["Both move with equal speeds","First stops, second moves with initial velocity","Both stop","Both gain same KE"],ans:1,sol:"v₁' = (m₁−m₂)u₁/(m₁+m₂) = 0; v₂' = 2m₁u₁/(m₁+m₂) = u₁. First stops, second moves."},
{id:30,subject:"Physics",q:"Work done by a conservative force around a closed path is:",opts:["Maximum","Positive","Zero","Path-dependent"],ans:2,sol:"Conservative force: ∮F·dr = 0. Work done around any closed loop is zero."},
{id:31,subject:"Physics",q:"Internal energy of an ideal gas in isothermal expansion:",opts:["Increases","Decreases","Remains constant","Becomes zero"],ans:2,sol:"Internal energy of ideal gas depends only on temperature. Isothermal → T = const → ΔU = 0."},
{id:32,subject:"Physics",q:"Electric field inside a uniformly charged conducting sphere is:",opts:["Maximum at centre","Uniform throughout","Zero","Proportional to r"],ans:2,sol:"Free charges reside on the surface. By Gauss's law, E = 0 inside conductor."},
{id:33,subject:"Physics",q:"Doppler formula when source of sound moves toward stationary observer is:",opts:["f' = f(v−v_s)/v","f' = fv/(v−v_s)","f' = f(v+v_s)/v","f' = fv/(v+v_s)"],ans:1,sol:"Source approaches: f' = f × v/(v − v_s). Frequency increases as denominator decreases."},
{id:34,subject:"Physics",q:"Binding energy per nucleon is maximum for:",opts:["Hydrogen (A=1)","Helium (A=4)","Iron (A=56)","Uranium (A=238)"],ans:2,sol:"Iron-56 has highest BE/nucleon ≈ 8.8 MeV. It is the most stable nucleus."},
{id:35,subject:"Physics",q:"Parallel plate capacitor with dielectric κ inserted at constant voltage. Energy stored:",opts:["Decreases by κ","Increases by κ","Remains same","Increases by κ²"],ans:1,sol:"U = ½CV². Inserting dielectric: C → κC. At constant V: U → κU. Energy increases by κ."},
{id:36,subject:"Chemistry",q:"Which of the following has the highest electronegativity?",opts:["Oxygen","Nitrogen","Fluorine","Chlorine"],ans:2,sol:"Fluorine has highest electronegativity (3.98 on Pauling scale) among all elements."},
{id:37,subject:"Chemistry",q:"Hybridisation of carbon in benzene (C₆H₆) is:",opts:["sp","sp²","sp³","sp³d"],ans:1,sol:"Each C in benzene forms 3 σ-bonds (2 C-C + 1 C-H) and participates in π-system → sp²."},
{id:38,subject:"Chemistry",q:"The pH of 0.01 M HCl solution is:",opts:["1","2","3","0.01"],ans:1,sol:"HCl fully dissociates → [H⁺] = 0.01 = 10⁻². pH = −log(10⁻²) = 2."},
{id:39,subject:"Chemistry",q:"Which of the following is a Lewis acid?",opts:["NH₃","H₂O","BF₃","NaOH"],ans:2,sol:"BF₃ has empty p-orbital on B (electron deficient) → electron pair acceptor → Lewis acid."},
{id:40,subject:"Chemistry",q:"IUPAC name of CH₃CH₂OH is:",opts:["Methanol","Ethanol","Propanol","Ethanone"],ans:1,sol:"CH₃CH₂OH has 2 carbons with −OH group → Ethanol (ethan-1-ol)."},
{id:41,subject:"Chemistry",q:"Which quantum number determines the shape of an orbital?",opts:["Principal (n)","Azimuthal (l)","Magnetic (m)","Spin (s)"],ans:1,sol:"Azimuthal quantum number l: l=0 (s-spherical), l=1 (p-dumbbell), l=2 (d), l=3 (f)."},
{id:42,subject:"Chemistry",q:"Number of σ and π bonds in ethyne (H−C≡C−H) are:",opts:["3σ, 1π","3σ, 2π","2σ, 2π","2σ, 3π"],ans:1,sol:"C−H bonds: 2σ. C≡C triple bond: 1σ + 2π. Total: 3σ + 2π."},
{id:43,subject:"Chemistry",q:"Which is the strongest oxidising agent among halogens?",opts:["F₂","Cl₂","Br₂","I₂"],ans:0,sol:"Oxidising power decreases down group 17. F₂ has highest reduction potential (+2.87 V)."},
{id:44,subject:"Chemistry",q:"Equivalent weight of H₂SO₄ (mol. wt. = 98) is:",opts:["98","49","32.7","24.5"],ans:1,sol:"H₂SO₄ furnishes 2 H⁺. Eq. wt. = Mol. wt./n-factor = 98/2 = 49 g/equiv."},
{id:45,subject:"Chemistry",q:"Dalton's Law states that total pressure of gas mixture equals:",opts:["Product of partial pressures","Sum of partial pressures","Average pressure","Geometric mean"],ans:1,sol:"Dalton's Law of Partial Pressures: P_total = P₁ + P₂ + P₃ + ..."},
{id:46,subject:"Chemistry",q:"Molecular geometry of NH₃ is:",opts:["Trigonal planar","Trigonal pyramidal","Tetrahedral","Linear"],ans:1,sol:"N has 3 bond pairs + 1 lone pair → sp³. Lone pair causes trigonal pyramidal geometry."},
{id:47,subject:"Chemistry",q:"Which compound satisfies Hückel's rule and is aromatic?",opts:["Cyclohexane","Cyclohexene","Benzene","1,3-Cyclobutadiene"],ans:2,sol:"Benzene: planar, cyclic, conjugated with 6π electrons (4n+2, n=1). Fully aromatic."},
{id:48,subject:"Chemistry",q:"Enthalpy change for H₂ + ½O₂ → H₂O is called:",opts:["Enthalpy of fusion","Enthalpy of combustion","Enthalpy of formation","Enthalpy of vaporisation"],ans:2,sol:"Formation of 1 mole of compound from elements in standard states = standard enthalpy of formation (ΔHf°)."},
{id:49,subject:"Chemistry",q:"Which element shows maximum catenation?",opts:["Nitrogen","Oxygen","Carbon","Silicon"],ans:2,sol:"Carbon shows maximum catenation due to strong, stable C−C bonds and versatile bonding."},
{id:50,subject:"Chemistry",q:"Order of a reaction is determined by:",opts:["Stoichiometry","Experiment","Balanced equation","Molar mass of reactants"],ans:1,sol:"Reaction order is determined experimentally, NOT from stoichiometric coefficients."},
{id:51,subject:"Chemistry",q:"Oxidation state of Mn in KMnO₄ is:",opts:["+5","+6","+7","+4"],ans:2,sol:"K(+1) + Mn + 4O(−2) = 0 → 1 + Mn − 8 = 0 → Mn = +7."},
{id:52,subject:"Chemistry",q:"[Co(NH₃)₅Cl]SO₄ and [Co(NH₃)₅SO₄]Cl show which type of isomerism?",opts:["Linkage","Ionisation","Coordination","Geometrical"],ans:1,sol:"They differ in which ion is inside the coordination sphere → ionisation isomerism."},
{id:53,subject:"Chemistry",q:"Major product of addition of HBr to propene (CH₃−CH=CH₂) is:",opts:["1-bromopropane","2-bromopropane","1,2-dibromopropane","Allyl bromide"],ans:1,sol:"Markovnikov's rule: H adds to terminal C (more H), Br to middle C → 2-bromopropane."},
{id:54,subject:"Chemistry",q:"Which of the following is a reducing sugar?",opts:["Sucrose","Glucose","Starch","Cellulose"],ans:1,sol:"Glucose has free −CHO group → reduces Fehling's and Tollens' reagent → reducing sugar."},
{id:55,subject:"Chemistry",q:"Van't Hoff factor (i) for K₂SO₄ in dilute aqueous solution is:",opts:["1","2","3","4"],ans:2,sol:"K₂SO₄ → 2K⁺ + SO₄²⁻ (3 ions). van't Hoff factor i = 3."},
{id:56,subject:"Chemistry",q:"Shape of XeF₄ molecule is:",opts:["Tetrahedral","Square planar","See-saw","Octahedral"],ans:1,sol:"Xe: 4 bond pairs + 2 lone pairs. Octahedral e⁻ geometry, 2 axial lone pairs → square planar."},
{id:57,subject:"Chemistry",q:"Catalyst used in Haber's process for manufacture of ammonia is:",opts:["Platinum","Iron with promoters","Nickel","V₂O₅"],ans:1,sol:"Haber's: N₂ + 3H₂ ⇌ 2NH₃. Catalyst = finely divided Fe with Al₂O₃ (K₂O as promoter)."},
{id:58,subject:"Chemistry",q:"Which of the following is NOT a colligative property?",opts:["Osmotic pressure","Boiling point elevation","Optical rotation","Vapour pressure lowering"],ans:2,sol:"Optical rotation depends on the nature (structure) of the solute, not just particle count → not colligative."},
{id:59,subject:"Chemistry",q:"Acid + Base → Salt + Water is called:",opts:["Oxidation","Neutralisation","Hydrolysis","Saponification"],ans:1,sol:"Neutralisation reaction: e.g. HCl + NaOH → NaCl + H₂O."},
{id:60,subject:"Chemistry",q:"Electronic configuration of Fe³⁺ (atomic no. of Fe = 26) is:",opts:["[Ar]3d⁵4s²","[Ar]3d⁵","[Ar]3d⁶","[Ar]3d⁴4s¹"],ans:1,sol:"Fe: [Ar]3d⁶4s². Fe³⁺ loses 4s² first, then 1 from 3d → [Ar]3d⁵ (half-filled, stable)."},
{id:61,subject:"Chemistry",q:"For a spontaneous process, Gibbs free energy change ΔG is:",opts:["ΔG > 0","ΔG = 0","ΔG < 0","ΔG = ΔH"],ans:2,sol:"Spontaneous: ΔG < 0. At equilibrium: ΔG = 0. Non-spontaneous: ΔG > 0."},
{id:62,subject:"Chemistry",q:"Castner-Kellner process is used to manufacture:",opts:["Sodium metal","Chlorine gas","Caustic soda (NaOH)","Bleaching powder"],ans:2,sol:"Castner-Kellner: electrolysis of brine → NaOH (caustic soda), Cl₂, H₂."},
{id:63,subject:"Chemistry",q:"Which molecule has sp³ hybridisation?",opts:["BeCl₂","BF₃","CH₄","C₂H₂"],ans:2,sol:"CH₄: C has 4 bond pairs, no lone pair → sp³, tetrahedral geometry (109.5°)."},
{id:64,subject:"Chemistry",q:"During electrolysis of water, gas collected at cathode is:",opts:["Oxygen","Hydrogen","Ozone","Steam"],ans:1,sol:"Cathode (reduction): 2H⁺ + 2e⁻ → H₂. Hydrogen gas is released at cathode."},
{id:65,subject:"Chemistry",q:"SN2 reaction causes which stereochemical change?",opts:["Racemisation","Retention of configuration","Inversion of configuration","No change"],ans:2,sol:"SN2 proceeds via backside attack → Walden inversion → complete inversion at chiral centre."},
{id:66,subject:"Chemistry",q:"Nylon-6,6 is formed by condensation polymerisation of:",opts:["Adipic acid + Hexamethylenediamine","Caprolactam alone","Glycol + Terephthalic acid","Phenol + Formaldehyde"],ans:0,sol:"Nylon-6,6: adipic acid (6C diacid) + hexamethylenediamine (6C diamine) → condensation polymer."},
{id:67,subject:"Chemistry",q:"Gas produced when excess NH₃ reacts with Cl₂ is:",opts:["NCl₃","N₂","HCl","NH₄Cl"],ans:1,sol:"8NH₃ + 3Cl₂ → N₂ + 6NH₄Cl. Excess NH₃ produces nitrogen gas N₂."},
{id:68,subject:"Chemistry",q:"Unit of rate constant for a first-order reaction is:",opts:["mol L⁻¹ s⁻¹","s⁻¹","L mol⁻¹ s⁻¹","L² mol⁻² s⁻¹"],ans:1,sol:"First-order: rate = k[A]. k = rate/[A] = (mol L⁻¹ s⁻¹)/(mol L⁻¹) = s⁻¹."},
{id:69,subject:"Mathematics",q:"If f(x) = x² + 2x + 1, then f'(x) is:",opts:["2x","2x + 1","2x + 2","x + 2"],ans:2,sol:"f'(x) = d/dx(x²) + d/dx(2x) + d/dx(1) = 2x + 2 + 0 = 2x + 2."},
{id:70,subject:"Mathematics",q:"∫₀¹ x² dx equals:",opts:["1/2","1/3","1/4","2/3"],ans:1,sol:"∫₀¹ x² dx = [x³/3]₀¹ = 1/3 − 0 = 1/3."},
{id:71,subject:"Mathematics",q:"If |z| = 2 and arg(z) = π/3, then z equals:",opts:["1 + i√3","√3 + i","2 + 2i","1 − i√3"],ans:0,sol:"z = 2(cos60° + i sin60°) = 2(½ + i√3/2) = 1 + i√3."},
{id:72,subject:"Mathematics",q:"Sum of the series 1 + 2 + 3 + … + n is:",opts:["n(n+1)","n(n+1)/2","n(n−1)/2","n²"],ans:1,sol:"Sum of first n natural numbers = n(n+1)/2 (AP with a=1, d=1)."},
{id:73,subject:"Mathematics",q:"Determinant of matrix A = [[2,3],[1,4]] is:",opts:["5","7","8","11"],ans:0,sol:"det(A) = 2×4 − 3×1 = 8 − 3 = 5."},
{id:74,subject:"Mathematics",q:"Distance between points (1, 2) and (4, 6) is:",opts:["5","6","7","√5"],ans:0,sol:"d = √[(4−1)² + (6−2)²] = √[9+16] = √25 = 5."},
{id:75,subject:"Mathematics",q:"General solution of dy/dx = y is:",opts:["y = Ce^x","y = Ce^(−x)","y = Cx","y = C + e^x"],ans:0,sol:"dy/y = dx → ln|y| = x + C₁ → y = Ce^x (C = e^C₁). Verified by substitution."},
{id:76,subject:"Mathematics",q:"The value of lim(x→0) (sin x)/x is:",opts:["0","∞","1","π"],ans:2,sol:"Standard fundamental limit: lim(x→0) (sinx)/x = 1. Proved by squeeze theorem."},
{id:77,subject:"Mathematics",q:"Number of ways 5 different books can be arranged on a shelf:",opts:["25","60","120","100"],ans:2,sol:"5! = 5 × 4 × 3 × 2 × 1 = 120 permutations."},
{id:78,subject:"Mathematics",q:"If tanθ = 3/4 and θ is in first quadrant, then sinθ equals:",opts:["3/5","4/5","3/4","4/3"],ans:0,sol:"tanθ = 3/4 → opposite=3, adjacent=4, hypotenuse=√(9+16)=5. sinθ = 3/5."},
{id:79,subject:"Mathematics",q:"Equation of circle with centre (0,0) and radius 5 is:",opts:["x² + y² = 5","x² + y² = 25","x + y = 5","(x+5)² + y² = 25"],ans:1,sol:"Standard: (x−h)² + (y−k)² = r². Centre (0,0), r=5 → x² + y² = 25."},
{id:80,subject:"Mathematics",q:"Which of the following is NOT an even function?",opts:["f(x) = x²","f(x) = cosx","f(x) = |x|","f(x) = x³"],ans:3,sol:"f(x) = x³: f(−x) = −x³ = −f(x) → odd function, not even."},
{id:81,subject:"Mathematics",q:"Value of ⁸C₃ is:",opts:["56","48","28","84"],ans:0,sol:"⁸C₃ = 8!/(3!·5!) = (8×7×6)/(3×2×1) = 336/6 = 56."},
{id:82,subject:"Mathematics",q:"Eccentricity of ellipse x²/16 + y²/9 = 1 is:",opts:["√7/4","3/4","√7/3","4/3"],ans:0,sol:"a²=16, b²=9. c² = a²−b² = 7. e = c/a = √7/4."},
{id:83,subject:"Mathematics",q:"If A and B are mutually exclusive events, P(A∪B) equals:",opts:["P(A)·P(B)","P(A)+P(B)","P(A)+P(B)−P(A∩B)","0"],ans:1,sol:"Mutually exclusive: P(A∩B) = 0. ∴ P(A∪B) = P(A) + P(B)."},
{id:84,subject:"Mathematics",q:"Derivative of sin(x²) with respect to x is:",opts:["cos(x²)","2x cos(x²)","2cos(x²)","x cos(x²)"],ans:1,sol:"Chain rule: d/dx[sin(x²)] = cos(x²) × d/dx(x²) = 2x cos(x²)."},
{id:85,subject:"Mathematics",q:"Sum of infinite GP: first term a, common ratio r (|r| < 1):",opts:["a/(1−r)","a/(r−1)","ar/(1−r)","a·r"],ans:0,sol:"S∞ = a/(1−r). Derived from Sₙ = a(1−rⁿ)/(1−r) as n→∞ and |r|<1 → rⁿ→0."},
{id:86,subject:"Mathematics",q:"Angle between vectors a = î + ĵ and b = î − ĵ is:",opts:["0°","45°","90°","180°"],ans:2,sol:"a·b = (1)(1) + (1)(−1) = 0 → vectors are perpendicular → angle = 90°."},
{id:87,subject:"Mathematics",q:"Number of real roots of x² + x + 1 = 0 is:",opts:["0","1","2","Infinite"],ans:0,sol:"D = b²−4ac = 1−4 = −3 < 0. No real roots; roots are complex conjugates."},
{id:88,subject:"Mathematics",q:"Value of log₂(32) is:",opts:["4","5","6","3"],ans:1,sol:"32 = 2⁵. So log₂(32) = log₂(2⁵) = 5."},
{id:89,subject:"Mathematics",q:"Area of triangle with vertices (0,0), (3,0), (0,4) is:",opts:["6","7","12","3.5"],ans:0,sol:"Area = ½ × base × height = ½ × 3 × 4 = 6 sq. units."},
{id:90,subject:"Mathematics",q:"Correct expansion of (a + b)³ is:",opts:["a³ + b³","a³ + 3ab + b³","a³ + 3a²b + 3ab² + b³","a³ + 2a²b + 2ab² + b³"],ans:2,sol:"(a+b)³ = a³ + 3a²b + 3ab² + b³. (Binomial theorem, row 3: 1,3,3,1.)"},
{id:91,subject:"Mathematics",q:"For f(x) = x³ − 3x, local minimum occurs at:",opts:["x = −1","x = 0","x = 1","x = −3"],ans:2,sol:"f'(x) = 3x²−3 = 0 → x = ±1. f''(x) = 6x. At x=1: f''(1)=6>0 → local minimum."},
{id:92,subject:"Mathematics",q:"Value of sin30° + cos60° is:",opts:["0","1","√3/2","√2"],ans:1,sol:"sin30° = 1/2, cos60° = 1/2. Sum = 1/2 + 1/2 = 1."},
{id:93,subject:"Mathematics",q:"If mean of 5 observations is 8, their sum is:",opts:["13","40","8","5"],ans:1,sol:"Sum = Mean × n = 8 × 5 = 40."},
{id:94,subject:"Mathematics",q:"Slope of line perpendicular to 2x − 3y + 6 = 0 is:",opts:["2/3","−3/2","3/2","−2/3"],ans:1,sol:"Slope of given line: m = 2/3. Perpendicular slope = −1/m = −3/2."},
{id:95,subject:"Mathematics",q:"∫ eˣ dx equals:",opts:["eˣ + C","e^(x+1) + C","xeˣ + C","eˣ/x + C"],ans:0,sol:"∫eˣ dx = eˣ + C. Exponential function is its own derivative and integral."},
{id:96,subject:"Mathematics",q:"General term in expansion of (x+y)ⁿ is:",opts:["ⁿCᵣ x^(n−r) yʳ","ⁿCᵣ xʳ y^(n−r)","ⁿCₙ xⁿ yʳ","n! xʳ y^(n−r)"],ans:0,sol:"T_{r+1} = ⁿCᵣ × x^(n−r) × yʳ, where r = 0, 1, 2, …, n."},
{id:97,subject:"Mathematics",q:"If A is 3×2 and B is 2×4 matrix, order of AB is:",opts:["2×2","3×4","2×4","3×2"],ans:1,sol:"Matrix multiplication: (m×n)(n×p) = m×p. (3×2)(2×4) = 3×4."},
{id:98,subject:"Mathematics",q:"Principal value of sin⁻¹(√3/2) is:",opts:["π/3","π/6","π/4","2π/3"],ans:0,sol:"sin(π/3) = √3/2. Principal range of sin⁻¹ is [−π/2, π/2]. Answer: π/3."},
{id:99,subject:"Mathematics",q:"Which function is NOT differentiable at x = 0?",opts:["f(x) = x²","f(x) = |x|","f(x) = sinx","f(x) = eˣ"],ans:1,sol:"f(x) = |x|: Left derivative = −1, Right derivative = +1. Not equal → not differentiable at x=0."},
{id:100,subject:"Mathematics",q:"Value of (1 + i)⁴ where i = √(−1) is:",opts:["4","−4","4i","−4i"],ans:1,sol:"(1+i)² = 1+2i+i² = 1+2i−1 = 2i. (1+i)⁴ = (2i)² = 4i² = 4×(−1) = −4."}
];

// STATE
let currentQ=0,userAnswers=Array(100).fill(null),questionState=Array(100).fill('unanswered');
// state: 'unanswered','answered-correct','answered-wrong','skipped'
let timerSec=0,timerInterval=null;
let scoreCorrect=0,scoreWrong=0;

// INIT
function init(){
  buildNavGrid();
  loadQuestion(0);
  startTimer();
}

function buildNavGrid(){
  const grid=document.getElementById('q-nav-grid');
  grid.innerHTML='';
  questions.forEach((q,i)=>{
    const btn=document.createElement('button');
    btn.className='q-nav-btn'+(i===0?' active':'');
    btn.id='nav-'+i;
    btn.textContent=i+1;
    btn.onclick=()=>loadQuestion(i);
    grid.appendChild(btn);
  });
}

function loadQuestion(idx){
  if(idx<0||idx>=100)return;
  currentQ=idx;
  // update nav
  document.querySelectorAll('.q-nav-btn').forEach((b,i)=>{
    b.classList.toggle('active',i===idx);
  });
  // update progress
  const answered=questionState.filter(s=>s!=='unanswered').length;
  document.getElementById('prog-bar').style.width=(answered/100*100)+'%';
  document.getElementById('prog-text').textContent=answered+' / 100';

  const q=questions[idx];
  document.getElementById('q-num-display').textContent='Q — '+String(idx+1).padStart(2,'0');
  const subTag=document.getElementById('q-subject-tag');
  subTag.textContent=q.subject.toUpperCase();
  subTag.className='q-subject-tag '+(q.subject==='Physics'?'phy':q.subject==='Chemistry'?'chem':'math');
  document.getElementById('q-text').textContent=q.q;

  // options
  const grid=document.getElementById('options-grid');
  grid.innerHTML='';
  const labels=['A','B','C','D'];
  q.opts.forEach((opt,i)=>{
    const btn=document.createElement('button');
    btn.className='option-btn';
    btn.innerHTML=`<span class="option-label">${labels[i]}.</span>${opt}`;
    const st=questionState[idx];
    if(st!=='unanswered'&&st!=='skipped'){
      btn.classList.add('locked');
      if(i===q.ans){
        btn.classList.add(st==='answered-correct'?'correct-glow':'correct-glow');
      }
      if(i===userAnswers[idx]&&userAnswers[idx]!==q.ans){
        btn.classList.add('selected-wrong');
      }
    } else {
      btn.onclick=()=>selectAnswer(idx,i,btn);
    }
    grid.appendChild(btn);
  });

  // solution
  const solBox=document.getElementById('solution-box');
  const btnSol=document.getElementById('btn-show-sol');
  const btnSkip=document.getElementById('btn-skip');
  solBox.classList.add('hidden');
  solBox.querySelector('#solution-text').textContent=q.sol;
  const st=questionState[idx];
  if(st==='answered-wrong'||st==='answered-correct'){
    btnSol.classList.remove('hidden');
    btnSkip.style.display='none';
  } else if(st==='skipped'){
    btnSol.classList.add('hidden');
    btnSkip.style.display='';
  } else {
    btnSol.classList.add('hidden');
    btnSkip.style.display='';
  }

  // animate
  const area=document.getElementById('question-area');
  area.style.animation='none';
  void area.offsetWidth;
  area.style.animation='fadeUp 0.35s ease both';

  updateSidebarScore();
}

function selectAnswer(qIdx,optIdx,btn){
  if(questionState[qIdx]!=='unanswered')return;
  const q=questions[qIdx];
  userAnswers[qIdx]=optIdx;
  const isCorrect=(optIdx===q.ans);
  questionState[qIdx]=isCorrect?'answered-correct':'answered-wrong';

  // lock all options
  const allOpts=document.querySelectorAll('.option-btn');
  allOpts.forEach(b=>b.classList.add('locked'));
  // apply styles
  allOpts.forEach((b,i)=>{
    if(i===q.ans) b.classList.add('correct-glow');
    if(i===optIdx&&!isCorrect) b.classList.add('selected-wrong');
  });

  // update nav btn
  const navBtn=document.getElementById('nav-'+qIdx);
  navBtn.classList.remove('active');
  navBtn.classList.add(isCorrect?'answered-correct':'answered-wrong');
  navBtn.classList.add('active');

  // score
  if(isCorrect) scoreCorrect++; else scoreWrong++;
  updateSidebarScore();

  // show solution button
  document.getElementById('btn-show-sol').classList.remove('hidden');
  document.getElementById('btn-skip').style.display='none';

  // update progress
  const answered=questionState.filter(s=>s!=='unanswered').length;
  document.getElementById('prog-bar').style.width=(answered/100*100)+'%';
  document.getElementById('prog-text').textContent=answered+' / 100';
}

function showSolution(){
  document.getElementById('solution-box').classList.remove('hidden');
}

function skipQuestion(){
  if(questionState[currentQ]==='unanswered'){
    questionState[currentQ]='skipped';
    const navBtn=document.getElementById('nav-'+currentQ);
    navBtn.classList.add('skipped');
    const answered=questionState.filter(s=>s!=='unanswered').length;
    document.getElementById('prog-bar').style.width=(answered/100*100)+'%';
    document.getElementById('prog-text').textContent=answered+' / 100';
    updateSidebarScore();
  }
  navigate(1);
}

function navigate(dir){
  let next=currentQ+dir;
  if(next<0)next=0;
  if(next>=100)next=99;
  loadQuestion(next);
}

function updateSidebarScore(){
  const marks=scoreCorrect*4 - scoreWrong*1;
  document.getElementById('sm-correct').textContent=scoreCorrect;
  document.getElementById('sm-wrong').textContent=scoreWrong;
  document.getElementById('sm-marks').textContent=marks;
}

function filterSubject(sub,el){
  document.querySelectorAll('.sub-filter-btn').forEach(b=>b.classList.remove('active-phy','active-chem','active-math'));
  if(sub==='Physics') el.classList.add('active-phy');
  else if(sub==='Chemistry') el.classList.add('active-chem');
  else if(sub==='Mathematics') el.classList.add('active-math');
  // navigate to first of that subject
  if(sub==='all'){loadQuestion(0);return;}
  const idx=questions.findIndex(q=>q.subject===sub);
  if(idx>=0)loadQuestion(idx);
}

// TIMER
function startTimer(){
  timerInterval=setInterval(()=>{
    timerSec++;
    const h=Math.floor(timerSec/3600).toString().padStart(2,'0');
    const m=Math.floor((timerSec%3600)/60).toString().padStart(2,'0');
    const s=(timerSec%60).toString().padStart(2,'0');
    document.getElementById('timer-display').textContent=h+':'+m+':'+s;
  },1000);
}

// SUBMIT
function submitQuiz(){
  if(!confirm('Submit the test? Unanswered questions will be marked as skipped.'))return;
  clearInterval(timerInterval);
  questions.forEach((q,i)=>{if(questionState[i]==='unanswered'){questionState[i]='skipped';}});
  showResults();
}

function showResults(){
  document.getElementById('quiz-layout').style.display='none';
  const rs=document.getElementById('result-screen');
  rs.style.display='block';

  const marks=scoreCorrect*4 - scoreWrong*1;
  const skipped=questionState.filter(s=>s==='skipped').length;
  const attempted=scoreCorrect+scoreWrong;
  const accuracy=attempted>0?Math.round(scoreCorrect/attempted*100):0;

  document.getElementById('res-score').textContent=marks<0?0:marks;
  document.getElementById('rs-correct').textContent=scoreCorrect;
  document.getElementById('rs-wrong').textContent=scoreWrong;
  document.getElementById('rs-skipped').textContent=skipped;
  document.getElementById('rs-accuracy').textContent=accuracy+'%';

  // grade
  const pct=marks/400*100;
  let grade,gradeColor;
  if(pct>=90){grade='S — LEGENDARY';gradeColor='var(--cyan)';}
  else if(pct>=75){grade='A — EXCELLENT';gradeColor='var(--green)';}
  else if(pct>=60){grade='B — GOOD';gradeColor='var(--gold)';}
  else if(pct>=45){grade='C — AVERAGE';gradeColor='var(--orange)';}
  else{grade='D — KEEP TRAINING';gradeColor='var(--pink)';}
  const gradeEl=document.getElementById('res-grade');
  gradeEl.textContent=grade;gradeEl.style.color=gradeColor;

  // subject breakdown
  ['Physics','Chemistry','Mathematics'].forEach(sub=>{
    const qs=questions.filter(q=>q.subject===sub);
    const correct=qs.filter((q,i)=>{
      const idx=questions.indexOf(q);
      return questionState[idx]==='answered-correct';
    }).length;
    const total=qs.length;
    const p=Math.round(correct/total*100);
    const id=sub==='Mathematics'?'math':sub.toLowerCase().slice(0,4);
    const barId='bar-'+id,pctId='pct-'+id;
    setTimeout(()=>{
      const bar=document.getElementById(barId);
      const pctEl=document.getElementById(pctId);
      if(bar)bar.style.width=p+'%';
      if(pctEl)pctEl.textContent=correct+'/'+total+' ('+p+'%)';
    },300);
  });

  // review grid
  const rg=document.getElementById('review-grid');
  rg.innerHTML='';
  questionState.forEach((st,i)=>{
    const pill=document.createElement('div');
    pill.className='review-pill '+(st==='answered-correct'?'correct':st==='answered-wrong'?'wrong':'skipped');
    pill.title='Q'+(i+1)+' '+st;
    pill.textContent='Q'+(i+1);
    rg.appendChild(pill);
  });

  setTimeout(()=>{rs.scrollTo({top:0,behavior:'smooth'});window.scrollTo({top:0,behavior:'smooth'});},100);
}

function restartQuiz(){
  currentQ=0;userAnswers=Array(100).fill(null);questionState=Array(100).fill('unanswered');
  scoreCorrect=0;scoreWrong=0;timerSec=0;
  document.getElementById('quiz-layout').style.display='grid';
  document.getElementById('result-screen').style.display='none';
  buildNavGrid();loadQuestion(0);
  clearInterval(timerInterval);startTimer();
  document.getElementById('prog-bar').style.width='0%';
  document.getElementById('prog-text').textContent='0 / 100';
  updateSidebarScore();
}

// STARS CANVAS
const canvas=document.getElementById('stars-canvas');
const ctx=canvas.getContext('2d');
let W,H,pts=[];
function resize(){W=canvas.width=window.innerWidth;H=canvas.height=window.innerHeight;}
resize();window.addEventListener('resize',()=>{resize();initPts();});
function initPts(){pts=[];const n=Math.floor(W*H/12000);for(let i=0;i<n;i++)pts.push({x:Math.random()*W,y:Math.random()*H,vx:(Math.random()-.5)*.18,vy:(Math.random()-.5)*.18,r:Math.random()*1.3+.3,a:Math.random()*.5+.1,c:['#00e5ff','#bd00ff','#ff2d78','#00ff9d','#ffd700'][Math.floor(Math.random()*5)]});}
initPts();
function drawStars(){ctx.clearRect(0,0,W,H);for(let i=0;i<pts.length;i++){for(let j=i+1;j<pts.length;j++){const dx=pts[i].x-pts[j].x,dy=pts[i].y-pts[j].y,d=Math.sqrt(dx*dx+dy*dy);if(d<90){ctx.beginPath();ctx.moveTo(pts[i].x,pts[i].y);ctx.lineTo(pts[j].x,pts[j].y);ctx.strokeStyle=`rgba(0,229,255,${.06*(1-d/90)})`;ctx.lineWidth=.4;ctx.stroke();}}const p=pts[i];ctx.beginPath();ctx.arc(p.x,p.y,p.r,0,Math.PI*2);ctx.fillStyle=p.c;ctx.globalAlpha=p.a;ctx.fill();ctx.globalAlpha=1;p.x+=p.vx;p.y+=p.vy;if(p.x<0||p.x>W)p.vx*=-1;if(p.y<0||p.y>H)p.vy*=-1;}requestAnimationFrame(drawStars);}
drawStars();

// CURSOR
const cursor=document.getElementById('cursor'),trail=document.getElementById('cursor-trail');
let mx=0,my=0,tx=0,ty=0;
document.addEventListener('mousemove',e=>{mx=e.clientX;my=e.clientY;cursor.style.transform=`translate(${mx-6}px,${my-6}px)`;});
(function anim(){tx+=(mx-tx)*.1;ty+=(my-ty)*.1;trail.style.transform=`translate(${tx-16}px,${ty-16}px)`;requestAnimationFrame(anim);})();
document.addEventListener('mouseover',e=>{if(e.target.matches('button,a,.option-btn,.q-nav-btn')){cursor.style.transform+=` scale(1.8)`;cursor.style.borderColor='#ff2d78';}});
document.addEventListener('mouseout',e=>{if(e.target.matches('button,a,.option-btn,.q-nav-btn')){cursor.style.borderColor='#00e5ff';}});

// RIPPLE on option click
document.addEventListener('click',function(e){
  const card=e.target.closest('.option-btn,.btn,.btn-restart');
  if(!card)return;
  const r=document.createElement('div');
  const rect=card.getBoundingClientRect();
  r.style.cssText=`position:fixed;width:4px;height:4px;background:#00e5ff;border-radius:50%;transform:scale(0);animation:rip .5s ease-out forwards;left:${e.clientX}px;top:${e.clientY}px;pointer-events:none;opacity:.3;z-index:9999;`;
  document.body.appendChild(r);
  setTimeout(()=>r.remove(),500);
});
const rs2=document.createElement('style');rs2.textContent='@keyframes rip{to{transform:scale(60);opacity:0;}}';document.head.appendChild(rs2);

// START
init();
</script>
</body>
</html>
