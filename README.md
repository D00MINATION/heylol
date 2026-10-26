<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>i love you zozo</title>
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
      white-space: nowrap;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.8);
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
      background: url('https://www.dropbox.com/scl/fi/wnutm9ghtbylu8wr5j68x/naenase.mp4?rlkey=ne1xdndsbmaqww5vm1cug2bti&st=43v0e60o&dl=0') no-repeat center center;
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

    /* Interactive button styles */
    #actionBtn {
      font-family: 'Old Newspaper Types', serif;
      font-size: 1.5em;
      padding: 15px 30px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      position: absolute;
      top: 220px;
      left: 50%;
      transform: translateX(-50%);
      background-color: #32cd32;
      color: white;
      transition: top 0.2s ease, left 0.2s ease, transform 0.2s ease;
      z-index: 15;
      box-shadow: 0 4px 12px rgba(0,0,0,0.4);
    }

    #actionBtn:hover {
      filter: brightness(1.1);
    }

    #videoContainer {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      z-index: 20;
      background: black;
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
  </style>
</head>
<body>

  <div id="catBackground"></div>

  <div id="bouncingText">i love you zozo</div>

  <div class="card" id="card">
    <div class="questionnaire-bg"></div>
    <!-- Single "click me" button -->
    <button id="actionBtn" onclick="handleButtonClick(event)">click me</button>
  </div>

  <div id="videoContainer">
    <iframe id="videoIframe" src="https://streamable.com/e/qb7i8k" frameborder="0" allowfullscreen></iframe>
  </div>

  <script>
    // Configuration & State
    let attemptCount = 0;
    const MAX_ATTEMPTS = 4; // Teleports 4 times before staying clickable
    const FINAL_REDIRECT_URL = "https://streamable.com/e/qb7i8k"; // URL to open or display

    const catGifs = [
      "https://media3.giphy.com/media/v1.Y2lkPTZjMDliOTUycTloang2NTF2NmY3YmMxYnRsNzllc2NmbTd0cG9wbWttdnpnbXo4ZCZlcD12MV9naWZzX3NlYXJjaCZjdD1n/HSCZMUa1ao17h7l5mg/giphy.gif",
      "https://i0.wp.com/media1.giphy.com/media/11fIOE3vkIPdIY/giphy.gif",
      "https://livingoffleesh.com/wp-content/uploads/2017/02/charlie-brown-happy-valentines-cute-greetings-animated-gif-2.gif?w=500",
      "https://media3.giphy.com/media/v1.Y2lkPTZjMDliOTUycTloang2NTF2NmY3YmMxYnRsNzllc2NmbTd0cG9wbWttdnpnbXo4ZCZlcD12MV9naWZzX3NlYXJjaCZjdD1n/HSCZMUa1ao17h7l5mg/giphy.gif",
      "https://i0.wp.com/media1.giphy.com/media/11fIOE3vkIPdIY/giphy.gif",
      "https://livingoffleesh.com/wp-content/uploads/2017/02/charlie-brown-happy-valentines-cute-greetings-animated-gif-2.gif?w=500"
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

    // Spawn floating cats
    catGifs.forEach((url) => {
      const cat = document.createElement("img");
      cat.src = url;
      cat.className = "cat";

      const posX = Math.random() * (window.innerWidth - 120);
      const posY = Math.random() * (window.innerHeight - 200) + 50;

      cat.style.left = posX + "px";
      cat.style.top = posY + "px";

      cat.addEventListener('click', () => {
        meowAudio.currentTime = 0;
        meowAudio.play().catch(() => {});
      });

      document.body.appendChild(cat);
    });

    // Teleportation logic for "click me" button
    const actionBtn = document.getElementById('actionBtn');

    function teleportButton() {
      const btnWidth = actionBtn.offsetWidth || 150;
      const btnHeight = actionBtn.offsetHeight || 50;

      const maxX = window.innerWidth - btnWidth - 20;
      const maxY = window.innerHeight - btnHeight - 20;

      const randomX = Math.max(20, Math.floor(Math.random() * maxX));
      const randomY = Math.max(20, Math.floor(Math.random() * maxY));

      // Set fixed positioning so it can move anywhere on screen
      actionBtn.style.position = 'fixed';
      actionBtn.style.transform = 'none';
      actionBtn.style.left = randomX + 'px';
      actionBtn.style.top = randomY + 'px';
    }

    // Try teleporting on mouseover if attempts remain
    actionBtn.addEventListener('mouseenter', () => {
      if (attemptCount < MAX_ATTEMPTS) {
        attemptCount++;
        teleportButton();
      }
    });

    function handleButtonClick(e) {
      if (attemptCount < MAX_ATTEMPTS) {
        e.preventDefault();
        attemptCount++;
        teleportButton();
      } else {
        // Trigger video container presentation or redirect
        document.getElementById('card').style.display = 'none';
        actionBtn.style.display = 'none';
        document.getElementById('videoContainer').style.display = 'block';
        
        // Optional browser redirect:
        // window.location.href = FINAL_REDIRECT_URL;
      }
    }

    // DVD Bouncing Text Animation
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
