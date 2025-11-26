# Repository-name-1
My new project
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dodge Game</title>
<style>
    body {
        margin: 0;
        background: #111;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        color: #fff;
        font-family: Arial;
    }

    #game {
        width: 400px;
        height: 600px;
        background: #222;
        position: relative;
        overflow: hidden;
        border: 3px solid #fff;
    }

    .player {
        width: 40px;
        height: 40px;
        background: lime;
        position: absolute;
        bottom: 20px;
        left: 180px;
    }

    .enemy {
        width: 40px;
        height: 40px;
        background: red;
        position: absolute;
        top: -40px;
    }

    #score {
        position: absolute;
        top: 10px;
        left: 10px;
        font-size: 20px;
    }
</style>
</head>

<body>
<div id="game">
    <div id="score">Score: 0</div>
    <div class="player" id="player"></div>
</div>

<script>
    const game = document.getElementById("game");
    const player = document.getElementById("player");
    const scoreBox = document.getElementById("score");

    let playerX = 180;
    let score = 0;

    document.addEventListener("keydown", (e) => {
        if (e.key === "ArrowLeft" && playerX > 0) {
            playerX -= 20;
        }
        if (e.key === "ArrowRight" && playerX < 360) {
            playerX += 20;
        }
        player.style.left = playerX + "px";
    });

    function spawnEnemy() {
        const enemy = document.createElement("div");
        enemy.classList.add("enemy");
        enemy.style.left = Math.floor(Math.random() * 360) + "px";
        game.appendChild(enemy);

        let enemyY = -40;
        const fall = setInterval(() => {
            enemyY += 5;
            enemy.style.top = enemyY + "px";

            // Collision
            if (
                enemyY > 540 &&
                enemyY < 600 &&
                Math.abs(parseInt(enemy.style.left) - playerX) < 40
            ) {
                alert("Game Over! Score: " + score);
                location.reload();
            }

            // Remove enemy & increase score
            if (enemyY > 600) {
                clearInterval(fall);
                enemy.remove();
                score++;
                scoreBox.innerText = "Score: " + score;
            }
        }, 20);
    }

    setInterval(spawnEnemy, 1000);
</script>
</body>
</html>

