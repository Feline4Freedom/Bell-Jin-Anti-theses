# Bell-Jin-Anti-theses[governance_wheel.html](https://github.com/user-attachments/files/25766276/governance_wheel.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Governance Dilemmas — Bell & Jin</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,400&family=Source+Serif+4:ital,wght@0,300;0,400;0,600;1,300;1,400&display=swap" rel="stylesheet">
<style>
/* ── PASTE YOUR GOOGLE APPS SCRIPT URL BELOW ── */
/* See setup_guide.md for instructions           */

:root {
  --ink:    #110D08;
  --paper:  #F4EDD8;
  --cream:  #FAF5E8;
  --gold:   #B8860B;
  --gold2:  #D4A520;
  --terra:  #C4622D;
  --terra2: #E07845;
  --teal:   #1A6B60;
  --teal2:  #2A9080;
  --red:    #8B1A1A;
  --mid:    #4A3020;
  --fade:   #9E8B72;
  --dark:   #1A1008;
  --card:   #2A1C0C;
}
*{margin:0;padding:0;box-sizing:border-box;}
body {
  background: var(--dark);
  font-family: 'Source Serif 4', Georgia, serif;
  color: var(--paper);
  min-height: 100vh;
  overflow-x: hidden;
  background-image:
    radial-gradient(ellipse at 20% 50%, rgba(196,98,45,0.06) 0%, transparent 50%),
    radial-gradient(ellipse at 80% 20%, rgba(26,107,96,0.06) 0%, transparent 50%);
}

/* ── REGISTRATION OVERLAY ── */
#reg-overlay {
  position: fixed; inset: 0; z-index: 200;
  background: rgba(10,6,2,0.97);
  display: flex; align-items: center; justify-content: center;
  padding: 24px;
}
.reg-card {
  background: var(--dark);
  border: 1px solid rgba(184,134,11,0.4);
  border-top: 4px solid var(--terra);
  max-width: 480px; width: 100%;
  padding: 40px 36px;
  box-shadow: 0 8px 48px rgba(0,0,0,0.7);
  animation: slideUp .4s ease;
}
.reg-eyebrow {
  font-size: 10px; letter-spacing: 3px; color: var(--terra2);
  text-transform: uppercase; margin-bottom: 12px;
}
.reg-title {
  font-family: 'Playfair Display', serif;
  font-size: 24px; font-weight: 900; color: white;
  margin-bottom: 8px;
}
.reg-sub {
  font-size: 13px; color: var(--fade); line-height: 1.6;
  margin-bottom: 28px; font-style: italic;
}
.reg-field { margin-bottom: 16px; }
.reg-label {
  display: block; font-size: 11px; letter-spacing: 1.5px;
  color: var(--fade); text-transform: uppercase; margin-bottom: 6px;
}
.reg-input {
  width: 100%; padding: 11px 14px;
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(158,139,114,0.3);
  color: var(--paper); font-family: 'Source Serif 4', serif;
  font-size: 14px; outline: none;
  transition: border-color .2s;
}
.reg-input:focus { border-color: var(--terra2); }
.reg-input::placeholder { color: rgba(158,139,114,0.5); }
.reg-btn {
  width: 100%; padding: 13px;
  background: linear-gradient(135deg, var(--terra), var(--terra2));
  border: none; color: white;
  font-family: 'Playfair Display', serif;
  font-size: 15px; font-weight: 700; letter-spacing: 2px;
  text-transform: uppercase; cursor: pointer;
  margin-top: 8px; transition: all .25s;
}
.reg-btn:hover { opacity: .9; transform: translateY(-1px); }
.reg-error {
  font-size: 12px; color: #E06060; margin-top: 8px;
  display: none;
}
.reg-error.show { display: block; }

/* ── STUDENT BADGE (top right) ── */
#student-badge {
  position: fixed; top: 12px; right: 16px; z-index: 50;
  background: rgba(42,28,12,0.92);
  border: 1px solid rgba(184,134,11,0.3);
  padding: 6px 14px;
  font-size: 11px; color: var(--fade);
  display: none;
}
#student-badge span { color: var(--gold2); font-weight: 600; }

/* ── HEADER ── */
.site-header {
  text-align: center; padding: 36px 24px 12px; position: relative;
}
.site-header::after {
  content:''; display:block; width:80px; height:2px;
  background: linear-gradient(90deg, transparent, var(--gold), transparent);
  margin: 18px auto 0;
}
.site-title {
  font-family:'Playfair Display', serif;
  font-size: clamp(22px,3vw,32px); font-weight:900;
  letter-spacing:2px; color: var(--paper);
}
.site-subtitle { font-size:13px; color:var(--fade); letter-spacing:1px; margin-top:6px; font-style:italic; }

/* ── PROGRESS ── */
.progress-bar { display:flex; justify-content:center; gap:8px; padding:16px 24px; flex-wrap:wrap; }
.prog-dot {
  width:28px; height:28px; border-radius:50%;
  border:1.5px solid var(--fade);
  display:flex; align-items:center; justify-content:center;
  font-size:11px; color:var(--fade); cursor:pointer;
  transition: all .3s;
  font-family:'Playfair Display',serif; font-weight:700;
}
.prog-dot.done { background:var(--teal); border-color:var(--teal2); color:white; }
.prog-dot.active { background:var(--terra); border-color:var(--terra2); color:white; transform:scale(1.15); }
.prog-label { text-align:center; font-size:11px; color:var(--fade); margin-bottom:4px; letter-spacing:.5px; }

/* ── WHEEL ── */
.wheel-section { display:flex; flex-direction:column; align-items:center; padding:20px 24px 32px; gap:20px; }
.wheel-wrap { position:relative; width:320px; height:320px; }
.wheel-pointer {
  position:absolute; top:-14px; left:50%; transform:translateX(-50%);
  width:0; height:0;
  border-left:12px solid transparent; border-right:12px solid transparent;
  border-top:22px solid var(--gold2); z-index:10;
  filter:drop-shadow(0 2px 4px rgba(0,0,0,.5));
}
canvas#wheel {
  border-radius:50%;
  box-shadow: 0 0 0 3px var(--gold), 0 0 40px rgba(196,98,45,.3), 0 8px 32px rgba(0,0,0,.6);
  cursor:pointer; transition:box-shadow .3s;
}
canvas#wheel:hover { box-shadow: 0 0 0 3px var(--gold2), 0 0 60px rgba(224,120,69,.4), 0 8px 32px rgba(0,0,0,.6); }
.spin-btn {
  padding:12px 40px;
  background:linear-gradient(135deg,var(--terra) 0%,var(--terra2) 100%);
  color:white; border:none;
  font-family:'Playfair Display',serif; font-size:15px; font-weight:700;
  letter-spacing:2px; text-transform:uppercase; cursor:pointer;
  border-radius:2px; box-shadow:0 4px 20px rgba(196,98,45,.4);
  transition:all .25s;
}
.spin-btn:hover:not(:disabled) { transform:translateY(-2px); box-shadow:0 6px 28px rgba(196,98,45,.55); }
.spin-btn:disabled { opacity:.5; cursor:not-allowed; }
.spin-hint { font-size:12px; color:var(--fade); font-style:italic; text-align:center; }

