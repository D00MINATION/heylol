<!DOCTYPE html>
<html>
<head>
  <title>heylol</title>
  <link href="https://fonts.googleapis.com/css2?family=Old+Newspaper+Types&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      font-family: 'Old Newspaper Types', serif;
      background: black;
      color: white;
      text-align: center;
      overflow: hidden;
      position: relative;
      height: 100vh;
      width: 100vw;
      z-index: 0;
    }

    @keyframes rainbow {
      0% { color: red; }
      14% { color: orange; }
      28% { color: yellow; }
      42% { color: green; }
      57% { color: blue; }
      71% { color: indigo; }
      85% { color: violet; }
      100% { color: red; }
    }

    #bouncingText {
      position: absolute;
      font-size: 2.5em;
      animation: rainbow 5s infinite;
      z-index: 10;
      user-select: none;
    }

    #catBackground {
      position: fixed;
      top: 0; left: 0;
      width: 100vw;
      height: 100vh;
      z-index: 0;
      pointer-events: none;
      background-position: center;
      background-repeat: no-repeat;
      background-size: contain;
      filter: brightness(0.7);
    }

    .questionnaire-bg {
      position: absolute;
      top: 110px;
      left: 0;
      right: 0;
      height: 180px;
      background: url('https://dl.dropboxusercontent.com/s/me8s6ds3k6ouixylctwv6/WhatsApp-Image-2025-05-07-at-23.29.15_aa5cb6f4.jpg?dl=0') no-repeat center center;
      background-size: cover;
      z-index: 4;
      filter: brightness(0.75);
      border-radius: 15px;
      max-width: 600px;
      margin: 0 auto;
    }

    .card {
      max-width: 600px;
      margin: 100px auto;
      position: relative;
      z-index: 5;
    }
.buttons {
  margin-top: 30px;
  display: flex;
  justify-content: center;
  gap: 40px;
  z-index: 6;
}

button {
  font-family: 'Old Newspaper Types', serif;
  font-size: 1.5em;
  padding: 15px 30px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: transform 0.3s ease;
  position: relative;
}

.yes {
  background-color: #32cd32;
  color: white;
}

.no {
  background-color: #dc143c;
  color: white;
}
    }

    #videoContainer {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      z-index: 20;
    }

    #videoContainer iframe {
      width: 100%;
      height: 100%;
      border: none;
    }

    .cat {
      position: fixed;
      width: 112px;
      animation: float 5s infinite ease-in-out;
      z-index: 1;
      cursor: pointer;
    }

    @keyframes float {
      0% { transform: translateY(0) rotate(0deg); }
      50% { transform: translateY(-20px) rotate(5deg); }
      100% { transform: translateY(0) rotate(0deg); }
    }

    .red-overlay {
      position: fixed;
      top: 0; left: 0;
      width: 100vw; height: 100vh;
      background: url('https://www.dropbox.com/scl/fi/dq43zxv8nd35mu0d2ayie/ja.jpg?rlkey=kb0r3edgs8mospwye8379a9tw&st=nl2scune&dl=1') no-repeat center center;
      background-size: cover;
      color: red;
      font-size: 2em;
      display: none;
      justify-content: center;
      align-items: center;
      z-index: 100;
      user-select: none;
      text-shadow: 1px 1px 4px black;
      flex-direction: column;
      padding: 20px;
      text-align: center;
      font-weight: bold;
      font-family: 'Old Newspaper Types', serif;
    }
  </style>
</head>
<body>

  <div id="catBackground"></div>

  <div id="bouncingText">heylol, we should like be together unplatonically..</div>

  <div class="card" id="card">
    <div class="questionnaire-bg"></div>
    <div class="buttons">
      <button class="yes" onclick="yesClicked()">YES</button>
      <button class="no" id="noBtn">NO</button>
    </div>
  </div>

  <div id="videoContainer">
    <iframe src="https://streamable.com/e/ct9xuk" frameborder="0" allowfullscreen></iframe>
  </div>

  <div class="red-overlay" id="redOverlay"></div>

  <script>
    const catGifs = [
      "https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExMjFlc2hjdnR1MzRncHd5aW1ueG1lczdqbWJjdTl1Nzh1aHN4c3hyZSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xI1pK446iNJeg/giphy.gif",
      "https://media4.giphy.com/media/GxN4ics7OlvsA/giphy.gif",
      "https://media4.giphy.com/media/NimEavznszKtW/giphy.gif",
      "https://media2.giphy.com/media/NfzERYyiWcXU4/giphy.gif",
      "https://media1.giphy.com/media/12bjQ7uASAaCKk/giphy.gif",
      "https://media1.giphy.com/media/dRcMsUUrnR8He/giphy.gif",
      "https://media2.giphy.com/media/bJJJODH3T9Fug/giphy.gif",
      "https://media4.giphy.com/media/pV0RpkmUZ5UB2/giphy.gif",
      "https://media3.giphy.com/media/amCh2vTHXpQyI/giphy.gif",
      "https://media2.giphy.com/media/13Rgcvb54ffxAc/giphy.gif"
    ];

    const catBackground = document.getElementById('catBackground');
    let currentIndex = 0;

    function showNextCat() {
      catBackground.style.backgroundImage = `url(${catGifs[currentIndex]})`;
      currentIndex = (currentIndex + 1) % catGifs.length;
    }

    showNextCat();
    setInterval(showNextCat, 5000);

    const meowAudio = new Audio('https://www.dl.dropboxusercontent.com/scl/fi/elhkh3jlikp2vsixi634n/cat-meow-14536.mp3?rlkey=ig1qswq3zr3y4sot9z71u7rlq&raw=1');

    catGifs.forEach((url) => {
      const cat = document.createElement("img");
      cat.src = url;
      cat.className = "cat";

      const posX = Math.random() * window.innerWidth;
      const posY = Math.random() * (window.innerHeight - 200) + 50;

      cat.style.left = posX + "px";
      cat.style.top = posY + "px";

      cat.addEventListener('click', () => {
        meowAudio.currentTime = 0;
        meowAudio.play();
      });

      document.body.appendChild(cat);
    });

    const noBtn = document.getElementById('noBtn');
    const redOverlay = document.getElementById('redOverlay');
    const noMessages = [
      "ur not supposed to pick this one",
      "NUHUH PRESS YES",
      "o hello",
      "the yes button is actually the no button like justsayinglike yknow",
      "yes dubao..",
      "OYE",
      "????",
      "PRESSYES",
      "bach jao",
      "rude.."
    ];

    noBtn.addEventListener('click', () => {
      const message = noMessages[Math.floor(Math.random() * noMessages.length)];
      redOverlay.textContent = message;
      redOverlay.style.display = 'flex';
      setTimeout(() => {
        redOverlay.style.display = 'none';
      }, 5000);
    });

    function yesClicked() {
      document.getElementById('card').style.display = 'none';
      document.getElementById('videoContainer').style.display = 'block';
    }

    // Bouncing DVD-style animation
    const bounceText = document.getElementById("bouncingText");
    let dx = 2;
    let dy = 2;
    let x = 100;
    let y = 100;

    function moveText() {
      const box = bounceText.getBoundingClientRect();
      const width = window.innerWidth;
      const height = window.innerHeight;

      if (x + box.width >= width || x <= 0) dx = -dx;
      if (y + box.height >= height || y <= 0) dy = -dy;

      x += dx;
      y += dy;

      bounceText.style.left = x + "px";
      bounceText.style.top = y + "px";
      requestAnimationFrame(moveText);
    }

    moveText();
  </script>
</body>
</html>
