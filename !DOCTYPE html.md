<!DOCTYPE html>  
<html lang="fa" dir="rtl">  
<head>  
<meta charset="UTF-8">  
<title>بازی کلمات هم‌آغاز - نگاره ۴</title>  
<style>  
  * { box-sizing: border-box; margin: 0; padding: 0; }  
  body {  
    font-family: 'Tahoma', 'B Nazanin', sans-serif;  
    background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%);  
    min-height: 100vh;  
    display: flex;  
    align-items: center;  
    justify-content: center;  
    padding: 20px;  
  }  
  .container {  
    background: white;  
    border-radius: 30px;  
    box-shadow: 0 20px 50px rgba(0,0,0,0.2);  
    padding: 30px;  
    max-width: 700px;  
    width: 100%;  
    text-align: center;  
    position: relative;  
  }  
  .music-btn {  
    position: absolute;  
    top: 15px;  
    left: 15px;  
    background: #eaf4fb;  
    border: 2px solid #3498db;  
    border-radius: 50%;  
    width: 50px;  
    height: 50px;  
    font-size: 22px;  
    cursor: pointer;  
    transition: all 0.3s;  
  }  
  .music-btn:hover { background: #d6eaf8; transform: scale(1.1); }  
  .music-btn.off { opacity: 0.5; }  
  h1 { color: #2980b9; font-size: 30px; margin-bottom: 8px; }  
  .subtitle { color: #7f8c8d; font-size: 17px; margin-bottom: 20px; }  
  .score-bar {  
    display: flex; justify-content: space-around;  
    background: #eaf4fb; border-radius: 15px;  
    padding: 12px; margin-bottom: 20px;  
    font-size: 18px; font-weight: bold; color: #34495e;  
  }  
  .score-bar span { color: #2980b9; }  
  .question-box {  
    background: #f0f8ff;  
    border: 3px dashed #3498db;  
    border-radius: 20px;  
    padding: 15px; margin-bottom: 20px;  
  }  
  .question-text { font-size: 19px; color: #555; margin-bottom: 10px; }  
  .main-word-emoji { font-size: 65px; line-height: 1; }  
  .main-word {  
    font-size: 50px; font-weight: bold;  
    color: #c0392b; margin: 5px 0;  
  }  
  .options {  
    display: grid; grid-template-columns: 1fr 1fr;  
    gap: 12px; margin-bottom: 18px;  
  }  
  .option-btn {  
    background: #f8f9fa;  
    border: 3px solid #bdc3c7;  
    border-radius: 18px;  
    padding: 15px 8px;  
    font-size: 24px; font-weight: bold;  
    cursor: pointer; transition: all 0.3s;  
    font-family: inherit; color: #2c3e50;  
  }  
  .option-btn:hover { background: #e8f4fd; transform: translateY(-3px); }  
  .option-btn.correct {  
    background: #2ecc71; border-color: #27ae60; color: white;  
    animation: pulse 0.5s;  
  }  
  .option-btn.wrong {  
    background: #e74c3c; border-color: #c0392b; color: white;  
    animation: shake 0.5s;  
  }  
  .option-btn .emoji { font-size: 38px; display: block; margin-bottom: 4px; }  
  .option-btn:disabled { cursor: not-allowed; }  
  .feedback {  
    font-size: 21px; font-weight: bold;  
    min-height: 32px; margin-bottom: 12px;  
  }  
  .feedback.good { color: #27ae60; }  
  .feedback.bad { color: #e74c3c; }  
  .next-btn {  
    background: #3498db; color: white; border: none;  
    border-radius: 15px; padding: 13px 35px;  
    font-size: 19px; cursor: pointer; font-family: inherit;  
    display: none; transition: all 0.3s;  
  }  
  .next-btn:hover { background: #2980b9; transform: scale(1.05); }  
  .end-screen { display: none; }  
  .end-screen h2 { font-size: 34px; color: #2980b9; margin-bottom: 15px; }  
  .end-screen .final-score { font-size: 60px; color: #27ae60; margin: 15px 0; }  
  .restart-btn {  
    background: #e67e22; color: white; border: none;  
    border-radius: 15px; padding: 13px 35px;  
    font-size: 19px; cursor: pointer; font-family: inherit; margin-top: 12px;  
  }  
  @keyframes pulse {  
    0%,100% { transform: scale(1); }  
    50% { transform: scale(1.1); }  
  }  
  @keyframes shake {  
    0%,100% { transform: translateX(0); }  
    25% { transform: translateX(-10px); }  
    75% { transform: translateX(10px); }  
  }  
  @media (max-width: 500px) {  
    .main-word { font-size: 36px; }  
    .main-word-emoji { font-size: 50px; }  
    h1 { font-size: 22px; }  
    .option-btn { font-size: 18px; padding: 12px 5px; }  
    .option-btn .emoji { font-size: 28px; }  
    .music-btn { width: 42px; height: 42px; font-size: 18px; }  
  }  
</style>  
</head>  
<body>  
<div class="container">  
  <button class="music-btn" id="musicBtn" title="قطع/وصل موسیقی">🎵</button>  
  
  <div id="gameScreen">  
    <h1>🎯 کلمات هم‌آغاز</h1>  
    <p class="subtitle">نگاره ۴ - فارسی پایه اول</p>  
  
    <div class="score-bar">  
      <div>سوال: <span id="qNum">1</span> از <span id="qTotal">6</span></div>  
      <div>امتیاز: <span id="score">0</span> ⭐</div>  
    </div>  
  
    <div class="question-box">  
      <div class="question-text">کدام کلمه با کلمه‌ی زیر <b>هم‌آغاز</b> است؟</div>  
      <div class="main-word-emoji" id="mainEmoji">💧</div>  
      <div class="main-word" id="mainWord">آب</div>  
    </div>  
  
    <div class="feedback" id="feedback"></div>  
    <div class="options" id="options"></div>  
    <button class="next-btn" id="nextBtn">سوال بعدی ➡️</button>  
  </div>  
  
  <div class="end-screen" id="endScreen">  
    <h2 id="endTitle">🎉 آفرین!</h2>  
    <p style="font-size:22px; color:#555;">بازی تمام شد</p>  
    <div class="final-score" id="finalScore">0</div>  
    <p style="font-size:20px; color:#777;">از <span id="totalQ">6</span> سوال</p>  
    <button class="restart-btn" onclick="startGame()">🔄 دوباره بازی</button>  
  </div>  
</div>  
  
<script>  
/* ========== سیستم صدا با Web Audio API ========== */  
let audioCtx = null;  
let musicEnabled = true;  
let musicInterval = null;  
  
function initAudio() {  
  if (!audioCtx) {  
    audioCtx = new (window.AudioContext || window.webkitAudioContext)();  
  }  
  if (audioCtx.state === 'suspended') {  
    audioCtx.resume();  
  }  
}  
  
function playTone(freq, duration, type = 'sine', volume = 0.15, delay = 0) {  
  if (!audioCtx) return;  
  const t = audioCtx.currentTime + delay;  
  const osc = audioCtx.createOscillator();  
  const gain = audioCtx.createGain();  
  osc.type = type;  
  osc.frequency.value = freq;  
  gain.gain.setValueAtTime(0, t);  
  gain.gain.linearRampToValueAtTime(volume, t + 0.01);  
  gain.gain.exponentialRampToValueAtTime(0.001, t + duration);  
  osc.connect(gain);  
  gain.connect(audioCtx.destination);  
  osc.start(t);  
  osc.stop(t + duration);  
}  
  
function playCorrectSound() {  
  playTone(523.25, 0.15, 'sine', 0.2, 0);  
  playTone(659.25, 0.15, 'sine', 0.2, 0.12);  
  playTone(783.99, 0.25, 'sine', 0.2, 0.24);  
  playTone(1046.5, 0.35, 'sine', 0.2, 0.36);  
}  
  
function playWrongSound() {  
  playTone(311.13, 0.2, 'sawtooth', 0.15, 0);  
  playTone(233.08, 0.35, 'sawtooth', 0.15, 0.18);  
}  
  
function playClickSound() {  
  playTone(880, 0.06, 'triangle', 0.1, 0);  
}  
  
function playEndSound() {  
  const notes = [  
    [523.25, 0.15], [523.25, 0.15], [523.25, 0.15],  
    [523.25, 0.3], [415.30, 0.3], [466.16, 0.3], [523.25, 0.6]  
  ];  
  let delay = 0;  
  notes.forEach(([f, d]) => {  
    playTone(f, d, 'sine', 0.2, delay);  
    delay += d + 0.05;  
  });  
}  
  
function startMusic() {  
  if (musicInterval) return;  
  const melody = [  
    [523.25, 0.4], [587.33, 0.4], [659.25, 0.4], [587.33, 0.4],  
    [523.25, 0.4], [493.88, 0.4], [440.00, 0.4], [493.88, 0.4],  
    [523.25, 0.4], [659.25, 0.4], [783.99, 0.4], [659.25, 0.4],  
    [587.33, 0.6], [523.25, 0.8]  
  ];  
  const totalDur = melody.reduce((s, [, d]) => s + d + 0.1, 0) * 1000;  
  
  const playMelody = () => {  
    if (!musicEnabled) return;  
    let delay = 0;  
    melody.forEach(([f, d]) => {  
      playTone(f, d * 0.9, 'sine', 0.05, delay);  
      playTone(f / 2, d * 0.9, 'triangle', 0.025, delay);  
      delay += d + 0.1;  
    });  
  };  
  
  playMelody();  
  musicInterval = setInterval(playMelody, totalDur);  
}  
  
function stopMusic() {  
  if (musicInterval) {  
    clearInterval(musicInterval);  
    musicInterval = null;  
  }  
}  
  
document.getElementById('musicBtn').onclick = () => {  
  initAudio();  
  musicEnabled = !musicEnabled;  
  const btn = document.getElementById('musicBtn');  
  if (musicEnabled) {  
    btn.textContent = '🎵';  
    btn.classList.remove('off');  
    startMusic();  
  } else {  
    btn.textContent = '🔇';  
    btn.classList.add('off');  
    stopMusic();  
  }  
  playClickSound();  
};  
  
/* ========== بازی ========== */  
const questions = [  
  {  
    word: "آب", emoji: "💧",  
    options: [  
      { text: "آبی", emoji: "🔵", correct: true },  
      { text: "کتاب", emoji: "📖", correct: false },  
      { text: "مدیر", emoji: "👩‍💼", correct: false },  
      { text: "مادر", emoji: "👩", correct: false }  
    ]  
  },  
  {  
    word: "آبی", emoji: "🔵",  
    options: [  
      { text: "کفش", emoji: "👟", correct: false },  
      { text: "آزاده", emoji: "🧕", correct: true },  
      { text: "مدرسه", emoji: "🏫", correct: false },  
      { text: "کیف", emoji: "👜", correct: false }  
    ]  
  },  
  {  
    word: "آزاده", emoji: "🧕",  
    options: [  
      { text: "مادر", emoji: "👩", correct: false },  
      { text: "کتاب", emoji: "📖", correct: false },  
      { text: "آمین", emoji: "👦", correct: true },  
      { text: "مسجد", emoji: "🕌", correct: false }  
    ]  
  },  
  {  
    word: "آمین", emoji: "👦",  
    options: [  
      { text: "آب", emoji: "💧", correct: true },  
      { text: "بابا", emoji: "👨", correct: false },  
      { text: "مدیر", emoji: "👩‍💼", correct: false },  
      { text: "کفش", emoji: "👟", correct: false }  
    ]  
  },  
  {  
    word: "مدرسه", emoji: "🏫",  
    options: [  
      { text: "کتاب", emoji: "📖", correct: false },  
      { text: "مادر", emoji: "👩", correct: true },  
      { text: "آب", emoji: "💧", correct: false },  
      { text: "کیف", emoji: "👜", correct: false }  
    ]  
  },  
  {  
    word: "مدیر", emoji: "👩‍💼",  
    options: [  
      { text: "آزاده", emoji: "🧕", correct: false },  
      { text: "کفش", emoji: "👟", correct: false },  
      { text: "مسجد", emoji: "🕌", correct: true },  
      { text: "بابا", emoji: "👨", correct: false }  
    ]  
  }  
];  
  
let currentQ = 0;  
let score = 0;  
let answered = false;  
  
function startGame() {  
  initAudio();  
  if (musicEnabled) startMusic();  
  currentQ = 0;  
  score = 0;  
  answered = false;  
  document.getElementById('gameScreen').style.display = 'block';  
  document.getElementById('endScreen').style.display = 'none';  
  document.getElementById('qTotal').textContent = questions.length;  
  document.getElementById('totalQ').textContent = questions.length;  
  document.getElementById('score').textContent = '0';  
  loadQuestion();  
}  
  
function loadQuestion() {  
  answered = false;  
  const q = questions[currentQ];  
  document.getElementById('qNum').textContent = currentQ + 1;  
  document.getElementById('mainWord').textContent = q.word;  
  document.getElementById('mainEmoji').textContent = q.emoji;  
  document.getElementById('feedback').textContent = '';  
  document.getElementById('feedback').className = 'feedback';  
  document.getElementById('nextBtn').style.display = 'none';  
  
  const optsDiv = document.getElementById('options');  
  optsDiv.innerHTML = '';  
  const shuffled = [...q.options].sort(() => Math.random() - 0.5);  
  
  shuffled.forEach(opt => {  
    const btn = document.createElement('button');  
    btn.className = 'option-btn';  
    btn.innerHTML = `<span class="emoji">${opt.emoji}</span>${opt.text}`;  
    btn.onclick = () => checkAnswer(btn, opt.correct);  
    optsDiv.appendChild(btn);  
  });  
}  
  
function checkAnswer(btn, isCorrect) {  
  if (answered) return;  
  answered = true;  
  
  const allBtns = document.querySelectorAll('.option-btn');  
  allBtns.forEach(b => b.disabled = true);  
  
  const fb = document.getElementById('feedback');  
  
  if (isCorrect) {  
    btn.classList.add('correct');  
    score++;  
    document.getElementById('score').textContent = score;  
    fb.textContent = '✅ آفرین! درست بود';  
    fb.className = 'feedback good';  
    playCorrectSound();  
  } else {  
    btn.classList.add('wrong');  
    fb.textContent = '❌ اشتباه بود! دوباره فکر کن';  
    fb.className = 'feedback bad';  
    playWrongSound();  
  }  
  
  document.getElementById('nextBtn').style.display = 'inline-block';  
}  
  
document.getElementById('nextBtn').onclick = () => {  
  playClickSound();  
  currentQ++;  
  if (currentQ < questions.length) {  
    loadQuestion();  
  } else {  
    endGame();  
  }  
};  
  
function endGame() {  
  document.getElementById('gameScreen').style.display = 'none';  
  document.getElementById('endScreen').style.display = 'block';  
  document.getElementById('finalScore').textContent = score;  
  
  const title = document.getElementById('endTitle');  
  if (score === questions.length) title.textContent = '🏆 عالی! تو یک قهرمانی!';  
  else if (score >= questions.length / 2) title.textContent = '😊 خوب بود! بازم تمرین کن';  
  else title.textContent = '💪 اشکالی نداره، دوباره تلاش کن!';  
  
  playEndSound();  
}  
  
document.body.addEventListener('click', function firstClick() {  
  initAudio();  
  if (musicEnabled && !musicInterval) startMusic();  
  document.body.removeEventListener('click', firstClick);  
}, { once: true });  
  
startGame();  
</script>  
</body>  
</html>  
