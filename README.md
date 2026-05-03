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

        /* شريط التقدم العلوي */
        .progress-container {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 6px;
            background: #1a1a1e;
            z-index: 1000;
        }
        .progress-bar {
            height: 100%; width: 10%;
            background: linear-gradient(90deg, var(--secondary), var(--primary));
            box-shadow: 0 0 10px var(--secondary);
            transition: width 0.5s ease;
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
            padding: 60px 20px;
            text-align: center;
        }

        .terminal-header {
            background: #1a1a1e; padding: 10px;
            border-radius: 10px 10px 0 0;
            border: 1px solid #333;
            display: flex; gap: 8px;
        }

        .dot { width: 12px; height: 12px; border-radius: 50%; }
        .red { background: #ff5f56; }
        .yellow { background: #ffbd2e; }
        .green { background: #27c93f; }

        .terminal-body {
            background: #16161a; padding: 35px;
            border-radius: 0 0 10px 10px;
            border: 1px solid #333;
            box-shadow: 0 25px 60px rgba(0,0,0,0.7);
            border-top: none;
        }

        h1 { color: var(--secondary); font-family: 'Courier New', monospace; font-size: 1.4rem; }
        p { line-height: 1.6; color: #ccc; }

        .btn {
            background: transparent; border: 1px solid var(--primary);
            color: var(--primary); padding: 12px 30px;
            border-radius: 25px; cursor: pointer;
            font-weight: bold; transition: 0.3s;
            margin-top: 20px; text-transform: uppercase;
        }

        .btn:hover { background: var(--primary); color: white; box-shadow: 0 0 20px var(--primary); }

        .heart-icon { color: var(--primary); font-size: 3.5rem; margin: 20px 0; animation: pulse 1.5s infinite; }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.15); }
            100% { transform: scale(1); }
        }

        .level { display: none; }
        .level.active { display: block; animation: fadeIn 0.8s ease; }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }

        .music-player { position: fixed; bottom: 20px; right: 20px; z-index: 100; }
        #run-btn-1, #run-btn-2 { position: relative; }

        .commit-style {
            text-align: left; background: #000; padding: 15px;
            border-radius: 5px; font-family: monospace; font-size: 0.85rem;
            border-left: 3px solid var(--success); margin-top: 20px;
        }
    </style>
</head>
<body onmousemove="drawHeart(event)">

<div class="progress-container"><div class="progress-bar" id="myBar"></div></div>
<div class="grid-bg"></div>

<div class="music-player">
    <button class="btn" onclick="toggleMusic()"><i class="fas fa-music"></i> Music</button>
    <audio id="bgMusic"
