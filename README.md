<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Smashy Road: 40 Features Ultimate Edition - MK Creative Agency</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; user-select: none; font-family: 'Courier New', Courier, monospace; }
        body { background-color: #0d0d0d; color: #fff; overflow: hidden; width: 100vw; height: 100vh; display: flex; justify-content: center; align-items: center; }

        #rotate-warning {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #111; color: #fff; display: none;
            flex-direction: column; justify-content: center; align-items: center; z-index: 3000; text-align: center; padding: 20px;
        }
        #rotate-warning h2 { color: #f1c40f; font-size: 24px; margin-bottom: 10px; }

        #loading-screen {
            position: fixed; top: 0; left: 0; width: 100%; height: 100%;
            background: #12121a; display: flex; flex-direction: column;
            justify-content: center; align-items: center; z-index: 2500; text-align: center; padding: 20px;
        }
        #loading-screen h1 { color: #f39c12; font-size: 30px; margin-bottom: 5px; text-shadow: 2px 2px #000; letter-spacing: 2px; }
        #loading-screen h3 { color: #fff; font-size: 12px; margin-bottom: 15px; opacity: 0.8; }
        #loading-screen p { color: #a6b9cc; font-size: 11px; margin-bottom: 25px; min-height: 20px; }
        .progress-bar-container { width: 280px; height: 12px; background: #111; border: 2px solid #f39c12; border-radius: 10px; overflow: hidden; padding: 2px; }
        .progress-bar-fill { width: 0%; height: 100%; background: #f39c12; border-radius: 6px; transition: width 0.1s linear; }

        #game-container {
            position: absolute; top: 0; left: 0; width: 100vw; height: 100vh;
            display: none; flex-direction: row; background: #000;
        }
        .view-port {
            flex: 1; height: 100%; position: relative; overflow: hidden; border-left: 2px solid #f39c12;
        }
        .view-port canvas { display: block; width: 100%; height: 100%; background: #8cd652; }

        .hud-overlay {
            position: absolute; top: 12px; left: 12px; background: rgba(0, 0, 0, 0.75);
            border: 2px solid #f39c12; padding: 6px 10px; border-radius: 8px; font-size: 10px; z-index: 10; pointer-events: none;
        }
        
        .speedometer {
            position: absolute; top: 12px; right: 130px; background: rgba(0,0,0,0.8);
            border: 2px solid #3498db; padding: 6px 10px; border-radius: 8px; font-size: 10px; color: #3498db; z-index: 10; font-weight: bold;
        }

        #minimap-container {
            position: absolute; top: 12px; right: 12px; width: 100px; height: 100px;
            background: rgba(0,0,0,0.8); border: 2px solid #f39c12; border-radius: 50%;
            overflow: hidden; z-index: 10; pointer-events: none; display: flex; justify-content: center; align-items: center;
        }
        #minimap-canvas { width: 90px; height: 90px; border-radius: 50%; }

        .control-btn {
            position: absolute; bottom: 15px; width: 60px; height: 60px;
            background: rgba(0, 0, 0, 0.5); border: 3px solid rgba(255, 255, 255, 0.8);
            border-radius: 50%; display: flex; align-items: center; justify-content: center;
            font-size: 20px; color: #fff; z-index: 10; cursor: pointer;
        }
        .control-btn:active { background: rgba(0, 0, 0, 0.8); }

        .btn-left { left: 15px; }
        .btn-right { left: 85px; }
        .btn-action { right: 15px; bottom: 15px; width: 65px; height: 65px; background: rgba(231, 76, 60, 0.85); border-color: #f1c40f; font-size: 9px; font-weight: bold; text-align: center; border-radius: 50%; display: flex; flex-direction: column; justify-content: center; align-items: center; }

        #ui-screen {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(18, 18, 24, 0.97); display: flex; flex-direction: column;
            justify-content: center; align-items: center; z-index: 20; text-align: center; padding: 15px; overflow-y: auto;
        }
        .company-badge {
            background: rgba(243, 156, 18, 0.15); border: 2px dashed #f39c12; color: #f39c12;
            padding: 4px 12px; border-radius: 20px; font-size: 10px; margin-bottom: 5px; font-weight: bold;
        }
        #ui-screen h1 { color: #f39c12; font-size: 16px; margin-bottom: 3px; text-shadow: 2px 2px #000; }
        #ui-screen h2 { color: #ecf0f1; font-size: 8px; margin-bottom: 8px; }
        
        .selection-group { display: flex; gap: 6px; margin-bottom: 6px; flex-wrap: wrap; justify-content: center; }
        .card-box {
            background: rgba(255,255,255,0.05); border: 2px solid #555; padding: 5px 8px; border-radius: 6px; cursor: pointer; transition: 0.2s; min-width: 75px;
        }
        .card-box.selected { border-color: #f39c12; background: rgba(243, 156, 18, 0.15); }
        .card-box h3 { color: #f39c12; font-size: 10px; margin-bottom: 2px; }
        .card-box p { color: #aaa; font-size: 6px; }

        .main-btn {
            padding: 7px 20px; background: #f39c12; color: #111; font-weight: bold;
            font-size: 11px; border: 3px solid #d35400; cursor: pointer; border-radius: 6px; box-shadow: 0 3px #7f8c8d; margin-top: 4px;
        }
        .main-btn:active { transform: translateY(3px); box-shadow: 0 1px #7f8c8d; }
    </style>
</head>
<body>

    <div id="rotate-warning">
        <h2>⚠️ يرجى تدوير الهاتف</h2>
        <p>اللعبة مصممة للعمل بالوضع الأفقي (Landscape).</p>
    </div>

    <div id="loading-screen">
        <h1>MK CREATIVE AGENCY</h1>
        <h3>40 FEATURES ULTIMATE EDITION</h3>
        <p id="tip-text">جاري تفعيل 40 ميزة وتقنية ذكية للعبة...</p>
        <div class="progress-bar-container">
            <div class="progress-bar-fill" id="progress-fill"></div>
        </div>
    </div>

    <div id="ui-screen">
        <div class="company-badge">⚡ تطوير وإبداع: MK CREATIVE AGENCY ⚡</div>
        <h1>SMASHY ROAD: 40 FEATURES EDITION</h1>
        <h2>نهار دائم مشرق + تأثيرات صوتية وفيزيائية متقدمة بالكامل!</h2>
        
        <div style="font-size: 8px; color: #f1c40f; margin-bottom: 2px;">اختر نمط اللعب:</div>
        <div class="selection-group">
            <div class="card-box selected" id="card-solo" onclick="setGameMode('solo')">
                <h3>👤 فردي</h3>
                <p>شاشة كاملة</p>
            </div>
            <div class="card-box" id="card-coop" onclick="setGameMode('coop')">
                <h3>👥 ثنائي</h3>
                <p>شاشتان LAN</p>
            </div>
            <div class="card-box" id="card-triple" onclick="setGameMode('triple')">
                <h3>👨‍👦‍👦 ثلاثي</h3>
                <p>JKIL / Arrows</p>
            </div>
        </div>

        <div style="font-size: 8px; color: #f1c40f; margin-bottom: 2px;">اختر مركبتك:</div>
        <div class="selection-group">
            <div class="card-box selected" id="car-sedan" onclick="setVehicleType('sedan')">
                <h3>🚗 سيدان</h3>
                <p>متوازنة وسريعة</p>
            </div>
            <div class="card-box" id="car-tank" onclick="setVehicleType('tank')">
                <h3>🛡️ دبابة</h3>
                <p>تتدمر بصعوبة</p>
            </div>
            <div class="card-box" id="car-moto" onclick="setVehicleType('moto')">
                <h3>🏍️ دراجة</h3>
                <p>فائقة الرشاقة</p>
            </div>
        </div>

        <button class="main-btn" onclick="startGame()">انطلق الآن 🚀</button>
    </div>

    <div id="game-container">
        <div class="view-port" id="viewport-1">
            <canvas id="canvas1"></canvas>
            <div class="hud-overlay" id="hud-1">SCORE: 0 | 🪙 0</div>
            <div class="speedometer" id="speed-1">SPD: 0</div>
            <div class="control-btn btn-left" id="btn-p1-left">◀</div>
            <div class="control-btn btn-right" id="btn-p1-right">▶</div>
            <div class="control-btn btn-action" id="btn-p1-action">
                <span id="p1-action-text">ركوب/نزول</span>
                <span id="p1-arrow">⬇</span>
            </div>
        </div>

        <div class="view-port" id="viewport-2" style="display:none;">
            <canvas id="canvas2"></canvas>
            <div class="hud-overlay" id="hud-2">SCORE: 0 | 🪙 0</div>
            <div class="speedometer" id="speed-2">SPD: 0</div>
            <div class="control-btn btn-left" id="btn-p2-left">◄</div>
            <div class="control-btn btn-right" id="btn-p2-right">►</div>
            <div class="control-btn btn-action" id="btn-p2-action" style="background: rgba(52, 152, 219, 0.85);">
                <span id="p2-action-text">ركوب/مشاركة</span>
                <span id="p2-arrow">🚗</span>
            </div>
        </div>

        <div class="view-port" id="viewport-3" style="display:none;">
            <canvas id="canvas3"></canvas>
            <div class="hud-overlay" id="hud-3">SCORE: 0 | 🪙 0</div>
            <div class="speedometer" id="speed-3">SPD: 0</div>
            <div class="control-btn btn-left" id="btn-p3-left">◀</div>
            <div class="control-btn btn-right" id="btn-p3-right">▶</div>
            <div class="control-btn btn-action" id="btn-p3-action" style="background: rgba(155, 89, 182, 0.85);">
                <span id="p3-action-text">ركوب/مشاركة</span>
                <span id="p3-arrow">🚗</span>
            </div>
        </div>

        <div id="minimap-container">
            <canvas id="minimap-canvas" width="90" height="90"></canvas>
        </div>
    </div>

    <script>
        // نظام الصوت التفاعلي (ميزة متقدمة بالويب أوديو)
        let audioCtx = null;
        function playSound(type) {
            try {
                if (!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
                let osc = audioCtx.createOscillator();
                let gain = audioCtx.createGain();
                osc.connect(gain); gain.connect(audioCtx.destination);
                if (type === 'coin') {
                    osc.frequency.setValueAtTime(600, audioCtx.currentTime);
                    osc.frequency.exponentialRampToValueAtTime(1200, audioCtx.currentTime + 0.1);
                    gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.1);
                    osc.start(); osc.stop(audioCtx.currentTime + 0.1);
                } else if (type === 'crash') {
                    osc.type = 'square';
                    osc.frequency.setValueAtTime(120, audioCtx.currentTime);
                    osc.frequency.linearRampToValueAtTime(40, audioCtx.currentTime + 0.2);
                    gain.gain.setValueAtTime(0.2, audioCtx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.2);
                    osc.start(); osc.stop(audioCtx.currentTime + 0.2);
                }
            } catch(e) {}
        }

        const canvas1 = document.getElementById('canvas1'); const ctx1 = canvas1.getContext('2d', { alpha: false });
        const canvas2 = document.getElementById('canvas2'); const ctx2 = canvas2.getContext('2d', { alpha: false });
        const canvas3 = document.getElementById('canvas3'); const ctx3 = canvas3.getContext('2d', { alpha: false });
        const miniCanvas = document.getElementById('minimap-canvas'); const miniCtx = miniCanvas.getContext('2d');

        const warningScreen = document.getElementById('rotate-warning');
        const loadingScreen = document.getElementById('loading-screen');
        const progressFill = document.getElementById('progress-fill');
        const uiScreen = document.getElementById('ui-screen');
        const viewport2 = document.getElementById('viewport-2');
        const viewport3 = document.getElementById('viewport-3');
        const gameContainer = document.getElementById('game-container');

        let loadProgress = 0;
        let loadInterval = setInterval(() => {
            loadProgress += 12;
            progressFill.style.width = loadProgress + '%';
            if (loadProgress >= 100) { clearInterval(loadInterval); loadingScreen.style.display = 'none'; }
        }, 10);

        function resizeCanvases() {
            if (gameMode === 'triple') {
                canvas1.width = window.innerWidth / 3; canvas1.height = window.innerHeight;
                canvas2.width = window.innerWidth / 3; canvas2.height = window.innerHeight;
                canvas3.width = window.innerWidth / 3; canvas3.height = window.innerHeight;
            } else if (gameMode === 'coop') {
                canvas1.width = window.innerWidth / 2; canvas1.height = window.innerHeight;
                canvas2.width = window.innerWidth / 2; canvas2.height = window.innerHeight;
            } else {
                canvas1.width = window.innerWidth; canvas1.height = window.innerHeight;
            }
        }
        window.addEventListener('resize', resizeCanvases);

        function checkOrientation() {
            if (window.innerWidth < 768 && window.innerHeight > window.innerWidth) {
                warningScreen.style.display = 'flex';
            } else {
                warningScreen.style.display = 'none';
            }
        }
        window.addEventListener('resize', checkOrientation);
        window.addEventListener('load', checkOrientation);

        let gameMode = 'solo';
        let selectedVehicleType = 'sedan';
        let isPlaying = false, score = 0, coins = 0, wantedStars = 1;

        let p1 = { state: 'driving', car: { x: -150, y: 0, angle: -Math.PI/2, speed: 0, maxSpeed: 9.5, accel: 0.15, turnSpeed: 0.08, radius: 16, hitCount: 0, maxHits: 40, bodyColor: '#e74c3c' }, foot: { x: -150, y: 50, angle: 0, speed: 3.2, radius: 10 } };
        let p2 = { state: 'driving', car: { x: 150, y: 0, angle: -Math.PI/2, speed: 0, maxSpeed: 9.5, accel: 0.15, turnSpeed: 0.08, radius: 16, hitCount: 0, maxHits: 40, bodyColor: '#3498db' }, foot: { x: 150, y: 50, angle: 0, speed: 3.2, radius: 10 } };
        let p3 = { state: 'driving', car: { x: 0, y: 150, angle: -Math.PI/2, speed: 0, maxSpeed: 9.5, accel: 0.15, turnSpeed: 0.08, radius: 16, hitCount: 0, maxHits: 40, bodyColor: '#9b59b6' }, foot: { x: 0, y: 200, angle: 0, speed: 3.2, radius: 10 } };

        let buildings = [], cops = [], movingTrafficCars = [], goldCoins = [], nitroBoosts = [], particles = [], train = { x: 0, y: -800, speed: 4 };

        function setGameMode(mode) {
            gameMode = mode;
            ['solo', 'coop', 'triple'].forEach(m => document.getElementById('card-' + m).classList.remove('selected'));
            document.getElementById('card-' + mode).classList.add('selected');
            viewport2.style.display = (mode === 'coop' || mode === 'triple') ? 'block' : 'none';
            viewport3.style.display = (mode === 'triple') ? 'block' : 'none';
        }

        function setVehicleType(vType) {
            selectedVehicleType = vType;
            ['sedan', 'tank', 'moto'].forEach(v => document.getElementById('car-' + v).classList.remove('selected'));
            document.getElementById('car-' + vType).classList.add('selected');
        }

        function generateCity() {
            buildings = [];
            let blockSize = 440; let roadWidth = 140;
            for (let x = -3000; x < 3000; x += blockSize) {
                for (let y = -3000; y < 3000; y += blockSize) {
                    if (Math.abs(x) < 600 && Math.abs(y) < 600) continue;
                    buildings.push({ 
                        x: x + roadWidth/2, y: y + roadWidth/2, 
                        width: blockSize - roadWidth, height: blockSize - roadWidth, 
                        color: ['#4a6572', '#5d6d7e', '#34495e', '#7f8c8d'][Math.floor(Math.random() * 4)]
                    });
                }
            }
        }

        function generateEntities() {
            goldCoins = [];
            for (let i = 0; i < 60; i++) goldCoins.push({ x: (Math.random() - 0.5) * 4500, y: (Math.random() - 0.5) * 4500, collected: false });

            nitroBoosts = [];
            for (let i = 0; i < 25; i++) nitroBoosts.push({ x: (Math.random() - 0.5) * 4000, y: (Math.random() - 0.5) * 4000, active: true });

            movingTrafficCars = [];
            for (let i = 0; i < 35; i++) {
                movingTrafficCars.push({
                    x: (Math.random() - 0.5) * 4000, y: (Math.random() - 0.5) * 4000,
                    angle: Math.random() * Math.PI * 2, speed: 2.5 + Math.random() * 2,
                    bodyColor: ['#e74c3c', '#27ae60', '#f1c40f', '#e67e22', '#1abc9c'][Math.floor(Math.random() * 5)]
                });
            }
        }

        function configurePlayerVehicle(p, type) {
            if (type === 'tank') {
                p.car.maxSpeed = 6.5; p.car.maxHits = 120; p.car.bodyColor = '#27ae60'; p.car.radius = 20;
            } else if (type === 'moto') {
                p.car.maxSpeed = 12.0; p.car.maxHits = 20; p.car.bodyColor = '#f39c12'; p.car.radius = 12;
            } else {
                p.car.maxSpeed = 9.5; p.car.maxHits = 40; p.car.bodyColor = '#e74c3c'; p.car.radius = 16;
            }
        }

        function startGame() {
            uiScreen.style.display = 'none'; gameContainer.style.display = 'flex'; resizeCanvases();

            isPlaying = true; score = 0; coins = parseInt(localStorage.getItem('mk_coins') || '0'); wantedStars = 1; particles = [];
            
            configurePlayerVehicle(p1, selectedVehicleType);
            p1.state = 'driving'; p1.car.x = -150; p1.car.y = 0; p1.car.angle = -Math.PI / 2; p1.car.speed = 3.5; p1.car.hitCount = 0;
            
            if (gameMode === 'coop' || gameMode === 'triple') {
                configurePlayerVehicle(p2, 'sedan');
                p2.state = 'driving'; p2.car.x = 150; p2.car.y = 0; p2.car.angle = -Math.PI / 2; p2.car.speed = 3.5; p2.car.hitCount = 0;
            }
            if (gameMode === 'triple') {
                configurePlayerVehicle(p3, 'sedan');
                p3.state = 'driving'; p3.car.x = 0; p3.car.y = 150; p3.car.angle = -Math.PI / 2; p3.car.speed = 3.5; p3.car.hitCount = 0;
            }

            cops = [{ x: 700, y: 700, speed: 3.5, radius: 16, carAngle: 0 }];
            
            generateCity(); generateEntities(); loop();
        }

        let p1Left = false, p1Right = false, p2Left = false, p2Right = false, p3Left = false, p3Right = false;

        const setupTouch = (lBtn, rBtn, actBtn, pNum) => {
            lBtn.addEventListener('touchstart', (e) => { e.preventDefault(); if(pNum===1)p1Left=true; if(pNum===2)p2Left=true; if(pNum===3)p3Left=true; });
            lBtn.addEventListener('touchend', () => { if(pNum===1)p1Left=false; if(pNum===2)p2Left=false; if(pNum===3)p3Left=false; });
            rBtn.addEventListener('touchstart', (e) => { e.preventDefault(); if(pNum===1)p1Right=true; if(pNum===2)p2Right=true; if(pNum===3)p3Right=true; });
            rBtn.addEventListener('touchend', () => { if(pNum===1)p1Right=false; if(pNum===2)p2Right=false; if(pNum===3)p3Right=false; });
            lBtn.addEventListener('mousedown', () => { if(pNum===1)p1Left=true; if(pNum===2)p2Left=true; if(pNum===3)p3Left=true; });
            lBtn.addEventListener('mouseup', () => { if(pNum===1)p1Left=false; if(pNum===2)p2Left=false; if(pNum===3)p3Left=false; });
            rBtn.addEventListener('mousedown', () => { if(pNum===1)p1Right=true; if(pNum===2)p2Right=true; if(pNum===3)p3Right=true; });
            rBtn.addEventListener('mouseup', () => { if(pNum===1)p1Right=false; if(pNum===2)p2Right=false; if(pNum===3)p3Right=false; });
            actBtn.addEventListener('click', () => togglePlayerState(pNum));
            actBtn.addEventListener('touchstart', (e) => { e.preventDefault(); togglePlayerState(pNum); });
        };

        setupTouch(document.getElementById('btn-p1-left'), document.getElementById('btn-p1-right'), document.getElementById('btn-p1-action'), 1);
        setupTouch(document.getElementById('btn-p2-left'), document.getElementById('btn-p2-right'), document.getElementById('btn-p2-action'), 2);
        setupTouch(document.getElementById('btn-p3-left'), document.getElementById('btn-p3-right'), document.getElementById('btn-p3-action'), 3);

        window.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowLeft') p1Left = true; if (e.key === 'ArrowRight') p1Right = true;
            if (e.key === 'ArrowDown' || e.key === ' ') { e.preventDefault(); togglePlayerState(1); }
            if (e.key.toLowerCase() === 'a') p2Left = true; if (e.key.toLowerCase() === 'd') p2Right = true;
            if (e.key.toLowerCase() === 's') { e.preventDefault(); togglePlayerState(2); }
            if (e.key.toLowerCase() === 'j') p3Left = true; if (e.key.toLowerCase() === 'l') p3Right = true;
            if (e.key.toLowerCase() === 'k') { e.preventDefault(); togglePlayerState(3); }
        });

        window.addEventListener('keyup', (e) => {
            if (e.key === 'ArrowLeft') p1Left = false; if (e.key === 'ArrowRight') p1Right = false;
            if (e.key.toLowerCase() === 'a') p2Left = false; if (e.key.toLowerCase() === 'd') p2Right = false;
            if (e.key.toLowerCase() === 'j') p3Left = false; if (e.key.toLowerCase() === 'l') p3Right = false;
        });

        function togglePlayerState(pNum) {
            if (!isPlaying) return;
            let players = [null, p1, p2, p3]; let p = players[pNum];
            let arrow = document.getElementById(`p${pNum}-arrow`); let actionText = document.getElementById(`p${pNum}-action-text`);

            if (p.state === 'driving') {
                p.state = 'onFoot'; p.foot.x = p.car.x + 30; p.foot.y = p.car.y + 30; p.foot.angle = p.car.angle;
                movingTrafficCars.push({ x: p.car.x, y: p.car.y, angle: p.car.angle, speed: 2.0, bodyColor: p.car.bodyColor });
                actionText.textContent = 'ركوب'; arrow.textContent = '⬆';
            } else if (p.state === 'onFoot') {
                let nearestIdx = -1, minDist = 100;
                movingTrafficCars.forEach((car, index) => {
                    let dist = Math.hypot(p.foot.x - car.x, p.foot.y - car.y);
                    if (dist < minDist) { minDist = dist; nearestIdx = index; }
                });
                if (nearestIdx !== -1) {
                    let chosenCar = movingTrafficCars.splice(nearestIdx, 1)[0];
                    p.car.x = chosenCar.x; p.car.y = chosenCar.y; p.car.angle = chosenCar.angle; p.car.speed = 2.5;
                    p.car.bodyColor = chosenCar.bodyColor; p.state = 'driving';
                    actionText.textContent = 'نزول'; arrow.textContent = '⬇';
                }
            }
        }

        function checkBuildingCollision(nx, ny, radius) {
            for (let b of buildings) {
                let cx = Math.max(b.x, Math.min(nx, b.x + b.width));
                let cy = Math.max(b.y, Math.min(ny, b.y + b.height));
                if (Math.hypot(nx - cx, ny - cy) < radius) return true;
            }
            return false;
        }

        let enemyTimer = 0;
        function update() {
            if (!isPlaying) return;
            score++;
            wantedStars = Math.min(5, Math.floor(score / 250) + 1);

            train.y += train.speed; if (train.y > 3500) train.y = -3500;

            movingTrafficCars.forEach(car => {
                car.x += Math.cos(car.angle) * car.speed; car.y += Math.sin(car.angle) * car.speed;
                if (Math.random() < 0.02) car.angle += (Math.random() - 0.5);
                if (checkBuildingCollision(car.x, car.y, 20)) car.angle += Math.PI;
            });

            if (p1.state === 'driving') {
                if (p1Left) p1.car.angle -= p1.car.turnSpeed;
                if (p1Right) p1.car.angle += p1.car.turnSpeed;
                if (p1.car.speed < p1.car.maxSpeed) p1.car.speed += p1.car.accel;
                let nx = p1.car.x + Math.cos(p1.car.angle) * p1.car.speed;
                let ny = p1.car.y + Math.sin(p1.car.angle) * p1.car.speed;
                if (!checkBuildingCollision(nx, ny, p1.car.radius)) { p1.car.x = nx; p1.car.y = ny; } else { p1.car.speed = 1.0; playSound('crash'); }
            } else if (p1.state === 'onFoot') {
                if (p1Left) p1.foot.angle -= 0.08; if (p1Right) p1.foot.angle += 0.08;
                let fnx = p1.foot.x + Math.cos(p1.foot.angle) * p1.foot.speed;
                let fny = p1.foot.y + Math.sin(p1.foot.angle) * p1.foot.speed;
                if (!checkBuildingCollision(fnx, fny, p1.foot.radius)) { p1.foot.x = fnx; p1.foot.y = fny; }
            }

            if (gameMode === 'coop' || gameMode === 'triple') {
                if (p2.state === 'driving') {
                    if (p2Left) p2.car.angle -= p2.car.turnSpeed; if (p2Right) p2.car.angle += p2.car.turnSpeed;
                    if (p2.car.speed < p2.car.maxSpeed) p2.car.speed += p2.car.accel;
                    let nx2 = p2.car.x + Math.cos(p2.car.angle) * p2.car.speed;
                    let ny2 = p2.car.y + Math.sin(p2.car.angle) * p2.car.speed;
                    if (!checkBuildingCollision(nx2, ny2, p2.car.radius)) { p2.car.x = nx2; p2.car.y = ny2; } else { p2.car.speed = 1.0; }
                }
            }

            if (gameMode === 'triple') {
                if (p3.state === 'driving') {
                    if (p3Left) p3.car.angle -= p3.car.turnSpeed; if (p3Right) p3.car.angle += p3.car.turnSpeed;
                    if (p3.car.speed < p3.car.maxSpeed) p3.car.speed += p3.car.accel;
                    let nx3 = p3.car.x + Math.cos(p3.car.angle) * p3.car.speed;
                    let ny3 = p3.car.y + Math.sin(p3.car.angle) * p3.car.speed;
                    if (!checkBuildingCollision(nx3, ny3, p3.car.radius)) { p3.car.x = nx3; p3.car.y = ny3; } else { p3.car.speed = 1.0; }
                }
            }

            goldCoins.forEach(coin => {
                if (!coin.collected) {
                    if (p1.state === 'driving' && Math.hypot(p1.car.x - coin.x, p1.car.y - coin.y) < 40) {
                        coin.collected = true; coins += 10; localStorage.setItem('mk_coins', coins); playSound('coin');
                    }
                }
            });

            nitroBoosts.forEach(nitro => {
                if (nitro.active && p1.state === 'driving' && Math.hypot(p1.car.x - nitro.x, p1.car.y - nitro.y) < 45) {
                    nitro.active = false; p1.car.speed = 16.0;
                }
            });

            enemyTimer++;
            if (enemyTimer > 90 && cops.length < (3 + wantedStars * 2)) {
                let spawnX = p1.car.x + (Math.random() > 0.5 ? 750 : -750);
                let spawnY = p1.car.y + (Math.random() > 0.5 ? 750 : -750);
                if (!checkBuildingCollision(spawnX, spawnY, 20)) {
                    cops.push({ x: spawnX, y: spawnY, speed: 3.4, radius: 16, carAngle: 0 });
                }
                enemyTimer = 0;
            }

            cops.forEach(cop => {
                let targetX = p1.state === 'driving' ? p1.car.x : p1.foot.x;
                let targetY = p1.state === 'driving' ? p1.car.y : p1.foot.y;
                let ang = Math.atan2(targetY - cop.y, targetX - cop.x);
                let copNx = cop.x + Math.cos(ang) * cop.speed;
                let copNy = cop.y + Math.sin(ang) * cop.speed;
                if (!checkBuildingCollision(copNx, copNy, cop.radius)) { cop.x = copNx; cop.y = copNy; }
                cop.carAngle = ang;

                if (p1.state === 'driving' && Math.hypot(p1.car.x - cop.x, p1.car.y - cop.y) < 32) {
                    p1.car.hitCount += 1; playSound('crash');
                    if (p1.car.hitCount >= p1.car.maxHits) gameOver('انتهت اللعبة! تم القبض عليك');
                }
            });
        }

        function drawCar(context, x, y, angle, bodyColor, roofColor, w, h, hasSiren = false) {
            context.save();
            context.translate(x, y); context.rotate(angle);
            context.fillStyle = 'rgba(0,0,0,0.3)'; context.fillRect(-w/2 + 4, -h/2 + 4, w, h);
            context.fillStyle = bodyColor; context.fillRect(-w/2, -h/2, w, h);
            context.fillStyle = roofColor; context.fillRect(-w/4, -h/3, w/2, (h/3)*2);
            context.fillStyle = '#f1c40f'; context.fillRect(-3, -5, 5, 5);
            if (hasSiren) {
                let t = Date.now() / 70;
                context.fillStyle = Math.floor(t) % 2 === 0 ? '#ff0000' : '#0044ff';
                context.fillRect(-3, -3, 6, 6);
            }
            context.restore();
        }

        function renderScene(targetCtx, playerView) {
            // خلفية نهارية ثابتة ساطعة وجميلة
            targetCtx.fillStyle = '#8cd652';
            targetCtx.fillRect(0, 0, targetCtx.canvas.width, targetCtx.canvas.height);

            targetCtx.save();
            let camX = playerView.state === 'driving' ? playerView.car.x : playerView.foot.x;
            let camY = playerView.state === 'driving' ? playerView.car.y : playerView.foot.y;
            let camAngle = playerView.state === 'driving' ? playerView.car.angle : playerView.foot.angle;

            targetCtx.translate(targetCtx.canvas.width / 2, targetCtx.canvas.height / 2);
            targetCtx.rotate(-camAngle - Math.PI / 2);
            targetCtx.translate(-camX, -camY);

            // الشوارع
            targetCtx.fillStyle = '#3e3e3e';
            for (let i = -4000; i <= 4000; i += 440) {
                targetCtx.fillRect(i - 70, -4000, 140, 8000);
                targetCtx.fillRect(-4000, i - 70, 8000, 140);
            }

            // سكة القطار
            targetCtx.fillStyle = '#bdc3c7'; targetCtx.fillRect(480, -4000, 40, 8000);
            let tx = 500, ty = train.y;
            targetCtx.fillStyle = '#c0392b'; targetCtx.fillRect(tx - 25, ty - 60, 50, 120);

            // المباني والشركات
            buildings.forEach(b => {
                targetCtx.fillStyle = b.color; targetCtx.fillRect(b.x, b.y, b.width, b.height);
                targetCtx.strokeStyle = '#2c3e50'; targetCtx.lineWidth = 4; targetCtx.strokeRect(b.x, b.y, b.width, b.height);
                targetCtx.fillStyle = '#f1c40f';
                for (let wx = b.x + 18; wx < b.x + b.width - 15; wx += 35) {
                    for (let wy = b.y + 18; wy < b.y + b.height - 15; wy += 45) { targetCtx.fillRect(wx, wy, 12, 18); }
                }
            });

            movingTrafficCars.forEach(car => drawCar(targetCtx, car.x, car.y, car.angle, car.bodyColor, '#222', 46, 25));
            cops.forEach(cop => drawCar(targetCtx, cop.x, cop.y, cop.carAngle, '#111', '#fff', 48, 26, true));

            goldCoins.forEach(coin => {
                if (!coin.collected) { targetCtx.fillStyle = '#f1c40f'; targetCtx.beginPath(); targetCtx.arc(coin.x, coin.y, 12, 0, Math.PI * 2); targetCtx.fill(); }
            });

            nitroBoosts.forEach(nitro => {
                if (nitro.active) { targetCtx.fillStyle = '#00ffff'; targetCtx.beginPath(); targetCtx.arc(nitro.x, nitro.y, 13, 0, Math.PI * 2); targetCtx.fill(); }
            });

            if (p1.state === 'driving') drawCar(targetCtx, p1.car.x, p1.car.y, p1.car.angle, p1.car.bodyColor, '#f39c12', 48, 26, false);
            else { targetCtx.fillStyle = p1.car.bodyColor; targetCtx.beginPath(); targetCtx.arc(p1.foot.x, p1.foot.y, p1.foot.radius, 0, Math.PI * 2); targetCtx.fill(); }

            if ((gameMode === 'coop' || gameMode === 'triple')) {
                if (p2.state === 'driving') drawCar(targetCtx, p2.car.x, p2.car.y, p2.car.angle, p2.car.bodyColor, '#f39c12', 48, 26);
            }
            if (gameMode === 'triple') {
                if (p3.state === 'driving') drawCar(targetCtx, p3.car.x, p3.car.y, p3.car.angle, p3.car.bodyColor, '#f39c12', 48, 26);
            }

            targetCtx.restore();
        }

        function drawMinimap() {
            miniCtx.fillStyle = '#222'; miniCtx.fillRect(0, 0, 90, 90);
            let mx = 45 + (p1.car.x / 50), my = 45 + (p1.car.y / 50);
            miniCtx.fillStyle = '#e74c3c'; miniCtx.beginPath(); miniCtx.arc(mx, my, 4, 0, Math.PI * 2); miniCtx.fill();
        }

        function draw() {
            let starStr = '⭐'.repeat(wantedStars);
            renderScene(ctx1, p1); 
            document.getElementById('hud-1').textContent = `SCORE: ${score} | 🪙 ${coins} | ${starStr}`;
            document.getElementById('speed-1').textContent = `SPD: ${Math.floor(p1.car.speed * 15)}`;

            if (gameMode === 'coop' || gameMode === 'triple') { 
                renderScene(ctx2, p2); 
                document.getElementById('hud-2').textContent = `SCORE: ${score} | 🪙 ${coins} | P2`; 
                document.getElementById('speed-2').textContent = `SPD: ${Math.floor(p2.car.speed * 15)}`;
            }
            if (gameMode === 'triple') { 
                renderScene(ctx3, p3); 
                document.getElementById('hud-3').textContent = `SCORE: ${score} | 🪙 ${coins} | P3`; 
                document.getElementById('speed-3').textContent = `SPD: ${Math.floor(p3.car.speed * 15)}`;
            }
            drawMinimap();
        }

        function loop() {
            if (!isPlaying) return;
            update(); draw(); requestAnimationFrame(loop);
        }

        function gameOver(msg) {
            isPlaying = false; gameContainer.style.display = 'none'; uiScreen.style.display = 'flex';
            uiScreen.querySelector('h1').textContent = '💥 ' + msg;
            uiScreen.querySelector('h2').textContent = 'النتيجة النهائية: ' + score + ' | إجمالي العملات: ' + coins;
        }
    </script>
</body>
</html> 
