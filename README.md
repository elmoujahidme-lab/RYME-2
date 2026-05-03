<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Relationship Patch v2.0 | Deployment</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <style>
        :root {
            --primary: #ff4d6d;
            --secondary: #00f2ff;
            --bg: #0a0a0c;
            --success: #27c93f;
        }

        body {
            background-color: var(--bg);
            color: white;
            font-family: 'Segoe UI', sans-serif;
            margin: 0;
            overflow-x: hidden;
            display: flex;
            flex-direction: column;
            align-items: center;
            cursor: crosshair;
        }

        /* شريط التقدم (Trust Meter) */
        .progress-container {
            width: 100%;
            height: 5px;
            background: #1a1a1e;
            position: fixed;
            top: 0;
            z-index: 1000;
        }
        .progress-bar {
            height: 100%;
            width: 10%;
            background: linear-gradient(90deg, var(--secondary), var(--primary));
            transition: 0.5s;
            box-shadow: 0 0 10px var(--secondary);
        }

        .grid-bg {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background-image: linear-gradient(rgba(0, 242, 255, 0.03) 1px, transparent 1px),
                              linear-gradient(90deg, rgba(0, 242, 255, 0.03) 1px, transparent 1px);
            background-size: 30px 30px;
            z-index: -1;
        }

        .container {
            max-width: 600px;
            padding: 60px 20px;
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
            background: rgba(22, 22, 26, 0.95);
            padding: 40px;
            border-radius: 0 0 10px 10px;
            border: 1px solid #333;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
            border-top: none;
            backdrop-filter: blur(10px);
        }

        h1 { color: var(--secondary); font-family: 'Courier New', monospace; font-size: 1.4rem; }
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
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        .level { display: none; }
        .level.active { display: block; animation: fadeIn 0.8s; }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* قسم الذكريات المشفرة */
        .memories {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
        }
        .memory-item {
            font-size: 1.5rem;
            color: var(--secondary);
            cursor: help;
            position: relative;
        }
        .memory-item:hover::after {
            content: attr(data-hint);
            position: absolute;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--primary);
            color: white;
            padding: 5px 10px;
            font-size: 0.7rem;
            border-radius: 5px;
            white-space: nowrap;
        }

        .music-player {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 100;
        }

        /* قلوب تتبع الماوس */
        .heart-particle {
            position: fixed;
            pointer-events: none;
            color: var(--primary);
            font-size: 10px;
            animation: fly 1s linear forwards;
        }

        @keyframes fly {
            to { transform: translateY(-50px); opacity: 0; }
        }
    </style>
</head>
<body>

<div class="progress-container"><div class="progress-bar" id="pBar"></div></div>
<div class="grid-bg"></div>

<div class="music-player">
    <button class="btn" onclick="toggleMusic()"><i class="fas fa-music"></i> Music</button>
    <audio id="bgMusic" loop>
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-8.mp3" type="audio/mpeg">
    </audio>
</div>

