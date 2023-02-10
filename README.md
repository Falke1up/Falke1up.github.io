<html>
  <head>
    <style>
      .evil-face {
        width: 200px;
        height: 200px;
        background-image: url('https://i.imgur.com/tL7uTqT.png');
        background-size: cover;
        animation: evil-laugh 1s linear infinite;
      }
      
      @keyframes evil-laugh {
        0% {
          transform: rotate(0deg);
        }
        20% {
          transform: rotate(10deg);
        }
        40% {
          transform: rotate(-10deg);
        }
        60% {
          transform: rotate(10deg);
        }
        80% {
          transform: rotate(-10deg);
        }
        100% {
          transform: rotate(0deg);
        }
      }
    </style>
  </head>
  <body>
    <div class="evil-face"></div>
  </body>
</html>
