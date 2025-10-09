[NoteQuizLive2.html](https://github.com/user-attachments/files/22798969/NoteQuizLive2.html)
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>D Major Scale Staff Position Trainer</title>
<style>
  :root{
    --bg:#10121a;
    --card:#f6f7fb;
    --accent:#1f7a8c;
    --ok:#2a9d8f;
    --high:#ef476f;
    --low:#ffd166;
    --muted:#666;
  }
  * {
    box-sizing: border-box;
  }
  body{
    font-family:Inter,Segoe UI,Roboto,-apple-system,BlinkMacSystemFont,Arial,sans-serif;
    background:var(--bg);
    color:var(--card);
    margin:0;
    padding:12px;
    min-height:100vh;
  }
  .container{
    width:100%;
    max-width:1200px;
    margin:0 auto;
    background:#fff;
    border-radius:12px;
    padding:18px;
    color:#111;
    box-shadow:0 8px 30px rgba(2,6,23,0.4);
  }
  header{
    display:flex;
    flex-direction:column;
    gap:12px;
    margin-bottom:12px;
  }
  header h1{
    font-size:20px;
    margin:0;
    text-align:center;
  }
  .controls{
    display:flex;
    flex-wrap:wrap;
    gap:8px;
    align-items:center;
    justify-content:center;
  }
  select,button,input[type=range]{
    font-size:16px; /* Larger for mobile */
    padding:10px 12px;
    border-radius:6px;
    border:1px solid #ddd;
    min-height:44px; /* Better touch targets */
  }
  button{
    cursor:pointer;
    transition:opacity 0.2s;
  }
  button:active{
    opacity:0.8;
  }
  .staff-wrap{
    display:flex;
    flex-direction:column;
    gap:18px;
  }
  @media (min-width: 768px) {
    .staff-wrap{
      flex-direction:row;
    }
    header{
      flex-direction:row;
      justify-content:space-between;
      align-items:center;
    }
    header h1{
      text-align:left;
    }
  }
  .staff-container{
    flex:1;
    min-height:200px;
    background:#fff;
    border-radius:8px;
    padding:12px;
    border:1px solid #ddd;
    overflow:hidden;
  }
  .staff{
    width:100%;
    height:200px;
    background:#fff;
  }
  @media (min-width: 768px) {
    .staff{
      height:250px;
    }
  }
  .info{
    flex:1;
    min-width:0;
  }
  .status{
    margin-top:12px;
    padding:12px;
    border-radius:8px;
    background:#f7f9fb;
    border:1px solid #e5eef2;
  }
  .meter{
    height:10px;
    background:#eee;
    border-radius:6px;
    overflow:hidden;
    margin-top:8px;
  }
  .meter > i{
    display:block;
    height:100%;
    width:0%;
    background:linear-gradient(90deg,var(--low),var(--ok));
    transition:width 0.3s ease;
  }
  .big-tt{
    font-size:24px;
    font-weight:700;
    margin-top:4px;
  }
  .small{
    font-size:14px;
    color:var(--muted)
  }
  .feedback{
    margin-top:10px;
    font-weight:700;
    font-size:16px;
    min-height:24px;
  }
  .note-name{
    font-weight:700;
    font-size:28px;
    margin-top:8px;
  }
  .footer{
    margin-top:12px;
    font-size:14px;
    color:#444;
    line-height:1.4;
  }
  .btn-danger{
    background:#ef476f;
    border:none;
    color:#fff;
    padding:10px 14px;
    border-radius:6px;
    cursor:pointer;
    min-width:80px;
  }
  .btn-primary{
    background:var(--accent);
    border:none;
    color:#fff;
    padding:10px 14px;
    border-radius:6px;
    cursor:pointer;
    min-width:80px;
  }
  .btn-success{
    background:#2a9d8f;
    border:none;
    color:#fff;
    padding:10px 14px;
    border-radius:6px;
    cursor:pointer;
    min-width:80px;
  }
  .clef-label{
    font-size:20px;
    font-weight:700;
    margin-bottom:4px;
    text-align:center;
  }
  @media (min-width: 768px) {
    .clef-label{
      text-align:left;
    }
  }
  .settings{
    margin-top:12px;
    display:flex;
    flex-wrap:wrap;
    gap:8px;
    align-items:center;
    justify-content:center;
  }
  .note-target {
    display:none;
  }
  .small-muted{
    font-size:14px;
    color:#777;
  }
  .legend{
    display:flex;
    gap:8px;
    margin-top:8px;
    flex-wrap:wrap;
    justify-content:center;
  }
  .legend span{
    background:#f3f6f8;
    border-radius:6px;
    padding:8px 10px;
    font-size:12px;
    border:1px solid #e4eef2;
  }
  .controls label{
    font-size:14px;
    color:#333;
    margin-right:6px;
  }
  .timer-score{
    display:flex;
    justify-content:space-between;
    margin-top:12px;
    padding:12px;
    border-radius:8px;
    background:#f0f7fa;
    border:1px solid #cce7f0;
  }
  .timer, .score{
    text-align:center;
  }
  .timer-value, .score-value{
    font-size:24px;
    font-weight:700;
    color:var(--accent);
  }
  .timer-label, .score-label{
    font-size:12px;
    color:var(--muted);
    margin-top:4px;
  }
  .share-section{
    margin-top:12px;
    padding:12px;
    border-radius:8px;
    background:#f0f9f7;
    border:1px solid #ccefe7;
    display:none;
  }
  .name-input{
    margin-bottom:12px;
  }
  .name-input label{
    display:block;
    font-size:14px;
    color:#777;
    margin-bottom:6px;
  }
  .name-input input{
    width:100%;
    padding:10px;
    border:1px solid #ddd;
    border-radius:4px;
    font-size:16px;
    box-sizing:border-box;
  }
  .share-link{
    display:flex;
    gap:8px;
    margin-top:8px;
  }
  .share-link input{
    flex:1;
    padding:10px;
    border:1px solid #ddd;
    border-radius:4px;
    font-size:14px;
    background:#f9f9f9;
  }
  .share-link button{
    padding:10px 14px;
    background:#2a9d8f;
    color:white;
    border:none;
    border-radius:4px;
    cursor:pointer;
    white-space:nowrap;
  }
  .share-message{
    font-size:14px;
    color:#2a9d8f;
    margin-top:6px;
    font-weight:600;
    text-align:center;
  }
  
  /* Mobile-specific improvements */
  @media (max-width: 767px) {
    body{
      padding:8px;
    }
    .container{
      padding:12px;
    }
    select, button, input[type=range]{
      font-size:14px;
      padding:8px 10px;
    }
    .staff{
      height:180px;
    }
    .controls{
      gap:6px;
    }
    .settings{
      gap:6px;
    }
  }

  /* New styles for disabled controls */
  .settings.disabled label {
    color: #999;
  }
  
  .settings.disabled input[type=range] {
    opacity: 0.6;
    cursor: not-allowed;
  }
  
  .settings.disabled span {
    color: #999;
  }
</style>
</head>
<body>
  <div class="container" role="application" aria-label="D Major Scale Staff Position Trainer">
    <header>
      <h1>D Major Scale — Staff Position Trainer</h1>
      <div class="controls">
        <label for="instrument">Instrument</label>
        <select id="instrument" aria-label="Instrument selector">
          <option value="violin">Violin (Treble)</option>
          <option value="viola">Viola (Alto)</option>
          <option value="cello">Cello (Bass)</option>
          <option value="doublebass">Double Bass (Bass 8vb)</option>
        </select>
        <button id="startMic" class="btn-primary">Start Microphone</button>
        <button id="stopMic" class="btn-danger" disabled>Stop</button>
      </div>
    </header>

    <div class="staff-wrap">
      <div class="staff-container">
        <div class="staff" id="staff">
          <!-- SVG staff drawn by JS -->
        </div>
      </div>

      <div class="info">
        <div class="clef-label" id="clefLabel">Treble Clef</div>
        
        <div class="timer-score">
          <div class="timer">
            <div class="timer-value" id="timerValue">01:00</div>
            <div class="timer-label">TIME REMAINING</div>
          </div>
          <div class="score">
            <div class="score-value" id="scoreValue">0</div>
            <div class="score-label">NOTES CORRECT</div>
          </div>
        </div>

        <div class="status" id="statusBox">
          <div class="small-muted">Detected pitch</div>
          <div class="big-tt" id="detectedFreq">— Hz</div>
          <div class="small-muted" id="detectedCents">— cents</div>
          <div class="feedback" id="feedback">Click "Start Microphone" to begin</div>
          <div class="meter"><i id="meterBar" style="width:0%"></i></div>
        </div>

        <div class="settings" id="settingsContainer">
          <label>Tolerance (cents)</label>
          <input id="tolerance" type="range" min="10" max="100" value="30" />
          <span id="tolVal">±30</span>

          <label>Hold time (ms)</label>
          <input id="hold" type="range" min="100" max="1500" value="700" />
          <span id="holdVal">700</span>

          <button id="refPlay">Play Reference</button>
          <button id="reset">Reset Sequence</button>
        </div>

        <!-- Share Score Section -->
        <div class="share-section" id="shareSection">
          <div class="small-muted">Share your score with your teacher:</div>
          <div class="name-input">
            <label for="studentName">Your Name (optional)</label>
            <input type="text" id="studentName" placeholder="Enter your name" maxlength="50">
          </div>
          <div class="share-link">
            <input type="text" id="shareLink" readonly placeholder="Share link will appear here">
            <button id="copyLink">Copy</button>
          </div>
          <div class="share-message" id="shareMessage"></div>
          <button id="shareScore" class="btn-success" style="margin-top:8px;width:100%">Generate Share Link</button>
        </div>

        <div class="legend">
          <span>Auto-advance when correct</span>
          <span>Sharps shown as ♯</span>
          <span>Microphone required</span>
        </div>

        <div class="footer">
          <strong>How it works:</strong> The trainer shows a note positioned exactly on staff lines/spaces/ledger lines for the chosen instrument and expects you to sing or play the matching pitch. Visual feedback appears in real time and the exercise auto-advances after a correct pitch is held. <strong>Timer starts when microphone is activated.</strong>
        </div>
      </div>
    </div>
  </div>

<script>
// Mobile compatibility fixes
document.addEventListener('DOMContentLoaded', function() {
  // Fix for iOS Safari 100vh issue
  function setAppHeight() {
    const doc = document.documentElement;
    doc.style.setProperty('--app-height', `${window.innerHeight}px`);
  }
  window.addEventListener('resize', setAppHeight);
  setAppHeight();

  // Prevent zoom on input focus for mobile
  document.addEventListener('touchstart', function() {}, {passive: true});
});

/*
  D Major Scale Staff Position Trainer
  - Mobile compatible version with fixed SVG rendering and microphone access
*/

// --- Configuration & note data ---
const instruments = {
  violin: {
    label: "Violin (Treble Clef)",
    clef: "treble",
    notes: [
      {name:"D4", freq:293.66, pos:{type:"space-below-line1"}},
      {name:"E4", freq:329.63, pos:{type:"line",n:1}},
      {name:"F♯4", freq:369.99, pos:{type:"space",n:1}, accidental:"#"},
      {name:"G4", freq:392.00, pos:{type:"line",n:2}},
      {name:"A4", freq:440.00, pos:{type:"space",n:2}},
      {name:"B4", freq:493.88, pos:{type:"line",n:3}},
      {name:"C♯5", freq:554.37, pos:{type:"space",n:3}, accidental:"#"},
      {name:"D5", freq:587.33, pos:{type:"line",n:4}}
    ]
  },
  viola: {
    label: "Viola (Alto Clef)",
    clef: "alto",
    notes:[
      {name:"D4", freq:293.66, pos:{type:"space",n:3}},
      {name:"E4", freq:329.63, pos:{type:"line",n:4}},
      {name:"F♯4", freq:369.99, pos:{type:"space",n:4}, accidental:"#"},
      {name:"G4", freq:392.00, pos:{type:"line",n:5}},
      {name:"A4", freq:440.00, pos:{type:"space-above-staff"}},
      {name:"B4", freq:493.88, pos:{type:"ledger-through",ledgers:1}},
      {name:"C♯5", freq:554.37, pos:{type:"space-above-ledger",ledgers:1}, accidental:"#"},
      {name:"D5", freq:587.33, pos:{type:"line-2-ledger",ledgers:2}}
    ]
  },
  cello: {
    label: "Cello (Bass Clef)",
    clef: "bass",
    notes:[
      {name:"D3", freq:146.83, pos:{type:"line",n:3}},
      {name:"E3", freq:164.81, pos:{type:"space",n:3}},
      {name:"F♯3", freq:184.99, pos:{type:"line",n:4}, accidental:"#"},
      {name:"G3", freq:196.00, pos:{type:"space",n:4}},
      {name:"A3", freq:220.00, pos:{type:"line",n:5}},
      {name:"B3", freq:246.94, pos:{type:"space-above-staff"}},
      {name:"C♯4", freq:277.18, pos:{type:"ledger-through",ledgers:1}, accidental:"#"},
      {name:"D4", freq:293.66, pos:{type:"space-above-ledger",ledgers:1}}
    ]
  },
  doublebass: {
    label: "Double Bass (Bass Clef 8vb)",
    clef: "bass-8vb",
    notes:[
      {name:"D2", freq:73.42, pos:{type:"line",n:3}},
      {name:"E2", freq:82.41, pos:{type:"space",n:3}},
      {name:"F♯2", freq:92.50, pos:{type:"line",n:4}, accidental:"#"},
      {name:"G2", freq:98.00, pos:{type:"space",n:4}},
      {name:"A2", freq:110.00, pos:{type:"line",n:5}},
      {name:"B2", freq:123.47, pos:{type:"space-above-staff"}},
      {name:"C♯3", freq:138.59, pos:{type:"ledger-through",ledgers:1}, accidental:"#"},
      {name:"D3", freq:146.83, pos:{type:"space-above-ledger",ledgers:1}}
    ]
  }
};

// --- Staff drawing utilities (SVG) - MOBILE FIXED ---
const staffEl = document.getElementById('staff');

function createSVG() {
  const svgNS = "http://www.w3.org/2000/svg";
  const svg = document.createElementNS(svgNS, 'svg');
  // Use responsive dimensions
  svg.setAttribute('viewBox', '0 0 720 300');
  svg.setAttribute('preserveAspectRatio', 'xMidYMid meet');
  svg.style.width = '100%';
  svg.style.height = '100%';
  svg.style.display = 'block';
  return svg;
}

// Initialize SVG
const svg = createSVG();
staffEl.appendChild(svg);

function drawStaffBase(clefGlyph, clefSuffix = '') {
  // Clear previous content
  while (svg.firstChild) {
    svg.removeChild(svg.firstChild);
  }
  
  const svgNS = "http://www.w3.org/2000/svg";
  const WIDTH = 720, HEIGHT = 300;

  // Staff positioning - adjusted for mobile
  const left = 80, right = WIDTH - 40;
  const top = 60;
  const spacing = 24;
  const lineCount = 5;
  const staffTop = top;
  const staffHeight = (lineCount - 1) * spacing;

  // Background
  const bg = document.createElementNS(svgNS, 'rect');
  bg.setAttribute('x', 0);
  bg.setAttribute('y', 0);
  bg.setAttribute('width', WIDTH);
  bg.setAttribute('height', HEIGHT);
  bg.setAttribute('fill', '#fff');
  svg.appendChild(bg);

  // Draw staff lines
  for(let i = 0; i < 5; i++) {
    const y = staffTop + i * spacing;
    const line = document.createElementNS(svgNS, 'line');
    line.setAttribute('x1', left);
    line.setAttribute('x2', right);
    line.setAttribute('y1', y);
    line.setAttribute('y2', y);
    line.setAttribute('stroke', '#111');
    line.setAttribute('stroke-width', '1.5');
    svg.appendChild(line);
  }

  // Clef glyph
  if (clefGlyph) {
    const clefFontSize = staffHeight;
    const clefText = document.createElementNS(svgNS, 'text');
    clefText.setAttribute('x', left - clefFontSize * 0.6);
    clefText.setAttribute('y', staffTop + staffHeight/2 + clefFontSize * 0.35);
    clefText.setAttribute('font-size', clefFontSize);
    clefText.setAttribute('font-weight', '700');
    clefText.setAttribute('fill', '#111');
    clefText.textContent = clefGlyph;
    svg.appendChild(clefText);

    if (clefSuffix) {
      const su = document.createElementNS(svgNS, 'text');
      su.setAttribute('x', left - clefFontSize * 0.15);
      su.setAttribute('y', staffTop + staffHeight + 20);
      su.setAttribute('font-size', '14');
      su.setAttribute('font-weight', '700');
      su.setAttribute('fill', '#111');
      su.textContent = clefSuffix;
      svg.appendChild(su);
    }
  }

  return {svg, left, right, staffTop, spacing, lineCount, staffHeight};
}

// Rest of the position calculation and rendering functions remain the same...
function yForPosition(pos, coords){
  const {staffTop, spacing} = coords;
  const lineYs = [];
  for(let i=0;i<5;i++){
    lineYs.push(staffTop + i*spacing);
  }
  function lineY(n){
    const idx = 5 - n;
    return lineYs[idx];
  }
  function spaceBetween(n){
    const y1 = lineY(n);
    const y2 = lineY(n+1);
    return (y1 + y2)/2;
  }

  switch(pos.type){
    case "line": return lineY(pos.n);
    case "space": return spaceBetween(pos.n);
    case "space-below-line1": return lineY(1) + spacing/2;
    case "on-top-line": return lineY(5) - spacing/2;
    case "space-above-staff": return lineY(5) - spacing/2;
    case "ledger-through": return lineY(5) - spacing;
    case "space-above-ledger": return lineY(5) - spacing - spacing/2;
    case "line-2-ledger": return lineY(5) - spacing*2;
    default: return (lineY(3) + lineY(2))/2;
  }
}

function renderNoteForInstrument(instKey, noteIndex){
  const inst = instruments[instKey];
  let glyph = '𝄞';
  let suffix = '';
  if (inst.clef === 'treble') glyph = '𝄞';
  else if (inst.clef === 'alto') glyph = '𝄡';
  else if (inst.clef === 'bass') glyph = '𝄢';
  else if (inst.clef === 'bass-8vb') { glyph = '𝄢'; suffix = '8vb'; }

  const coords = drawStaffBase(glyph, suffix);
  const svgNS = "http://www.w3.org/2000/svg";
  const target = inst.notes[noteIndex];
  const noteX = coords.left + (coords.right - coords.left) * 0.6;
  const y = yForPosition(target.pos, coords);

  // Draw ledger lines if needed
  function drawLedgerAt(yline){
    const ln = document.createElementNS(svgNS,'line');
    ln.setAttribute('x1', noteX - 28);
    ln.setAttribute('x2', noteX + 28);
    ln.setAttribute('y1', yline);
    ln.setAttribute('y2', yline);
    ln.setAttribute('stroke','#111');
    ln.setAttribute('stroke-width',2);
    svg.appendChild(ln);
  }

  if (target.pos.ledgers) {
    if (target.pos.ledgers >= 1) {
      drawLedgerAt(coords.staffTop - coords.spacing);
    }
    if (target.pos.ledgers >= 2) {
      drawLedgerAt(coords.staffTop - coords.spacing * 2);
    }
  }

  // Draw note head
  const note = document.createElementNS(svgNS,'ellipse');
  note.setAttribute('cx',noteX);
  note.setAttribute('cy',y);
  note.setAttribute('rx',14);
  note.setAttribute('ry',10);
  note.setAttribute('fill','#111');
  note.setAttribute('transform',`rotate(-15 ${noteX} ${y})`);
  svg.appendChild(note);

  // Draw accidental
  if (target.accidental === '#') {
    const acc = document.createElementNS(svgNS,'text');
    acc.setAttribute('x', noteX - 36);
    acc.setAttribute('y', y + 6);
    acc.setAttribute('font-size',22);
    acc.setAttribute('font-weight',700);
    acc.textContent = '♯';
    svg.appendChild(acc);
  }

  return {target, y, noteX};
}

// --- Pitch detection (autocorrelation) ---
function autoCorrelate(buf, sampleRate) {
  // ... (same as before)
  const SIZE = buf.length;
  let rms = 0;
  for (let i = 0; i < SIZE; i++) {
    const val = buf[i];
    rms += val * val;
  }
  rms = Math.sqrt(rms / SIZE);
  if (rms < 0.01) return -1;

  let r1 = 0, r2 = SIZE - 1, thres = 0.2;
  for (let i = 0; i < SIZE / 2; i++) {
    if (Math.abs(buf[i]) < thres) { r1 = i; break; }
  }
  for (let i = 1; i < SIZE / 2; i++) {
    if (Math.abs(buf[SIZE - i]) < thres) { r2 = SIZE - i; break; }
  }

  buf = buf.slice(r1, r2);
  const newSize = buf.length;

  const c = new Array(newSize).fill(0);
  for (let i = 0; i < newSize; i++) {
    for (let j = 0; j < newSize - i; j++) {
      c[i] = c[i] + buf[j] * buf[j + i];
    }
  }

  let d = 0;
  while (c[d] > c[d + 1]) d++;
  let maxval = -1, maxpos = -1;
  for (let i = d; i < newSize; i++) {
    if (c[i] > maxval) {
      maxval = c[i];
      maxpos = i;
    }
  }
  let T0 = maxpos;

  const x1 = c[T0 - 1], x2 = c[T0], x3 = c[T0 + 1];
  const a = (x1 + x3 - 2 * x2) / 2;
  const b = (x3 - x1) / 2;
  if (a) T0 = T0 - b / (2 * a);

  const freq = sampleRate / T0;
  if (freq > 20000 || freq < 40) return -1;
  return freq;
}

// --- Audio setup & detection loop - MOBILE FIXED ---
let audioContext = null;
let analyser = null;
let mediaStream = null;
let buflen = 2048;
let buf = new Float32Array(buflen);
let running = false;

// Timer and score variables
let timerInterval = null;
let timeRemaining = 60;
let score = 0;

// UI references
const instrSelect = document.getElementById('instrument');
const startBtn = document.getElementById('startMic');
const stopBtn = document.getElementById('stopMic');
const detectedFreqEl = document.getElementById('detectedFreq');
const detectedCentsEl = document.getElementById('detectedCents');
const feedbackEl = document.getElementById('feedback');
const meterBar = document.getElementById('meterBar');
const clefLabel = document.getElementById('clefLabel');
const toleranceSlider = document.getElementById('tolerance');
const tolVal = document.getElementById('tolVal');
const holdSlider = document.getElementById('hold');
const holdVal = document.getElementById('holdVal');
const refPlay = document.getElementById('refPlay');
const resetBtn = document.getElementById('reset');
const timerValue = document.getElementById('timerValue');
const scoreValue = document.getElementById('scoreValue');
const settingsContainer = document.getElementById('settingsContainer');

// Share score elements
const shareSection = document.getElementById('shareSection');
const studentName = document.getElementById('studentName');
const shareLink = document.getElementById('shareLink');
const copyLink = document.getElementById('copyLink');
const shareMessage = document.getElementById('shareMessage');
const shareScore = document.getElementById('shareScore');

let instKey = instrSelect.value;
let inst = instruments[instKey];
let playOrder = [];
let currentIndex = 0;
let currentRendered = null;
let firstRoundCompleted = false;
let tuningCheckCompleted = false; // NEW: Track if tuning check is done
let toleranceCents = parseInt(toleranceSlider.value,10);
let holdTime = parseInt(holdSlider.value,10);
let holdTimer = null;

// NEW: Functions to lock/unlock settings
function lockSettings() {
  toleranceSlider.disabled = true;
  holdSlider.disabled = true;
  settingsContainer.classList.add('disabled');
}

function unlockSettings() {
  toleranceSlider.disabled = false;
  holdSlider.disabled = false;
  settingsContainer.classList.remove('disabled');
}

// Timer functions (same as before)
function startTimer() {
  timeRemaining = 60;
  score = 0;
  updateTimerDisplay();
  updateScoreDisplay();
  
  // NEW: Lock settings when timer starts
  lockSettings();
  
  timerInterval = setInterval(() => {
    timeRemaining--;
    updateTimerDisplay();
    
    if (timeRemaining <= 0) {
      stopTimer();
      stopAudio();
      feedbackEl.textContent = "Time's up! Final score: " + score;
      feedbackEl.style.color = '#1f7a8c';
      shareSection.style.display = 'block';
    }
  }, 1000);
}

function stopTimer() {
  if (timerInterval) {
    clearInterval(timerInterval);
    timerInterval = null;
  }
  
  // NEW: Unlock settings when timer stops
  unlockSettings();
}

function updateTimerDisplay() {
  const minutes = Math.floor(timeRemaining / 60);
  const seconds = timeRemaining % 60;
  timerValue.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
  timerValue.style.color = timeRemaining <= 10 ? '#ef476f' : '#1f7a8c';
}

function updateScoreDisplay() {
  scoreValue.textContent = score;
}

function incrementScore() {
  score++;
  updateScoreDisplay();
}

// Share score functionality - MODIFIED to include settings
function generateShareLink() {
  const instrument = instrSelect.options[instrSelect.selectedIndex].text;
  const date = new Date().toLocaleDateString();
  const time = new Date().toLocaleTimeString();
  const name = studentName.value.trim() || 'Anonymous Student';
  
  // Include tolerance and hold time in the shared data
  const shareData = {
    name: name,
    instrument: instrument,
    score: score,
    date: date,
    time: time,
    maxPossible: inst.notes.length * 2,
    tolerance: toleranceCents,
    holdTime: holdTime
  };
  
  const encodedData = btoa(JSON.stringify(shareData));
  const baseUrl = window.location.href.split('#')[0];
  const shareUrl = `${baseUrl}#score=${encodedData}`;
  
  shareLink.value = shareUrl;
  shareMessage.textContent = 'Share this link with your teacher!';
  return shareUrl;
}

function copyToClipboard() {
  shareLink.select();
  shareLink.setSelectionRange(0, 99999);
  
  try {
    navigator.clipboard.writeText(shareLink.value).then(() => {
      shareMessage.textContent = 'Link copied to clipboard!';
      setTimeout(() => {
        shareMessage.textContent = 'Share this link with your teacher!';
      }, 3000);
    });
  } catch (err) {
    document.execCommand('copy');
    shareMessage.textContent = 'Link copied to clipboard!';
    setTimeout(() => {
      shareMessage.textContent = 'Share this link with your teacher!';
    }, 3000);
  }
}

function checkForSharedScore() {
  const hash = window.location.hash;
  if (hash.includes('score=')) {
    const encodedData = hash.split('score=')[1];
    try {
      const shareData = JSON.parse(atob(encodedData));
      // Updated message to include settings
      const message = `🎵 Music Practice Results 🎵

Student: ${shareData.name}
Instrument: ${shareData.instrument}
Score: ${shareData.score} notes correct
Settings: ±${shareData.tolerance} cents tolerance, ${shareData.holdTime}ms hold time
Date: ${shareData.date}
Time: ${shareData.time}

Great job ${shareData.name.split(' ')[0]}! 🎉`;
      
      alert(message);
      window.location.hash = '';
    } catch (e) {
      console.log('Invalid share data');
    }
  }
}

// NEW: Modified to start with D and A (open strings)
function initPlayOrder() {
  // Start with just D and A notes (open strings)
  if (!tuningCheckCompleted) {
    // Find indices of D and A notes
    const dIndex = inst.notes.findIndex(note => note.name.includes('D'));
    const aIndex = inst.notes.findIndex(note => note.name.includes('A'));
    playOrder = [dIndex, aIndex];
  } else {
    // After tuning check, use all notes
    playOrder = inst.notes.map((_, i) => i);
  }
  currentIndex = 0;
  firstRoundCompleted = false;
}

// Fisher-Yates shuffle
function shuffleArray(array) {
  for (let i = array.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [array[i], array[j]] = [array[j], array[i]];
  }
}

// Render current note
function renderCurrentNote() {
  if (!inst || playOrder.length === 0) return;
  const realIndex = playOrder[currentIndex];
  currentRendered = renderNoteForInstrument(instKey, realIndex);
  
  // NEW: Update feedback message based on stage
  if (!tuningCheckCompleted && currentIndex < 2) {
    const noteName = inst.notes[realIndex].name;
    feedbackEl.textContent = `Tuning check: Play your open ${noteName} string`;
    feedbackEl.style.color = '#1f7a8c';
  } else {
    feedbackEl.textContent = 'Sing/play the displayed pitch';
    feedbackEl.style.color = '#333';
  }
}

// Update instrument
function updateInstrument(){
  instKey = instrSelect.value;
  inst = instruments[instKey];
  if (inst.clef === 'treble') clefLabel.textContent = inst.label.split(' ')[0] + ' (Treble Clef)';
  else if (inst.clef === 'alto') clefLabel.textContent = inst.label.split(' ')[0] + ' (Alto Clef)';
  else if (inst.clef === 'bass') clefLabel.textContent = inst.label.split(' ')[0] + ' (Bass Clef)';
  else if (inst.clef === 'bass-8vb') clefLabel.textContent = inst.label.split(' ')[0] + ' (Bass Clef 8vb)';
  
  // NEW: Reset tuning check when instrument changes
  tuningCheckCompleted = false;
  initPlayOrder();
  renderCurrentNote();
}

// Event listeners
instrSelect.addEventListener('change', updateInstrument);

toleranceSlider.addEventListener('input', ()=>{
  toleranceCents = parseInt(toleranceSlider.value,10);
  tolVal.textContent = '±' + toleranceCents;
});

holdSlider.addEventListener('input', ()=>{
  holdTime = parseInt(holdSlider.value,10);
  holdVal.textContent = holdTime;
});

// Reference oscillator
let oscCtx = null;
let oscNode = null;
refPlay.addEventListener('click', ()=>{
  if (!oscCtx) oscCtx = new (window.AudioContext || window.webkitAudioContext)();
  if (oscNode) { oscNode.stop(); oscNode.disconnect(); oscNode = null; return; }
  oscNode = oscCtx.createOscillator();
  const gain = oscCtx.createGain();
  gain.gain.value = 0.1;
  oscNode.type = 'sine';
  const realIndex = playOrder[currentIndex];
  oscNode.frequency.value = inst.notes[realIndex].freq;
  oscNode.connect(gain);
  gain.connect(oscCtx.destination);
  oscNode.start();
  setTimeout(()=>{ if (oscNode){ oscNode.stop(); oscNode.disconnect(); oscNode=null; } }, 1200);
});

resetBtn.addEventListener('click', ()=>{
  // NEW: Reset both tuning check and sequence
  tuningCheckCompleted = false;
  initPlayOrder();
  renderCurrentNote();
  feedbackEl.textContent = 'Sequence reset. Starting with tuning check.';
});

// Share score button
shareScore.addEventListener('click', generateShareLink);
copyLink.addEventListener('click', copyToClipboard);

// Start microphone - MOBILE FIXED
startBtn.addEventListener('click', async ()=>{
  if (running) return;
  
  // Mobile-specific user gesture requirement
  try {
    // First ensure we're in a user gesture context
    if (audioContext && audioContext.state === 'suspended') {
      await audioContext.resume();
    }
    
    // Request microphone access
    mediaStream = await navigator.mediaDevices.getUserMedia({audio:true, video:false});
    
    // Create audio context if needed
    if (!audioContext) {
      audioContext = new (window.AudioContext || window.webkitAudioContext)();
    }
    
    const source = audioContext.createMediaStreamSource(mediaStream);
    analyser = audioContext.createAnalyser();
    analyser.fftSize = 2048;
    source.connect(analyser);
    
    running = true;
    startBtn.disabled = true;
    stopBtn.disabled = false;
    feedbackEl.textContent = 'Listening...';
    
    // Start timer when microphone is activated
    startTimer();
    
    // Start detection loop
    detectPitch();
  } catch (err) {
    console.error('Error starting microphone:', err);
    feedbackEl.textContent = 'Microphone access denied or not available.';
  }
});

// Stop microphone
stopBtn.addEventListener('click', ()=>{
  stopAudio();
});

function stopAudio() {
  running = false;
  if (mediaStream) {
    mediaStream.getTracks().forEach(track => track.stop());
    mediaStream = null;
  }
  startBtn.disabled = false;
  stopBtn.disabled = true;
  feedbackEl.textContent = 'Microphone stopped.';
  stopTimer();
}

// NEW: Modified pitch detection to handle tuning check progression
function detectPitch() {
  if (!running) return;
  
  const dataArray = new Float32Array(analyser.fftSize);
  analyser.getFloatTimeDomainData(dataArray);
  
  const freq = autoCorrelate(dataArray, audioContext.sampleRate);
  
  if (freq !== -1) {
    detectedFreqEl.textContent = freq.toFixed(1) + ' Hz';
    
    const realIndex = playOrder[currentIndex];
    const targetFreq = inst.notes[realIndex].freq;
    const cents = 1200 * Math.log2(freq / targetFreq);
    
    detectedCentsEl.textContent = cents.toFixed(1) + ' cents';
    
    const absCents = Math.abs(cents);
    if (absCents < toleranceCents) {
      feedbackEl.textContent = 'Perfect!';
      feedbackEl.style.color = '#2a9d8f';
      meterBar.style.background = 'linear-gradient(90deg,var(--low),var(--ok))';
      meterBar.style.width = '100%';
      
      if (!holdTimer) {
        holdTimer = setTimeout(() => {
          // Advance to next note
          currentIndex++;
          
          // NEW: Handle progression from tuning check to full scale
          if (!tuningCheckCompleted && currentIndex >= playOrder.length) {
            // Tuning check completed, switch to full scale
            tuningCheckCompleted = true;
            initPlayOrder(); // This will now create the full scale order
            feedbackEl.textContent = 'Tuning check complete! Now playing full D Major scale.';
            feedbackEl.style.color = '#1f7a8c';
          } else if (currentIndex >= playOrder.length) {
            // Full scale completed, shuffle and continue
            currentIndex = 0;
            firstRoundCompleted = true;
            shuffleArray(playOrder);
          }
          
          renderCurrentNote();
          incrementScore();
          holdTimer = null;
        }, holdTime);
      }
    } else {
      feedbackEl.textContent = cents > 0 ? 'Too high' : 'Too low';
      feedbackEl.style.color = cents > 0 ? '#ef476f' : '#ffd166';
      meterBar.style.background = cents > 0 ? '#ef476f' : '#ffd166';
      meterBar.style.width = Math.min(100, absCents / 2) + '%';
      
      if (holdTimer) {
        clearTimeout(holdTimer);
        holdTimer = null;
      }
    }
  } else {
    detectedFreqEl.textContent = '— Hz';
    detectedCentsEl.textContent = '— cents';
    feedbackEl.textContent = 'No pitch detected';
    feedbackEl.style.color = '#666';
    meterBar.style.width = '0%';
    
    if (holdTimer) {
      clearTimeout(holdTimer);
      holdTimer = null;
    }
  }
  
  requestAnimationFrame(detectPitch);
}

// Initialize
updateInstrument();
checkForSharedScore();
</script>
</body>
</html>
