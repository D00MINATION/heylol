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

    /* Background image behind the card */
    body::before {
      content: "";
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: url('https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=1950&q=80') no-repeat center center fixed;
      background-size: cover;
      opacity: 0.2;
      z-index: 0;
    }

    .card {
      background: rgba(26, 26, 26, 0.85);
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

    /* Hide default buttons */
    button {
      border: none;
      background: none;
      cursor: pointer;
      position: absolute;
      transition: transform 0.3s ease;
      width: 120px;
      height: 60px;
      padding: 0;
    }

    /* Use images inside buttons */
    button img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      pointer-events: none;
      user-select: none;
    }

    .yes {
      left: 30%;
      top: 20px;
    }

    .no {
      left: 60%;
      top: 20px;
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
      width: 112px; /* 80 * 1.4 = 112 */
      animation: float 5s infinite ease-in-out;
      z-index: 1;
      cursor: pointer;
    }

    @keyframes float {
      0% { transform: translateY(0) rotate(0deg); }
      50% { transform: translateY(-20px) rotate(5deg); }
      100% { transform: translateY(0) rotate(0deg); }
    }

    /* Shake animation */
    @keyframes shake {
      0%, 100% { transform: translate(0, 0) rotate(0deg); }
      20% { transform: translate(-10px, 5px) rotate(-5deg); }
      40% { transform: translate(10px, -5px) rotate(5deg); }
      60% { transform: translate(-10px, 5px) rotate(-5deg); }
      80% { transform: translate(10px, -5px) rotate(5deg); }
    }

    .red-overlay {
      position: fixed;
      top: 0; left: 0;
      width: 100vw; height: 100vh;
      background-color: red;
      color: black;
      font-size: 2em;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 100;
      display: none;
      user-select: none;
    }
  </style>
</head>
<body>
  <div class="card" id="card">
    <h1>heylol,</h1>
    <p>we should like be together unplatonically..</p>
    <div class="buttons">
      <button class="yes" onclick="yesClicked()">
        <img src="https://i.imgur.com/1JQZPvm.png" alt="Yes Button"/>
      </button>
      <button class="no" id="noBtn">
        <img src="https://i.imgur.com/k5vH0n9.png" alt="No Button"/>
      </button>
    </div>
  </div>

  <div id="videoContainer">
    <iframe src="https://www.youtube.com/embed/[YOUTUBE_VIDEO_ID]?autoplay=1" allow="autoplay; encrypted-media" allowfullscreen></iframe>
  </div>

  <!-- Red overlay div -->
  <div class="red-overlay" id="redOverlay">rude..</div>

  <script>
    const catGifs = [
      "https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExMjFlc2hjdnR1MzRncHd5aW1ueG1lczdqbWJjdTl1Nzh1aHN4c3hyZSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xI1pK446iNJeg/giphy.gif",
      "https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExeXdqY3k4bTh4aDFza2JyMzB0ZW0wZTJ0NXoyd3JvMmlhNm5sMDVyZSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/GxN4ics7OlvsA/giphy.gif",
      "https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExYWk1cnY3MGNjcHhjNmhzaWgzMDRuN2drbGZoenh1Z2J6NDluMDZqZCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/NimEavznszKtW/giphy.gif",
      "https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExanVndXI3M2ttbTVzaTkxbzRzYXA0NTFxM3dia2ExdG1scnBoeXNrZSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/NfzERYyiWcXU4/giphy.gif",
      "https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExM3QzdTE0b3E1bnoydzFremdkM3JlYnFjaWhnMDh1YmVqajltOGJjOCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/12bjQ7uASAaCKk/giphy.gif",
      "https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExdDl1NHA0a2tiOTF1aGY3YmMyZWFuY29mdjdxYjhra3Z0d2wycnV4diZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/dRcMsUUrnR8He/giphy.gif",
      "https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExbWdnOGV1NzNtZW9xcXFwcHR5MWd6cDdnb25ha2g3Nmk1YTJpNG1ldyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/bJJJODH3T9Fug/giphy.gif",
      "https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExNTFrOTQ0dnozMTJma2Z2eHBjOXk5azc0bDd3bmJpbGM5MDhpMjQ0eiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/pV0RpkmUZ5UB2/giphy.gif",
      "https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExb3gyZnptaW1lM24yaTN6NGw4czJ6eWJjOHl6cWY4NDdvMDFsajJobiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/amCh2vTHXpQyI/giphy.gif",
      "https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExdXhhM3M1YXpxY3hoMm4ybXdxMWhmMHhoZ295ZGp0dGhsNnZvYjhqdSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/13Rgcvb54ffxAc/giphy.gif"
    ];

    // Create audio element for meow
    const meowAudio = new Audio('https://www.soundjay.com/animal/cat-meow-1.mp3');

    catGifs.forEach((url) => {
      const cat = document.createElement("img");
      cat.src = url;
      cat.className = "cat";

      const posX = Math.random() * window.innerWidth;
      const posY = Math.random() * (window.innerHeight - 200) + 50;

      cat.style.left = posX + "px";
      cat.style.top = posY + "px";

      // Play meow on click
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
    let clickCount = 0;

    noBtn.addEventListener('click', () => {
      // Move button to random place on screen
      const btnWidth = noBtn.offsetWidth;
      const btnHeight = noBtn.offsetHeight;

      const maxX = window.innerWidth - btnWidth;
      const maxY = window.innerHeight - btnHeight;

      const newX = Math.random() * maxX;
      const newY = Math.random() * maxY;

      noBtn.style.transform = `translate(${newX - noBtn.offsetLeft}px, ${newY - noBtn.offsetTop}px)`;

      // Show red overlay with message & shake
      const message = noMessages[clickCount % noMessages.length];
      redOverlay.textContent = message;
      redOverlay.style.display = 'flex';
      redOverlay.style.animation = 'shake 0.5s';

      // Remove shake animation after done so it can be replayed later
      redOverlay.addEventListener('animationend', () => {
        redOverlay.style.animation = '';
      }, { once: true });

      setTimeout(() => {
        redOverlay.style.display = 'none';
      }, 5000);

      clickCount++;
    });

    function yesClicked() {
      document.getElementById('card').style.display = 'none';
      document.getElementById('videoContainer').style.display = 'block';
    }
  </script>
</body>
</html>
