<!DOCTYPE html>
<html>
<head>
  <title>Hey [Their Name] 😊</title>
  <style>
    body {
      font-family: 'Comic Sans MS', cursive;
      background: #fff0f5;
      text-align: center;
      padding: 50px;
    }

    .card {
      background: white;
      border-radius: 20px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.1);
      padding: 40px;
      max-width: 600px;
      margin: auto;
      position: relative;
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
  </style>
</head>
<body>
  <div class="card">
    <h1>Hey [Their Name],</h1>
    <p>I was wondering... would you go out with me? 💕</p>
    <div class="buttons">
      <button class="yes" onclick="alert('YAY! 🎉 Let me know when you’re free!')">Yes 💖</button>
      <button class="no" id="noBtn">No 😢</button>
    </div>
  </div>

  <script>
    const noBtn = document.getElementById('noBtn');
    const noMessages = [
      "You're not supposed to click this 😠",
      "Seriously, don't press that again 🙃",
      "Rude. Try again? 😤",
      "Now you're just messing with me 😑",
      "Click yes. Just do it 😩",
      "Help. I'm fragile 💔",
      "You're hurting my CSS feelings 🥲",
      "YES IS RIGHT THERE 💡",
      "Okay now I'm crying 😭",
      "I'll never financially recover from this 🐅"
    ];
    let clickCount = 0;

    // Move button randomly
    noBtn.addEventListener('mouseover', () => {
      const btn = noBtn;
      const offsetX = Math.random() * 300 - 150;
      const offsetY = Math.random() * 100 - 50;
      btn.style.transform = `translate(${offsetX}px, ${offsetY}px)`;
    });

    // Show different messages on each click
    noBtn.addEventListener('click', () => {
      alert(noMessages[clickCount % noMessages.length]);
      clickCount++;
    });
  </script>
</body>
</html>
