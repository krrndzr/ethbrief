<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="ETH Brief">
<title>ETH Morning Brief</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@700;800&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
–bg: #0a0a0f;
–card: #111118;
–border: #1e1e2e;
–eth: #627EEA;
–eth-glow: rgba(98, 126, 234, 0.35);
–gold: #f0b429;
–text: #e8e8f0;
–muted: #5a5a7a;
–green: #3dd68c;
–red: #f87171;
}

html, body {
height: 100%;
background: var(–bg);
color: var(–text);
font-family: ‘Space Mono’, monospace;
overflow: hidden;
}

body {
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
min-height: 100dvh;
padding: 24px 20px;
position: relative;
}

/* Background effects */
.bg-orb {
position: fixed;
border-radius: 50%;
filter: blur(80px);
pointer-events: none;
z-index: 0;
}
.bg-orb-1 {
width: 300px; height: 300px;
background: radial-gradient(circle, rgba(98,126,234,0.15) 0%, transparent 70%);
top: -80px; left: -80px;
animation: drift1 8s ease-in-out infinite alternate;
}
.bg-orb-2 {
width: 200px; height: 200px;
background: radial-gradient(circle, rgba(240,180,41,0.08) 0%, transparent 70%);
bottom: 60px; right: -40px;
animation: drift2 10s ease-in-out infinite alternate;
}

@keyframes drift1 { from { transform: translate(0,0); } to { transform: translate(30px, 40px); } }
@keyframes drift2 { from { transform: translate(0,0); } to { transform: translate(-20px, -30px); } }

/* Grid lines */
.grid-bg {
position: fixed;
inset: 0;
background-image:
linear-gradient(rgba(98,126,234,0.04) 1px, transparent 1px),
linear-gradient(90deg, rgba(98,126,234,0.04) 1px, transparent 1px);
background-size: 40px 40px;
z-index: 0;
}

.content {
position: relative;
z-index: 1;
width: 100%;
max-width: 360px;
display: flex;
flex-direction: column;
align-items: center;
gap: 28px;
}

/* Header */
.header {
text-align: center;
}

.eth-logo {
width: 64px;
height: 64px;
margin: 0 auto 16px;
position: relative;
}

.eth-logo svg {
width: 100%;
height: 100%;
filter: drop-shadow(0 0 16px var(–eth-glow));
animation: pulse-logo 3s ease-in-out infinite;
}

@keyframes pulse-logo {
0%, 100% { filter: drop-shadow(0 0 16px var(–eth-glow)); }
50% { filter: drop-shadow(0 0 28px rgba(98,126,234,0.6)); }
}

