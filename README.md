<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Relationship Patch v2.0</title>
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
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            overflow-x: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .grid-bg {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-image: linear-gradient(rgba(0, 242, 255, 0.05) 1px, transparent 1px),
                              linear-gradient(90deg, rgba(0, 242, 255, 0.05) 1px, transparent 1px);
            background-size: 30px 30px;
            z-index: -1;
        }

        .container {
            max-width: 600px;
            padding: 40px 20px;
            text-align: center;
        }

        .terminal-header {
            background: #1a1a1e;
            padding: 10px;
            border-radius: 10px 10px 0 0;
            border: 1px solid #333;
            display: flex; gap: 8px;
        }

        .dot { width: 12px; height: 12px; border-radius: 50%; }
        .red { background: #ff5f56; }
        .yellow { background: #ffbd2e; }
        .green { background: #27c93f; }

        .terminal-body {
            background: #16161a;
            padding: 30px;
            border-radius: 0 0 10px 10px;
            border: 1px solid #333;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
            border-top: none;
        }

        h1 { color: var(--secondary); font-family: 'Courier New', Courier, monospace; font-size: 1.5rem; }
        p { line-height: 1.6; color: #ccc; }

        .btn {
            background: transparent;
            border: 1px solid var(--primary);
            color: var(--primary);
            padding: 12px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-weight: bold;
            transition: 0.3s;
            margin-top: 20px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn:hover {
            background: var(--primary);
            color: white;
            box-shadow: 0 0 20px var(--primary);
        }

        .heart-icon {
            color: var(--primary);
            font-size: 3rem;
            margin: 20px 0;
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); }
            100% { transform: scale(1); }
        }

        .level { display: none; }
        .level.active { display: block; animation: fadeIn 0.8s; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .music-player {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 100;
        }

        #run-btn { position: relative; }
    </style>
</head>
<body>

<div class="grid-bg"></div>

<div class="music-player">
    <button class="btn" onclick="toggleMusic()"><i class="fas fa-music"></i> Play Music</button>
    <audio id="bgMusic" loop preload="auto">
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-8.mp3" type="audio/mpeg">
    </audio>
</div>

<div class="container">
    <div class="terminal-header">
        <div class="dot red"></div>
        <div class="dot yellow"></div>
        <div class="dot green"></div>
    </div>
    
    <div class="terminal-body">
        
        <div id="level1" class="level active">
            <i class="fas fa-code-branch heart-icon" style="color: var(--secondary);"></i>
            <h1>[RYME AZZMAN]</h1>
            <p>> Detecting 1 Critical Error in <b>Heart_Sync</b> module...</p>
            <p>> A conflict was found between <b>Logic.exe</b> and <b>Emotions.lib</b>.</p>
            <button class="btn" onclick="nextLevel(2)">Initialize Debugging</button>
        </div>

        <div id="level2" class="level">
            <i class="fas fa-heart heart-icon"></i>
            <h1>The "Ego Bug" Fix</h1>
            <p>I realized my code was wrong. I was looking at the process instead of your happiness.</p>
            <p>You weren't "acting", you were <b>shining</b>. I should have been your biggest fan.</p>
            <button class="btn" onclick="nextLevel(3)">Merge Changes?</button>
        </div>

        <div id="level3" class="level">
            <i class="fas fa-shield-alt heart-icon" style="color: #FFD700;"></i>
            <h1>Security Protocol</h1>
            <p>I promise to never make you hide your feelings. Your tears are a 'System Crash' I can't afford.</p>
            <p>Update to <b>v2.0</b>: More trust, less comparison.</p>
            <button class="btn" onclick="nextLevel(4)">Update System</button>
        </div>

        <div id="level4" class="level">
            <i class="fas fa-question-circle heart-icon" style="color: var(--secondary);"></i>
            <h1>Verification Required</h1>
            <h1>Do you still love me?</h1>
            <div style="display: flex; justify-content: center; gap: 20px;">
                <button class="btn" onclick="nextLevel(5)">Yes, I do</button>
                <button id="run-btn-1" class="btn" onmouseover="moveButton('run-btn-1')">No</button>
            </div>
        </div>

        <div id="level5" class="level">
            <i class="fas fa-kiss-wink-heart heart-icon"></i>
            <h1>Final Confirmation</h1>
            <h1>So... do you forgive me?</h1>
            <div style="display: flex; justify-content: center; gap: 20px;">
                <button class="btn" onclick="finalCelebrate()">I Forgive You</button>
                <button id="run-btn-2" class="btn" onmouseover="moveButton('run-btn-2')">Still Mad</button>
            </div>
        </div>

    </div>
    
    <p style="font-family: monospace; font-size: 0.8rem; margin-top: 20px; color: #555;">
        -- Local Host: Your Favorite Engineer Amine --
    </p>
</div>

<script>
    function nextLevel(lvl) {
        const music = document.getElementById('bgMusic');
        if (music.paused) {
            music.play().catch(e => console.log("Audio deferred"));
        }
        document.querySelectorAll('.level').forEach(l => l.classList.remove('active'));
        document.getElementById('level' + lvl).classList.add('active');
    }

    // تعديل الدالة لتعمل مع أي زر
    function moveButton(id) {
        const btn = document.getElementById(id);
        const x = Math.random() * (window.innerWidth - btn.clientWidth - 100);
        const y = Math.random() * (window.innerHeight - btn.clientHeight - 100);
        btn.style.position = 'fixed';
        btn.style.left = x + 'px';
        btn.style.top = y + 'px';
    }

    function finalCelebrate() {
        confetti({
            particleCount: 200,
            spread: 80,
            origin: { y: 0.6 },
            colors: ['#ff4d6d', '#00f2ff', '#ffffff']
        });
        
        const terminal = document.querySelector('.terminal-body');
        terminal.innerHTML = `
            <h1 style="color: #27c93f;">SYSTEM STABILIZED</h1>
            <p>Connection fully restored. Love.exe is running perfectly.</p>
            <p>I love you more than words (and code) can say, Ryme.</p>
            <i class="fas fa-check-circle" style="font-size: 4rem; color: #27c93f; margin-top: 15px;"></i>
        `;
    }

    function toggleMusic() {
        const music = document.getElementById('bgMusic');
        if (music.paused) {
            music.play();
        } else {
            music.pause();
        }
    }
</script>
</body>
</html>
