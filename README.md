<!DOCTYPE html>
<html>
<head>
  <title>heylol</title>
  <style>
    body {
      margin: 0;
      font-family: 'Comic Sans MS', cursive;
      background-color: black;
      color: white;
      text-align: center;
      overflow: hidden;
    }

    .card {
      background: #1a1a1a;
      border-radius: 20px;
      box-shadow: 0 10px 30px rgba(255, 255, 255, 0.1);
      padding: 40px;
      max-width: 600px;
      margin: 100px auto;
      position: relative;
      z-index: 5;
    }

    h1 {
      font-size: 2.5em;
      color: #ff69b4;
    }

    .buttons {
      margin-top: 30px;
      position: relative;
      height: 100px;
    }

    button {
      font-size: 20px;
      padding: 10px 20px;
      border: none;
      border-radius: 10px;
      margin: 10px;
      cursor: pointer;
      position: absolute;
      transition: transform 0.3s ease;
      user-select: none;
    }

    .yes {
      background-color: #ff69b4;
      color: white;
      left: 30%;
      z-index: 10;
    }

    .no {
      background-color: #ccc;
      left: 60%;
      z-index: 10;
    }

    /* Glass Shatter Styles */
    .glass-shatter-container {
      position: fixed;
      top: 0; left: 0;
      width: 100vw; height: 100vh;
      pointer-events: none;
      z-index: 100;
      backdrop-filter: brightness(0.6) blur(1.5px);
    }

    .shard {
      position: absolute;
      width: 150px;
      height: 150px;
      background: url('https://i.imgur.com/0x7KxZf.png') no-repeat center/contain;
      opacity: 1;
      animation: shardFly 1s forwards;
    }

    @keyframes shardFly {
      to {
        opacity: 0;
        transform: translate(var(--x), var(--y)) rotate(var(--rot));
      }
    }

    #videoContainer {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      z-index: 20;
    }

    iframe {
      width: 100%;
      height: 100%;
      border: none;
    }

    /* Floating Cat GIFs */
    .cat {
      position: fixed;
      width: 80px;
      animation: float 5s infinite ease-in-out;
      z-index: 1;
      user-select: none;
      pointer-events: none;
    }

    @keyframes float {
      0% { transform: translateY(0) rotate(0deg); }
      50% { transform: translateY(-20px) rotate(5deg); }
      100% { transform: translateY(0) rotate(0deg); }
    }
  </style>
</head>
<body>
  <div class="card" id="card">
    <h1>heylol,</h1>
    <p>we should like be together unplatonically..</p>
    <div class="buttons">
      <button class="yes" onclick="yesClicked()">YES</button>
      <button class="no" id="noBtn">no</button>
    </div>
  </div>

  <div id="videoContainer">
    <iframe src="https://www.youtube.com/embed/[YOUTUBE_VIDEO_ID]?autoplay=1" allow="autoplay; encrypted-media" allowfullscreen></iframe>
  </div>

  <!-- Floating Cat GIFs -->
  <script>
    const catGifs = [
      "https://media.giphy.com/media/JIX9t2j0ZTN9S/giphy.gif",
      "https://media.giphy.com/media/mlvseq9yvZhba/giphy.gif",
      "https://media.giphy.com/media/13borq7Zo2kulO/giphy.gif",
      "https://media.giphy.com/media/l1J9urFG4lFQK0pTO/giphy.gif"
    ];

    for (let i = 0; i < 5; i++) {
      const cat = document.createElement("img");
      cat.src = catGifs[i % catGifs.length];
      cat.className = "cat";

      const posX = Math.random() * window.innerWidth;
      const posY = Math.random() * (window.innerHeight - 200) + 50;

      cat.style.left = posX + "px";
      cat.style.top = posY + "px";

      document.body.appendChild(cat);
    }
  </script>

  <script>
    const noBtn = document.getElementById('noBtn');
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
    let clickCount = 0;

    noBtn.addEventListener('mouseenter', () => {
      const offsetX = Math.random() * 300 - 150;
      const offsetY = Math.random() * 100 - 50;
      noBtn.style.transform = `translate(${offsetX}px, ${offsetY}px)`;
    });

    noBtn.addEventListener('click', () => {
      alert(noMessages[clickCount % noMessages.length]);
      clickCount++;
    });

    function createShatter() {
      const container = document.createElement('div');
      container.className = 'glass-shatter-container';

      const shardCount = 8;
      for(let i = 0; i < shardCount; i++) {
        const shard = document.createElement('div');
        shard.className = 'shard';

        shard.style.top = (window.innerHeight / 2 + (Math.random() * 100 - 50)) + 'px';
        shard.style.left = (window.innerWidth / 2 + (Math.random() * 100 - 50)) + 'px';

        const x = (Math.random() * 600 - 300) + 'px';
        const y = (Math.random() * 600 - 300) + 'px';
        const rot = (Math.random() * 720 - 360) + 'deg';

        shard.style.setProperty('--x', x);
        shard.style.setProperty('--y', y);
        shard.style.setProperty('--rot', rot);

        shard.style.animationDelay = (i * 0.1) + 's';

        container.appendChild(shard);
      }

      document.body.appendChild(container);

      setTimeout(() => container.remove(), 1200);
    }

    function yesClicked() {
      createShatter();

      setTimeout(() => {
        document.getElementById('card').style.display = 'none';
        document.getElementById('videoContainer').style.display = 'block';
      }, 1200);
    }
  </script>
</body>
</html>