.title {
font-family: ‘Syne’, sans-serif;
font-size: 28px;
font-weight: 800;
letter-spacing: -0.5px;
background: linear-gradient(135deg, #ffffff 0%, var(–eth) 100%);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
background-clip: text;
line-height: 1.1;
}

.subtitle {
font-size: 11px;
color: var(–muted);
letter-spacing: 2px;
text-transform: uppercase;
margin-top: 6px;
}

/* What you’ll get card */
.preview-card {
width: 100%;
background: var(–card);
border: 1px solid var(–border);
border-radius: 16px;
padding: 20px;
position: relative;
overflow: hidden;
}

.preview-card::before {
content: ‘’;
position: absolute;
top: 0; left: 0; right: 0;
height: 2px;
background: linear-gradient(90deg, transparent, var(–eth), transparent);
}

.preview-label {
font-size: 9px;
letter-spacing: 3px;
text-transform: uppercase;
color: var(–eth);
margin-bottom: 14px;
}

.preview-items {
display: flex;
flex-direction: column;
gap: 10px;
}

.preview-item {
display: flex;
align-items: center;
gap: 12px;
font-size: 12px;
color: #a0a0c0;
}

.preview-item .dot {
width: 6px;
height: 6px;
border-radius: 50%;
background: var(–eth);
flex-shrink: 0;
box-shadow: 0 0 6px var(–eth);
}

.preview-item .dot.gold { background: var(–gold); box-shadow: 0 0 6px var(–gold); }
.preview-item .dot.green { background: var(–green); box-shadow: 0 0 6px var(–green); }

/* Main CTA Button */
.cta-btn {
width: 100%;
display: block;
text-decoration: none;
background: linear-gradient(135deg, #3d52c4 0%, var(–eth) 100%);
color: #fff;
font-family: ‘Syne’, sans-serif;
font-size: 17px;
font-weight: 800;
letter-spacing: 0.5px;
text-align: center;
padding: 20px 24px;
border-radius: 16px;
border: none;
cursor: pointer;
position: relative;
overflow: hidden;
box-shadow: 0 8px 32px rgba(98,126,234,0.4), 0 2px 8px rgba(0,0,0,0.4);
transition: transform 0.15s ease, box-shadow 0.15s ease;
-webkit-tap-highlight-color: transparent;
}

.cta-btn::before {
content: ‘’;
position: absolute;
inset: 0;
background: linear-gradient(135deg, rgba(255,255,255,0.15) 0%, transparent 60%);
}

.cta-btn:active {
transform: scale(0.97);
box-shadow: 0 4px 16px rgba(98,126,234,0.3);
}

.cta-btn .btn-icon {
font-size: 22px;
display: block;
margin-bottom: 4px;
}

.cta-btn .btn-sub {
font-family: ‘Space Mono’, monospace;
font-size: 10px;
font-weight: 400;
opacity: 0.75;
letter-spacing: 1px;
display: block;
margin-top: 4px;
}

/* Time display */
.time-display {
font-size: 11px;
color: var(–muted);
letter-spacing: 1px;
}

#clock {
color: var(–eth);
}

/* Footer */
.footer {
font-size: 10px;
color: var(–muted);
text-align: center;
line-height: 1.7;
letter-spacing: 0.5px;
}

.footer a {
color: var(–eth);
text-decoration: none;
}
</style>

</head>
<body>

<div class="grid-bg"></div>
<div class="bg-orb bg-orb-1"></div>
<div class="bg-orb bg-orb-2"></div>

<div class="content">

  <div class="header">
    <div class="eth-logo">
      <svg viewBox="0 0 64 64" fill="none" xmlns="http://www.w3.org/2000/svg">
        <polygon points="32,4 52,32 32,42 12,32" fill="#627EEA" opacity="0.9"/>
        <polygon points="32,4 52,32 32,42" fill="#8EA4F0" opacity="0.6"/>
        <polygon points="32,42 52,32 32,60 12,32" fill="#627EEA" opacity="0.7"/>
        <polygon points="32,42 52,32 32,60" fill="#8EA4F0" opacity="0.4"/>
      </svg>
    </div>
    <div class="title">ETH Morning<br>Brief</div>
    <div class="subtitle">Powered by Claude AI</div>
  </div>

  <div class="preview-card">
    <div class="preview-label">What you'll get</div>
    <div class="preview-items">
      <div class="preview-item"><span class="dot"></span>Live ETH price + 24h movement</div>
      <div class="preview-item"><span class="dot gold"></span>Top news affecting price today</div>
      <div class="preview-item"><span class="dot"></span>Macro signals (Fed, USD, BTC)</div>
      <div class="preview-item"><span class="dot gold"></span>Whale & institutional activity</div>
      <div class="preview-item"><span class="dot green"></span>Tomorrow's price prediction</div>
    </div>
  </div>

  <a class="cta-btn" id="briefBtn" href="#" onclick="openBrief(event)">
    <span class="btn-icon">⚡</span>
    Get Today's ETH Brief
    <span class="btn-sub">OPENS CLAUDE · ONE TAP</span>
  </a>

  <div class="time-display">TODAY — <span id="clock"></span></div>

  <div class="footer">
    Save this page to your Home Screen<br>for instant one-tap access each morning.<br><br>
    <a href="#" onclick="showInstructions(event)">How to add to Home Screen →</a>
  </div>

</div>

<!-- Instructions overlay -->

<div id="overlay" style="display:none; position:fixed; inset:0; background:rgba(0,0,0,0.92); z-index:100; padding:32px 24px; overflow-y:auto;">
  <div style="max-width:360px; margin:0 auto; font-size:13px; line-height:1.8; color:#c0c0d8;">
    <div style="font-family:'Syne',sans-serif; font-size:20px; font-weight:800; color:#fff; margin-bottom:20px;">Add to Home Screen</div>
    <div style="color:#627EEA; font-size:10px; letter-spacing:2px; text-transform:uppercase; margin-bottom:12px;">iPhone Steps</div>
    <ol style="padding-left:18px; display:flex; flex-direction:column; gap:10px;">
      <li>Open this page in <strong style="color:#fff">Safari</strong> (not Chrome)</li>
      <li>Tap the <strong style="color:#fff">Share button</strong> (square with arrow at bottom)</li>
      <li>Scroll down and tap <strong style="color:#fff">"Add to Home Screen"</strong></li>
      <li>Name it <strong style="color:#fff">ETH Brief</strong> → tap <strong style="color:#fff">Add</strong></li>
      <li>✅ Done! Tap the icon every morning</li>
    </ol>
    <div style="margin-top:28px; padding:16px; background:#111118; border:1px solid #1e1e2e; border-radius:12px; font-size:11px; color:#5a5a7a;">
      Note: You'll need to be logged into Claude.ai for the brief to run.
    </div>
    <button onclick="document.getElementById('overlay').style.display='none'"
      style="margin-top:24px; width:100%; padding:16px; background:#627EEA; color:#fff; border:none; border-radius:12px; font-family:'Syne',sans-serif; font-size:16px; font-weight:800; cursor:pointer;">
      Got it ✓
    </button>
  </div>
</div>

<script>
  // Clock
  function updateClock() {
    const now = new Date();
    document.getElementById('clock').textContent = now.toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'});
  }
  updateClock();
  setInterval(updateClock, 1000);

  // The pre-filled prompt for Claude
  const prompt = `Give me my ETH Morning Brief for today. Please cover:

1. 📈 Current ETH price and 24h % change
2. 📰 Top 3 news stories affecting ETH price today (macro + crypto-specific)
3. 🐋 Any notable whale movements, institutional buys, or ETF flows
4. 🌍 Macro signals: Fed news, USD strength, Bitcoin dominance
5. 🔮 Your prediction: will ETH price go UP, DOWN, or SIDEWAYS tomorrow? Give a confidence level and your reasoning.

Be concise and direct. I want actionable insight, not fluff.`;

  function openBrief(e) {
    e.preventDefault();
    const encoded = encodeURIComponent(prompt);
    const url = `https://claude.ai/new?q=${encoded}`;
    window.open(url, '_blank');
  }

  function showInstructions(e) {
    e.preventDefault();
    document.getElementById('overlay').style.display = 'block';
  }
</script>

</body>
</html>
