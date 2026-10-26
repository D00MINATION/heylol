<!DOCTYPE html>
<html>
<head>
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
      left
