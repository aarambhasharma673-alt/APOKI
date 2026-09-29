# APOKI
#An Ai assistant from Kattel Industries 
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>APOKI — Kattel Industries</title>
<style>
  * { margin:0; padding:0; box-sizing:border-box; font-family: 'Courier New', monospace; -webkit-tap-highlight-color: transparent; }

  body {
    background: #000308;
    background-image:
      radial-gradient(circle at 50% 30%, #00243d 0%, #000308 70%),
      linear-gradient(rgba(0,229,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,255,0.03) 1px, transparent 1px);
    background-size: 100% 100%, 30px 30px, 30px 30px;
    color: #00e5ff;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    padding: 20px 16px;
    overflow: hidden;
    position: relative;
  }

  /* Top brand bar */
  .top-bar {
    width: 100%;
    text-align: center;
    padding: 8px 0 4px;
    border-bottom: 1px solid #003344;
    position: relative;
  }
  .top-bar::after {
    content: '';
    position: absolute;
    bottom: -1px; left: 50%; transform: translateX(-50%);
    width: 60px; height: 2px;
    background: #00e5ff;
    box-shadow: 0 0 12px #00e5ff;
  }
  .brand {
    font-size: 13px;
    letter-spacing: 5px;
    color: #00e5ff;
    text-shadow: 0 0 10px #00e5ff88;
    font-weight: bold;
  }
  .brand-sub {
    font-size: 8px;
    letter-spacing: 3px;
    color: #446677;
    margin-top: 3px;
  }

  /* Middle section */
  .middle {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    max-width: 420px;
  }

  /* Ring */
  .ring-wrap {
    position: relative;
    width: 200px;
    height: 200px;
    margin-bottom: 22px;
  }
  .ring-outer {
    position: absolute; inset: 0;
    border-radius: 50%;
    border: 1px dashed #005566;
    animation: rotate 30s linear infinite;
  }
  .ring-mid {
    position: absolute; inset: 15px;
    border-radius: 50%;
    border: 1px solid #0088aa33;
  }
  .ring-core {
    position: absolute; inset: 28px;
    border-radius: 50%;
    border: 3px solid #00e5ff;
    box-shadow: 0 0 25px #00e5ff, inset 0 0 30px #00e5ff44;
    display: flex; align-items: center; justify-content: center;
    transition: all 0.3s ease;
  }
  .ring-core .dot {
    width: 22px; height: 22px;
    border-radius: 50%;
    background: #00e5ff;
    box-shadow: 0 0 20px #00e5ff, 0 0 40px #00e5ff88;
    transition: all 0.3s ease;
  }

  .ring-core.listening {
    border-color: #00ff88;
    box-shadow: 0 0 35px #00ff88, inset 0 0 35px #00ff8844;
    animation: pulse 1s infinite;
  }
  .ring-core.listening .dot {
    background: #00ff88;
    box-shadow: 0 0 25px #00ff88, 0 0 45px #00ff8899;
  }
  .ring-core.thinking {
    border-color: #ffaa00;
    box-shadow: 0 0 35px #ffaa00, inset 0 0 35px #ffaa0044;
    animation: pulse 0.8s infinite;
  }
  .ring-core.thinking .dot {
    background: #ffaa00;
    box-shadow: 0 0 25px #ffaa00;
  }

  @keyframes pulse { 0%,100%{transform:scale(1)} 50%{transform:scale(1.05)} }
  @keyframes rotate { to { transform: rotate(360deg); } }

  /* Title */
  h1 {
    font-size: 28px;
    letter-spacing: 8px;
    margin-bottom: 4px;
    text-shadow: 0 0 18px #00e5ff88;
  }
  .tagline {
    font-size: 9px;
    letter-spacing: 4px;
    color: #446677;
    margin-bottom: 18px;
  }

  /* Status */
  .status {
    font-size: 12px;
    letter-spacing: 2px;
    color: #88ccdd;
    min-height: 18px;
    margin-bottom: 14px;
    text-transform: uppercase;
  }

  /* Log */
  .log {
    background: rgba(0, 20, 32, 0.7);
    border: 1px solid #003a4d;
    border-radius: 12px;
    padding: 14px;
    width: 100%;
    min-height: 90px;
    max-height: 160px;
    font-size: 12px;
    line-height: 1.5;
    text-align: left;
    overflow-y: auto;
    backdrop-filter: blur(6px);
    box-shadow: inset 0 0 20px #00000088;
  }
  .log:empty::before {
    content: 'Awaiting input...';
    color: #335566;
    font-style: italic;
  }
  .log .user { color: #00ff88; margin-bottom: 5px; }
  .log .ai   { color: #00e5ff; margin-bottom: 9px; }

  /* Mic button */
  .mic-btn {
    margin-top: 18px;
    background: linear-gradient(180deg, #003344 0%, #001a26 100%);
    color: #00e5ff;
    border: 2px solid #00e5ff;
    padding: 14px 44px;
    border-radius: 40px;
    font-size: 15px;
    font-family: inherit;
    letter-spacing: 3px;
    cursor: pointer;
    box-shadow: 0 0 20px #00e5ff44, inset 0 0 12px #00e5ff22;
    transition: all 0.2s;
    display: flex; align-items: center; gap: 10px;
  }
  .mic-btn:active, .mic-btn.pressed {
    background: #00e5ff;
    color: #000;
    box-shadow: 0 0 35px #00e5ff;
  }

  /* Bottom credit */
  .credit {
    width: 100%;
    text-align: center;
    padding: 10px 0 4px;
    border-top: 1px solid #003344;
    position: relative;
  }
  .credit::before {
    content: '';
    position: absolute;
    top: -1px; left: 50%; transform: translateX(-50%);
    width: 40px; height: 1px;
    background: #00e5ff;
    box-shadow: 0 0 8px #00e5ff;
  }
  .credit-line {
    font-size: 10px;
    letter-spacing: 2px;
    color: #5588aa;
  }
  .credit-line strong {
    color: #00e5ff;
    font-weight: normal;
    text-shadow: 0 0 8px #00e5ff88;
  }
  .credit-ver {
    font-size: 8px;
    color: #335566;
    letter-spacing: 2px;
    margin-top: 2px;
  }
</style>
</head>
<body>

  <!-- TOP BRAND -->
  <div class="top-bar">
    <div class="brand">KATTEL INDUSTRIES</div>
    <div class="brand-sub">ADVANCED AI DIVISION</div>
  </div>

  <!-- MIDDLE -->
  <div class="middle">

    <div class="ring-wrap">
      <div class="ring-outer"></div>
      <div class="ring-mid"></div>
      <div class="ring-core" id="ring">
        <div class="dot"></div>
      </div>
    </div>

    <h1>APOKI</h1>
    <div class="tagline">A P O K I · SYSTEM ONLINE</div>

    <div class="status" id="status">Tap below to speak</div>

    <div class="log" id="log"></div>

    <button class="mic-btn" id="micBtn">
      <span>🎤</span> SPEAK
    </button>

  </div>

  <!-- BOTTOM CREDIT -->
  <div class="credit">
    <div class="credit-line">Made by <strong>Aarambha Kattel</strong></div>
    <div class="credit-ver">v0.3 · KATTEL INDUSTRIES</div>
  </div>

<script>
// ============ KATTEL INDUSTRIES — CONFIG ============
const GROQ_API_KEY = "const GROQ_API_KEY = "...";";
const AI_NAME = "APOKI";
const COMPANY = "Kattel Industries";
const FOUNDER = "Aarambha Kattel";
// ===================================================

const SYSTEM_PROMPT = `You are ${AI_NAME}, an AI assistant built by ${COMPANY}, founded by ${FOUNDER}. You are calm, witty, loyal, and speak like a British butler. Call the user 'sir'. Keep replies short — 1 to 3 sentences unless asked for more. You are very smart and can answer any question about science, history, math, coding, or the world.`;

const ring = document.getElementById('ring');
const statusEl = document.getElementById('status');
const log = document.getElementById('log');
const micBtn = document.getElementById('micBtn');

function addLog(who, text) {
  const p = document.createElement('p');
  p.className = who;
  p.textContent = (who === 'user' ? '▸ You: ' : '▸ APOKI: ') + text;
  log.appendChild(p);
  log.scrollTop = log.scrollHeight;
}

function setState(state, text) {
  ring.className = 'ring-core ' + state;
  statusEl.textContent = text;
}

function speak(text) {
  const u = new SpeechSynthesisUtterance(text);
  u.rate = 1.05; u.pitch = 0.9; u.lang = 'en-GB';
  const voices = speechSynthesis.getVoices();
  const british = voices.find(v => v.lang === 'en-GB' && /male|daniel|george/i.test(v.name))
               || voices.find(v => v.lang === 'en-GB');
  if (british) u.voice = british;
  u.onend = () => setState('', 'Tap below to speak');
  speechSynthesis.speak(u);
}

async function askBrain(userText) {
  setState('thinking', 'Processing...');
  try {
    const res = await fetch('https://api.groq.com/openai/v1/chat/completions', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer ' + GROQ_API_KEY
      },
      body: JSON.stringify({
        model: 'llama-3.3-70b-versatile',
        messages: [
          { role: 'system', content: SYSTEM_PROMPT },
          { role: 'user', content: userText }
        ],
        max_tokens: 200
      })
    });
    const data = await res.json();
    if (data.error) {
      addLog('ai', 'Error: ' + data.error.message);
      setState('', 'Error — check API key');
      return;
    }
    const reply = data.choices[0].message.content;
    addLog('ai', reply);
    setState('', 'Speaking...');
    speak(reply);
  } catch (e) {
    addLog('ai', 'Error: ' + e.message);
    setState('', 'Error — check internet');
  }
}

const SR = window.SpeechRecognition || window.webkitSpeechRecognition;
if (!SR) {
  setState('', 'Voice not supported. Use Chrome.');
} else {
  const rec = new SR();
  rec.lang = 'en-US';
  rec.interimResults = false;
  rec.maxAlternatives = 1;

  rec.onstart = () => { setState('listening', 'Listening...'); micBtn.classList.add('pressed'); };
  rec.onerror = (e) => { setState('', 'Error: ' + e.error); micBtn.classList.remove('pressed'); };
  rec.onend = () => { micBtn.classList.remove('pressed'); if (ring.classList.contains('listening')) setState('', 'Tap below to speak'); };
  rec.onresult = (e) => {
    const text = e.results[0][0].transcript;
    addLog('user', text);
    askBrain(text);
  };

  micBtn.onclick = () => {
    speechSynthesis.cancel();
    rec.start();
  };
}
</script>
</body>
</html>
