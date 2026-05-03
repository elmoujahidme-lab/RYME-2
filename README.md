<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Message for Ryme</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --primary: #ff4d6d;
            --secondary: #00f2ff;
            --bg: #0a0a0c;
        }

        body {
            background-color: var(--bg);
            color: white;
            font-family: 'Segoe UI', Arial, sans-serif;
            margin: 0;
            overflow-x: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            touch-action: manipulation; /* لتحسين اللمس على الهاتف */
        }

        /* شريط التقدم علوي */
        .progress-container {
            width: 100%; height: 4px; background: #1a1a1e;
            position: fixed; top: 0; z-index: 1000;
        }
        .progress-bar {
            height: 100%; width: 10%; background: var(--primary);
            transition: 0.5s; box-shadow: 0 0 10px var(--primary);
        }

        .container {
            width: 90%; /* تناسب الهاتف */
            max-width: 400px;
            margin-top: 50px;
            text-align: center;
        }

        .terminal-body {
            background: rgba(22, 22, 26, 0.98);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid #333;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        h1 { color: var(--secondary); font-size: 1.2rem; margin-bottom: 15px; }
        p { font-size: 0.95rem; line-height: 1.5; color: #ddd; }

        .btn {
            background: var(--primary);
            border: none;
            color: white;
            padding: 15px 25px;
            border-radius: 30px;
            cursor: pointer;
            font-weight: bold;
            margin-top: 20px;
            width: 100%; /* أسهل للضغط على الهاتف */
            font-size: 1rem;
        }

        .heart-icon {
            color: var(--primary);
            font-size: 2.5rem;
            margin: 15px 0;
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        .level { display: none; }
        .level.active { display: block; }

        .music-player {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 100;
        }

        .music-btn {
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid white;
            color: white;
            padding: 10px;
            border-radius: 50%;
            width: 45px; height: 45px;
        }

        #run-btn-1, #run-btn-2 { 
            background: transparent; 
            border: 1px solid #555; 
            color: #888;
        }
    </style>
</head>
<body>

<div class="progress-container"><div class="progress-bar" id="pBar"></div></div>

<div class="music-player">
    <button class="music-btn" onclick="toggleMusic()"><i class="fas fa-music"></i></button>
    <audio id="bgMusic" loop>
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-15.mp3" type="audio/mpeg">
    </audio>
</div>

<div class="container">
    <div class="terminal-body">
        <div id="level1" class="level active">
            <i class="fas fa-heart heart-icon"></i>
            <h1>Hello Ryme...</h1>
            <p>I am sorry for what happened in class. I made a mistake and I want to fix it.</p>
            <button class="btn" onclick="nextLevel(2, 40)">Click to start</button>
        </div>

        <div id="level2" class="level">
            <i class="fas fa-star heart-icon" style="color: gold;"></i>
            <h1>You were amazing!</h1>
            <p>You worked hard and did a great job with your team. I should have been proud of you instead of being upset.</p>
            <button class="btn" onclick="nextLevel(3, 70)">Next</button>
        </div>

        <div id="level3" class="level">
            <i class="fas fa-user-shield heart-icon" style="color: var(--secondary);"></i>
            <h1>My Promise</h1>
            <p>I will always respect your feelings. No more silence, only love and support.</p>
            <button class="btn" onclick="nextLevel(4, 90)">Almost there...</button>
        </div>

        <div id="level4" class="level">
            <h1>Do you still love me?</h1>
            <button class="btn" onclick="nextLevel(5, 100)">YES</button>
            <button id="run-btn-1" class="btn" onmouseover="moveButton('run-btn-1')" onclick="moveButton('run-btn-1')">NO</button>
        </div>

        <div id="level5" class="level">
            <h1>Do you forgive me?</h1>
            <button class="btn" onclick="finalCelebrate()">I forgive you</button>
            <button id="run-btn-2" class="btn" onmouseover="moveButton('run-btn-2')" onclick="moveButton('run-btn-2')">Still mad</button>
        </div>
    </div>
</div>

<script>
    function nextLevel(lvl, progress) {
        const music = document.getElementById('bgMusic');
        if (music.paused) music.play().catch(e => {});

        document.getElementById('pBar').style.width = progress + '%';
        document.querySelectorAll('.level').forEach(l => l.classList.remove('active'));
        document.getElementById('level' + lvl).classList.add('active');
    }

    function moveButton(id) {
        const btn = document.getElementById(id);
        // جعل الحركة أصغر لتناسب شاشة الهاتف
        btn.style.position = 'absolute';
        btn.style.left = Math.random() * 60 + '%';
        btn.style.top = Math.random() * 60 + '%';
    }

    function finalCelebrate() {
        confetti({ particleCount: 150, spread: 70, origin: { y: 0.6 } });
        const terminal = document.querySelector('.terminal-body');
        terminal.innerHTML = `
            <i class="fas fa-check-circle" style="font-size: 3rem; color: #27c93f;"></i>
            <h1 style="color: #27c93f;">Thank you, Ryme!</h1>
            <p>I love you so much. Let's start fresh and be happy again.</p>
            <p style="font-size: 0.8rem; color: #666;">-- Your Amine --</p>
        `;
    }

    function toggleMusic() {
        const music = document.getElementById('bgMusic');
        music.paused ? music.play() : music.pause();
    }
</script>
</body>
</html>
