# tower-game <!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>لعبة البرج</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
            background-color: #f0f0f0;
        }
        canvas {
            background-color: #87ceeb;
            display: block;
            margin: 0 auto;
            border: 2px solid #000;
        }
        button {
            padding: 10px 20px;
            font-size: 18px;
            cursor: pointer;
        }
    </style>
</head>
<body>

<h1>لعبة البرج</h1>
<canvas id="gameCanvas" width="500" height="600"></canvas>
<button onclick="addFloor()">أضف طابق</button>

<script>
// الحصول على عنصر الـ canvas
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");

// المتغيرات
let floors = []; // مصفوفة لتخزين الطوابق
let obstacles = []; // لتخزين العوائق في كل طابق
let floorHeight = 40; // ارتفاع كل طابق
let currentHeight = canvas.height; // موقع البرج على المحور الرأسي

// رسم البرج
function drawTower() {
    ctx.clearRect(0, 0, canvas.width, canvas.height); // مسح الشاشة

    // رسم الطوابق
    floors.forEach((floor) => {
        ctx.fillStyle = "darkblue";
        ctx.fillRect(floor.x, floor.y, floor.width, floor.height); // رسم الطابق
    });

    // رسم العوائق
    drawObstacles();
}

// رسم العوائق في كل طابق
function drawObstacles() {
    obstacles.forEach((obstacle) => {
        ctx.fillStyle = "red";
        ctx.fillRect(obstacle.x, obstacle.y, obstacle.width, obstacle.height);
    });
}

// إضافة طابق جديد
function addFloor() {
    const floorWidth = Math.random() * (canvas.width - 100) + 50; // عرض الطابق عشوائي بين 50 و 450
    const floorX = (canvas.width - floorWidth) / 2; // مركز الطابق في العرض
    const floorY = currentHeight - floorHeight; // تحديد ارتفاع الطابق

    // إضافة الطابق إلى المصفوفة
    floors.push({ x: floorX, y: floorY, width: floorWidth, height: floorHeight });

    // إضافة العائق إلى الطابق
    if (Math.random() > 0.5) { // عائق يظهر بنسبة 50%
        const obstacleWidth = 20 + Math.random() * 40; // عرض العائق عشوائي
        const obstacleX = floorX + Math.random() * (floorWidth - obstacleWidth); // تحديد مكان العائق داخل الطابق
        const obstacleHeight = 20; // ارتفاع العائق ثابت

        obstacles.push({
            x: obstacleX,
            y: floorY - obstacleHeight, // وضع العائق على نفس مستوى الطابق
            width: obstacleWidth,
            height: obstacleHeight
        });
    }

    // تحديث الارتفاع الحالي
    currentHeight -= floorHeight;

    // رسم البرج من جديد
    drawTower();
}

// استدعاء الدالة عند تحميل الصفحة
drawTower();
</script>

</body>
</html>