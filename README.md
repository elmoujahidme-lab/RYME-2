<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Our Special World</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --soft-pink: #fce4ec;
            --rose-gold: #e57373;
            --deep-love: #d81b60;
            --warm-cream: #fff9f9;
        }

        body {
            background: var(--warm-cream);
            color: #444;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
            -webkit-tap-highlight-color: transparent;
        }

        /* قلوب متساقطة رقيقة */
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

        /* شريط التنقل السفلي */
        .navbar {
            background: white;
            padding: 12px 0;
            display: flex;
            justify-content: space-around;
            position: fixed;
            bottom: 0;
            width: 100%;
            z-index: 1100;
            box-shadow: 0 -3px 15px rgba(0,0,0,0.06);
            border-radius: 20px 20px 0 0;
        }

        .nav-item {
            color: #bbb;
            text-decoration: none;
            font-size: 0.8rem;
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
            padding: 20px 20px 100px 20px;
            animation: fadeIn 0.6s ease-out;
            max-width: 450px;
            margin: auto;
        }

        .page.active { display: block; }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

        /* الهوية البصرية */
        .hero { text-align: center; padding: 70px 20px 40px 20px; }
        .hero i { font-size: 60px; color: var(--deep-love); margin-bottom: 20px; text-shadow: 0 5px 15px rgba(216,27,96,0.2); }
        
        /* لعبة الحب */
        .game-title { font-size: 1.2rem; color: var(--deep-love); margin-bottom: 20px; font-weight: bold; }
        .love-cards {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
        }

        .l-card {
            background: white;
            height: 140px;
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            box-shadow: 0 8px 20px rgba(0,0,0,0.04);
            cursor: pointer;
            border: 2px solid transparent;
            transition: 0.3s;
            padding: 10px;
            text-align: center;
        }

        .l-card i { font-size: 2rem; color: var(--rose-gold); margin-bottom: 10px; }
        .l-card span { font-size: 0.85rem; color: #666; font-weight: 500; }
        .l-card.clicked { border-color: var(--rose-gold); background: #fffafa; }

        /* الأنشطة المفضلة لريم */
        .activity-box {
            background: white;
            padding: 20px;
            margin: 15px 0;
            border-radius: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.02);
            display: flex;
            align-items: center;
            gap: 20px;
            text-align: left;
        }
        .activity-box i { background: var(--soft-pink); color: var(--deep-love); padding: 12px; border-radius: 15px; font-size: 1.2rem; }
        .act-text b { display: block; color: #333; margin-bottom: 4px; }
        .act-text span { font-size: 0.85rem; color: #888; }

        /* مشغل الموسيقى */
        .music-toggle {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            padding: 10px 18px;
            border-radius: 30px;
            z-index: 1200;
            display: flex;
            align-items: center;
            gap: 10px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
            font-size: 0.85rem;
            color: var(--deep-love);
            font-weight: bold;
        }

        .btn-confirm {
            background: var(--deep-love);
            color: white;
            border: none;
            padding: 18px;
            border-radius: 35px;
            font-weight: bold;
            width: 100%;
            margin-top: 40px;
            box-shadow: 0 6px 20px rgba(216, 27, 96, 0.25);
            font-size: 1rem;
        }

        h1 { color: var(--deep-love); font-family: 'Times New Roman', serif; font-size: 2.2rem; margin-bottom: 10px; }
        p.intro { color: #777; font-size: 0.95rem; line-height: 1.6; }
    </style>
</head>
<body>

    <div class="music-toggle" onclick="toggleMusic()">
        <i id="mIcon" class="fas fa-play"></i>
        <span id="mText">Quiet Piano</span>
        <audio id="bgMusic" loop>
            <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-15.mp3" type="audio/mpeg">
        </audio>
    </div>

    <div class="navbar">
        <a href="javascript:void(0)" class="nav-item active" id="n-home" onclick="go('home')">
            <i class="fas fa-heart"></i><span>Ryme</span>
        </a>
        <a href="javascript:void(0)" class="nav-item" id="n-game" onclick="go('game')">
            <i class="fas fa-magic"></i><span>Moments</span>
        </a>
        <a href="javascript:void(0)" class="nav-item" id="n-plans" onclick="go('plans')">
            <i class="fas fa-stars"></i><span>Dates</span>
        </a>
        <a href="javascript:void(0)" class="nav-item" id="n-love" onclick="go('love')">
            <i class="fas fa-envelope"></i><span>Note</span>
        </a>
    </div>

    <div id="home" class="page active">
        <div class="hero">
            <i class="fas fa-hand-holding-heart"></i>
            <h1>For Ryme</h1>
            <p class="intro">I made this space for you. No code, no stress, just my love for you. Every button and card here is a piece of my heart.</p>
        </div>
    </div>

    <div id="game" class="page">
        <div class="game-title">Things I Love About Us</div>
        <div class="love-cards">
            <div class="l-card" onclick="this.classList.toggle('clicked')">
                <i class="fas fa-utensils"></i>
                <span>Our spicy fries dates</span>
            </div>
            <div class="l-card" onclick="this.classList.toggle('clicked')">
                <i class="fas fa-running"></i>
                <span>Training together</span>
            </div>
            <div class="l-card" onclick="this.classList.toggle('clicked')">
                <i class="fas fa-moon"></i>
                <span>Late night walks</span>
            </div>
            <div class="l-card" onclick="this.classList.toggle('clicked')">
                <i class="fas fa-user-friends"></i>
                <span>Just being alone</span>
            </div>
        </div>
    </div>

    <div id="plans" class="page">
        <div class="game-title">Our Next Adventures</div>
        <div class="activity-box">
            <i class="fas fa-fire"></i>
            <div class="act-text"><b>Spicy Fries Night</b><span>Salte, spicy, and extra hot - just how you like it.</span></div>
        </div>
        <div class="activity-box">
            <i class="fas fa-dumbbell"></i>
            <div class="act-text"><b>Gym Partners</b><span>Working out together is better than anything.</span></div>
        </div>
        <div class="activity-box">
            <i class="fas fa-shoe-prints"></i>
            <div class="act-text"><b>Night Escapes</b><span>Walking under the stars, just me and you.</span></div>
        </div>
        <div class="activity-box">
            <i class="fas fa-lock"></i>
            <div class="act-text"><b>Private Time</b><span>Focusing only on us, no world outside.</span></div>
        </div>
    </div>

    <div id="love" class="page">
        <div class="game-title">From Amine's Heart</div>
        <p class="intro">I'm sorry for everything that made you sad. I want to show you how much I truly love you, not in words, but in how I treat you every single day.</p>
        <p class="intro">You are my queen, and your happiness is my priority.</p>
        <button class="btn-confirm" onclick="celebrate()">Accept My Love ❤️</button>
    </div>

    <script>
        function go(id) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
            document.getElementById(id).classList.add('active');
            document.getElementById('n-' + id).classList.add('active');
            window.scrollTo(0,0);
        }

        function toggleMusic() {
            const m = document.getElementById('bgMusic');
            const icon = document.getElementById('mIcon');
            const text = document.getElementById('mText');
            if (m.paused) {
                m.play();
                icon.className = "fas fa-pause";
                text.innerText = "Enjoy Piano";
            } else {
                m.pause();
                icon.className = "fas fa-play";
                text.innerText = "Quiet Piano";
            }
        }

        function celebrate() {
            confetti({ particleCount: 250, spread: 100, origin: { y: 0.6 }, colors: ['#d81b60', '#e57373', '#ffffff'] });
            setTimeout(() => { alert("I love you, Ryme! ❤️"); }, 500);
        }

        function createHeart() {
            const h = document.createElement('div');
            h.className = 'heart-particle';
            h.innerHTML = '❤️';
            h.style.left = Math.random() * 100 + 'vw';
            h.style.fontSize = (Math.random() * 10 + 12) + 'px';
            h.style.animationDuration = (Math.random() * 3 + 3) + 's';
            h.style.opacity = Math.random() * 0.5 + 0.3;
            document.body.appendChild(h);
            setTimeout(() => h.remove(), 6000);
        }
        setInterval(createHeart, 800);
    </script>
</body>
</html>
