<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Ryme - Our Safe Place</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --primary-love: #d81b60;
            --soft-pink: #fce4ec;
            --cream: #fff9fb;
        }

        body {
            background: var(--cream);
            color: #444;
            font-family: 'Segoe UI', sans-serif;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
        }

        /* قلوب متساقطة */
        .heart-particle {
            position: fixed; top: -10px; pointer-events: none;
            animation: fall linear forwards; z-index: 1000;
        }
        @keyframes fall { to { transform: translateY(105vh) rotate(360deg); } }

        /* شريط التنقل السفلي */
        .navbar {
            background: white; padding: 10px 0; display: flex;
            justify-content: space-around; position: fixed; bottom: 0;
            width: 100%; z-index: 1100; box-shadow: 0 -2px 15px rgba(0,0,0,0.05);
            border-radius: 20px 20px 0 0;
        }
        .nav-item {
            color: #bbb; text-decoration: none; font-size: 0.8rem;
            display: flex; flex-direction: column; align-items: center; transition: 0.3s;
        }
        .nav-item.active { color: var(--primary-love); }

        .page {
            display: none; padding: 20px 20px 100px 20px;
            animation: fadeIn 0.6s ease; max-width: 450px; margin: auto;
        }
        .page.active { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* لعبة الذاكرة */
        .memory-game {
            display: grid; grid-template-columns: repeat(4, 1fr); gap: 8px; margin-top: 20px;
        }
        .memory-card {
            height: 80px; background: var(--primary-love); border-radius: 10px;
            display: flex; align-items: center; justify-content: center;
            font-size: 2rem; color: white; cursor: pointer;
            transform-style: preserve-3d; transition: transform 0.5s;
        }
        .memory-card.flip { transform: rotateY(180deg); background: white; border: 2px solid var(--soft-pink); }
        .memory-card .front, .memory-card .back { position: absolute; backface-visibility: hidden; }
        .memory-card .back { transform: rotateY(180deg); }

        /* الأنشطة */
        .activity-card {
            background: white; padding: 15px; margin: 12px 0; border-radius: 15px;
            display: flex; align-items: center; gap: 15px; box-shadow: 0 4px 10px rgba(0,0,0,0.02);
        }
        .activity-card i { color: var(--primary-love); font-size: 1.2rem; }

        .music-btn {
            position: fixed; top: 20px; right: 20px; background: white;
            padding: 8px 15px; border-radius: 20px; z-index: 1200;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05); font-size: 0.8rem;
        }

        h1 { color: var(--primary-love); text-align: center; margin-top: 50px; }
        .btn-love {
            background: var(--primary-love); color: white; border: none;
            padding: 15px; border-radius: 30px; width: 100%; margin-top: 30px;
            font-weight: bold; box-shadow: 0 5px 15px rgba(216, 27, 96, 0.2);
        }
    </style>
