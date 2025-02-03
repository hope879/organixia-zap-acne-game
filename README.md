<!DOCTYPE html>
<html>
<head>
    <title>Zap Acne! - Organixia</title>
    <style>
        body {
            background: url('https://example.com/skincare-bg.jpg');
            margin: 0;
            overflow: hidden;
        }
        #game-container {
            width: 300px;
            height: 500px;
            position: relative;
        }
        .acne {
            width: 50px;
            height: 50px;
            position: absolute;
            cursor: pointer;
            background: url('https://example.com/acne-icon.png');
            animation: float 3s infinite;
        }
        #score {
            color: #ff69b4;
            font-size: 24px;
            position: absolute;
            top: 10px;
            left: 10px;
        }
        #timer {
            color: #ff69b4;
            font-size: 24px;
            position: absolute;
            top: 10px;
            right: 10px;
        }
        @keyframes float {
            0% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0); }
        }
    </style>
</head>
<body>
    <div id="game-container">
        <div id="score">Score: 0</div>
        <div id="timer">Time: 30</div>
    </div>

    <script>
        let score = 0;
        let timeLeft = 30;
        const targetScore = 15; // Score needed to win discount
        
        // Spawn acne randomly
        function createAcne() {
            const acne = document.createElement('div');
            acne.className = 'acne';
            acne.style.left = Math.random() * 250 + 'px';
            acne.style.top = Math.random() * 450 + 'px';
            
            acne.onclick = () => {
                score++;
                document.getElementById('score').textContent = `Score: ${score}`;
                acne.remove();
                if(score >= targetScore) showDiscount();
            };
            
            document.getElementById('game-container').appendChild(acne);
        }

        // Game timer
        const timer = setInterval(() => {
            timeLeft--;
            document.getElementById('timer').textContent = `Time: ${timeLeft}`;
            if(timeLeft <= 0) endGame();
        }, 1000);

        // Spawn acne every 0.8 seconds
        setInterval(createAcne, 800);

        function showDiscount() {
            clearInterval(timer);
            document.getElementById('game-container').innerHTML = `
                <div style="text-align:center; padding-top:200px;">
                    <h2>🎉 You won!</h2>
                    <p>Use code: GLOW20</p>
                    <p>20% OFF Organixia Acne Care Kit</p>
                    <button onclick="window.location.href='https://organixia.com'">CLAIM NOW</button>
                </div>
            `;
        }

        function endGame() {
            document.getElementById('game-container').innerHTML = `
                <div style="text-align:center; padding-top:200px;">
                    <h2>Time's up! 😢</h2>
                    <p>Try again to unlock your discount!</p>
                </div>
            `;
        }
    </script>
</body>
</html>
