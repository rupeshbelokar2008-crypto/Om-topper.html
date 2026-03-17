<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Story Game</title>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial;
}

body {
  background: black;
}

/* Story container */
.story {
  width: 100%;
  max-width: 360px;
  height: 100vh;
  margin: auto;
  background: linear-gradient(to top, #000, #1a1a1a);
  position: relative;
  overflow: hidden;
  color: white;
}

/* Progress bar */
.progress {
  height: 4px;
  width: 0%;
  background: white;
  position: absolute;
  top: 0;
  left: 0;
}

/* Game section */
.game {
  text-align: center;
  margin-top: 120px;
}

.circle {
  width: 70px;
  height: 70px;
  background: red;
  border-radius: 50%;
  margin: 20px auto;
  cursor: pointer;
  position: relative;
}

/* Score */
.score {
  margin-top: 10px;
  font-size: 18px;
}

/* Message */
.message {
  position: absolute;
  bottom: 80px;
  width: 100%;
  text-align: center;
  font-size: 22px;
  opacity: 0;
  transition: 0.5s;
}

.show {
  opacity: 1;
}

/* Start Button */
.startBtn {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  padding: 10px 20px;
  border: none;
  border-radius: 10px;
  background: white;
  font-weight: bold;
}
</style>

</head>
<body>

<div class="story">
  
  <div id="bar" class="progress"></div>

  <div class="game">
    <h3>Tap Fast 🎯</h3>
    <div id="circle" class="circle"></div>
    <div class="score">Score: <span id="score">0</span></div>
  </div>

  <div id="msg" class="message">
    🔥 OM TOPPER HAI 😎
  </div>

  <button class="startBtn" onclick="startGame()">START</button>

</div>

<script>
let score = 0;
let time = 0;
let gameRunning = false;

function startGame() {
  gameRunning = true;
  document.querySelector(".startBtn").style.display = "none";

  // progress bar start
  let bar = document.getElementById("bar");
  let interval = setInterval(() => {
    if (time >= 100) {
      clearInterval(interval);
      endGame();
    } else {
      time++;
      bar.style.width = time + "%";
    }
  }, 100);

  // click event
  document.getElementById("circle").onclick = () => {
    if (!gameRunning) return;

    score++;
    document.getElementById("score").innerText = score;

    // move circle randomly
    let c = document.getElementById("circle");
    c.style.position = "absolute";
    c.style.top = Math.random() * 500 + "px";
    c.style.left = Math.random() * 250 + "px";
  };
}

function endGame() {
  gameRunning = false;

  if (score >= 5) {
    document.getElementById("msg").classList.add("show");
  } else {
    document.getElementById("msg").innerText = "😂 Too Slow!";
    document.getElementById("msg").classList.add("show");
  }
}
</script>

</body>
</html>
