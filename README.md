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
      position: relative;
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
      width: 112px; /* 80px + 40% */
      animation: float 5s infinite ease-in-out;
      z-index: 1;
    }

    @keyframes float {
      0% { transform: translateY(0) rotate(0deg); }
      50% { transform: translateY(-20px) rotate(5deg); }
      100% { transform: translateY(0) rotate(0deg); }
    }

    /* Red Wall overlay for "no" clicks */
    #redWall {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100vw;
      height: 100vh;
      background-color: red;
      color: black;
      font-size: 3em;
      font-weight: bold;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 200;
      user-select: none;
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

  <div id="redWall">NOOOOOOOO 😠</div>

  <!-- Floating Cat GIFs -->
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
    const redWall = document.getElementById('redWall');
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

      // Show red wall overlay
      redWall.style.display = 'flex';

      // Hide red wall after 1.5 seconds
      setTimeout(() => {
        redWall.style.display = 'none';
      }, 1500);
    });

    function yesClicked() {
      // Just hide card and show video - no glass shatter effect
      document.getElementById('card').style.display = 'none';
      document.getElementById('videoContainer').style.display = 'block';
    }
  </script>
</body>
</html>
