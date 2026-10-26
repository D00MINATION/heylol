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
      background: url('https://www.dropbox.com/scl/fi/exrhhdu9sxtqc01i9kndg/7568db94-ac22-4e82-8bde-9fe5e2836d32.jpg?rlkey=tgwj8mvegqxdg2m9wqay86oe0&st=ydfvgyt9&dl=0') no-repeat center center;
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
      position: relative;
      height: 100px;
      z-index: 6;
    }

    button.interactive-btn {
      font-family: 'Old Newspaper Types', serif;
      font-size: 1.5em;
      padding: 15px 30px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      transition: top 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275), 
                  left 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275), 
                  transform 0.2s ease,
                  background-color 0.3s ease;
      z-index: 50;
      background-color: #32cd32;
      color: white;
      box-shadow: 0 8px 20px rgba(0,0,0,0.5);
    }

    button.interactive-btn:hover {
      filter: brightness(1.1);
    }

    /* Embedded Popup Container Animations */
    #embedModal {
      display: flex;
      opacity: 0;
      pointer-events: none;
      position: fixed;
      top: 0; left: 0;
      width: 100vw; height: 100vh;
      background: rgba(0, 0, 0, 0.65);
      backdrop-filter: blur(6px);
      z-index: 100;
      justify-content: center;
      align-items: center;
      transition: opacity 0.4s ease;
    }

    #embedModal.active {
      opacity: 1;
      pointer-events: auto;
    }

    .embed-card {
      background: rgba(20, 20, 20, 0.95);
      border: 2px solid rgba(255, 255, 255, 0.2);
      border-radius: 20px;
      padding: 24px;
      width: 90%;
      max-width: 720px;
      box-shadow: 0 20px 50px rgba(0,0,0,0.8);
      transform: scale(0.7);
      transition: transform 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      display: flex;
      flex-direction: column;
      align-items: center;
      position: relative;
    }

    #embedModal.active .embed-card {
      transform: scale(1);
    }

    .embed-card-header {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 15px;
    }

    .embed-card-title {
      font-size: 1.8em;
      margin: 0;
      animation: rainbow 4s infinite;
      letter-spacing: 1px;
    }

    .close-btn {
      background: rgba(255, 255, 255, 0.15);
      border: none;
      color: white;
      font-size: 1.2em;
      width: 36px;
      height: 36px;
      border-radius: 50%;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: background 0.2s ease;
    }

    .close-btn:hover {
      background: rgba(255, 0, 0, 0.6);
    }

    .video-wrapper {
      width: 100%;
      aspect-ratio: 16 / 9;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.5);
    }

    .video-wrapper iframe {
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
    <div class="buttons">
      <button class="interactive-btn" id="clickBtn">click me</button>
    </div>
  </div>

  <!-- Animated Embed Container -->
  <div id="embedModal" onclick="handleModalBgClick(event)">
    <div class="embed-card">
      <div class="embed-card-header">
        <h3 class="embed-card-title">❤️ for my goated wife ❤️</h3>
        <button class="close-btn" onclick="closeEmbedModal()">✕</button>
      </div>
      <div class="video-wrapper">
        <!-- Using the /e/ embed route for clean playback without website banners -->
        <iframe id="videoIframe" src="https://streamable.com/khscec" allow="autoplay" allowfullscreen></iframe>
      </div>
    </div>
  </div>

  <script>
    const catGifs = [
      "https://media3.giphy.com/media/v1.Y2lkPTZjMDliOTUycTloang2NTF2NmY3YmMxYnRsNzllc2NmbTd0cG9wbWttdnpnbXo4ZCZlcD12MV9naWZzX3NlYXJjaCZjdD1n/HSCZMUa1ao17h7l5mg/giphy.gif",
      "https://i0.wp.com/media1.giphy.com/media/11fIOE3vkIPdIY/giphy.gif",
      "https://livingoffleesh.com/wp-content/uploads/2017/02/charlie-brown-happy-valentines-cute-greetings-animated-gif-2.gif?w=500",
      "https://media3.giphy.com/media/v1.Y2lkPTZjMDliOTUycTloang2NTF2NmY3YmMxYnRsNzllc2NmbTd0cG9wbWttdnpnbXo4ZCZlcD12MV9naWZzX3NlYXJjaCZjdD1n/HSCZMUa1ao17h7l5mg/giphy.gif",
      "https://i0.wp.com/media1.giphy.com/media/11fIOE3vkIPdIY/giphy.gif",
      "https://livingoffleesh.com/wp-content/uploads/2017/02/charlie-brown-happy-valentines-cute-greetings-animated-gif-2.gif?w=500",
      "https://media3.giphy.com/media/v1.Y2lkPTZjMDliOTUycTloang2NTF2NmY3YmMxYnRsNzllc2NmbTd0cG9wbWttdnpnbXo4ZCZlcD12MV9naWZzX3NlYXJjaCZjdD1n/HSCZMUa1ao17h7l5mg/giphy.gif",
      "https://i0.wp.com/media1.giphy.com/media/11fIOE3vkIPdIY/giphy.gif"
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

    // Teleportation Logic
    const clickBtn = document.getElementById('clickBtn');
    let attempts = 0;
    const maxAttempts = 4; // Teleports 4 times before action

    function teleportButton() {
      if (attempts < maxAttempts) {
        attempts++;
        const btnWidth = clickBtn.offsetWidth || 150;
        const btnHeight = clickBtn.offsetHeight || 50;
        const padding = 80;

        const maxX = window.innerWidth - btnWidth - padding;
        const maxY = window.innerHeight - btnHeight - padding;

        const newX = Math.max(padding, Math.floor(Math.random() * maxX));
        const newY = Math.max(padding, Math.floor(Math.random() * maxY));
        
        clickBtn.style.left = newX + 'px';
        clickBtn.style.top = newY + 'px';
        clickBtn.style.transform = 'none';

        if (attempts === maxAttempts) {
          clickBtn.textContent = "my fault big dawg ill let u click me now ❤️";
          clickBtn.style.backgroundColor = "#ff1493";
        }
      } else {
        openEmbedModal();
      }
    }

    clickBtn.addEventListener('mouseover', () => {
      if (attempts < maxAttempts) {
        teleportButton();
      }
    });

    clickBtn.addEventListener('click', (e) => {
      e.stopPropagation();
      teleportButton();
    });

    // Embed Modal Animation functions
    const embedModal = document.getElementById('embedModal');

    function openEmbedModal() {
      // Option A: Clean embed popup modal (active by default)
      embedModal.classList.add('active');

      // Option B: If you prefer opening Streamable in a new browser tab directly instead, uncomment the line below:
      // window.open('https://streamable.com/khscec', '_blank');
    }

    function closeEmbedModal() {
      embedModal.classList.remove('active');
    }

    function handleModalBgClick(e) {
      if (e.target === embedModal) {
        closeEmbedModal();
      }
    }

    // Bouncing DVD-style text animation
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
