<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Neon Car Runner</title>
<style>
    * { box-sizing: border-box; }
    body {
        margin: 0;
        overflow: hidden;
        background: #101020;
        font-family: Arial;
    }

    canvas {
        display: block;
        margin: auto;
        background: linear-gradient(#15152e, #202040);
    }

    #info {
        position: fixed;
        top: 15px;
        left: 15px;
        color: white;
        font-size: 22px;
        font-weight: bold;
        text-shadow: 0 0 10px cyan;
    }
</style>
</head>

<body>

<div id="info">Score: 0</div>
<canvas id="game" width="500" height="700"></canvas>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let car = {
    x: 225,
    y: 590,
    width: 50,
    height: 90,
    speed: 7
};

let enemies = [];
let score = 0;
let gameOver = false;
let roadSpeed = 6;

const keys = {};

document.addEventListener("keydown", e => {
    keys[e.key] = true;

    if (gameOver && e.key === "Enter") {
        location.reload();
    }
});

document.addEventListener("keyup", e => {
    keys[e.key] = false;
});

function drawRoad() {
    // Grass
    ctx.fillStyle = "#16823b";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    // Road
    ctx.fillStyle = "#303038";
    ctx.fillRect(80, 0, 340, canvas.height);

    // Road edges
    ctx.fillStyle = "#ffffff";
    ctx.fillRect(75, 0, 5, canvas.height);
    ctx.fillRect(420, 0, 5, canvas.height);

    // Lane lines
    ctx.fillStyle = "#ffe600";

    for (let y = -40; y < canvas.height; y += 100) {
        let yy = (y + score * roadSpeed) % 100;
        ctx.fillRect(165, yy, 8, 55);
        ctx.fillRect(327, yy, 8, 55);
    }
}

function drawCar() {
    // Shadow
    ctx.fillStyle = "rgba(0,0,0,0.4)";
    ctx.beginPath();
    ctx.ellipse(car.x + 25, car.y + 85, 30, 10, 0, 0, Math.PI * 2);
    ctx.fill();

    // Body
    let gradient = ctx.createLinearGradient(
        car.x, car.y, car.x + 50, car.y + 90
    );

    gradient.addColorStop(0, "#00eaff");
    gradient.addColorStop(0.5, "#0066ff");
    gradient.addColorStop(1, "#8a00ff");

    ctx.fillStyle = gradient;
    ctx.roundRect(car.x, car.y, 50, 90, 12);
    ctx.fill();

    // Windows
    ctx.fillStyle = "#111827";
    ctx.roundRect(car.x + 8, car.y + 12, 34, 28, 8);
    ctx.fill();

    // Lights
    ctx.fillStyle = "#fff700";
    ctx.fillRect(car.x + 6, car.y + 5, 12, 7);
    ctx.fillRect(car.x + 32, car.y + 5, 12, 7);

    // Wheels
    ctx.fillStyle = "#080808";
    ctx.fillRect(car.x - 6, car.y + 18, 7, 25);
    ctx.fillRect(car.x + 49, car.y + 18, 7, 25);
    ctx.fillRect(car.x - 6, car.y + 58, 7, 25);
    ctx.fillRect(car.x + 49, car.y + 58, 7, 25);
}

function drawEnemy(enemy) {
    ctx.fillStyle = enemy.color;
    ctx.roundRect(enemy.x, enemy.y, 50, 90, 12);
    ctx.fill();

    ctx.fillStyle = "#111";
    ctx.roundRect(enemy.x + 8, enemy.y + 12, 34, 28, 8);
    ctx.fill();

    ctx.fillStyle = "#ff2222";
    ctx.fillRect(enemy.x + 7, enemy.y + 75, 12, 7);
    ctx.fillRect(enemy.x + 31, enemy.y + 75, 12, 7);
}

function spawnEnemy() {
    const lanes = [105, 225, 345];

    enemies.push({
        x: lanes[Math.floor(Math.random() * lanes.length)],
        y: -100,
        color: ["#ff1744", "#ff9100", "#00e676", "#e040fb"][
            Math.floor(Math.random() * 4)
        ]
    });
}

function collision(a, b) {
    return (
        a.x < b.x + 50 &&
        a.x + a.width > b.x &&
        a.y < b.y + 90 &&
        a.y + a.height > b.y
    );
}

function update() {
    if (gameOver) return;

    if (keys["ArrowLeft"] && car.x > 85)
        car.x -= car.speed;

    if (keys["ArrowRight"] && car.x < 365)
        car.x += car.speed;

    enemies.forEach(enemy => {
        enemy.y += roadSpeed;

        if (collision(car, enemy)) {
            gameOver = true;
        }
    });

    enemies = enemies.filter(enemy => {
        if (enemy.y > canvas.height) {
            score++;
            return false;
        }
        return true;
    });

    if (Math.random() < 0.025)
        spawnEnemy();

    roadSpeed = 6 + score * 0.03;

    document.getElementById("info").innerText =
        "Score: " + score;
}

function draw() {
    drawRoad();

    enemies.forEach(drawEnemy);
    drawCar();

    if (gameOver) {
        ctx.fillStyle = "rgba(0,0,0,0.7)";
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        ctx.fillStyle = "#fff";
        ctx.textAlign = "center";
        ctx.font = "bold 50px Arial";
        ctx.fillText("GAME OVER", 250, 320);

        ctx.font = "25px Arial";
        ctx.fillText("Press ENTER to restart", 250, 370);
        ctx.fillText("Score: " + score, 250, 420);
    }
}

function gameLoop() {
    update();
    draw();
    requestAnimationFrame(gameLoop);
}

gameLoop();
</script>

</body>
</html>
