<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>MK CREATIVE - First Person 3D</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            user-select: none;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: #030712;
            color: #fff;
            overflow: hidden;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        #rotate-warning {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #030712;
            display: none;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            text-align: center;
            padding: 20px;
        }
        #rotate-warning h2 {
            color: #00ffcc;
            font-size: 24px;
            margin-bottom: 10px;
        }
        #rotate-warning p {
            color: #8892b0;
            font-size: 14px;
        }

        canvas {
            display: block;
            width: 100vw;
            height: 100vh;
            background: #050b14;
        }

        #ui-screen {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(5, 11, 20, 0.95);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 20;
            text-align: center;
            padding: 20px;
        }
        #ui-screen h1 {
            color: #00ffcc;
            font-size: 34px;
            margin-bottom: 8px;
            text-shadow: 0 0 20px rgba(0, 255, 204, 0.5);
        }
        #ui-screen p {
            color: #8892b0;
            font-size: 15px;
            margin-bottom: 25px;
        }
        .main-btn {
            padding: 14px 40px;
            background: #00ffcc;
            color: #050b14;
            font-weight: bold;
            font-size: 18px;
            border: none;
            cursor: pointer;
            border-radius: 8px;
            box-shadow: 0 0 20px rgba(0, 255, 204, 0.4);
            transition: 0.3s;
        }
        .main-btn:hover {
            background: #64ffda;
            transform: scale(1.05);
        }
    </style>
</head>
<body>

    <div id="rotate-warning">
        <h2>⚠️ يرجى تدوير الهاتف</h2>
        <p>لتجربة منظور الشخص الأول ثلاثي الأبعاد، يرجى وضع هاتفك في الوضع الأفقي (Landscape)</p>
    </div>

    <div id="ui-screen">
        <h1>MK CREATIVE 3D WORLD</h1>
        <p>ادخل عالم الوكالة بمنظور ثلاثي الأبعاد وتفادى العوائق!</p>
        <button class="main-btn" onclick="startGame()">ابدأ التجربة</button>
    </div>

    <canvas id="gameCanvas"></canvas>

    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const warningScreen = document.getElementById('rotate-warning');
        const uiScreen = document.getElementById('ui-screen');

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        function checkOrientation() {
            if (window.innerHeight > window.innerWidth) {
                warningScreen.style.display = 'flex';
            } else {
                warningScreen.style.display = 'none';
            }
        }
        window.addEventListener('resize', checkOrientation);
        window.addEventListener('load', checkOrientation);

        let isPlaying = false;
        let score = 0;
        let playerX = 0; // -1 (يسار), 0 (وسط), 1 (يمين)
        let obstacles = [];
        let speed = 4;

        function startGame() {
            if (window.innerHeight > window.innerWidth) {
                alert("يرجى تدوير الهاتف بالعرض أولاً!");
                return;
            }
            uiScreen.style.display = 'none';
            isPlaying = true;
            score = 0;
            playerX = 0;
            obstacles = [];
            speed = 4;
            loop();
        }

        // تحكم باللمس أو الأسهم يمين ويسار
        window.addEventListener('keydown', (e) => {
            if (!isPlaying) return;
            if (e.key === 'ArrowLeft' && playerX > -1) playerX--;
            if (e.key === 'ArrowRight' && playerX < 1) playerX++;
        });

        // تحكم باللمس على الشاشة (النصف الأيمن والأيسر)
        window.addEventListener('touchstart', (e) => {
            if (!isPlaying) return;
            let touchX = e.touches[0].clientX;
            if (touchX < window.innerWidth / 2 && playerX > -1) {
                playerX--;
            } else if (touchX >= window.innerWidth / 2 && playerX < 1) {
                playerX++;
            }
        });

        function spawnObstacle() {
            let lanes = [-1, 0, 1];
            let lane = lanes[Math.floor(Math.random() * lanes.length)];
            obstacles.push({
                lane: lane,
                z: 100 // يبعد من الأعماق
            });
        }

        let spawnTimer = 0;

        function update() {
            if (!isPlaying) return;

            spawnTimer++;
            if (spawnTimer > 60) {
                spawnObstacle();
                spawnTimer = 0;
            }

            for (let i = obstacles.length - 1; i >= 0; i--) {
                let obs = obstacles[i];
                obs.z -= speed;

                // التحقق من الاصطدام عندما تقترب العقبة منك (z close to 0)
                if (obs.z <= 5 && obs.z >= 0) {
                    if (obs.lane === playerX) {
                        gameOver();
                    }
                }

                // حساب النقاط عند تجاوز العقبة
                if (obs.z < 0) {
                    obstacles.splice(i, 1);
                    score += 10;
                    if (score % 50 === 0) speed += 0.5;
                }
            }
        }

        function draw() {
            ctx.fillStyle = '#030712';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            let cx = canvas.width / 2;
            let cy = canvas.height / 2;

            // رسم خطوط المنظور (Tunnel Effect)
            ctx.strokeStyle = '#1e293b';
            ctx.lineWidth = 2;

            // نقطة التلاشي في المنتصف
            let vanishX = cx;
            let vanishY = cy - 50;

            // أرضية الوكالة 3D
            ctx.fillStyle = '#0a192f';
            ctx.beginPath();
            ctx.moveTo(0, canvas.height);
            ctx.lineTo(canvas.width, canvas.height);
            ctx.lineTo(vanishX + 100, vanishY);
            ctx.lineTo(vanishX - 100, vanishY);
            ctx.closePath();
            ctx.fill();

            // رسم العقبات القادمة بمنظور 3D
            for (let obs of obstacles) {
                let scale = 100 / obs.z;
                if (scale <= 0) continue;

                let laneWidth = 120 * scale;
                let objX = vanishX + (obs.lane * laneWidth) - (40 * scale);
                let objY = vanishY + (obs.z * 2 * scale);
                let objSize = 80 * scale;

                ctx.fillStyle = '#00ffcc';
                ctx.shadowBlur = 15;
                ctx.shadowColor = '#00ffcc';
                ctx.fillRect(objX, objY, objSize, objSize);
                ctx.shadowBlur = 0;
            }

            // رسم مكان اللاعب الحالي (مؤشر تحت)
            ctx.fillStyle = '#64ffda';
            let playerIndicatorX = vanishX + (playerX * 120) - 25;
            ctx.fillRect(playerIndicatorX, canvas.height - 60, 50, 15);

            // واجهة النصوص والأعلى
            ctx.fillStyle = '#ffffff';
            ctx.font = 'bold 22px Segoe UI';
            ctx.textAlign = 'right';
            ctx.fillText('النقاط: ' + score, canvas.width - 30, 40);
            ctx.textAlign = 'left';
            ctx.fillText('MK CREATIVE AGENCY (3D)', 30, 40);
        }

        function loop() {
            if (!isPlaying) return;
            update();
            draw();
            requestAnimationFrame(loop);
        }

        function gameOver() {
            isPlaying = false;
            uiScreen.style.display = 'flex';
            uiScreen.querySelector('h1').textContent = 'اصطدام!';
            uiScreen.querySelector('p').textContent = 'حققت نتيجة: ' + score + ' نقطة في عالم 3D. تحب تحاول تاني؟';
            uiScreen.querySelector('.main-btn').textContent = 'إلعب مرة أخرى';
        }
    </script>
</body>
</html> 
