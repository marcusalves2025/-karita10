<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Karita 10 - Plataforma de Jogos</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            color: white;
            overflow-x: hidden;
            padding: 20px;
        }

        .game-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .game-title {
            font-size: 3rem;
            font-weight: bold;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4, #45b7d1, #96ceb4, #ffd93d, #ff6b6b);
            background-size: 600% 600%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: rainbowGlow 4s ease-in-out infinite, bounce 2s ease-in-out infinite, pulse 3s ease-in-out infinite;
            text-shadow: 0 0 30px rgba(255, 107, 107, 0.5), 0 0 60px rgba(78, 205, 196, 0.3);
            position: relative;
            display: inline-block;
            transform-origin: center;
        }

        .game-title::before {
            content: '';
            position: absolute;
            top: -10px;
            left: -10px;
            right: -10px;
            bottom: -10px;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4, #45b7d1, #96ceb4, #ffd93d);
            background-size: 400% 400%;
            border-radius: 20px;
            z-index: -1;
            opacity: 0.3;
            animation: rainbowGlow 4s ease-in-out infinite;
            filter: blur(15px);
        }

        .game-title::after {
            content: '✨';
            position: absolute;
            top: -20px;
            right: -20px;
            font-size: 1.5rem;
            animation: sparkle 2s ease-in-out infinite;
        }

        @keyframes rainbowGlow {
            0%, 100% { 
                background-position: 0% 50%;
                filter: hue-rotate(0deg) brightness(1.2);
            }
            25% { 
                background-position: 100% 50%;
                filter: hue-rotate(90deg) brightness(1.4);
            }
            50% { 
                background-position: 200% 50%;
                filter: hue-rotate(180deg) brightness(1.6);
            }
            75% { 
                background-position: 300% 50%;
                filter: hue-rotate(270deg) brightness(1.4);
            }
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% {
                transform: translateY(0) scale(1);
            }
            40% {
                transform: translateY(-10px) scale(1.05);
            }
            60% {
                transform: translateY(-5px) scale(1.02);
            }
        }

        @keyframes pulse {
            0%, 100% {
                transform: scale(1);
                text-shadow: 0 0 30px rgba(255, 107, 107, 0.5), 0 0 60px rgba(78, 205, 196, 0.3);
            }
            50% {
                transform: scale(1.08);
                text-shadow: 0 0 40px rgba(255, 107, 107, 0.8), 0 0 80px rgba(78, 205, 196, 0.6), 0 0 120px rgba(69, 183, 209, 0.4);
            }
        }

        @keyframes sparkle {
            0%, 100% {
                opacity: 0.7;
                transform: rotate(0deg) scale(1);
            }
            25% {
                opacity: 1;
                transform: rotate(90deg) scale(1.2);
            }
            50% {
                opacity: 0.8;
                transform: rotate(180deg) scale(0.9);
            }
            75% {
                opacity: 1;
                transform: rotate(270deg) scale(1.1);
            }
        }

        .game-subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
            margin-bottom: 20px;
        }

        .level-selector {
            margin-bottom: 20px;
            text-align: center;
        }

        .level-selector select {
            background: rgba(255,255,255,0.2);
            color: white;
            border: 1px solid rgba(255,255,255,0.3);
            padding: 10px 20px;
            border-radius: 10px;
            font-size: 1rem;
            backdrop-filter: blur(10px);
        }

        .level-selector option {
            background: #764ba2;
            color: white;
        }

        .game-selector {
            margin-bottom: 20px;
            text-align: center;
        }

        .game-selector select {
            background: rgba(255,255,255,0.2);
            color: white;
            border: 1px solid rgba(255,255,255,0.3);
            padding: 10px 20px;
            border-radius: 10px;
            font-size: 1rem;
            backdrop-filter: blur(10px);
        }

        .game-stats {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .stat-item {
            background: rgba(255,255,255,0.2);
            padding: 12px 18px;
            border-radius: 15px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.3);
            text-align: center;
            min-width: 90px;
        }

        .stat-label {
            font-size: 0.8rem;
            opacity: 0.8;
            margin-bottom: 5px;
        }

        .stat-value {
            font-size: 1.2rem;
            font-weight: bold;
        }

        .game-area {
            width: 100%;
            max-width: 800px;
            margin-bottom: 30px;
            min-height: 400px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .memory-board {
            display: grid;
            gap: 8px;
            margin-bottom: 20px;
        }

        .memory-card {
            aspect-ratio: 1;
            background: linear-gradient(145deg, #ffffff, #e6e6e6);
            border-radius: 12px;
            cursor: pointer;
            position: relative;
            transform-style: preserve-3d;
            transition: transform 0.6s ease;
            box-shadow: 0 6px 12px rgba(0,0,0,0.2);
            min-height: 50px;
        }

        .memory-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 24px rgba(0,0,0,0.3);
        }

        .memory-card.flipped {
            transform: rotateY(180deg);
        }

        .memory-card.matched {
            animation: matchPulse 0.6s ease;
            pointer-events: none;
            opacity: 0.7;
        }

        @keyframes matchPulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 12px;
            backface-visibility: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            font-weight: bold;
        }

        .card-back {
            background: linear-gradient(145deg, #ff6b6b, #ee5a52);
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .card-front {
            transform: rotateY(180deg);
            color: white;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .puzzle-game {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 5px;
            width: 300px;
            height: 300px;
            background: rgba(255,255,255,0.1);
            padding: 10px;
            border-radius: 15px;
        }

        .puzzle-piece {
            background: linear-gradient(145deg, #4ecdc4, #44a08d);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .puzzle-piece:hover {
            transform: scale(1.05);
        }

        .puzzle-piece.empty {
            background: rgba(255,255,255,0.2);
        }

        .quiz-container {
            text-align: center;
            max-width: 600px;
        }

        .question {
            font-size: 1.5rem;
            margin-bottom: 30px;
            padding: 20px;
            background: rgba(255,255,255,0.1);
            border-radius: 15px;
        }

        .quiz-options {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-bottom: 20px;
        }

        .quiz-option {
            padding: 15px;
            background: rgba(255,255,255,0.2);
            border: none;
            border-radius: 10px;
            color: white;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .quiz-option:hover {
            background: rgba(255,255,255,0.3);
            transform: translateY(-2px);
        }

        .quiz-option.correct {
            background: linear-gradient(145deg, #4ecdc4, #44a08d);
        }

        .quiz-option.incorrect {
            background: linear-gradient(145deg, #ff6b6b, #ee5a52);
        }

        .snake-game {
            width: 400px;
            height: 400px;
            background: rgba(0,0,0,0.3);
            border-radius: 15px;
            position: relative;
            overflow: hidden;
        }

        .snake-pixel {
            position: absolute;
            width: 20px;
            height: 20px;
            background: #4ecdc4;
            border-radius: 3px;
        }

        .food-pixel {
            position: absolute;
            width: 20px;
            height: 20px;
            background: #ff6b6b;
            border-radius: 50%;
        }

        .controls {
            display: flex;
            gap: 15px;
            margin-bottom: 40px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .btn {
            background: linear-gradient(145deg, #4ecdc4, #44a08d);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 25px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.3);
        }

        .victory-message {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: linear-gradient(145deg, #4ecdc4, #44a08d);
            color: white;
            padding: 30px;
            border-radius: 20px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            z-index: 1000;
            display: none;
        }

        .victory-message h2 {
            font-size: 2rem;
            margin-bottom: 10px;
        }

        .time-section {
            width: 100%;
            max-width: 800px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 40px;
        }

        .digital-clock, .stopwatch {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            border: 1px solid rgba(255,255,255,0.2);
            text-align: center;
        }

        .digital-clock h3, .stopwatch h3 {
            margin-bottom: 20px;
            font-size: 1.5rem;
            color: white;
        }

        .clock-display, .stopwatch-display {
            font-size: 3rem;
            font-weight: bold;
            font-family: 'Courier New', monospace;
            background: linear-gradient(145deg, #4ecdc4, #44a08d);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 15px;
            text-shadow: 0 0 20px rgba(78, 205, 196, 0.3);
        }

        .date-display {
            font-size: 1.2rem;
            opacity: 0.8;
            margin-bottom: 10px;
        }

        .stopwatch-controls {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin-bottom: 20px;
        }

        .time-btn {
            background: linear-gradient(145deg, #667eea, #764ba2);
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1rem;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }

        .time-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0,0,0,0.3);
        }

        .time-btn.active {
            background: linear-gradient(145deg, #ff6b6b, #ee5a52);
        }

        .lap-times {
            max-height: 200px;
            overflow-y: auto;
            background: rgba(255,255,255,0.05);
            border-radius: 10px;
            padding: 15px;
        }

        .lap-time {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid rgba(255,255,255,0.1);
            font-family: 'Courier New', monospace;
        }

        .lap-time:last-child {
            border-bottom: none;
        }

        @media (max-width: 768px) {
            .game-title {
                font-size: 2rem;
            }
            
            .card-face {
                font-size: 1rem;
            }
            
            .game-stats {
                gap: 10px;
            }

            .time-section {
                grid-template-columns: 1fr;
                gap: 20px;
            }

            .clock-display, .stopwatch-display {
                font-size: 2.5rem;
            }

            .stopwatch-controls {
                flex-wrap: wrap;
            }

            .puzzle-game {
                width: 250px;
                height: 250px;
            }

            .snake-game {
                width: 300px;
                height: 300px;
            }
        }
    </style>
</head>
<body>
    <div class="game-header">
        <h1 class="game-title">Karita 10</h1>
        <p class="game-subtitle">Plataforma de Jogos - 70 Níveis</p>
    </div>

    <div class="level-selector">
        <label for="levelSelect">Escolha o Nível: </label>
        <select id="levelSelect" onchange="changeLevel()">
            <!-- Levels will be populated by JavaScript -->
        </select>
    </div>

    <div class="game-selector" id="gameSelector" style="display: none;">
        <label for="gameSelect">Escolha o Jogo: </label>
        <select id="gameSelect" onchange="changeGame()">
            <!-- Games will be populated by JavaScript -->
        </select>
    </div>

    <div class="game-stats">
        <div class="stat-item">
            <div class="stat-label">Nível</div>
            <div class="stat-value" id="currentLevel">1</div>
        </div>
        <div class="stat-item">
            <div class="stat-label">Pontos</div>
            <div class="stat-value" id="score">0</div>
        </div>
        <div class="stat-item">
            <div class="stat-label">Tempo</div>
            <div class="stat-value" id="timer">00:00</div>
        </div>
        <div class="stat-item">
            <div class="stat-label">Jogo</div>
            <div class="stat-value" id="currentGame">Memória</div>
        </div>
    </div>

    <div class="game-area" id="gameArea">
        <!-- Game content will be dynamically loaded here -->
    </div>

    <div class="controls">
        <button class="btn" onclick="startNewGame()">Novo Jogo</button>
        <button class="btn" onclick="resetGame()">Reiniciar</button>
        <button class="btn" onclick="nextLevel()">Próximo Nível</button>
    </div>

    <div class="victory-message" id="victoryMessage">
        <h2>🎉 Parabéns! 🎉</h2>
        <p>Você completou o desafio!</p>
        <p id="finalStats"></p>
        <button class="btn" onclick="nextLevel(); hideVictory();" style="margin-top: 15px;">Próximo Nível</button>
        <button class="btn" onclick="startNewGame(); hideVictory();" style="margin-top: 15px;">Jogar Novamente</button>
    </div>

    <div class="time-section">
        <div class="digital-clock">
            <h3>🕐 Relógio Digital</h3>
            <div class="clock-display" id="digitalClock">00:00:00</div>
            <div class="date-display" id="dateDisplay">Segunda, 1 de Janeiro de 2024</div>
        </div>
        
        <div class="stopwatch">
            <h3>⏱️ Cronômetro</h3>
            <div class="stopwatch-display" id="stopwatchDisplay">00:00:00</div>
            <div class="stopwatch-controls">
                <button class="time-btn" id="startStopBtn" onclick="toggleStopwatch()">Iniciar</button>
                <button class="time-btn" onclick="resetStopwatch()">Zerar</button>
                <button class="time-btn" onclick="lapTime()">Volta</button>
            </div>
            <div class="lap-times" id="lapTimes"></div>
        </div>
    </div>

    <script>
        let currentLevel = 1;
        let currentGameIndex = 0;
        let score = 0;
        let gameStarted = false;
        let startTime = null;
        let timerInterval = null;

        // Configurações dos 70 níveis
        const levelConfigs = [
            // Nível 1: 30 jogos de memória diferentes
            {
                type: 'memory_collection',
                games: [
                    { name: 'Animais', symbols: ['🐶', '🐱', '🐭', '🐹'], pairs: 4, cols: 4 },
                    { name: 'Frutas', symbols: ['🍎', '🍌', '🍊', '🍇'], pairs: 4, cols: 4 },
                    { name: 'Flores', symbols: ['🌸', '🌺', '🌻', '🌷'], pairs: 4, cols: 4 },
                    { name: 'Esportes', symbols: ['⚽', '🏀', '🎾', '🏐'], pairs: 4, cols: 4 },
                    { name: 'Instrumentos', symbols: ['🎸', '🎹', '🎺', '🎻'], pairs: 4, cols: 4 },
                    { name: 'Veículos', symbols: ['🚗', '🚕', '🚙', '🚌'], pairs: 4, cols: 4 },
                    { name: 'Comidas', symbols: ['🍕', '🍔', '🌭', '🥪'], pairs: 4, cols: 4 },
                    { name: 'Bebidas', symbols: ['☕', '🥤', '🧃', '🍵'], pairs: 4, cols: 4 },
                    { name: 'Doces', symbols: ['🍭', '🍬', '🧁', '🍪'], pairs: 4, cols: 4 },
                    { name: 'Emoções', symbols: ['😀', '😍', '🤔', '😎'], pairs: 4, cols: 4 },
                    { name: 'Natureza', symbols: ['🌳', '🌲', '🌿', '🍀'], pairs: 4, cols: 4 },
                    { name: 'Clima', symbols: ['☀️', '🌙', '⭐', '🌈'], pairs: 4, cols: 4 },
                    { name: 'Oceano', symbols: ['🐠', '🐙', '🦈', '🐚'], pairs: 4, cols: 4 },
                    { name: 'Insetos', symbols: ['🦋', '🐝', '🐞', '🦗'], pairs: 4, cols: 4 },
                    { name: 'Pássaros', symbols: ['🦅', '🦆', '🦉', '🐧'], pairs: 4, cols: 4 },
                    { name: 'Joias', symbols: ['💎', '💍', '👑', '📿'], pairs: 4, cols: 4 },
                    { name: 'Ferramentas', symbols: ['🔨', '🔧', '⚙️', '🔩'], pairs: 4, cols: 4 },
                    { name: 'Escola', symbols: ['📚', '✏️', '📐', '🎒'], pairs: 4, cols: 4 },
                    { name: 'Casa', symbols: ['🏠', '🚪', '🪟', '🛏️'], pairs: 4, cols: 4 },
                    { name: 'Roupas', symbols: ['👕', '👖', '👗', '👠'], pairs: 4, cols: 4 },
                    { name: 'Tecnologia', symbols: ['💻', '📱', '⌚', '🎧'], pairs: 4, cols: 4 },
                    { name: 'Medicina', symbols: ['💊', '🩺', '💉', '🏥'], pairs: 4, cols: 4 },
                    { name: 'Viagem', symbols: ['✈️', '🚢', '🚂', '🗺️'], pairs: 4, cols: 4 },
                    { name: 'Festa', symbols: ['🎉', '🎈', '🎂', '🎁'], pairs: 4, cols: 4 },
                    { name: 'Magia', symbols: ['🔮', '🎭', '🎪', '🎨'], pairs: 4, cols: 4 },
                    { name: 'Espaço', symbols: ['🚀', '🛸', '👽', '🌌'], pairs: 4, cols: 4 },
                    { name: 'Piratas', symbols: ['🏴‍☠️', '⚓', '🗡️', '💰'], pairs: 4, cols: 4 },
                    { name: 'Dinossauros', symbols: ['🦕', '🦖', '🦴', '🥚'], pairs: 4, cols: 4 },
                    { name: 'Fantasia', symbols: ['🦄', '🐉', '🧚', '🧙'], pairs: 4, cols: 4 },
                    { name: 'Símbolos', symbols: ['❤️', '⭐', '🔥', '💫'], pairs: 4, cols: 4 }
                ]
            },
            // Níveis 2-10: Quebra-cabeças numéricos
            ...Array(9).fill().map((_, i) => ({
                type: 'puzzle',
                name: `Quebra-cabeça ${i + 1}`,
                size: 3,
                difficulty: i + 1
            })),
            // Níveis 11-20: Quiz de conhecimentos gerais
            ...Array(10).fill().map((_, i) => ({
                type: 'quiz',
                name: `Quiz ${i + 1}`,
                category: ['História', 'Geografia', 'Ciências', 'Arte', 'Esportes'][i % 5],
                questions: 5
            })),
            // Níveis 21-30: Jogo da cobra
            ...Array(10).fill().map((_, i) => ({
                type: 'snake',
                name: `Cobra ${i + 1}`,
                speed: Math.max(200 - i * 20, 80),
                target: (i + 1) * 5
            })),
            // Níveis 31-40: Memória avançada
            ...Array(10).fill().map((_, i) => ({
                type: 'memory',
                name: `Memória Avançada ${i + 1}`,
                pairs: 6 + i,
                cols: 4 + Math.floor(i / 3),
                symbols: ['🌟', '🎈', '🎨', '🎭', '🎪', '🎯', '🎲', '🎸', '🎺', '🎻', '🎹', '🎤', '🎧', '🎬', '🎮']
            })),
            // Níveis 41-50: Quebra-cabeças complexos
            ...Array(10).fill().map((_, i) => ({
                type: 'puzzle',
                name: `Quebra-cabeça Avançado ${i + 1}`,
                size: 4,
                difficulty: i + 10
            })),
            // Níveis 51-60: Quiz especializado
            ...Array(10).fill().map((_, i) => ({
                type: 'quiz',
                name: `Quiz Especializado ${i + 1}`,
                category: ['Matemática', 'Física', 'Química', 'Biologia', 'Literatura'][i % 5],
                questions: 8
            })),
            // Níveis 61-70: Desafios mistos
            ...Array(10).fill().map((_, i) => ({
                type: ['memory', 'puzzle', 'quiz', 'snake'][i % 4],
                name: `Desafio Final ${i + 1}`,
                difficulty: 'expert'
            }))
        ];

        // Dados para quiz
        const quizData = {
            'História': [
                { q: 'Em que ano o Brasil foi descoberto?', a: ['1500', '1498', '1502', '1499'], c: 0 },
                { q: 'Quem foi o primeiro presidente do Brasil?', a: ['Deodoro da Fonseca', 'Getúlio Vargas', 'Juscelino Kubitschek', 'Tancredo Neves'], c: 0 },
                { q: 'Qual foi a primeira capital do Brasil?', a: ['Salvador', 'Rio de Janeiro', 'São Paulo', 'Brasília'], c: 0 }
            ],
            'Geografia': [
                { q: 'Qual é o maior país do mundo?', a: ['Rússia', 'China', 'Estados Unidos', 'Brasil'], c: 0 },
                { q: 'Qual é o rio mais longo do mundo?', a: ['Nilo', 'Amazonas', 'Mississippi', 'Yangtzé'], c: 0 },
                { q: 'Quantos continentes existem?', a: ['7', '5', '6', '8'], c: 0 }
            ],
            'Ciências': [
                { q: 'Qual é o planeta mais próximo do Sol?', a: ['Mercúrio', 'Vênus', 'Terra', 'Marte'], c: 0 },
                { q: 'Quantos ossos tem o corpo humano adulto?', a: ['206', '208', '204', '210'], c: 0 },
                { q: 'Qual é a fórmula da água?', a: ['H2O', 'CO2', 'O2', 'H2SO4'], c: 0 }
            ]
        };

        function initializeLevelSelector() {
            const select = document.getElementById('levelSelect');
            for (let i = 1; i <= 70; i++) {
                const option = document.createElement('option');
                option.value = i;
                option.textContent = `Nível ${i}`;
                select.appendChild(option);
            }
        }

        function changeLevel() {
            const select = document.getElementById('levelSelect');
            currentLevel = parseInt(select.value);
            currentGameIndex = 0;
            setupLevel();
        }

        function changeGame() {
            const select = document.getElementById('gameSelect');
            currentGameIndex = parseInt(select.value);
            startNewGame();
        }

        function setupLevel() {
            const config = levelConfigs[currentLevel - 1];
            
            if (config.type === 'memory_collection') {
                // Mostrar seletor de jogos para o nível 1
                document.getElementById('gameSelector').style.display = 'block';
                const gameSelect = document.getElementById('gameSelect');
                gameSelect.innerHTML = '';
                
                config.games.forEach((game, index) => {
                    const option = document.createElement('option');
                    option.value = index;
                    option.textContent = game.name;
                    gameSelect.appendChild(option);
                });
            } else {
                document.getElementById('gameSelector').style.display = 'none';
            }
            
            startNewGame();
        }

        function nextLevel() {
            if (currentLevel < 70) {
                currentLevel++;
                document.getElementById('levelSelect').value = currentLevel;
                currentGameIndex = 0;
                setupLevel();
            }
        }

        function startNewGame() {
            resetGameState();
            const config = levelConfigs[currentLevel - 1];
            
            document.getElementById('currentLevel').textContent = currentLevel;
            
            switch (config.type) {
                case 'memory_collection':
                    startMemoryGame(config.games[currentGameIndex]);
                    document.getElementById('currentGame').textContent = config.games[currentGameIndex].name;
                    break;
                case 'memory':
                    startMemoryGame(config);
                    document.getElementById('currentGame').textContent = 'Memória';
                    break;
                case 'puzzle':
                    startPuzzleGame(config);
                    document.getElementById('currentGame').textContent = 'Quebra-cabeça';
                    break;
                case 'quiz':
                    startQuizGame(config);
                    document.getElementById('currentGame').textContent = 'Quiz';
                    break;
                case 'snake':
                    startSnakeGame(config);
                    document.getElementById('currentGame').textContent = 'Cobra';
                    break;
            }
        }

        function resetGameState() {
            clearInterval(timerInterval);
            score = 0;
            gameStarted = false;
            startTime = null;
            document.getElementById('score').textContent = '0';
            document.getElementById('timer').textContent = '00:00';
            hideVictory();
        }

        function startGame() {
            if (!gameStarted) {
                gameStarted = true;
                startTime = Date.now();
                timerInterval = setInterval(updateTimer, 1000);
            }
        }

        function updateTimer() {
            if (!startTime) return;
            
            const elapsed = Math.floor((Date.now() - startTime) / 1000);
            const minutes = Math.floor(elapsed / 60).toString().padStart(2, '0');
            const seconds = (elapsed % 60).toString().padStart(2, '0');
            
            document.getElementById('timer').textContent = `${minutes}:${seconds}`;
        }

        function updateScore(points) {
            score += points;
            document.getElementById('score').textContent = score;
        }

        function endGame(success = true) {
            clearInterval(timerInterval);
            if (success) {
                const finalTime = document.getElementById('timer').textContent;
                document.getElementById('finalStats').textContent = 
                    `Nível ${currentLevel} | Tempo: ${finalTime} | Pontos: ${score}`;
                document.getElementById('victoryMessage').style.display = 'block';
            }
        }

        function hideVictory() {
            document.getElementById('victoryMessage').style.display = 'none';
        }

        function resetGame() {
            startNewGame();
        }

        // Jogo de Memória
        let memoryCards = [];
        let flippedCards = [];
        let memoryPairs = 0;
        let totalMemoryPairs = 0;

        function startMemoryGame(config) {
            const gameArea = document.getElementById('gameArea');
            gameArea.innerHTML = '<div class="memory-board" id="memoryBoard"></div>';
            
            totalMemoryPairs = config.pairs;
            memoryPairs = 0;
            flippedCards = [];
            
            const symbols = [...config.symbols.slice(0, config.pairs), ...config.symbols.slice(0, config.pairs)];
            symbols.sort(() => Math.random() - 0.5);
            
            memoryCards = symbols.map((symbol, index) => ({
                id: index,
                symbol: symbol,
                isFlipped: false,
                isMatched: false
            }));
            
            const board = document.getElementById('memoryBoard');
            board.style.gridTemplateColumns = `repeat(${config.cols}, 1fr)`;
            
            memoryCards.forEach(card => {
                const cardElement = document.createElement('div');
                cardElement.className = 'memory-card';
                cardElement.onclick = () => flipMemoryCard(card.id);
                
                cardElement.innerHTML = `
                    <div class="card-face card-back">?</div>
                    <div class="card-face card-front" style="background: linear-gradient(145deg, #4ecdc4, #44a08d);">${card.symbol}</div>
                `;
                
                board.appendChild(cardElement);
            });
        }

        function flipMemoryCard(cardId) {
            startGame();
            
            const card = memoryCards[cardId];
            if (card.isFlipped || card.isMatched || flippedCards.length >= 2) return;
            
            card.isFlipped = true;
            flippedCards.push(card);
            updateMemoryDisplay();
            
            if (flippedCards.length === 2) {
                setTimeout(() => {
                    checkMemoryMatch();
                }, 1000);
            }
        }

        function checkMemoryMatch() {
            const [card1, card2] = flippedCards;
            
            if (card1.symbol === card2.symbol) {
                card1.isMatched = true;
                card2.isMatched = true;
                memoryPairs++;
                updateScore(10);
                
                if (memoryPairs === totalMemoryPairs) {
                    endGame(true);
                }
            } else {
                card1.isFlipped = false;
                card2.isFlipped = false;
            }
            
            flippedCards = [];
            updateMemoryDisplay();
        }

        function updateMemoryDisplay() {
            memoryCards.forEach((card, index) => {
                const cardElement = document.querySelectorAll('.memory-card')[index];
                cardElement.className = 'memory-card';
                
                if (card.isFlipped || card.isMatched) {
                    cardElement.classList.add('flipped');
                }
                if (card.isMatched) {
                    cardElement.classList.add('matched');
                }
            });
        }

        // Jogo de Quebra-cabeça
        let puzzleState = [];

        function startPuzzleGame(config) {
            const gameArea = document.getElementById('gameArea');
            gameArea.innerHTML = '<div class="puzzle-game" id="puzzleGame"></div>';
            
            const size = config.size;
            puzzleState = [];
            
            // Criar estado inicial embaralhado
            for (let i = 0; i < size * size - 1; i++) {
                puzzleState.push(i + 1);
            }
            puzzleState.push(0); // Espaço vazio
            
            // Embaralhar
            for (let i = 0; i < 100; i++) {
                const emptyIndex = puzzleState.indexOf(0);
                const possibleMoves = getPossibleMoves(emptyIndex, size);
                const randomMove = possibleMoves[Math.floor(Math.random() * possibleMoves.length)];
                [puzzleState[emptyIndex], puzzleState[randomMove]] = [puzzleState[randomMove], puzzleState[emptyIndex]];
            }
            
            updatePuzzleDisplay(size);
        }

        function getPossibleMoves(emptyIndex, size) {
            const moves = [];
            const row = Math.floor(emptyIndex / size);
            const col = emptyIndex % size;
            
            if (row > 0) moves.push(emptyIndex - size); // Up
            if (row < size - 1) moves.push(emptyIndex + size); // Down
            if (col > 0) moves.push(emptyIndex - 1); // Left
            if (col < size - 1) moves.push(emptyIndex + 1); // Right
            
            return moves;
        }

        function updatePuzzleDisplay(size) {
            const puzzleGame = document.getElementById('puzzleGame');
            puzzleGame.innerHTML = '';
            puzzleGame.style.gridTemplateColumns = `repeat(${size}, 1fr)`;
            
            puzzleState.forEach((value, index) => {
                const piece = document.createElement('div');
                piece.className = 'puzzle-piece';
                
                if (value === 0) {
                    piece.classList.add('empty');
                } else {
                    piece.textContent = value;
                    piece.onclick = () => movePuzzlePiece(index, size);
                }
                
                puzzleGame.appendChild(piece);
            });
        }

        function movePuzzlePiece(index, size) {
            startGame();
            
            const emptyIndex = puzzleState.indexOf(0);
            const possibleMoves = getPossibleMoves(emptyIndex, size);
            
            if (possibleMoves.includes(index)) {
                [puzzleState[emptyIndex], puzzleState[index]] = [puzzleState[index], puzzleState[emptyIndex]];
                updatePuzzleDisplay(size);
                updateScore(1);
                
                // Verificar se está resolvido
                const isSolved = puzzleState.every((value, index) => 
                    index === puzzleState.length - 1 ? value === 0 : value === index + 1
                );
                
                if (isSolved) {
                    endGame(true);
                }
            }
        }

        // Jogo de Quiz
        let currentQuestions = [];
        let currentQuestionIndex = 0;

        function startQuizGame(config) {
            const gameArea = document.getElementById('gameArea');
            gameArea.innerHTML = '<div class="quiz-container" id="quizContainer"></div>';
            
            // Selecionar perguntas aleatórias
            const allQuestions = quizData[config.category] || quizData['História'];
            currentQuestions = [];
            
            for (let i = 0; i < config.questions && i < allQuestions.length; i++) {
                currentQuestions.push(allQuestions[i]);
            }
            
            currentQuestionIndex = 0;
            showQuestion();
        }

        function showQuestion() {
            const container = document.getElementById('quizContainer');
            const question = currentQuestions[currentQuestionIndex];
            
            container.innerHTML = `
                <div class="question">${question.q}</div>
                <div class="quiz-options" id="quizOptions"></div>
                <div style="margin-top: 20px;">Pergunta ${currentQuestionIndex + 1} de ${currentQuestions.length}</div>
            `;
            
            const optionsContainer = document.getElementById('quizOptions');
            question.a.forEach((answer, index) => {
                const button = document.createElement('button');
                button.className = 'quiz-option';
                button.textContent = answer;
                button.onclick = () => selectAnswer(index);
                optionsContainer.appendChild(button);
            });
        }

        function selectAnswer(selectedIndex) {
            startGame();
            
            const question = currentQuestions[currentQuestionIndex];
            const options = document.querySelectorAll('.quiz-option');
            
            options.forEach((option, index) => {
                if (index === question.c) {
                    option.classList.add('correct');
                } else if (index === selectedIndex) {
                    option.classList.add('incorrect');
                }
                option.onclick = null;
            });
            
            if (selectedIndex === question.c) {
                updateScore(20);
            }
            
            setTimeout(() => {
                currentQuestionIndex++;
                if (currentQuestionIndex < currentQuestions.length) {
                    showQuestion();
                } else {
                    endGame(true);
                }
            }, 2000);
        }

        // Jogo da Cobra
        let snake = [];
        let food = {};
        let direction = { x: 20, y: 0 };
        let snakeGameRunning = false;

        function startSnakeGame(config) {
            const gameArea = document.getElementById('gameArea');
            gameArea.innerHTML = `
                <div class="snake-game" id="snakeGame"></div>
                <div style="margin-top: 20px; text-align: center;">
                    <p>Use as setas do teclado para mover</p>
                    <p>Meta: ${config.target} pontos</p>
                </div>
            `;
            
            snake = [{ x: 200, y: 200 }];
            direction = { x: 20, y: 0 };
            snakeGameRunning = true;
            
            generateFood();
            updateSnakeDisplay();
            
            // Controles do teclado
            document.addEventListener('keydown', handleSnakeControls);
            
            // Loop do jogo
            setTimeout(() => gameSnakeLoop(config), config.speed);
        }

        function handleSnakeControls(e) {
            if (!snakeGameRunning) return;
            
            startGame();
            
            switch(e.key) {
                case 'ArrowUp':
                    if (direction.y === 0) direction = { x: 0, y: -20 };
                    break;
                case 'ArrowDown':
                    if (direction.y === 0) direction = { x: 0, y: 20 };
                    break;
                case 'ArrowLeft':
                    if (direction.x === 0) direction = { x: -20, y: 0 };
                    break;
                case 'ArrowRight':
                    if (direction.x === 0) direction = { x: 20, y: 0 };
                    break;
            }
        }

        function gameSnakeLoop(config) {
            if (!snakeGameRunning) return;
            
            // Mover cobra
            const head = { x: snake[0].x + direction.x, y: snake[0].y + direction.y };
            
            // Verificar colisões com paredes
            if (head.x < 0 || head.x >= 400 || head.y < 0 || head.y >= 400) {
                snakeGameRunning = false;
                endGame(false);
                return;
            }
            
            // Verificar colisão com próprio corpo
            if (snake.some(segment => segment.x === head.x && segment.y === head.y)) {
                snakeGameRunning = false;
                endGame(false);
                return;
            }
            
            snake.unshift(head);
            
            // Verificar se comeu comida
            if (head.x === food.x && head.y === food.y) {
                updateScore(5);
                generateFood();
                
                // Verificar vitória
                if (score >= config.target * 5) {
                    snakeGameRunning = false;
                    endGame(true);
                    return;
                }
            } else {
                snake.pop();
            }
            
            updateSnakeDisplay();
            setTimeout(() => gameSnakeLoop(config), config.speed);
        }

        function generateFood() {
            food = {
                x: Math.floor(Math.random() * 20) * 20,
                y: Math.floor(Math.random() * 20) * 20
            };
        }

        function updateSnakeDisplay() {
            const gameContainer = document.getElementById('snakeGame');
            gameContainer.innerHTML = '';
            
            // Desenhar cobra
            snake.forEach(segment => {
                const snakeElement = document.createElement('div');
                snakeElement.className = 'snake-pixel';
                snakeElement.style.left = segment.x + 'px';
                snakeElement.style.top = segment.y + 'px';
                gameContainer.appendChild(snakeElement);
            });
            
            // Desenhar comida
            const foodElement = document.createElement('div');
            foodElement.className = 'food-pixel';
            foodElement.style.left = food.x + 'px';
            foodElement.style.top = food.y + 'px';
            gameContainer.appendChild(foodElement);
        }

        // Sistema de relógio digital e cronômetro
        let clockInterval = null;
        let stopwatchInterval = null;
        let stopwatchStartTime = null;
        let stopwatchElapsed = 0;
        let isStopwatchRunning = false;
        let lapCounter = 1;

        function startClock() {
            clockInterval = setInterval(updateClock, 1000);
            updateClock(); // Atualizar imediatamente
        }

        function updateClock() {
            const now = new Date();
            
            // Atualizar relógio digital
            const hours = now.getHours().toString().padStart(2, '0');
            const minutes = now.getMinutes().toString().padStart(2, '0');
            const seconds = now.getSeconds().toString().padStart(2, '0');
            
            document.getElementById('digitalClock').textContent = `${hours}:${minutes}:${seconds}`;
            
            // Atualizar data
            const days = ['Domingo', 'Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta', 'Sábado'];
            const months = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 
                           'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
            
            const dayName = days[now.getDay()];
            const day = now.getDate();
            const month = months[now.getMonth()];
            const year = now.getFullYear();
            
            document.getElementById('dateDisplay').textContent = `${dayName}, ${day} de ${month} de ${year}`;
        }

        function toggleStopwatch() {
            const button = document.getElementById('startStopBtn');
            
            if (!isStopwatchRunning) {
                // Iniciar cronômetro
                stopwatchStartTime = Date.now() - stopwatchElapsed;
                stopwatchInterval = setInterval(updateStopwatch, 10);
                isStopwatchRunning = true;
                button.textContent = 'Pausar';
                button.classList.add('active');
            } else {
                // Pausar cronômetro
                clearInterval(stopwatchInterval);
                isStopwatchRunning = false;
                button.textContent = 'Continuar';
                button.classList.remove('active');
            }
        }

        function resetStopwatch() {
            clearInterval(stopwatchInterval);
            stopwatchElapsed = 0;
            isStopwatchRunning = false;
            lapCounter = 1;
            
            document.getElementById('stopwatchDisplay').textContent = '00:00:00';
            document.getElementById('startStopBtn').textContent = 'Iniciar';
            document.getElementById('startStopBtn').classList.remove('active');
            document.getElementById('lapTimes').innerHTML = '';
        }

        function updateStopwatch() {
            stopwatchElapsed = Date.now() - stopwatchStartTime;
            
            const totalSeconds = Math.floor(stopwatchElapsed / 1000);
            const minutes = Math.floor(totalSeconds / 60);
            const seconds = totalSeconds % 60;
            const centiseconds = Math.floor((stopwatchElapsed % 1000) / 10);
            
            const display = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}:${centiseconds.toString().padStart(2, '0')}`;
            document.getElementById('stopwatchDisplay').textContent = display;
        }

        function lapTime() {
            if (!isStopwatchRunning && stopwatchElapsed === 0) return;
            
            const currentTime = document.getElementById('stopwatchDisplay').textContent;
            const lapTimesContainer = document.getElementById('lapTimes');
            
            const lapElement = document.createElement('div');
            lapElement.className = 'lap-time';
            lapElement.innerHTML = `
                <span>Volta ${lapCounter}</span>
                <span>${currentTime}</span>
            `;
            
            lapTimesContainer.insertBefore(lapElement, lapTimesContainer.firstChild);
            lapCounter++;
            
            // Limitar a 10 voltas visíveis
            const lapTimes = lapTimesContainer.querySelectorAll('.lap-time');
            if (lapTimes.length > 10) {
                lapTimesContainer.removeChild(lapTimes[lapTimes.length - 1]);
            }
        }

        // Inicializar o jogo e relógio
        initializeLevelSelector();
        setupLevel();
        startClock();
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'972439b6338432a9',t:'MTc1NTcxNzM5MC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
