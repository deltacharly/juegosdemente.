<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="theme-color" content="#667eea">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <title>¡Juegos de Mente! 🧠</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@700&display=swap');
        
        * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        
        body {
            font-family: 'Nunito', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            overflow: hidden;
            position: relative;
            touch-action: manipulation;
        }
        
        .bubbles {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: 0;
        }
        
        .bubble {
            position: absolute;
            bottom: -100px;
            background: rgba(255,255,255,0.1);
            border-radius: 50%;
            animation: rise 15s infinite ease-in;
        }
        
        @keyframes rise {
            0% { bottom: -100px; transform: translateX(0); }
            50% { transform: translateX(100px); }
            100% { bottom: 1080px; transform: translateX(-200px); }
        }
        
        .container {
            position: relative;
            z-index: 10;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 20px;
        }
        
        .character-container {
            position: relative;
            width: 250px;
            height: 250px;
            margin-bottom: 20px;
        }
        
        .character {
            width: 100%;
            height: 100%;
            background: linear-gradient(145deg, #FFD93D, #F6AD55);
            border-radius: 50%;
            position: relative;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            animation: bounce 2s infinite, float 3s ease-in-out infinite;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }
        
        @keyframes float {
            0%, 100% { transform: translateX(0); }
            50% { transform: translateX(10px); }
        }
        
        .face {
            position: relative;
            width: 160px;
            height: 120px;
        }
        
        .eyes {
            display: flex;
            justify-content: space-around;
            margin-top: 30px;
        }
        
        .eye {
            width: 35px;
            height: 45px;
            background: white;
            border-radius: 50%;
            position: relative;
            animation: blink 4s infinite;
        }
        
        @keyframes blink {
            0%, 96%, 100% { transform: scaleY(1); }
            98% { transform: scaleY(0.1); }
        }
        
        .pupil {
            width: 18px;
            height: 22px;
            background: #333;
            border-radius: 50%;
            position: absolute;
            top: 12px;
            left: 8px;
            animation: lookAround 5s infinite;
        }
        
        @keyframes lookAround {
            0%, 100% { transform: translate(0, 0); }
            25% { transform: translate(5px, -5px); }
            50% { transform: translate(-5px, 5px); }
            75% { transform: translate(5px, 5px); }
        }
        
        .mouth {
            width: 70px;
            height: 35px;
            background: #FF6B6B;
            border-radius: 0 0 70px 70px;
            margin: 15px auto;
            position: relative;
            overflow: hidden;
            animation: smile 2s infinite;
        }
        
        @keyframes smile {
            0%, 100% { width: 70px; height: 35px; }
            50% { width: 80px; height: 45px; }
        }
        
        .tongue {
            width: 35px;
            height: 18px;
            background: #FF8E8E;
            border-radius: 50%;
            position: absolute;
            bottom: -5px;
            left: 17px;
        }
        
        .cheeks {
            position: absolute;
            width: 100%;
            top: 65px;
            display: flex;
            justify-content: space-between;
            padding: 0 15px;
        }
        
        .cheek {
            width: 25px;
            height: 15px;
            background: rgba(255, 107, 107, 0.6);
            border-radius: 50%;
        }
        
        .arms {
            position: absolute;
            width: 100%;
            top: 50%;
            pointer-events: none;
        }
        
        .arm {
            width: 50px;
            height: 80px;
            background: linear-gradient(145deg, #FFD93D, #F6AD55);
            border-radius: 25px;
            position: absolute;
            transform-origin: top center;
        }
        
        .arm.left {
            left: -25px;
            transform: rotate(-30deg);
            animation: waveLeft 2s infinite;
        }
        
        .arm.right {
            right: -25px;
            transform: rotate(30deg);
            animation: waveRight 2s infinite;
        }
        
        @keyframes waveLeft {
            0%, 100% { transform: rotate(-30deg); }
            50% { transform: rotate(-50deg); }
        }
        
        @keyframes waveRight {
            0%, 100% { transform: rotate(30deg); }
            50% { transform: rotate(50deg); }
        }
        
        .speech-bubble {
            background: white;
            border-radius: 25px;
            padding: 25px;
            max-width: 90%;
            width: 100%;
            max-width: 500px;
            text-align: center;
            box-shadow: 0 10px 40px rgba(0,0,0,0.2);
            position: relative;
            margin-bottom: 20px;
            animation: popIn 0.5s ease-out;
        }
        
        @keyframes popIn {
            0% { transform: scale(0); opacity: 0; }
            80% { transform: scale(1.1); }
            100% { transform: scale(1); opacity: 1; }
        }
        
        .speech-bubble::before {
            content: '';
            position: absolute;
            bottom: -15px;
            left: 50%;
            transform: translateX(-50%);
            border-width: 15px 15px 0;
            border-style: solid;
            border-color: white transparent transparent transparent;
        }
        
        .speech-text {
            font-family: 'Fredoka One', cursive;
            font-size: 22px;
            color: #5a67d8;
            line-height: 1.4;
            min-height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .audio-indicator {
            display: flex;
            justify-content: center;
            gap: 4px;
            margin-top: 10px;
            height: 25px;
            align-items: flex-end;
        }
        
        .bar {
            width: 5px;
            background: #48bb78;
            border-radius: 3px;
            animation: soundWave 0.5s infinite ease-in-out;
        }
        
        .bar:nth-child(1) { height: 8px; animation-delay: 0s; }
        .bar:nth-child(2) { height: 16px; animation-delay: 0.1s; }
        .bar:nth-child(3) { height: 12px; animation-delay: 0.2s; }
        .bar:nth-child(4) { height: 20px; animation-delay: 0.3s; }
        .bar:nth-child(5) { height: 10px; animation-delay: 0.4s; }
        
        @keyframes soundWave {
            0%, 100% { transform: scaleY(1); }
            50% { transform: scaleY(1.5); }
        }
        
        .controls {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            justify-content: center;
        }
        
        .btn {
            font-family: 'Fredoka One', cursive;
            font-size: 20px;
            padding: 15px 30px;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s;
            text-transform: uppercase;
            box-shadow: 0 6px 20px rgba(0,0,0,0.2);
            touch-action: manipulation;
        }
        
        .btn:active {
            transform: scale(0.95);
        }
        
        .btn-primary {
            background: linear-gradient(145deg, #48bb78, #38a169);
            color: white;
        }
        
        .btn-primary:hover, .btn-primary:active {
            transform: translateY(-3px) scale(1.05);
            box-shadow: 0 10px 30px rgba(72, 187, 120, 0.4);
        }
        
        .btn-secondary {
            background: white;
            color: #667eea;
        }
        
        .btn-secondary:hover, .btn-secondary:active {
            transform: translateY(-3px);
            background: #f7fafc;
        }
        
        .exercise-scene {
            display: none;
            background: rgba(255,255,255,0.95);
            border-radius: 25px;
            padding: 30px;
            max-width: 90%;
            width: 100%;
            max-width: 500px;
            text-align: center;
            animation: fadeIn 0.5s;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .exercise-title {
            font-family: 'Fredoka One', cursive;
            font-size: 28px;
            color: #667eea;
            margin-bottom: 15px;
        }
        
        .memory-game {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
            max-width: 320px;
            margin: 15px auto;
        }
        
        .card {
            aspect-ratio: 1;
            background: linear-gradient(145deg, #667eea, #764ba2);
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 30px;
            cursor: pointer;
            transition: transform 0.3s;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            user-select: none;
        }
        
        .card:active {
            transform: scale(0.9);
        }
        
        .card.flipped {
            background: white;
            border: 3px solid #667eea;
        }
        
        .final-scene {
            display: none;
            text-align: center;
            animation: zoomIn 0.5s;
        }
        
        @keyframes zoomIn {
            from { transform: scale(0); }
            to { transform: scale(1); }
        }
        
        .hands-up {
            font-size: 100px;
            animation: handsUp 1s infinite;
            margin: 15px;
        }
        
        @keyframes handsUp {
            0%, 100% { transform: translateY(0) rotate(-10deg); }
            50% { transform: translateY(-20px) rotate(10deg); }
        }
        
        .final-text {
            font-family: 'Fredoka One', cursive;
            font-size: 36px;
            color: white;
            text-shadow: 3px 3px 6px rgba(0,0,0,0.3);
            margin-bottom: 20px;
            animation: pulse 1.5s infinite;
        }
        
        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }
        
        .stars {
            position: absolute;
            width: 100%;
            height: 100%;
            pointer-events: none;
        }
        
        .star {
            position: absolute;
            color: #FFD93D;
            font-size: 24px;
            animation: twinkle 2s infinite;
        }
        
        @keyframes twinkle {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.5; transform: scale(0.8); }
        }
        
        .start-screen {
            text-align: center;
            color: white;
        }
        
        .start-screen h1 {
            font-family: 'Fredoka One', cursive;
            font-size: 42px;
            margin-bottom: 15px;
            text-shadow: 4px 4px 8px rgba(0,0,0,0.3);
            animation: titleBounce 2s infinite;
        }
        
        @keyframes titleBounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        
        .start-screen p {
            font-size: 20px;
            margin-bottom: 30px;
            opacity: 0.9;
        }
        
        .hidden {
            display: none !important;
        }
        
        /* Botón de instalación PWA */
        .install-banner {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: white;
            padding: 15px;
            box-shadow: 0 -5px 20px rgba(0,0,0,0.2);
            display: none;
            z-index: 1000;
            text-align: center;
        }
        
        .install-banner.show {
            display: block;
            animation: slideUp 0.3s ease-out;
        }
        
        @keyframes slideUp {
            from { transform: translateY(100%); }
            to { transform: translateY(0); }
        }
        
        .install-text {
            font-family: 'Nunito', sans-serif;
            font-size: 16px;
            color: #333;
            margin-bottom: 10px;
        }
        
        @media (max-width: 400px) {
            .character-container {
                width: 200px;
                height: 200px;
            }
            
            .face {
                width: 130px;
                height: 90px;
            }
            
            .eye {
                width: 28px;
                height: 36px;
            }
            
            .pupil {
                width: 14px;
                height: 18px;
                top: 9px;
                left: 7px;
            }
            
            .mouth {
                width: 55px;
                height: 28px;
            }
            
            .speech-text {
                font-size: 18px;
            }
            
            .btn {
                font-size: 16px;
                padding: 12px 25px;
            }
            
            .start-screen h1 {
                font-size: 32px;
            }
        }
    </style>
</head>
<body>
    <div class="bubbles" id="bubbles"></div>
    <div class="stars" id="stars"></div>

    <div class="container">
        <div class="start-screen" id="startScreen">
            <h1>🧠 ¡Juegos de Mente! 🎮</h1>
            <p>Una aventura para hacer tu cerebro súper fuerte</p>
            <button class="btn btn-primary" onclick="startExperience()">
                ▶ ¡Comenzar Aventura!
            </button>
        </div>

        <div class="character-container hidden" id="mainScene">
            <div class="character">
                <div class="arms">
                    <div class="arm left"></div>
                    <div class="arm right"></div>
                </div>
                <div class="face">
                    <div class="eyes">
                        <div class="eye"><div class="pupil"></div></div>
                        <div class="eye"><div class="pupil"></div></div>
                    </div>
                    <div class="cheeks">
                        <div class="cheek"></div>
                        <div class="cheek"></div>
                    </div>
                    <div class="mouth">
                        <div class="tongue"></div>
                    </div>
                </div>
            </div>
        </div>

        <div class="speech-bubble hidden" id="speechBubble">
            <div class="speech-text" id="speechText">¡Hola, pequeño genio!</div>
            <div class="audio-indicator" id="audioIndicator">
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
                <div class="bar"></div>
            </div>
        </div>

        <div class="controls hidden" id="controls">
            <button class="btn btn-secondary" onclick="previousScene()" id="btnPrev">⬅ Anterior</button>
            <button class="btn btn-primary" onclick="nextScene()" id="btnNext">Siguiente ➡</button>
        </div>

        <div class="exercise-scene" id="exerciseScene">
            <h2 class="exercise-title">🎯 ¡Vamos a entrenar!</h2>
            <p style="font-size: 18px; color: #555; margin-bottom: 15px;">
                Toca las tarjetas para encontrar las parejas iguales
            </p>
            <div class="memory-game" id="memoryGame"></div>
            <button class="btn btn-primary" onclick="finishExercise()" style="margin-top: 20px;">
                ¡Lo logré! 🎉
            </button>
        </div>

        <div class="final-scene" id="finalScene">
            <div class="hands-up">🙌</div>
            <div class="final-text">¿Listo para jugar?</div>
            <button class="btn btn-primary" onclick="restartExperience()" style="font-size: 24px; padding: 18px 40px;">
                ¡SÍ, VAMOS! 🚀
            </button>
        </div>
    </div>

    <!-- Banner de instalación PWA -->
    <div class="install-banner" id="installBanner">
        <div class="install-text">📱 ¡Instala esta app en tu celular!</div>
        <button class="btn btn-primary" onclick="installApp()" style="font-size: 16px; padding: 10px 25px;">
            Instalar Ahora
        </button>
    </div>

    <audio id="bgMusic" loop>
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg">
    </audio>

    <script>
        // Service Worker para PWA (funciona offline)
        if ('serviceWorker' in navigator) {
            const swCode = `
                self.addEventListener('install', e => {
                    e.waitUntil(
                        caches.open('juegos-mente-v1').then(cache => {
                            return cache.addAll(['./']);
                        })
                    );
                    self.skipWaiting();
                });
                self.addEventListener('fetch', e => {
                    e.respondWith(
                        caches.match(e.request).then(response => {
                            return response || fetch(e.request);
                        })
                    );
                });
            `;
            
            const blob = new Blob([swCode], { type: 'application/javascript' });
            const swUrl = URL.createObjectURL(blob);
            
            navigator.serviceWorker.register(swUrl).then(() => {
                console.log('Service Worker registrado');
            }).catch(err => {
                console.log('SW no registrado, pero la app funciona igual');
            });
        }

        // Detección de instalación PWA
        let deferredPrompt;
        window.addEventListener('beforeinstallprompt', (e) => {
            e.preventDefault();
            deferredPrompt = e;
            setTimeout(() => {
                document.getElementById('installBanner').classList.add('show');
            }, 3000);
        });

        function installApp() {
            if (deferredPrompt) {
                deferredPrompt.prompt();
                deferredPrompt.userChoice.then((choiceResult) => {
                    if (choiceResult.outcome === 'accepted') {
                        console.log('Usuario instaló la app');
                    }
                    document.getElementById('installBanner').classList.remove('show');
                    deferredPrompt = null;
                });
            } else {
                alert('Para instalar: Chrome menú (3 puntos) → "Agregar a pantalla de inicio"');
            }
        }

        // Guion del video
        const script = [
            { text: "¡Hola, pequeño genio! 👋 Soy Cerebrito, tu amigo especial.", duration: 3000, action: 'bounce' },
            { text: "Hoy vamos a jugar con nuestra mente para que sea más rápida y fuerte 💪🧠", duration: 4000, action: 'excited' },
            { text: "¿Sabías que tu cerebro es como un músculo? ¡Cuanto más lo usas, más poderoso se vuelve! ✨", duration: 5000, action: 'think' },
            { text: "Los juegos de mente son ejercicios divertidos que hacen que tu cerebro trabaje 🎮", duration: 5000, action: 'explain' },
            { text: "Por ejemplo: buscar diferencias, recordar sonidos, resolver acertijos ¡Es como un gimnasio para tu cabecita! 🏋️‍♂️", duration: 5000, action: 'show' },
            { text: "¡Mira! Vamos a probar un juego de memoria. Toca las tarjetas y encuentra las parejas 🃏", duration: 4000, action: 'exercise' },
            { text: "¡Increíble! Estás haciendo que tu cerebro sea súper poderoso 🌟", duration: 3000, action: 'celebrate' },
            { text: "Recuerda: jugar con la mente es divertido y te hace más inteligente cada día 📚", duration: 4000, action: 'happy' },
            { text: "¿Listo para jugar?", duration: 3000, action: 'final' }
        ];

        let currentScene = 0;
        let speechTimeout;
        let matchedPairs = 0;
        let flippedCards = [];

        function createBubbles() {
            const container = document.getElementById('bubbles');
            for (let i = 0; i < 10; i++) {
                const bubble = document.createElement('div');
                bubble.className = 'bubble';
                const size = Math.random() * 50 + 20;
                bubble.style.width = size + 'px';
                bubble.style.height = size + 'px';
                bubble.style.left = Math.random() * 100 + '%';
                bubble.style.animationDelay = Math.random() * 15 + 's';
                bubble.style.animationDuration = (Math.random() * 10 + 10) + 's';
                container.appendChild(bubble);
            }
        }

        function createStars() {
            const container = document.getElementById('stars');
            for (let i = 0; i < 15; i++) {
                const star = document.createElement('div');
                star.className = 'star';
                star.innerHTML = '⭐';
                star.style.left = Math.random() * 100 + '%';
                star.style.top = Math.random() * 100 + '%';
                star.style.animationDelay = Math.random() * 2 + 's';
                container.appendChild(star);
            }
        }

        function startExperience() {
            document.getElementById('startScreen').classList.add('hidden');
            document.getElementById('mainScene').classList.remove('hidden');
            document.getElementById('speechBubble').classList.remove('hidden');
            document.getElementById('controls').classList.remove('hidden');
            
            const music = document.getElementById('bgMusic');
            music.volume = 0.3;
            music.play().catch(e => {});
            
            showScene(0);
        }

        function showScene(index) {
            if (index >= script.length) return;
            
            currentScene = index;
            const scene = script[index];
            const textElement = document.getElementById('speechText');
            const character = document.querySelector('.character');
            
            textElement.style.opacity = 0;
            setTimeout(() => {
                textElement.textContent = scene.text;
                textElement.style.opacity = 1;
            }, 200);
            
            character.style.animation = 'none';
            setTimeout(() => {
                switch(scene.action) {
                    case 'bounce': character.style.animation = 'bounce 1s infinite'; break;
                    case 'excited': character.style.animation = 'bounce 0.5s infinite, float 1s ease-in-out infinite'; break;
                    case 'exercise': showExercise(); return;
                    case 'final': showFinal(); return;
                    default: character.style.animation = 'bounce 2s infinite, float 3s ease-in-out infinite';
                }
            }, 10);
            
            if (scene.action !== 'exercise' && scene.action !== 'final') {
                clearTimeout(speechTimeout);
                speechTimeout = setTimeout(() => {
                    if (currentScene === index) nextScene();
                }, scene.duration);
            }
            
            updateButtons();
        }

        function updateButtons() {
            document.getElementById('btnPrev').style.visibility = currentScene > 0 ? 'visible' : 'hidden';
            document.getElementById('btnNext').textContent = currentScene === script.length - 1 ? '🔄 Repetir' : 'Siguiente ➡';
        }

        function nextScene() {
            if (currentScene < script.length - 1) {
                showScene(currentScene + 1);
            } else {
                restartExperience();
            }
        }

        function previousScene() {
            if (currentScene > 0) showScene(currentScene - 1);
        }

        function showExercise() {
            document.getElementById('mainScene').classList.add('hidden');
            document.getElementById('speechBubble').classList.add('hidden');
            document.getElementById('controls').classList.add('hidden');
            document.getElementById('exerciseScene').style.display = 'block';
            createMemoryGame();
        }

        function createMemoryGame() {
            const game = document.getElementById('memoryGame');
            game.innerHTML = '';
            const emojis = ['🐶', '🐱', '🐭', '🐹', '🐰', '🦊', '🐻', '🐼'];
            const cards = [...emojis, ...emojis].sort(() => Math.random() - 0.5);
            
            cards.forEach((emoji, index) => {
                const card = document.createElement('div');
                card.className = 'card';
                card.dataset.emoji = emoji;
                card.innerHTML = '?';
                card.onclick = () => flipCard(card, emoji);
                game.appendChild(card);
            });
        }

        function flipCard(card, emoji) {
            if (flippedCards.length < 2 && !card.classList.contains('flipped')) {
                card.classList.add('flipped');
                card.textContent = emoji;
                flippedCards.push(card);
                
                if (flippedCards.length === 2) {
                    setTimeout(checkMatch, 1000);
                }
            }
        }

        function checkMatch() {
            const [card1, card2] = flippedCards;
            if (card1.dataset.emoji === card2.dataset.emoji) {
                matchedPairs++;
                card1.style.background = '#48bb78';
                card2.style.background = '#48bb78';
                if (matchedPairs === 8) setTimeout(finishExercise, 500);
            } else {
                card1.classList.remove('flipped');
                card2.classList.remove('flipped');
                card1.textContent = '?';
                card2.textContent = '?';
            }
            flippedCards = [];
        }

        function finishExercise() {
            document.getElementById('exerciseScene').style.display = 'none';
            document.getElementById('mainScene').classList.remove('hidden');
            document.getElementById('speechBubble').classList.remove('hidden');
            document.getElementById('controls').classList.remove('hidden');
            matchedPairs = 0;
            flippedCards = [];
            showScene(currentScene + 1);
        }

        function showFinal() {
            document.getElementById('mainScene').classList.add('hidden');
            document.getElementById('speechBubble').classList.add('hidden');
            document.getElementById('controls').classList.add('hidden');
            document.getElementById('finalScene').style.display = 'block';
            createConfetti();
        }

        function createConfetti() {
            for (let i = 0; i < 30; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.style.position = 'fixed';
                    confetti.style.left = Math.random() * 100 + '%';
                    confetti.style.top = '-10px';
                    confetti.style.width = '12px';
                    confetti.style.height = '12px';
                    confetti.style.backgroundColor = ['#FFD93D', '#FF6B6B', '#4ECDC4', '#45B7D1'][Math.floor(Math.random() * 4)];
                    confetti.style.borderRadius = '50%';
                    confetti.style.zIndex = '1000';
                    confetti.style.animation = `fall ${Math.random() * 3 + 2}s linear forwards`;
                    document.body.appendChild(confetti);
                    setTimeout(() => confetti.remove(), 5000);
                }, i * 100);
            }
        }

        function restartExperience() {
            document.getElementById('finalScene').style.display = 'none';
            document.getElementById('startScreen').classList.remove('hidden');
            currentScene = 0;
            matchedPairs = 0;
            flippedCards = [];
        }

        const style = document.createElement('style');
        style.textContent = `@keyframes fall { to { transform: translateY(100vh) rotate(360deg); opacity: 0; } }`;
        document.head.appendChild(style);

        createBubbles();
        createStars();

        // Detectar si ya está instalada
        if (window.matchMedia('(display-mode: standalone)').matches || window.navigator.standalone) {
            console.log('App instalada');
        }
    </script>
</body>
</html>
