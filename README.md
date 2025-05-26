<!DOCTYPE html>
<html>
<head>
  <title>heylol</title>
  <style>
    body {
      margin: 0;
      font-family: 'Comic Sans MS', cursive;
      background: black;
      color: white;
      text-align: center;
      overflow: hidden;
      position: relative;
      height: 100vh;
      width: 100vw;
      z-index: 0;
    }

    /* Fullscreen cat gif background slideshow */
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

    /* Questionnaire background behind yes/no buttons */
    .questionnaire-bg {
      position: absolute;
      top: 110px; /* aligned under card header */
      left: 0;
      right: 0;
      height: 180px; /* roughly the height behind buttons */
      background: url('https://dl.dropboxusercontent.com/s/me8s6ds3k6ouixylctwv6/WhatsApp-Image-2025-05-07-at-23.29.15_aa5cb6f4.jpg?dl=0') no-repeat center center;
      background-size: cover;
      z-index: 4;
      filter: brightness(0.75);
      border-radius: 15px;
      max-width: 600px;
      margin: 0 auto;
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
      z-index: 6;
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

    #videoContainer iframe {
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
      background: url('https://dl.dropboxusercontent.com/s/dq43zxv8nd35mu0d2ayie/ja.jpg?dl=0') no-repeat center center;
      background-size: cover;
      color: black;
      font-size: 2em;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 100;
      user-select: none;
      text-shadow: 1px 1px 2px white;
      display: none;
    }
  </style>
</head>
<body>

  <!-- Fullscreen cat gif background slideshow -->
  <div id="catBackground"></div>

  <div class="card" id="card">
    <h1>heylol,</h1>
    <p>we should like be together unplatonically..</p>
    
    <!-- Questionnaire background behind buttons -->
    <div class="questionnaire-bg"></div>

    <div class="buttons">
      <button class="yes" onclick="yesClicked()">
        <img src="https://www.dropbox.com/scl/fi/e02jjrs99hczwqe6y0ztp/yes.png?rlkey=drwjuaxhzppjiw4pr31zw3ob8&st=fvzqqes9&dl=1" alt="Yes Button"/>
      </button>
      <button class="no" id="noBtn">
        <img src="https://www.dropbox.com/scl/fi/uko3m164r6uwzic8w5h2y/no.png?rlkey=w4q01c1czp3v2ifi07q6qsfx3&st=0h41kaeb&dl=1" alt="No Button"/>
      </button>
    </div>
  </div>

  <div id="videoContainer">
    <iframe src="https://www.youtube.com/embed/[YOUTUBE_VIDEO_ID]?autoplay=1" allow="autoplay; encrypted-media" allowfullscreen></iframe>
  </div>

  <!-- Overlay that replaces the red wall -->
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

    // Fullscreen cat background slideshow variables
    const catBackground = document.getElementById('catBackground');
    let currentIndex = 0;

    function showNextCat() {
      catBackground.style.backgroundImage = `url(${catGifs[currentIndex]})`;
      currentIndex = (currentIndex + 1) % catGifs.length;
    }

    // Start slideshow
    showNextCat();
    setInterval(showNextCat, 5000); // Change every 5 seconds

    // Create floating small cats on screen with meow sound on click
    const meowAudio = new Audio('https://www.soundjay.com/animal/cat-meow-1.mp3');

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

    // No button logic
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
      const btnWidth = noBtn.offsetWidth;
      const btnHeight = noBtn.offsetHeight;

      const maxX = window.innerWidth - btnWidth;
      const maxY = window.innerHeight - btnHeight;

      const newX = Math.random() * maxX;
      const newY = Math.random() * maxY;

      noBtn.style.transform = `translate(${newX - noBtn.offsetLeft}px, ${newY - noBtn.offsetTop}px)`;

      // Show message immediately, with shake animation
      const message = noMessages[clickCount % noMessages.length];
      redOverlay.textContent = message;
      redOverlay.style.display = 'flex';
      redOverlay.style.animation = 'shake 0.5s';

      // Remove animation on end so it can be retriggered next time
      redOverlay.addEventListener('animationend', () => {
        redOverlay.style.animation = '';
      }, { once: true });

      // Hide message after 5 seconds
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