</head>
<body>

    <div class="music-btn" onclick="toggleMusic()">
        <i id="mIcon" class="fas fa-play"></i> <span id="mText">Music</span>
        <audio id="bgMusic" loop><source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-15.mp3" type="audio/mpeg"></audio>
    </div>

    <div class="navbar">
        <a href="#" class="nav-item active" id="n-home" onclick="show('home')"><i class="fas fa-heart"></i><span>Us</span></a>
        <a href="#" class="nav-item" id="n-game" onclick="show('game')"><i class="fas fa-puzzle-piece"></i><span>Play</span></a>
        <a href="#" class="nav-item" id="n-plans" onclick="show('plans')"><i class="fas fa-star"></i><span>Plans</span></a>
        <a href="#" class="nav-item" id="n-note" onclick="show('note')"><i class="fas fa-envelope"></i><span>Note</span></a>
    </div>

    <div id="home" class="page active">
        <h1>For Ryme</h1>
        <p style="text-align: center; color: #666;">I built this place for you. To remember our beautiful moments and the things we love.</p>
        <div style="text-align: center; font-size: 4rem;">🦋</div>
    </div>

    <div id="game" class="page">
        <h2 style="color: var(--primary-love); text-align: center;">Match the Cards</h2>
        <p style="text-align: center; font-size: 0.9rem;">Find the pairs of things that make us happy!</p>
        <div class="memory-game" id="gameGrid"></div>
    </div>

    <div id="plans" class="page">
        <h2 style="color: var(--primary-love);">Our Next Dates</h2>
        <div class="activity-card"><i class="fas fa-hotdog"></i><div><b>Spicy Chips Night</b><br>Your favorite salty & spicy snacks.</div></div>
        <div class="activity-card"><i class="fas fa-dumbbell"></i><div><b>Training Session</b><br>Our gym time together is special.</div></div>
        <div class="activity-card"><i class="fas fa-moon"></i><div><b>Night Walk</b><br>Just walking and talking under the stars.</div></div>
        <div class="activity-card"><i class="fas fa-user-lock"></i><div><b>Private Time</b><br>Focusing only on our love.</div></div>
    </div>

    <div id="note" class="page">
        <h2 style="color: var(--primary-love);">From Amine</h2>
        <p>I am truly sorry. I want to spend every moment showing you how much I love you. You are my queen.</p>
        <button class="btn-love" onclick="celebrate()">I Forgive You ❤️</button>
    </div>

    <script>
        function show(id) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            document.getElementById('n-' + id).classList.add('active');
        }

        function toggleMusic() {
            const m = document.getElementById('bgMusic');
            m.paused ? (m.play(), mIcon.className="fas fa-pause") : (m.pause(), mIcon.className="fas fa-play");
        }

        // Memory Game Logic
        const cardsArray = ['🌶️', '🌶️', '💖', '💖', '🦋', '🦋', '🍟', '🍟', '⭐', '⭐', '🏃‍♀️', '🏃‍♀️'];
        let hasFlippedCard = false, lockBoard = false, firstCard, secondCard;
        const gameGrid = document.getElementById('gameGrid');

        cardsArray.sort(() => 0.5 - Math.random()).forEach(symbol => {
            const card = document.createElement('div');
            card.className = 'memory-card';
            card.dataset.symbol = symbol;
            card.innerHTML = `<div class="front">❓</div><div class="back">${symbol}</div>`;
            card.onclick = function() {
                if (lockBoard || this === firstCard) return;
                this.classList.add('flip');
                if (!hasFlippedCard) { hasFlippedCard = true; firstCard = this; return; }
                secondCard = this; checkForMatch();
            };
            gameGrid.appendChild(card);
        });

        function checkForMatch() {
            let isMatch = firstCard.dataset.symbol === secondCard.dataset.symbol;
            isMatch ? disableCards() : unflipCards();
        }

        function disableCards() { firstCard.onclick = null; secondCard.onclick = null; resetBoard(); }
        function unflipCards() {
            lockBoard = true;
            setTimeout(() => { firstCard.classList.remove('flip'); secondCard.classList.remove('flip'); resetBoard(); }, 1000);
        }
        function resetBoard() { [hasFlippedCard, lockBoard] = [false, false]; [firstCard, secondCard] = [null, null]; }

        function celebrate() {
            confetti({ particleCount: 200, spread: 100, origin: { y: 0.6 } });
            setTimeout(() => alert("I love you more than anything, Ryme! ❤️"), 500);
        }

        setInterval(() => {
            const h = document.createElement('div');
            h.className = 'heart-particle'; h.innerHTML = '❤️';
            h.style.left = Math.random() * 100 + 'vw'; h.style.fontSize = Math.random() * 10 + 15 + 'px';
            h.style.animationDuration = Math.random() * 3 + 3 + 's'; h.style.opacity = '0.4';
            document.body.appendChild(h); setTimeout(() => h.remove(), 5000);
        }, 800);
    </script>
</body>
</html>