/* ── WORKSHEET OVERLAY ── */
.worksheet-overlay {
  display:none; position:fixed; inset:0;
  background:rgba(10,6,2,.92); z-index:100;
  overflow-y:auto; padding:20px 16px 60px;
  backdrop-filter:blur(4px);
}
.worksheet-overlay.open { display:block; }
.worksheet-card {
  max-width:860px; margin:0 auto;
  background:var(--dark);
  border:1px solid rgba(184,134,11,.3);
  border-top:4px solid var(--terra);
  box-shadow:0 8px 48px rgba(0,0,0,.6);
  animation:slideUp .4s ease;
}
@keyframes slideUp { from{opacity:0;transform:translateY(30px)} to{opacity:1;transform:translateY(0)} }

.ws-header {
  padding:24px 32px 20px;
  background:linear-gradient(135deg,var(--card) 0%,#1E1208 100%);
  border-bottom:1px solid rgba(184,134,11,.2); position:relative;
}
.ws-scenario-num { font-size:11px; letter-spacing:3px; color:var(--terra2); text-transform:uppercase; margin-bottom:6px; }
.ws-title { font-family:'Playfair Display',serif; font-size:clamp(20px,3vw,28px); font-weight:900; color:white; line-height:1.2; }
.ws-subtitle { font-size:13px; color:var(--fade); font-style:italic; margin-top:4px; }
.ws-body { padding:24px 32px; }
.ws-section { margin-bottom:24px; }
.ws-section-head { display:flex; align-items:center; gap:10px; margin-bottom:10px; }
.ws-section-badge {
  padding:4px 12px; font-size:10px; letter-spacing:2px;
  text-transform:uppercase; font-weight:600; border-radius:1px;
  font-family:'Source Serif 4',serif; white-space:nowrap;
}
.badge-context  { background:rgba(158,139,114,.2); color:var(--fade);   border:1px solid rgba(158,139,114,.3); }
.badge-bell     { background:rgba(26,107,96,.2);   color:var(--teal2);  border:1px solid rgba(26,107,96,.4); }
.badge-jin      { background:rgba(196,98,45,.2);   color:var(--terra2); border:1px solid rgba(196,98,45,.4); }
.badge-crack    { background:rgba(139,26,26,.2);   color:#E06060;       border:1px solid rgba(139,26,26,.4); }
.badge-discuss  { background:rgba(184,134,11,.2);  color:var(--gold2);  border:1px solid rgba(184,134,11,.4); }
.badge-response { background:rgba(42,120,168,.2);  color:#70B8E0;       border:1px solid rgba(42,120,168,.4); }

.ws-text { font-size:14.5px; color:rgba(244,237,216,.88); line-height:1.75; }
.ws-text p { margin-bottom:10px; }
.ws-text p:last-child { margin-bottom:0; }
.crack-box { background:rgba(139,26,26,.1); border-left:3px solid #C03030; padding:14px 18px; border-radius:0 2px 2px 0; }
.crack-box .ws-text { color:rgba(244,200,200,.9); }
.discuss-box { background:rgba(184,134,11,.07); border:1px solid rgba(184,134,11,.2); padding:16px 20px; }
.discuss-q { display:flex; gap:12px; margin-bottom:12px; align-items:flex-start; }
.discuss-q:last-child { margin-bottom:0; }
.q-num {
  background:var(--gold); color:var(--dark);
  font-size:11px; font-weight:700; padding:3px 8px;
  flex-shrink:0; margin-top:2px;
  font-family:'Playfair Display',serif;
}
.q-text { font-size:14px; color:rgba(244,237,216,.85); line-height:1.6; }
.ws-divider { height:1px; background:linear-gradient(90deg,transparent,rgba(184,134,11,.2),transparent); margin:20px 0; }

/* ── RESPONSE SECTION ── */
.response-block { margin-top:12px; }
.response-item { margin-bottom:16px; }
.response-q-label {
  font-size:11px; letter-spacing:1.5px; color:#70B8E0;
  text-transform:uppercase; margin-bottom:6px; display:block;
}
.response-textarea {
  width:100%; min-height:100px;
  background:rgba(42,80,120,.1);
  border:1px solid rgba(42,120,168,.25);
  border-left:3px solid rgba(42,120,168,.5);
  color:var(--paper);
  font-family:'Source Serif 4',serif; font-size:13.5px;
  line-height:1.65; padding:12px 14px;
  outline:none; resize:vertical;
  transition:border-color .2s;
}
.response-textarea:focus { border-color:rgba(42,120,168,.7); background:rgba(42,80,120,.15); }
.response-textarea::placeholder { color:rgba(158,139,114,.4); font-style:italic; }
.response-textarea:disabled { opacity:.5; cursor:not-allowed; resize:none; }
.char-count { font-size:10px; color:var(--fade); text-align:right; margin-top:3px; }

.submit-status {
  padding:10px 16px; margin-top:8px;
  font-size:13px; border-radius:1px; display:none;
}
.submit-status.sending { display:block; background:rgba(184,134,11,.1); color:var(--gold2); border:1px solid rgba(184,134,11,.2); }
.submit-status.success { display:block; background:rgba(26,107,96,.15); color:var(--teal2); border:1px solid rgba(26,107,96,.3); }
.submit-status.error   { display:block; background:rgba(139,26,26,.15); color:#E06060; border:1px solid rgba(139,26,26,.3); }

/* ── FOOTER ── */
.ws-footer {
  padding:16px 32px 24px;
  display:flex; justify-content:space-between; align-items:center;
  border-top:1px solid rgba(184,134,11,.15);
  flex-wrap:wrap; gap:12px;
}
.ws-close-btn {
  padding:10px 28px; background:transparent;
  border:1px solid var(--fade); color:var(--fade);
  font-family:'Source Serif 4',serif; font-size:13px;
  cursor:pointer; letter-spacing:1px; transition:all .2s;
}
.ws-close-btn:hover { border-color:var(--paper); color:var(--paper); }
.ws-submit-btn {
  padding:10px 28px;
  background:linear-gradient(135deg,var(--terra),var(--terra2));
  border:none; color:white;
  font-family:'Source Serif 4',serif; font-size:13px;
  cursor:pointer; letter-spacing:1px; transition:all .2s;
}
.ws-submit-btn:hover:not(:disabled) { opacity:.9; transform:translateY(-1px); }
.ws-submit-btn:disabled { background:var(--mid); color:var(--fade); cursor:default; transform:none; }
.ws-submit-btn.done { background:var(--teal); cursor:default; transform:none; }
.ws-nav-btns { display:flex; gap:8px; }
.ws-nav-btn {
  padding:10px 18px;
  background:rgba(184,134,11,.15);
  border:1px solid rgba(184,134,11,.3);
  color:var(--gold2);
  font-family:'Source Serif 4',serif; font-size:12px;
  cursor:pointer; transition:all .2s;
}
.ws-nav-btn:hover { background:rgba(184,134,11,.25); }

/* ── ALL DONE ── */
.all-done { display:none; flex-direction:column; align-items:center; padding:40px 24px; text-align:center; gap:16px; }
.all-done.show { display:flex; }
.all-done-title { font-family:'Playfair Display',serif; font-size:28px; color:var(--gold2); }
.all-done-sub { font-size:14px; color:var(--fade); max-width:480px; line-height:1.7; }

/* ── SCENARIO LIST ── */
.scenario-list { max-width:860px; margin:0 auto; padding:0 24px 48px; display:grid; grid-template-columns:repeat(auto-fill,minmax(240px,1fr)); gap:12px; }
.sc-card { background:var(--card); border:1px solid rgba(158,139,114,.2); border-left:3px solid var(--fade); padding:14px 16px; cursor:pointer; transition:all .25s; }
.sc-card:hover { border-left-color:var(--terra2); background:rgba(42,28,12,.9); transform:translateX(3px); }
.sc-card.done-card { border-left-color:var(--teal2); opacity:.75; }
.sc-card-num { font-size:10px; letter-spacing:2px; color:var(--fade); margin-bottom:4px; }
.sc-card-title { font-family:'Playfair Display',serif; font-size:14px; color:var(--paper); line-height:1.3; }
.sc-card-tag { font-size:10px; color:var(--fade); font-style:italic; margin-top:4px; }
.sc-done-badge { display:none; font-size:10px; color:var(--teal2); letter-spacing:1px; margin-top:4px; }
.sc-card.done-card .sc-done-badge { display:block; }
</style>
</head>
<body>

<!-- REGISTRATION OVERLAY -->
<div id="reg-overlay">
  <div class="reg-card">
    <div class="reg-eyebrow">Governance Dilemmas · Bell &amp; Jin</div>
    <div class="reg-title">Please Register to Begin</div>
    <div class="reg-sub">Your name and email let your instructor track participation. Your responses to each scenario will be saved when you submit.</div>
    <div class="reg-field">
      <label class="reg-label" for="reg-name">Full Name</label>
      <input class="reg-input" id="reg-name" type="text" placeholder="e.g. Chan Tai Man" autocomplete="name" />
    </div>
    <div class="reg-field">
      <label class="reg-label" for="reg-email">Email Address</label>
      <input class="reg-input" id="reg-email" type="email" placeholder="your@email.com" autocomplete="email" />
    </div>
    <button class="reg-btn" onclick="register()">Begin the Exercise →</button>
    <div class="reg-error" id="reg-error">Please enter both your name and a valid email address.</div>
  </div>
</div>

<!-- STUDENT BADGE -->
<div id="student-badge">Logged in as: <span id="badge-name"></span></div>

<header class="site-header">
  <div class="site-title">Governance Dilemmas</div>
  <div class="site-subtitle">Bell · Jin · CCP — Eight Universal Scenarios</div>
</header>

<div class="prog-label">PROGRESS — <span id="done-count">0</span> / 8 submitted</div>
<div class="progress-bar" id="progress-bar"></div>

<div class="wheel-section">
  <div class="wheel-wrap">
    <div class="wheel-pointer"></div>
    <canvas id="wheel" width="320" height="320"></canvas>
  </div>
  <button class="spin-btn" id="spin-btn" onclick="spinWheel()">SPIN</button>
  <div class="spin-hint">Click the wheel or press SPIN — or select any scenario below</div>
</div>

<div class="all-done" id="all-done-msg">
  <div class="all-done-title">All Eight Scenarios Submitted</div>
  <div class="all-done-sub">Your responses have been recorded. The shared silence in both Bell and Jin — the absent mechanism for saying "no" to power — runs through all eight cases. That silence is the course's central question.</div>
</div>

<div class="scenario-list" id="scenario-list"></div>

<!-- WORKSHEET OVERLAY -->
<div class="worksheet-overlay" id="ws-overlay">
  <div class="worksheet-card" id="ws-card">
    <div class="ws-header">
      <div class="ws-scenario-num" id="ws-num"></div>
      <div class="ws-title" id="ws-title"></div>
      <div class="ws-subtitle" id="ws-subtitle"></div>
    </div>
    <div class="ws-body" id="ws-body"></div>
    <div class="ws-footer">
      <div class="ws-nav-btns">
        <button class="ws-nav-btn" onclick="navScenario(-1)">← Prev</button>
        <button class="ws-nav-btn" onclick="navScenario(1)">Next →</button>
      </div>
      <button class="ws-submit-btn" id="ws-submit-btn" onclick="submitScenario()">Submit Responses ↑</button>
      <button class="ws-close-btn" onclick="closeWS()">Close ✕</button>
    </div>
  </div>
</div>

<script>
// ══════════════════════════════════════════════════════
// ⚙️  CONFIGURATION — paste your Apps Script URL here
// ══════════════════════════════════════════════════════
const APPS_SCRIPT_URL = 'PASTE_YOUR_APPS_SCRIPT_URL_HERE';

// ══════════════════════════════════════════════════════
// SCENARIO DATA
// ══════════════════════════════════════════════════════
const SCENARIOS = [
  {
    id:1, short:"Generational\nConflict",
    color1:"#3D2810", color2:"#5C3C18", accent:"#C8970A",
    title:"Generational Conflict",
    subtitle:"Old voters vs. young futures — who does governance serve?",
    tag:"Intergenerational equity · Electoral structure",
    context:`<p>In ageing societies, older voters outnumber younger ones — and they vote at higher rates. Democracies therefore systematically favour pension protection, healthcare subsidies and housing price stability, at the direct expense of young people's housing affordability, climate action and education investment.</p><p>Japan, the UK, and Italy all display this pattern structurally. It is not a failure of individual politicians — it is a <em>designed outcome</em> of majoritarian democracy. The question is whether a non-electoral system does better.</p>`,
    bell:`Bell argues that meritocratic governance is freed from the tyranny of the electoral age structure. A Confucian official selected for competence and long-term vision — not votes — has both the mandate and the incentive to make decisions on behalf of future generations. The three-tier system places the long-range planning function precisely at the top tier, away from the immediate pressures of village-level elections.`,
    jin:`Jin's incentive-structure argument runs parallel: the Mayor Economy rewards officials not for pleasing current retirees, but for GDP growth, industrial clusters, and attracting talent. The tournament-style evaluation system creates a structural bias toward long-term investment in productive capacity — not toward protecting legacy entitlements. Local officials are effectively "equity stakeholders" in their region's future workforce.`,
    crack:`In 2024, China's youth unemployment exceeded 21% — the government stopped publishing the data for several months. The retirement age extension triggered the strongest public backlash of the Xi era. Bell's argument requires us to trust that officials genuinely internalise the interests of those who have no vote and no institutional voice. Jin's argument requires the incentive structure to remain stable — but when growth slows, young people absorb the cost, with no mechanism to contest that allocation. Both models share the same gap: there is no institutional channel through which young people can say "this is wrong."`,
    questions:["Bell says meritocratic officials represent long-term interests better than elected politicians. What evidence would you need to test this claim? What would falsify it?","Jin argues the Mayor Economy incentivises long-term investment. How does the youth unemployment figure interact with this argument? Is it a falsification, or can it be explained away?","Design a minimum accountability mechanism that would allow young people to challenge intergenerational allocation decisions — without using elections. What would it look like in a Chinese context?"]
  },
  {
    id:2, short:"Public Health\nInformation",
    color1:"#0D2E28", color2:"#143D35", accent:"#2AA898",
    title:"Public Health Information",
    subtitle:"Truth vs. stability — who controls what the public knows?",
    tag:"Information suppression · State capacity · Li Wenliang",
    context:`<p>Every government faces the same dilemma at the start of an epidemic: early disclosure risks panic and market disruption; suppression risks delayed response and amplified spread. This is not a uniquely Chinese problem — the US delayed H1N1 reporting in 2009, and multiple European governments mishandled early COVID communications.</p><p>The question is not whether governments suppress information in crises. They all do. The question is what determines when suppression ends and correction begins — and who bears the cost of the gap.</p>`,
    bell:`Bell's steelman: meritocratic governance produces officials capable of making technically sophisticated decisions without the distorting pressure of media panic. Once information is confirmed, a capable state can mobilise at a scale and speed impossible in electoral systems. The extraordinary construction of field hospitals, the city-wide quarantine logistics, the 2020 economic performance (+2.3% GDP, the only major economy to grow) — all vindicate the claim that strong state capacity is a genuine governance advantage.`,
    jin:`Jin's version is structural: the "strong state capacity" that delivered COVID management is exactly what she describes as the governance advantage of the Chinese hybrid. Markets cannot build a 1,000-bed hospital in 72 hours. Democratic legislatures cannot mandate universal QR-code health tracking overnight. The thousand-arm Buddha's visible hands are not a metaphor — they are an operational capability that 2020 demonstrated concretely.`,
    crack:`Dr. Li Wenliang sent his warning on December 30, 2019. He was summoned by police on January 3. The official acknowledgment of human-to-human transmission came on January 20. That 20-day gap — produced by the same suppression mechanism Bell calls "stability management" — cost the world its containment window. Jin's "strong state capacity" argument works perfectly for Phase 2 (response) and goes silent on Phase 1 (suppression). More fundamentally: the policy that sustained three years of Zero-COVID was abandoned in one month in late 2022 — with no policy evaluation, no official accountability, no compensation framework for those who lost businesses and livelihoods. Bell calls this "adaptability." But adaptability without accountability is indistinguishable from the powerful changing their minds.`,
    questions:["Bell's model requires a mechanism for dissenting information to travel upward. The Li Wenliang case is the precise failure of that mechanism. Can Bell's argument survive this case — and if so, how must it be modified?","Jin describes the state's COVID response as evidence of strong state capacity. Is she analysing the same event as Bell, or a different phase of it? Does selecting which phase to analyse change the conclusion?","The Zero-COVID reversal in 2022 happened without explanation. Under what institutional design could that reversal have been handled transparently? What elements of the current system would need to change?"]
  },
  {
    id:3, short:"Minority\nRights",
    color1:"#2A1010", color2:"#3D1818", accent:"#E06060",
    title:"Minority Rights",
    subtitle:"Integration vs. cultural preservation — who defines the nation?",
    tag:"Ethnic minority · Legitimacy · Structural exclusion",
    context:`<p>Every multi-ethnic state faces this tension: minority cultural preservation vs. national coherence. France bans religious symbols in schools. Canada confronts the legacy of indigenous residential schools. The US debates immigration assimilation. There is no universally agreed solution — but the question of <em>how</em> decisions about minorities are made, and <em>who has standing</em> in those decisions, marks the boundary between different models of governance.</p>`,
    bell:`Bell's Confucian framework includes a state responsibility for moral education (教化) — the cultivation of a shared civic culture. In this reading, integration policies are not suppression but the state's fulfilment of its duty to guide society toward civilised order. Short-term cultural friction is the price of long-term social cohesion. The ruler who allows disorder in the name of pluralism has failed his Confucian obligation.`,
    jin:`Jin's book is almost entirely silent on minority rights. She explicitly frames her analysis as economic, separating political arrangements from economic performance. This is not accidental — it is a structural feature of her argument. The silence is the data point.`,
    crack:`Bell's three-tier architecture — village democracy, provincial experimentation, central meritocracy — has no designed space for minority political representation. This is not a technical omission; it is a structural exclusion. Jin's silence is, if anything, more analytically honest — she does not try to rationalise what she cannot explain within her framework. But both models share the same hidden premise: the state has good intentions toward those it governs. When that premise is contested by the governed themselves, both frameworks lose their foundation simultaneously.`,
    questions:["Bell says the Confucian state has a moral duty to educate and civilise. Who gets to define 'civilised'? Is there any version of Bell's argument that could accommodate a minority group's refusal of that definition?","Jin's silence on minority rights is conspicuous. Is it intellectually defensible to analyse economic governance performance while bracketing the political conditions under which that performance occurs? What are the costs of that analytic choice?","Design a governance mechanism within Bell's three-tier framework that would give minority communities institutional voice over policies affecting their cultural practices. Is such a mechanism compatible with Bell's model, or does adding it fundamentally change the model?"]
  },
  {
    id:4, short:"Platform\nMonopoly",
    color1:"#1A1A08", color2:"#2A2A10", accent:"#D4A520",
    title:"Platform Monopoly",
    subtitle:"Efficiency vs. accountability — when does regulation become punishment?",
    tag:"Antitrust · Jack Ma · Institutional indistinguishability",
    context:`<p>All market economies face the same structural problem: digital platform monopolies generate efficiency gains (network effects, data economies of scale) while simultaneously enabling market foreclosure, data exploitation, and political influence. The US spent a decade debating Facebook regulation with little result. The EU's Digital Markets Act took seven years to pass. The question is whether a system free from corporate lobbying can regulate more effectively — and at what cost.</p>`,
    bell:`Bell's steelman is perhaps at its most compelling here. Meritocratic regulators, insulated from corporate political donations, can identify systemic risk and act before a company becomes "too big to regulate." What took the EU seven years, China achieved in 18 months: Alibaba fined ¥18.2B (historic record), Ant Financial IPO cancelled, Didi forced off app stores, Tencent required to divest exclusive music rights. The incapacity of democratic systems to discipline corporate power is not hypothetical — it is empirically demonstrated.`,
    jin:`Jin explicitly endorses this reading under her "Common Prosperity" framework. Platform monopolies concentrate wealth, entrench inequality, and undermine the market competition that drives innovation. The state's intervention is not arbitrary power — it is the correction of market failure that Western democracies are structurally unable to make because regulated entities fund the regulators' political careers. Jin argues this is a systemic advantage of the Chinese model.`,
    crack:`Jack Ma delivered a speech criticising financial regulators on October 24, 2020. The Ant Financial IPO was suspended on November 3. Ten days. Ma disappeared from public view for three months. Jin frames this as antitrust regulation. But in the absence of independent judicial review, "antitrust" and "political punishment for criticism" are institutionally indistinguishable — they use the same regulatory instruments, initiated by the same political authorities, with no independent body to adjudicate the difference. This is not a bug in Bell's system — it is his structural feature: the absence of external accountability.`,
    questions:["Is there an empirical test that could distinguish 'genuine antitrust regulation' from 'political punishment dressed as regulation'? What evidence would you need, and is that evidence available?","Jin says China can regulate monopolies faster than democracies because there is no corporate lobbying. Evaluate this claim. What is it getting right? What does it leave out?","Design an institutional mechanism that would allow the Chinese state to regulate platform monopolies effectively while preventing the same mechanism from being used as political retaliation. Is such a mechanism compatible with the current system?"]
  },
  {
    id:5, short:"Infrastructure\nDebt",
    color1:"#101A20", color2:"#182530", accent:"#4AACCC",
    title:"Infrastructure and Intergenerational Debt",
    subtitle:"Strategic investment vs. political engineering — how do we know the difference?",
    tag:"High-speed rail · Fiscal debt · Verification problem",
    context:`<p>Large infrastructure investment creates a classic political economy dilemma: the costs are immediate and visible (debt, displacement, construction disruption), while the benefits are long-term and diffuse (spatial economic integration, productivity gains, urbanisation). Democratic governments systematically under-invest because voters discount future benefits. The question is whether a system freed from electoral short-termism actually invests better — or just invests more.</p>`,
    bell:`Bell's most structurally sound case: a meritocratic government with a long time horizon can make the infrastructure commitments that electoral democracies cannot. The HS2 project in the UK took 15 years of planning and political debate before a scaled-back version was approved. China built 40,000 km of HSR in 15 years. Bell would say this is not despite political centralisation — it is because of it.`,
    jin:`Jin's "state as co-investor" argument is at its most persuasive here. The 1994 Tax Sharing Reform created local governments as equity stakeholders in regional development — they have a direct financial interest in the spatial reorganisation that high-speed rail enables. The external economic benefits of HSR (labour market integration, knowledge spillovers, real estate appreciation) far exceed ticket revenue. Jin explicitly notes that market mechanisms would never have financed this network — the time horizon is too long.`,
    crack:`China Railway Group carries over ¥6 trillion in debt. Local government hidden liabilities are estimated at over 50% of GDP. Some HSR lines run at a fraction of break-even passenger volumes. Bell says "long-term investment." Jin says "state co-investor logic." But without independent auditing, open fiscal debate, or competitive project evaluation, there is no institutional mechanism to distinguish "strategic long-term investment" from "politically motivated construction that benefits officials' promotion metrics." The debt is real. Who bears it was never put to any form of public deliberation.`,
    questions:["Bell argues that freedom from electoral cycles enables better long-term investment. What evidence would support this? What would count as evidence against it — and is that evidence available in the Chinese case?","Jin says the state co-investor model is justified when market time horizons are too short. Apply this logic to a HSR line running at 20% capacity. Does the argument still hold? Under what conditions?","The verification problem: in a system without independent auditing, how can citizens or analysts distinguish strategic infrastructure investment from politically motivated spending? Is this problem solvable within Jin's framework?"]
  },
  {
    id:6, short:"Free Speech\nvs Harmony",
    color1:"#101828", color2:"#182438", accent:"#7090D0",
    title:"Free Expression vs. Social Cohesion",
    subtitle:"Who draws the line — and what protects the person drawing it?",
    tag:"Censorship · Remonstrance tradition · Dissent",
    context:`<p>Every society regulates speech — Germany bans Nazi symbols, the US restricts incitement to violence, European platforms remove hate speech. The debate is never about whether limits exist, but about <em>where</em> the line is and <em>who draws it</em>. In Confucian political theory, the remonstrance tradition (諫) gave officials a moral duty to convey uncomfortable truths upward. The question is whether that tradition has a functional modern equivalent.</p>`,
    bell:`Bell draws on the Confucian remonstrance tradition: a system that allows criticism to flow upward, within the constraints of hierarchy and respect for order. Modern equivalents — Weibo exposure of local corruption, internal party discipline channels — show that the system does allow a form of critical feedback. The goal of speech, in this view, is not self-expression but social improvement, and the state is the legitimate arbiter of that boundary.`,
    jin:`Jin's version is more empirical: she describes Chinese social media as a "two-way monitoring platform" — the government monitors citizens, but citizens also use public pressure to hold local officials accountable. She cites cases where Weibo campaigns led to official investigations and dismissals. Jin frames this as evidence that informal accountability mechanisms partially substitute for formal ones.`,
    crack:`The remonstrance tradition Bell invokes depended on the moral quality of the official who received the criticism — there was no institutional protection for the critic. Modern equivalents: rights lawyers (709 crackdown, 2015), investigative journalists, citizen reporters during COVID (Chen Qiushi, Li Zehua disappeared for months). The informal accountability mechanisms Jin describes work for local officials on local issues — they systematically fail when the target of criticism is the central authority itself. Both Bell and Jin require the same implicit condition: the people at the top are willing to receive bad news. When they are not, the remonstrance tradition produces martyrs, not policy correction.`,
    questions:["Bell says the Confucian remonstrance tradition provides an alternative to electoral accountability. Evaluate this claim using Li Wenliang and the 709 lawyers' crackdown as test cases. Does it hold? Under what conditions?","Jin argues informal accountability (Weibo, public pressure) partially substitutes for formal mechanisms. What are the structural limits of this substitution? When does informal accountability systematically fail?","Design a speech regulation system that preserves the social cohesion function Bell values while providing institutional protection for critics. What elements of the current Chinese system would it retain? What would it require changing?"]
  },
  {
    id:7, short:"Environment\nvs Growth",
    color1:"#0D1E10", color2:"#142818", accent:"#5AAA70",
    title:"Environmental Protection vs. Economic Growth",
    subtitle:"The strongest case for the China model — and where it still breaks down",
    tag:"Climate policy · One-veto rule · Data verification",
    context:`<p>The climate crisis is the most structurally damaging problem for electoral democracy's reputation. The US withdrew from the Paris Agreement. Australia's coal lobby shapes energy policy. The EU carbon border mechanism took a decade. The structural argument against electoral democracy on long-term environmental goods is empirically strong — short-term voter preferences systematically discount costs that will fall on future generations. This is the scenario where Bell and Jin's argument is <em>most</em> compelling. Engage with it at full strength before looking for cracks.</p>`,
    bell:`Bell's strongest case: a meritocratic government with a long time horizon can commit to environmental targets that electoral governments cannot sustain across political cycles. The 2013 "one-veto rule" — officials cannot be promoted if they miss environmental targets, regardless of other performance — is a direct implementation of Bell's accountability-within-the-system logic. The 2060 carbon neutrality commitment, the mandatory EV transition, the rapid solar and wind deployment — all represent the kind of structural long-term commitment that no democratic system has matched.`,
    jin:`Jin's state co-investor argument maps cleanly here: renewable energy deployment requires coordinated infrastructure investment (grid, manufacturing scale, supply chain) that market mechanisms cannot produce at the necessary speed. China is now the world's largest manufacturer of solar panels, wind turbines, and EV batteries. Jin would say this is not despite state coordination — it is because of it. The market cannot price in 2060 carbon costs at 2024 investment decisions. The state can mandate that it does.`,
    crack:`Local environmental data falsification has been a persistent problem throughout the same period. The mechanism that reports performance on environmental targets is the same mechanism that is being evaluated on those targets. Without independent verification, the one-veto rule is only as strong as the integrity of the reporting system. A study published in Nature (2019) found that China's satellite-measured NO₂ emissions were systematically higher than ground-station-reported figures in multiple industrial provinces. Bell and Jin both need to answer: when the accountability mechanism and the reported performance exist within the same political system, what does "accountability" actually mean?`,
    questions:["This scenario is designed to present the strongest possible case for Bell and Jin. Before looking for weaknesses — where is the argument most persuasive? What democratic failure does it expose most clearly?","The data falsification problem is structural, not individual. What institutional design would be required to make environmental accountability genuine within the Chinese system? Would that design be compatible with the current political structure?","Compare China's solar/wind deployment record with Germany's Energiewende. What does the comparison show about the relative advantages and disadvantages of different governance models for climate policy?"]
  },
  {
    id:8, short:"Emergency\nPowers",
    color1:"#28100A", color2:"#3A1810", accent:"#E07845",
    title:"Emergency Powers and Their Limits",
    subtitle:"Activating power is easy. Terminating it is where governance fails.",
    tag:"Zero-COVID · Sunset clauses · The final Bell question",
    context:`<p>Every political system expands state power in crises. The challenge is never activation — it is termination. Democratic systems have sunset clauses, parliamentary votes, judicial review, and media pressure that create friction against indefinite emergency powers. The US PATRIOT Act (2001) took 23 years to partially sunset. France's COVID state of emergency was challenged by the Constitutional Council after 18 months. The question is not whether emergency powers are used — it is what determines when they end, and who bears the cost if they end badly.</p>`,
    bell:`Bell's version: a meritocratic government committed to long-term stability has both the capacity and the incentive to maintain consistent emergency policy without the volatility of public opinion forcing premature reversal. The discipline of Zero-COVID — maintained for nearly three years across a population of 1.4 billion — is a demonstration of policy coherence that no electoral system could have sustained. When adaptation was necessary, it came — rapidly and decisively.`,
    jin:`Jin's version: strong state capacity means the crisis response is actually implemented, not merely announced. The field hospitals, the quarantine infrastructure, the economic stabilisation — these required the kind of coordinated state action that market mechanisms and fragmented democratic governance cannot produce. The 2020 economic result (the only major economy to grow) is Jin's empirical anchor.`,
    crack:`Zero-COVID was abandoned in December 2022 — in approximately four weeks, with no policy evaluation, no official accountability, no public explanation, and no compensation framework for those who lost businesses, savings, or family members to the enforcement of that policy. Bell's "adaptability" here means: the leadership changed its mind. Jin's "strong state capacity" here means: the same machinery that enforced lockdowns also enforced the opening. Bell's three-tier architecture has no mechanism by which any level can institutionally constrain the top. The Confucian Mandate of Heaven was the original termination clause. In the nuclear age, that mechanism is unavailable. Bell's model has removed the only termination clause the tradition ever had — and replaced it with nothing.`,
    questions:["Bell describes the Zero-COVID reversal as 'adaptability.' Is there an institutional difference between 'adaptive self-correction' and 'the leadership changed its mind'? If so, what is it? If not, what does that mean for Bell's argument?","Jin's strong state capacity argument explains Phase 1 (crisis response) well. What does it say about Phase 2 (post-crisis accountability)? Is post-crisis accountability a necessary component of a legitimate governance model?","The Mandate of Heaven was the Confucian system's original accountability mechanism — ultimate removal of a failed dynasty. Bell's modern meritocracy has no equivalent. Design a functional substitute. What would it need to do? Is it compatible with Bell's model, or does adding it fundamentally change what the model is?"]
  }
];

// ══════════════════════════════════════════════════════
// STATE
// ══════════════════════════════════════════════════════
let studentName  = '';
let studentEmail = '';
let completed    = new Set();
let submitted    = new Set();   // scenarios actually sent to sheet
let responses    = {};          // { scenarioId: {q1:'',q2:'',q3:''} }
let currentScenario = null;
let spinning     = false;
let currentAngle = 0;

// ══════════════════════════════════════════════════════
// REGISTRATION
// ══════════════════════════════════════════════════════
function register() {
  const name  = document.getElementById('reg-name').value.trim();
  const email = document.getElementById('reg-email').value.trim();
  const err   = document.getElementById('reg-error');

  if (!name || !email || !email.includes('@')) {
    err.classList.add('show');
    return;
  }
  err.classList.remove('show');
  studentName  = name;
  studentEmail = email;

  document.getElementById('reg-overlay').style.display = 'none';
  document.getElementById('student-badge').style.display = 'block';
  document.getElementById('badge-name').textContent = name;
}

// Allow Enter key in registration
document.addEventListener('keydown', e => {
  if (e.key === 'Enter' && document.getElementById('reg-overlay').style.display !== 'none') {
    register();
  }
});

// ══════════════════════════════════════════════════════
// WHEEL DRAWING
// ══════════════════════════════════════════════════════
const canvas = document.getElementById('wheel');
const ctx    = canvas.getContext('2d');
const N      = 8;
const sliceAngle = (2 * Math.PI) / N;

function drawWheel(angle) {
  ctx.clearRect(0,0,320,320);
  const cx = 160, cy = 160, r = 155;

  for (let i = 0; i < N; i++) {
    const sc     = SCENARIOS[i];
    const startA = angle + i * sliceAngle - Math.PI/2;
    const endA   = startA + sliceAngle;
    const isDone = submitted.has(i+1);

    const grad = ctx.createRadialGradient(cx,cy,20,cx,cy,r);
    grad.addColorStop(0, isDone ? '#1A3A30' : sc.color2);
    grad.addColorStop(1, isDone ? '#0D2018' : sc.color1);

    ctx.beginPath(); ctx.moveTo(cx,cy);
    ctx.arc(cx,cy,r,startA,endA); ctx.closePath();
    ctx.fillStyle = grad; ctx.fill();
    ctx.strokeStyle = isDone ? '#2A5A48' : sc.accent+'66';
    ctx.lineWidth = 1; ctx.stroke();

    ctx.beginPath(); ctx.arc(cx,cy,r-8,startA+0.04,endA-0.04);
    ctx.strokeStyle = isDone ? '#3A8060' : sc.accent;
    ctx.lineWidth = isDone ? 1 : 2; ctx.stroke();

    const numA = startA + sliceAngle/2;
    const nx = cx + 30*Math.cos(numA), ny = cy + 30*Math.sin(numA);
    ctx.fillStyle = isDone ? '#3A8060' : sc.accent;
    ctx.font = 'bold 14px "Playfair Display",serif';
    ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
    ctx.fillText(String(i+1), nx, ny);

    const tx = cx + 100*Math.cos(numA), ty = cy + 100*Math.sin(numA);
    ctx.save(); ctx.translate(tx,ty); ctx.rotate(numA+Math.PI/2);
    const lines = sc.short.split('\n');
    ctx.font = `${isDone?'normal':'600'} 10px "Source Serif 4",serif`;
    ctx.fillStyle = isDone ? '#4A7A68' : '#F4EDD8CC';
    ctx.textAlign = 'center';
    lines.forEach((line,li) => ctx.fillText(line, 0, (li-(lines.length-1)/2)*13));
    ctx.restore();
  }

  ctx.beginPath(); ctx.arc(cx,cy,22,0,Math.PI*2);
  ctx.fillStyle = '#1A1008'; ctx.fill();
  ctx.strokeStyle = '#B8860B'; ctx.lineWidth = 1.5; ctx.stroke();
  ctx.fillStyle = '#D4A520';
  ctx.font = 'bold 11px "Playfair Display",serif';
  ctx.textAlign = 'center'; ctx.textBaseline = 'middle';
  ctx.fillText('⊕',cx,cy);
}

drawWheel(0);
canvas.addEventListener('click', spinWheel);

// ══════════════════════════════════════════════════════
// SPIN LOGIC
// ══════════════════════════════════════════════════════
function spinWheel() {
  if (spinning) return;
  const incomplete = SCENARIOS.filter(s => !submitted.has(s.id));
  if (incomplete.length === 0) { openScenario(1); return; }

  spinning = true;
  document.getElementById('spin-btn').disabled = true;

  const chosen      = incomplete[Math.floor(Math.random()*incomplete.length)];
  const targetSlice = chosen.id - 1;
  const targetCenter = targetSlice * sliceAngle + sliceAngle/2;
  const fullRotations = (5 + Math.floor(Math.random()*4)) * 2 * Math.PI;
  const targetAngle  = fullRotations - targetCenter;
  const duration     = 3500 + Math.random()*1000;
  const startTime    = performance.now();
  const startAngle   = currentAngle;

  function animate(now) {
    const elapsed  = now - startTime;
    const progress = Math.min(elapsed/duration, 1);
    const eased    = 1 - Math.pow(1-progress,4);
    currentAngle   = (startAngle + (targetAngle-startAngle)*eased) % (2*Math.PI);
    drawWheel(currentAngle);
    if (progress < 1) { requestAnimationFrame(animate); }
    else {
      spinning = false;
      document.getElementById('spin-btn').disabled = false;
      setTimeout(() => openScenario(chosen.id), 300);
    }
  }
  requestAnimationFrame(animate);
}

// ══════════════════════════════════════════════════════
// WORKSHEET
// ══════════════════════════════════════════════════════
function openScenario(id) {
  currentScenario = id;
  const sc = SCENARIOS[id-1];
  const isSubmitted = submitted.has(id);

  document.getElementById('ws-num').textContent = `Scenario ${id} of 8  ·  ${sc.tag}`;
  document.getElementById('ws-title').textContent = sc.title;
  document.getElementById('ws-subtitle').textContent = sc.subtitle;
  document.getElementById('ws-card').style.borderTopColor = sc.accent;

  // Update submit button
  const btn = document.getElementById('ws-submit-btn');
  if (isSubmitted) {
    btn.textContent = '✓ Submitted';
    btn.className = 'ws-submit-btn done';
    btn.disabled = true;
  } else {
    btn.textContent = 'Submit Responses ↑';
    btn.className = 'ws-submit-btn';
    btn.disabled = false;
  }

  // Restore saved responses
  const saved = responses[id] || {q1:'',q2:'',q3:''};

  document.getElementById('ws-body').innerHTML = `
    <div class="ws-section">
      <div class="ws-section-head"><span class="ws-section-badge badge-context">Universal Dilemma</span></div>
      <div class="ws-text">${sc.context}</div>
    </div>
    <div class="ws-divider"></div>
    <div class="ws-section">
      <div class="ws-section-head"><span class="ws-section-badge badge-bell">Bell's Rationalisation</span></div>
      <div class="ws-text"><p>${sc.bell}</p></div>
    </div>
    <div class="ws-section">
      <div class="ws-section-head"><span class="ws-section-badge badge-jin">Jin's Rationalisation</span></div>
      <div class="ws-text"><p>${sc.jin}</p></div>
    </div>
    <div class="ws-divider"></div>
    <div class="ws-section">
      <div class="ws-section-head"><span class="ws-section-badge badge-crack">Where Both Frameworks Fail</span></div>
      <div class="crack-box"><div class="ws-text"><p>${sc.crack}</p></div></div>
    </div>
    <div class="ws-divider"></div>
    <div class="ws-section">
      <div class="ws-section-head"><span class="ws-section-badge badge-discuss">Discussion Questions</span></div>
      <div class="discuss-box">
        ${sc.questions.map((q,i)=>`
          <div class="discuss-q">
            <span class="q-num">Q${i+1}</span>
            <span class="q-text">${q}</span>
          </div>`).join('')}
      </div>
    </div>
    <div class="ws-divider"></div>
    <div class="ws-section">
      <div class="ws-section-head"><span class="ws-section-badge badge-response">Your Responses</span></div>
      <div class="response-block">
        ${sc.questions.map((q,i)=>`
          <div class="response-item">
            <label class="response-q-label" for="resp-${id}-${i+1}">Response to Q${i+1}</label>
            <textarea
              class="response-textarea"
              id="resp-${id}-${i+1}"
              placeholder="Write your response here…"
              ${isSubmitted ? 'disabled' : ''}
              oninput="saveResponse(${id},${i+1},this.value)"
            >${escHtml(saved['q'+(i+1)])}</textarea>
            <div class="char-count" id="cc-${id}-${i+1}">${saved['q'+(i+1)].length} characters</div>
          </div>`).join('')}
        <div class="submit-status" id="submit-status-${id}"></div>
      </div>
    </div>`;

  updateProgress();
  document.getElementById('ws-overlay').classList.add('open');
  document.getElementById('ws-overlay').scrollTop = 0;
}

function escHtml(str) {
  return String(str)
    .replace(/&/g,'&amp;').replace(/</g,'&lt;')
    .replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}

function saveResponse(id, qNum, value) {
  if (!responses[id]) responses[id] = {q1:'',q2:'',q3:''};
  responses[id]['q'+qNum] = value;
  const cc = document.getElementById(`cc-${id}-${qNum}`);
  if (cc) cc.textContent = value.length + ' characters';
}

function closeWS() {
  document.getElementById('ws-overlay').classList.remove('open');
  currentScenario = null;
}

function navScenario(dir) {
  if (!currentScenario) return;
  let next = currentScenario + dir;
  if (next < 1) next = 8;
  if (next > 8) next = 1;
  openScenario(next);
}

// ══════════════════════════════════════════════════════
// SUBMISSION
// ══════════════════════════════════════════════════════
async function submitScenario() {
  const id  = currentScenario;
  const sc  = SCENARIOS[id-1];
  const res = responses[id] || {q1:'',q2:'',q3:''};
  const statusEl = document.getElementById(`submit-status-${id}`);
  const btn = document.getElementById('ws-submit-btn');

  // Require at least one response
  const hasContent = res.q1.trim() || res.q2.trim() || res.q3.trim();
  if (!hasContent) {
    statusEl.className = 'submit-status error';
    statusEl.textContent = '⚠ Please write at least one response before submitting.';
    statusEl.style.display = 'block';
    return;
  }

  btn.disabled = true;
  statusEl.className = 'submit-status sending';
  statusEl.textContent = '⏳ Sending your responses…';
  statusEl.style.display = 'block';

  const payload = {
    name:           studentName,
    email:          studentEmail,
    timestamp:      new Date().toISOString(),
    scenarioId:     id,
    scenarioTitle:  sc.title,
    q1_question:    sc.questions[0],
    q1_response:    res.q1,
    q2_question:    sc.questions[1],
    q2_response:    res.q2,
    q3_question:    sc.questions[2],
    q3_response:    res.q3
  };

  try {
    if (!APPS_SCRIPT_URL || APPS_SCRIPT_URL === 'PASTE_YOUR_APPS_SCRIPT_URL_HERE') {
      // Demo mode — no real URL configured
      await new Promise(r => setTimeout(r, 900));
    } else {
      await fetch(APPS_SCRIPT_URL, {
        method: 'POST',
        mode:   'no-cors',
        body:   JSON.stringify(payload)
      });
    }

    // Mark success
    submitted.add(id);
    completed.add(id);

    statusEl.className = 'submit-status success';
    statusEl.textContent = '✓ Responses submitted successfully. Thank you!';

    btn.textContent  = '✓ Submitted';
    btn.className    = 'ws-submit-btn done';
    btn.disabled     = true;

    // Disable textareas
    [1,2,3].forEach(n => {
      const ta = document.getElementById(`resp-${id}-${n}`);
      if (ta) ta.disabled = true;
    });

    updateProgress();
    drawWheel(currentAngle);
    renderScenarioList();

    if (submitted.size === 8) {
      document.getElementById('all-done-msg').classList.add('show');
    }

  } catch(err) {
    statusEl.className = 'submit-status error';
    statusEl.textContent = '✗ Could not reach the server. Please check your connection and try again.';
    btn.disabled = false;
  }
}

// ══════════════════════════════════════════════════════
// PROGRESS & SCENARIO LIST
// ══════════════════════════════════════════════════════
function updateProgress() {
  document.getElementById('done-count').textContent = submitted.size;
  const bar = document.getElementById('progress-bar');
  bar.innerHTML = '';
  for (let i=1; i<=8; i++) {
    const dot = document.createElement('div');
    dot.className = 'prog-dot' +
      (submitted.has(i) ? ' done' : '') +
      (currentScenario===i ? ' active' : '');
    dot.textContent = i;
    dot.onclick = () => openScenario(i);
    bar.appendChild(dot);
  }
}

function renderScenarioList() {
  document.getElementById('scenario-list').innerHTML = SCENARIOS.map(sc=>`
    <div class="sc-card ${submitted.has(sc.id)?'done-card':''}" onclick="openScenario(${sc.id})">
      <div class="sc-card-num">Scenario ${sc.id}</div>
      <div class="sc-card-title">${sc.title}</div>
      <div class="sc-card-tag">${sc.tag.split(' · ')[0]}</div>
      <div class="sc-done-badge">✓ Submitted</div>
    </div>`).join('');
}

// ══════════════════════════════════════════════════════
// INIT
// ══════════════════════════════════════════════════════
updateProgress();
renderScenarioList();
</script>
</body>
</html>
