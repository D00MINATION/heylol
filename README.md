<!DOCTYPE html>
<html>
<head>
  <title>Hey, I have a question for you...</title>
  <style>
    body {
      font-family: sans-serif;
      background: #fbeeff;
      text-align: center;
      padding-top: 100px;
    }
    .card {
      background: white;
      padding: 40px;
      margin: auto;
      border-radius: 20px;
      max-width: 500px;
      box-shadow: 0 10px 20px rgba(0,0,0,0.1);
    }
    button {
      padding: 10px 20px;
      font-size: 18px;
      margin: 10px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }
    .yes { background: #ff69b4; color: white; }
    .no { background: #cccccc; }
  </style>
</head>
<body>
  <div class="card">
    <h1>Will you go out with me? 💖</h1>
    <button class="yes" onclick="alert('YAY! 🎉 Text me 😄')">Yes!</button>
    <button class="no" onclick="alert('Aww... maybe next time 😢')">No</button>
  </div>
</body>
</html>