<div class="container">
    <div class="terminal-header">
        <div class="dot red"></div><div class="dot yellow"></div><div class="dot green"></div>
    </div>
    
    <div class="terminal-body">
        <div id="level1" class="level active">
            <i class="fas fa-robot heart-icon" style="color: var(--secondary);"></i>
            <h1>[RYME_AZZMAN_OS]</h1>
            <p>> System Crash Detected in <b>Communication_Module</b>.</p>
            <p>> Error 404: Understanding not found.</p>
            <button class="btn" onclick="nextLevel(2, 30)">Run Diagnostics</button>
        </div>

        <div id="level2" class="level">
            <i class="fas fa-microchip heart-icon"></i>
            <h1>Logic Overhaul</h1>
            <p>I forgot that humans don't run on code. You were <b>shining</b> in your team, and I was stuck in my own loop.</p>
            <div class="memories">
                <i class="fas fa-graduation-cap memory-item" data-hint="Our shared classes"></i>
                <i class="fas fa-project-diagram memory-item" data-hint="Your brilliant energy"></i>
                <i class="fas fa-heart memory-item" data-hint="My true feelings"></i>
            </div>
            <button class="btn" onclick="nextLevel(3, 55)">Rewrite Memory</button>
        </div>

        <div id="level3" class="level">
            <i class="fas fa-code-merge heart-icon" style="color: #FFD700;"></i>
            <h1>Safety Protocol 2.0</h1>
            <p>No more "Silent Exits". No more unhandled exceptions.</p>
            <p>I value your passion more than any project result.</p>
            <button class="btn" onclick="nextLevel(4, 80)">Update Protocols</button>
        </div>

        <div id="level4" class="level">
            <i class="fas fa-fingerprint heart-icon" style="color: var(--secondary);"></i>
            <h1>Verification</h1>
            <h1>Do you still love your silly engineer?</h1>
            <div style="display: flex; justify-content: center; gap: 20px;">
                <button class="btn" onclick="nextLevel(5, 95)">YES, ALWAYS</button>
                <button id="run-btn-1" class="btn" onmouseover="moveButton('run-btn-1')">NO</button>
            </div>
        </div>

        <div id="level5" class="level">
            <i class="fas fa-unlock-alt heart-icon"></i>
            <h1>Final Patch</h1>
            <h1>Can we start a new 'Sprint' together?</h1>
            <div style="display: flex; justify-content: center; gap: 20px;">
                <button class="btn" onclick="finalCelebrate()">FORGIVEN</button>
                <button id="run-btn-2" class="btn" onmouseover="moveButton('run-btn-2')">STILL MAD</button>
            </div>
        </div>
    </div>
    
    <p style="font-family: monospace; font-size: 0.7rem; margin-top: 20px; color: #444;">
        // Localhost: Amine | Status: Repairing...
    </p>
</div>

<script>
    // تأثير القلوب عند تحريك الماوس
    document.addEventListener('mousemove', (e) => {
        if (Math.random() > 0.9) {
            const heart = document.createElement('i');
            heart.className = 'fas fa-heart heart-particle';
            heart.style.left = e.clientX + 'px';
            heart.style.top = e.clientY + 'px';
            document.body.appendChild(heart);
            setTimeout(() => heart.remove(), 1000);
        }
    });

    function nextLevel(lvl, progress) {
        const music = document.getElementById('bgMusic');
        if (music.paused) music.play().catch(e => {});
        
        document.getElementById('pBar').style.width = progress + '%';
        document.querySelectorAll('.level').forEach(l => l.classList.remove('active'));
        document.getElementById('level' + lvl).classList.add('active');
    }

    function moveButton(id) {
        const btn = document.getElementById(id);
        btn.style.position = 'fixed';
        btn.style.left = Math.random() * (window.innerWidth - 100) + 'px';
        btn.style.top = Math.random() * (window.innerHeight - 100) + 'px';
    }

    function finalCelebrate() {
        document.getElementById('pBar').style.width = '100%';
        confetti({ particleCount: 250, spread: 100, origin: { y: 0.6 } });
        
        const terminal = document.querySelector('.terminal-body');
        terminal.innerHTML = `
            <h1 style="color: var(--success);">COMMIT SUCCESSFUL!</h1>
            <div style="text-align: left; font-family: monospace; font-size: 0.8rem; background: #000; padding: 15px; border-radius: 5px; margin: 15px 0;">
                <span style="color: var(--secondary)">Author:</span> Amine<br>
                <span style="color: var(--secondary)">Status:</span> Fixed Ego Bug<br>
                <span style="color: var(--secondary)">Message:</span> Merged with Eternal Love for Ryme.
            </div>
            <p>I love you more than all the code in the world.</p>
            <i class="fas fa-check-circle" style="font-size: 4rem; color: var(--success);"></i>
        `;
    }

    function toggleMusic() {
        const music = document.getElementById('bgMusic');
        music.paused ? music.play() : music.pause();
    }
</script>
</body>
</html>
