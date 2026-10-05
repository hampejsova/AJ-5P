# AJ-5P
angličtina pro 5P
<!DOCTYPE html>
<html lang="cs">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Angličtina 5. třída – Slovíčka a měsíce</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #4f46e5;
      --primary-light: #e0e7ff;
      --success: #10b981;
      --success-light: #d1fae5;
      --danger: #ef4444;
      --danger-light: #fee2e2;
      --warning: #f59e0b;
      --bg-gradient: linear-gradient(135deg, #6366f1 0%, #a855f7 50%, #ec4899 100%);
      --card-bg: #ffffff;
      --text: #1f2937;
      --text-muted: #6b7280;
      --radius: 20px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Nunito', sans-serif;
    }

    body {
      min-height: 100vh;
      background: var(--bg-gradient);
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 16px;
      color: var(--text);
    }

    .game-card {
      background: var(--card-bg);
      width: 100%;
      max-width: 580px;
      border-radius: var(--radius);
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
      padding: 28px 24px;
      position: relative;
      overflow: hidden;
    }

    /* Hlavička a ukazatel */
    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 16px;
    }

    .badge {
      background: var(--primary-light);
      color: var(--primary);
      font-weight: 700;
      font-size: 0.9rem;
      padding: 6px 14px;
      border-radius: 999px;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .score-badge {
      background: #fef3c7;
      color: #b45309;
    }

    .progress-bar {
      width: 100%;
      height: 10px;
      background: #f3f4f6;
      border-radius: 999px;
      overflow: hidden;
      margin-bottom: 24px;
    }

    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, #4f46e5, #ec4899);
      width: 0%;
      transition: width 0.3s ease;
      border-radius: 999px;
    }

    /* Karta otázky */
    .question-box {
      text-align: center;
      background: #f8fafc;
      border: 2px dashed #cbd5e1;
      border-radius: 16px;
      padding: 24px 16px;
      margin-bottom: 20px;
    }

    .question-hint {
      font-size: 0.95rem;
      color: var(--text-muted);
      font-weight: 600;
      margin-bottom: 8px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .word-prompt {
      font-family: 'Fredoka', cursive, sans-serif;
      font-size: 2.2rem;
      font-weight: 700;
      color: #312e81;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 12px;
      flex-wrap: wrap;
    }

    .sound-btn {
      background: #e0e7ff;
      border: none;
      color: #4338ca;
      width: 44px;
      height: 44px;
      border-radius: 50%;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: transform 0.15s, background 0.2s;
    }

    .sound-btn:hover {
      background: #c7d2fe;
      transform: scale(1.08);
    }

    .sound-btn svg {
      width: 22px;
      height: 22px;
      fill: currentColor;
    }

    /* Tlačítka možností */
    .options-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
      margin-bottom: 20px;
    }

    @media (max-width: 480px) {
      .options-grid {
        grid-template-columns: 1fr;
      }
      .word-prompt {
        font-size: 1.8rem;
      }
    }

    .option-btn {
      background: #ffffff;
      border: 2px solid #e2e8f0;
      border-radius: 14px;
      padding: 14px 16px;
      font-size: 1.05rem;
      font-weight: 700;
      color: #334155;
      cursor: pointer;
      text-align: center;
      transition: all 0.2s ease;
      position: relative;
    }

    .option-btn:hover:not(:disabled) {
      border-color: #6366f1;
      background: #f5f3ff;
      transform: translateY(-2px);
    }

    .option-btn.correct {
      background: var(--success-light) !important;
      border-color: var(--success) !important;
      color: #065f46 !important;
    }

    .option-btn.wrong {
      background: var(--danger-light) !important;
      border-color: var(--danger) !important;
      color: #991b1b !important;
    }

    .option-btn:disabled {
      cursor: default;
    }

    /* Zpětná vazba */
    .feedback-box {
      border-radius: 14px;
      padding: 14px;
      font-size: 0.95rem;
      font-weight: 600;
      text-align: center;
      margin-bottom: 20px;
      display: none;
      animation: fadeIn 0.3s ease;
    }

    .feedback-box.correct {
      background: var(--success-light);
      color: #065f46;
      border: 1px solid #a7f3d0;
      display: block;
    }

    .feedback-box.wrong {
      background: var(--danger-light);
      color: #991b1b;
      border: 1px solid #fecaca;
      display: block;
    }

    .next-btn {
      width: 100%;
      background: linear-gradient(135deg, #4f46e5, #7c3aed);
      color: white;
      border: none;
      border-radius: 14px;
      padding: 14px 20px;
      font-size: 1.1rem;
      font-weight: 800;
      cursor: pointer;
      transition: opacity 0.2s, transform 0.1s;
      display: none;
    }

    .next-btn:hover {
      opacity: 0.95;
      transform: translateY(-2px);
    }

    /* Obrazovka výsledků */
    .results-screen {
      text-align: center;
      display: none;
      padding: 20px 0;
    }

    .results-title {
      font-family: 'Fredoka', cursive, sans-serif;
      font-size: 2rem;
      margin-bottom: 12px;
      color: #312e81;
    }

    .results-score {
      font-size: 3rem;
      font-weight: 800;
      color: #ec4899;
      margin-bottom: 12px;
    }

    .results-comment {
      font-size: 1.15rem;
      color: var(--text-muted);
      margin-bottom: 28px;
    }

    .restart-btn {
      background: linear-gradient(135deg, #10b981, #059669);
      color: white;
      border: none;
      border-radius: 14px;
      padding: 15px 32px;
      font-size: 1.1rem;
      font-weight: 800;
      cursor: pointer;
      transition: all 0.2s;
    }

    .restart-btn:hover {
      transform: scale(1.05);
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(6px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Plátno na konfety */
    #confettiCanvas {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 100;
    }
  </style>
</head>
<body>

  <div class="game-card">
    <canvas id="confettiCanvas"></canvas>

    <!-- Hrací plocha -->
    <div id="gamePlay">
      <div class="header">
        <div class="badge" id="stepCounter">Otázka 1 / 10</div>
        <div class="badge score-badge" id="scoreCounter">⭐ Skóre: 0</div>
      </div>

      <div class="progress-bar">
        <div class="progress-fill" id="progressFill"></div>
      </div>

      <div class="question-box">
        <div class="question-hint">Jaký je český význam?</div>
        <div class="word-prompt">
          <span id="promptWord">Today</span>
          <button class="sound-btn" id="soundBtn" title="Přehrát výslovnost">
            <svg viewBox="0 0 24 24"><path d="M3 9v6h4l5 5V4L7 9H3zm13.5 3c0-1.77-1.02-3.29-2.5-4.03v8.05c1.48-.73 2.5-2.25 2.5-4.02zM14 3.23v2.06c2.89.86 5 3.54 5 6.71s-2.11 5.85-5 6.71v2.06c4.01-.91 7-4.49 7-8.77s-2.99-7.86-7-8.77z"/></svg>
          </button>
        </div>
      </div>

      <div class="options-grid" id="optionsGrid"></div>

      <div class="feedback-box" id="feedbackBox"></div>

      <button class="next-btn" id="nextBtn">Další otázka ➔</button>
    </div>

    <!-- Závěrečná obrazovka -->
    <div class="results-screen" id="resultsScreen">
      <div style="font-size: 3.5rem; margin-bottom: 8px;">🏆</div>
      <h2 class="results-title">Skvělá práce!</h2>
      <div class="results-score" id="finalScore">8 / 10</div>
      <p class="results-comment" id="resultsComment">Super výsledek, slovíčka ti jdou na jedničku!</p>
      <button class="restart-btn" id="restartBtn">🔄 Hrát znovu</button>
    </div>
  </div>

  <script>
    // Kompletní databáze: 10 slovíček z tabule + 12 měsíců
    const VOCABULARY_DATABASE = [
      // Slovíčka z tabule
      { en: "Today", cz: "dnes", example: "Today is a great day." },
      { en: "Holiday", cz: "prázdniny", example: "Summer holiday is the best." },
      { en: "Tomorrow", cz: "zítra", example: "See you tomorrow!" },
      { en: "First", cz: "první", example: "January is the first month." },
      { en: "Like", cz: "mít rád", example: "I like ice cream." },
      { en: "Because", cz: "protože", example: "I'm happy because it's sunny." },
      { en: "Trip", cz: "výlet", example: "We are going on a school trip." },
      { en: "From", cz: "od", example: "A letter from my friend." },
      { en: "Visit", cz: "navštívit", example: "We will visit my grandma." },
      { en: "Celebrate", cz: "oslava, oslavit", example: "Let's celebrate your birthday!" },

      // 12 měsíců v roce
      { en: "January", cz: "leden", example: "January is cold." },
      { en: "February", cz: "únor", example: "February has 28 or 29 days." },
      { en: "March", cz: "březen", example: "Spring starts in March." },
      { en: "April", cz: "duben", example: "April has sunny and rainy days." },
      { en: "May", cz: "květen", example: "Flowers bloom in May." },
      { en: "June", cz: "červen", example: "School ends in June." },
      { en: "July", cz: "červenec", example: "We swim in July." },
      { en: "August", cz: "srpen", example: "August is warm and sunny." },
      { en: "September", cz: "září", example: "School starts in September." },
      { en: "October", cz: "říjen", example: "Leaves turn yellow in October." },
      { en: "November", cz: "listopad", example: "November can be foggy." },
      { en: "December", cz: "prosinec", example: "Christmas is in December." }
    ];

    const TOTAL_QUESTIONS = 10;
    let currentQuiz = [];
    let currentIndex = 0;
    let score = 0;
    let audioCtx = null;

    // Zvukový syntetizátor (Web Audio API)
    function playBeep(isSuccess) {
      try {
        if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();
        osc.connect(gain);
        gain.connect(audioCtx.destination);

        if (isSuccess) {
          osc.type = "sine";
          osc.frequency.setValueAtTime(523.25, audioCtx.currentTime); // C5
          osc.frequency.setValueAtTime(659.25, audioCtx.currentTime + 0.08); // E5
          gain.gain.setValueAtTime(0.2, audioCtx.currentTime);
          gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.25);
          osc.start();
          osc.stop(audioCtx.currentTime + 0.25);
        } else {
          osc.type = "triangle";
          osc.frequency.setValueAtTime(220, audioCtx.currentTime);
          osc.frequency.setValueAtTime(170, audioCtx.currentTime + 0.1);
          gain.gain.setValueAtTime(0.2, audioCtx.currentTime);
          gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
          osc.start();
          osc.stop(audioCtx.currentTime + 0.3);
        }
      } catch (e) {
        console.warn("Audio unavailable:", e);
      }
    }

    // Předčítání anglické výslovnosti
    function speakWord(text) {
      if ('speechSynthesis' in window) {
        window.speechSynthesis.cancel();
        const utterance = new SpeechSynthesisUtterance(text);
        utterance.lang = 'en-GB';
        utterance.rate = 0.85;
        window.speechSynthesis.speak(utterance);
      }
    }

    function shuffleArray(array) {
      return [...array].sort(() => Math.random() - 0.5);
    }

    function initGame() {
      // Vybereme 10 náhodných slovíček z celé databáze
      const shuffledAll = shuffleArray(VOCABULARY_DATABASE);
      currentQuiz = shuffledAll.slice(0, TOTAL_QUESTIONS);
      currentIndex = 0;
      score = 0;

      document.getElementById("gamePlay").style.display = "block";
      document.getElementById("resultsScreen").style.display = "none";
      updateScoreUI();
      renderQuestion();
    }

    function updateScoreUI() {
      document.getElementById("stepCounter").innerText = `Otázka ${currentIndex + 1} / ${TOTAL_QUESTIONS}`;
      document.getElementById("scoreCounter").innerText = `⭐ Skóre: ${score}`;
      const progressPercent = (currentIndex / TOTAL_QUESTIONS) * 100;
      document.getElementById("progressFill").style.width = `${progressPercent}%`;
    }

    function renderQuestion() {
      const q = currentQuiz[currentIndex];
      updateScoreUI();

      document.getElementById("promptWord").innerText = q.en;
      document.getElementById("feedbackBox").className = "feedback-box";
      document.getElementById("feedbackBox").innerText = "";
      document.getElementById("nextBtn").style.display = "none";

      // Vytvoření 4 možností (1 správná + 3 náhodné špatné)
      const wrongPool = VOCABULARY_DATABASE.filter(item => item.cz !== q.cz);
      const wrongChoices = shuffleArray(wrongPool).slice(0, 3).map(item => item.cz);
      const allChoices = shuffleArray([q.cz, ...wrongChoices]);

      const grid = document.getElementById("optionsGrid");
      grid.innerHTML = "";

      allChoices.forEach(choice => {
        const btn = document.createElement("button");
        btn.className = "option-btn";
        btn.innerText = choice;
        btn.onclick = () => handleAnswer(choice, q.cz, btn);
        grid.appendChild(btn);
      });

      // Přehrát výslovnost
      speakWord(q.en);
    }

    function handleAnswer(selected, correct, selectedBtn) {
      const allButtons = document.querySelectorAll(".option-btn");
      allButtons.forEach(b => b.disabled = true);

      const feedback = document.getElementById("feedbackBox");
      const currentItem = currentQuiz[currentIndex];

      if (selected === correct) {
        score++;
        playBeep(true);
        selectedBtn.classList.add("correct");
        feedback.className = "feedback-box correct";
        feedback.innerHTML = `🎉 <strong>Správně!</strong> ${currentItem.en} = ${currentItem.cz}.<br><small style="opacity:0.9;">Příklad: "${currentItem.example}"</small>`;
      } else {
        playBeep(false);
        selectedBtn.classList.add("wrong");
        allButtons.forEach(b => {
          if (b.innerText === correct) b.classList.add("correct");
        });
        feedback.className = "feedback-box wrong";
        feedback.innerHTML = `❌ <strong>Pozor:</strong> ${currentItem.en} znamená <strong>${currentItem.cz}</strong>.<br><small style="opacity:0.9;">Příklad: "${currentItem.example}"</small>`;
      }

      document.getElementById("scoreCounter").innerText = `⭐ Skóre: ${score}`;
      document.getElementById("nextBtn").style.display = "block";
    }

    document.getElementById("soundBtn").addEventListener("click", () => {
      const currentWord = currentQuiz[currentIndex].en;
      speakWord(currentWord);
    });

    document.getElementById("nextBtn").addEventListener("click", () => {
      currentIndex++;
      if (currentIndex < TOTAL_QUESTIONS) {
        renderQuestion();
      } else {
        showResults();
      }
    });

    function showResults() {
      document.getElementById("progressFill").style.width = "100%";
      document.getElementById("gamePlay").style.display = "none";
      const results = document.getElementById("resultsScreen");
      results.style.display = "block";

      document.getElementById("finalScore").innerText = `${score} / ${TOTAL_QUESTIONS}`;
      const comment = document.getElementById("resultsComment");

      if (score === 10) {
        comment.innerText = "Naprostá jednička s hvězdičkou! Znáš všechna slovíčka bez chyby!";
        startConfetti();
      } else if (score >= 7) {
        comment.innerText = "Velmi pěkný výsledek! Slovíčka ti jdou skvěle.";
        startConfetti();
      } else if (score >= 4) {
        comment.innerText = "Dobrá práce, ale ještě si měsíce a slovíčka raději procvič.";
      } else {
        comment.innerText = "Nevadí, zkus to ještě jednou a slovíčka se ti brzy uloží do hlavy!";
      }
    }

    document.getElementById("restartBtn").addEventListener("click", initGame);

    // Animace konfet na oslavu
    function startConfetti() {
      const canvas = document.getElementById("confettiCanvas");
      const ctx = canvas.getContext("2d");
      canvas.width = canvas.parentElement.clientWidth;
      canvas.height = canvas.parentElement.clientHeight;

      const particles = Array.from({ length: 45 }, () => ({
        x: Math.random() * canvas.width,
        y: -10,
        r: Math.random() * 6 + 4,
        d: Math.random() * 20,
        color: ["#4f46e5", "#ec4899", "#10b981", "#f59e0b", "#06b6d4"][Math.floor(Math.random() * 5)],
        tilt: Math.floor(Math.random() * 10) - 10,
        tiltInc: (Math.random() * 0.07) + 0.05
      }));

      let animationFrames = 0;
      function draw() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        particles.forEach(p => {
          ctx.beginPath();
          ctx.lineWidth = p.r / 2;
          ctx.strokeStyle = p.color;
          ctx.moveTo(p.x + p.tilt + (p.r / 4), p.y);
          ctx.lineTo(p.x + p.tilt, p.y + p.tilt + (p.r / 4));
          ctx.stroke();

          p.y += 2.5;
          p.tilt = Math.sin(p.tiltInc += 0.05) * 12;
        });

        animationFrames++;
        if (animationFrames < 160) {
          requestAnimationFrame(draw);
        } else {
          ctx.clearRect(0, 0, canvas.width, canvas.height);
        }
      }
      draw();
    }

    // Spuštění po načtení
    window.addEventListener("DOMContentLoaded", initGame);
  </script>
</body>
</html>
