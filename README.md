<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For My Beautiful Ryme</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        body {
            margin: 0;
            padding: 0;
            background: #fff5f7; /* لون وردي ناعم جداً */
            font-family: 'Georgia', serif;
            color: #4a4a4a;
            display: flex;
            flex-direction: column;
            align-items: center;
            overflow-x: hidden;
        }

        .header {
            padding: 40px 20px;
            text-align: center;
        }

        .header h1 {
            font-size: 1.8rem;
            color: #d63384;
            margin-bottom: 10px;
        }

        .header p {
            font-style: italic;
            font-size: 1rem;
            color: #888;
        }

        /* لعبة البطاقات */
        .game-container {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            padding: 20px;
            width: 90%;
            max-width: 400px;
        }

        .card {
            background: white;
            height: 120px;
            border-radius: 15px;
            display: flex;
            justify-content: center;
            align-items: center;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            cursor: pointer;
            transition: transform 0.3s;
            position: relative;
            border: 1px solid #ffe0e6;
        }

        .card i {
            font-size: 2rem;
            color: #ff85a2;
        }

        .card-content {
            display: none;
            padding: 10px;
            text-align: center;
            font-size: 0.9rem;
            color: #d63384;
            font-weight: bold;
        }

        .card.flipped {
            transform: rotateY(180deg);
            background: #fff0f3;
        }

        .card.flipped i { display: none; }
        .card.flipped .card-content { 
            display: block; 
            transform: rotateY(180deg); 
        }

        /* زر الموسيقى */
        .music-player {
            position: fixed;
            bottom: 20px;
            background: white;
            padding: 10px 20px;
            border-radius: 30px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            display: flex;
            align-items: center;
            gap: 10px;
            cursor: pointer;
            z-index: 100;
        }

        .final-message {
            display: none;
            text-align: center;
            padding: 40px 20px;
            animation: fadeIn 1s;
        }

        @keyframes fadeIn {
            from { opacity: 0; } to { opacity: 1; }
        }

        .btn-restart {
            margin-top: 20px;
            padding: 10px 25px;
            background: #d63384;
            color: white;
            border: none;
            border-radius: 20px;
            font-size: 1rem;
        }
    </style>
</head>
<body>

    <div class="music-player" onclick="toggleMusic()">
        <i class="fas fa-music" style="color: #d63384;"></i>
        <span style="font-size: 0.8rem; font-weight: bold;">Tap for Music</span>
        <audio id="loveAudio" loop>
            <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-8.mp3" type="audio/mpeg">
        </audio>
    </div>

    <div id="main-content">
        <div class="header">
            <h1>Thinking of You</h1>
            <p>I made this simple game to remind us of the good things. Tap the cards to reveal what's inside...</p>
        </div>

        <div class="game-container" id="game">
            <div class="card" onclick="flipCard(this)">
                <i class="fas fa-heart"></i>
                <div class="card-content">The way you smile makes my day.</div>
            </div>
            <div class="card" onclick="flipCard(this)">
                <i class="fas fa-star"></i>
                <div class="card-content">I'm so proud of your hard work.</div>
            </div>
            <div class="card" onclick="flipCard(this)">
                <i class="fas fa-cloud"></i>
                <div class="card-content">I'm sorry for being silly lately.</div>
            </div>
            <div class="card" onclick="flipCard(this)">
                <i class="fas fa-moon"></i>
                <div class="card-content">You are my best friend and love.</div>
            </div>
        </div>
    </div>

    <div id="final-message" class="final-message">
        <i class="fas fa-envelope-open-heart" style="font-size: 4rem; color: #d63384;"></i>
        <h2 style="color: #d63384;">To Ryme, My Everything</h2>
        <p>This was just a small way to say I love you and I value every moment with you. Can we forget the bad days and focus on the beautiful ones?</p>
        <p style="font-size: 1.2rem; color: #ff85a2;">❤️ I Love You ❤️</p>
        <button class="btn-restart" onclick="location.reload()">See the cards again</button>
    </div>

    <script>
        let flippedCount = 0;

        function toggleMusic() {
            const audio = document.getElementById('loveAudio');
            if (audio.paused) {
                audio.play();
                document.querySelector('.music-player span').innerText = "Music is Playing...";
            } else {
                audio.pause();
                document.querySelector('.music-player span').innerText = "Music Paused";
            }
        }

        function flipCard(card) {
            if (!card.classList.contains('flipped')) {
                card.classList.add('flipped');
                flippedCount++;

                // تشغيل الموسيقى تلقائياً عند أول تفاعل
                const audio = document.getElementById('loveAudio');
                if (audio.paused) audio.play();

                if (flippedCount === 4) {
                    setTimeout(showFinalMessage, 1500);
                }
            }
        }

        function showFinalMessage() {
            confetti({
                particleCount: 150,
                spread: 70,
                origin: { y: 0.6 },
                colors: ['#d63384', '#ff85a2', '#ffffff']
            });
            document.getElementById('main-content').style.display = 'none';
            document.getElementById('final-message').style.display = 'block';
        }
    </script>
</body>
</html>
