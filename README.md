<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Our Special Place</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --soft-pink: #fce4ec;
            --rose-gold: #e57373;
            --deep-love: #d81b60;
            --cream: #fff9fb;
        }

        body {
            background: var(--cream);
            color: #444;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
        }

        /* Falling Hearts Background */
        .heart-particle {
            position: fixed;
            top: -10px;
            pointer-events: none;
            animation: fall linear forwards;
            z-index: 1000;
        }

        @keyframes fall {
            to { transform: translateY(105vh) rotate(360deg); }
        }

        /* Navbar for multiple pages */
        .navbar {
            background: white;
            padding: 10px 0;
            display: flex;
            justify-content: space-around;
            position: fixed;
            bottom: 0;
            width: 100%;
            z-index: 1000;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.05);
        }

        .nav-item {
            color: #888;
            text-decoration: none;
            font-size: 0.75rem;
            font-weight: bold;
            display: flex;
            flex-direction: column;
            align-items: center;
            transition: 0.3s;
        }

        .nav-item.active {
            color: var(--deep-love);
        }

        .page {
            display: none;
            padding: 20px 20px 80px 20px;
            animation: fadeIn 0.5s ease-in;
            max-width: 500px;
            margin: auto;
        }

        .page.active { display: block; }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        /* Sections Styling */
        .hero { text-align: center; padding: 60px 20px; }
        .hero i { font-size: 60px; color: var(--deep-love); margin-bottom: 20px; }
        
        .card-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-top: 20px;
        }

        .card {
            background: white;
            height: 120px;
            border-radius: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 30px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
            cursor: pointer;
            transition: transform 0.3s;
        }

        .card:active { transform: scale(0.95); }

        .activity-card {
            background: white;
            padding: 20px;
            margin: 15px 0;
            border-radius: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.03);
            text-align: left;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .activity-card i { color: var(--rose-gold); font-size: 1.5rem; }

        /* Music Controls */
        .music-bar {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.8);
            backdrop-filter: blur(5px);
            padding: 8px 15px;
            border-radius: 25px;
            z-index: 1100;
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 0.8rem;
            border: 1px solid var(--soft-pink);
        }

        .btn-main {
            background: var(--deep-love);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 30px;
            font-weight: bold;
            width: 100%;
            margin-top: 30px;
            box-shadow: 0 4px 15px rgba(216, 27, 96, 0.3);
        }

        h1 { color: var(--deep-love); font-family: 'Georgia', serif; }
        h2 { color: var(--rose-gold); margin-bottom: 5px; }
        p.subtitle { color: #888; font-size: 0.9rem; margin-top: 0; }
    </style>
</head>
<body>

    <div class="music-bar" onclick="toggleMusic()">
        <i id="musicIcon" class="fas fa-play"></i>
        <span id="musicText">Tap for Music</span>
        <audio id="bgMusic" loop>
            <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-15.mp3" type="audio/mpeg">
        </audio>
    </div>

    <div class="navbar">
        <a href="javascript:void(0)" class="nav-item active" id="nav-home" onclick="showPage('home')">
            <i class="fas fa-heart"></i><span>Home</span>
        </a>
        <a href="javascript:void(0)" class="nav-item" id="nav-game" onclick="showPage('game')">
            <i class="fas fa-puzzle-piece"></i><span>Fun</span>
        </a>
        <a href="javascript:void(0)" class="nav-item" id="nav-bucket" onclick="showPage('bucket')">
            <i class="fas fa-star"></i><span>Plans</span>
        </a>
        <a href="javascript:void(0)" class="nav-item" id="nav-letter" onclick="showPage('letter')">
            <i class="fas fa-envelope-open"></i><span>Note</span>
        </a>
    </div>

    <!-- Home Page -->
    <div id="home" class="page active">
        <div class="hero">
            <i class="fas fa-crown"></i>
            <h1>For Ryme</h1>
            <p>I wanted to create a place that is as soft and beautiful as you are. A place where we can forget the world and just be "us".</p>
        </div>
    </div>

    <!-- Game Page -->
    <div id="game" class="page">
        <h1>Mini Game</h1>
        <p class="subtitle">Flip the cards to find our happiness symbols.</p>
        <div class="card-grid" id="gameGrid"></div>
    </div>

    <!-- Bucket List Page -->
    <div id="bucket" class="page">
        <h1>Our Future</h1>
        <p class="subtitle">Activities I want to do with you very soon:</p>
        <div class="activity-card"><i class="fas fa-mug-hot"></i><div><b>Coffee Date</b><br>Just us talking for hours.</div></div>
        <div class="activity-card"><i class="fas fa-moon"></i><div><b>Night Walk</b><br>Watching the stars together.</div></div>
        <div class="activity-card"><i class="fas fa-cookie-bite"></i><div><b>Baking Session</b><br>Making something sweet.</div></div>
        <div class="activity-card"><i class="fas fa-camera-retro"></i><div><b>Photoshoot</b><br>Capturing your beautiful smile.</div></div>
    </div>

    <!-- Special Letter Page -->
    <div id="letter" class="page">
        <h1>A Small Note</h1>
        <p>I am truly sorry. My world is much brighter when you are happy. I promise to be better and more supportive of everything you do.</p>
        <p>Will you give us a fresh start today?</p>
        <button class="btn-main" onclick="celebrate()">I Forgive You ❤️</button>
    </div>

    <script>
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            document.getElementById('nav-' + pageId).classList.add('active');
            window.scrollTo(0,0);
        }

        function toggleMusic() {
            const music = document.getElementById('bgMusic');
            const icon = document.getElementById('musicIcon');
            const text = document.getElementById('musicText');
            if (music.paused) {
                music.play();
                icon.className = "fas fa-pause";
                text.innerText = "Quiet Piano On";
            } else {
                music.pause();
                icon.className = "fas fa-play";
                text.innerText = "Music Paused";
            }
        }

        // Memory Game
        const symbols = ['🌸', '🌸', '💖', '💖', '✨', '✨', '🦋', '🦋'];
        const grid = document.getElementById('gameGrid');
        symbols.sort(() => Math.random() - 0.5);

        symbols.forEach(s => {
            const card = document.createElement('div');
            card.className = 'card';
            card.innerText = '☁️';
            card.onclick = () => {
                if(card.innerText === '☁️') {
                    card.innerText = s;
                    card.style.background = '#fff';
                    card.style.border = '2px solid var(--soft-pink)';
                } else {
                    card.innerText = '☁️';
                    card.style.background = 'white';
                    card.style.border = 'none';
                }
            };
            grid.appendChild(card);
        });

        function celebrate() {
            confetti({
                particleCount: 200,
                spread: 100,
                origin: { y: 0.6 },
                colors: ['#d81b60', '#e57373', '#ffffff']
            });
            setTimeout(() => {
                alert("Thank you for being you, Ryme! ❤️");
            }, 500);
        }

        // Falling Hearts logic
        function createHeart() {
            const h = document.createElement('div');
            h.className = 'heart-particle';
            h.innerHTML = '❤️';
            h.style.left = Math.random() * 100 + 'vw';
            h.style.fontSize = (Math.random() * 10 + 10) + 'px';
            h.style.animationDuration = (Math.random() * 3 + 2) + 's';
            h.style.opacity = Math.random();
            document.body.appendChild(h);
            setTimeout(() => h.remove(), 5000);
        }
        setInterval(createHeart, 600);
    </script>
</body>
</html>
