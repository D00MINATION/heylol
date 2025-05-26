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
    }

    .yes {
      background-color: #ff69b4;
      color: white;
      left: 30%;
    }

    .no {
      background-color: #ccc;
      left: 60%;
    }

    .crack-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: url('https://i.imgur.com/0x7KxZf.png') center center no-repeat;
      background-size: cover;
      z-index: 10;
      animation: crackFade 1.2s ease-out forwards;
      pointer-events: none;
    }

    @keyframes crackFade {
      0% { opacity: 0; transform: scale(1.5); }
      50% { opacity: 1; transform: scale(1); }
      100% { opacity: 0; }
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

    .cat {
      position: fixed;
      width: 80px;
      animation: float 5s infinite ease-in-out;
      z-index: 1;
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

    noBtn.addEventListener('mouseover', () => {
      const offsetX = Math.random() * 300 - 150;
      const offsetY = Math.random() * 100 - 50;
      noBtn.style.transform = `translate(${offsetX}px, ${offsetY}px)`;
    });

    noBtn.addEventListener('click', () => {
      alert(noMessages[clickCount % noMessages.length]);
      clickCount++;
    });

    function yesClicked() {
      const crack = document.createElement('div');
      crack.classList.add('crack-overlay');
      document.body.appendChild(crack);

      setTimeout(() => {
        document.getElementById('card').style.display = 'none';
        document.getElementById('videoContainer').style.display = 'block';
      }, 1200);
    }
  </script>
</body>
</html>
