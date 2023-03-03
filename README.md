<html>
  <head>
    <meta charset="UTF-8">
    <title>Kuhstall - Garderobe</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 0;
      }
      h1 {
        font-size: 36px;
        text-align: center;
        margin-top: 20px;
      }
      p {
        font-size: 24px;
        margin: 20px 0;
        text-align: center;
      }
      #ticket {
        background-color: #ffffff;
        border: 2px solid #007bff;
        padding: 20px;
        text-align: center;
      }
      #used {
        background-color: #f8f9fa;
        color: #6c757d;
        text-decoration: line-through;
      }
    </style>
  </head>
  <body>
    <h1>Kuhstall - Garderobe</h1>
    <div id="ticket">
      <p>Ticket number: <span id="randomNumber"></span></p>
      <p>Valid from: <span id="loadTime"></span></p>
    </div>
    <div>
      <input type="range" min="0" max="1" value="0" id="slider">
    </div>

    <script>
      // Generate a random number between 1 and 300
      const randomNumber = Math.floor(Math.random() * 300) + 1;
      
      // Get the current date and time
      const loadTime = new Date();
      
      // Update the HTML elements with the random number and load time
      document.getElementById("randomNumber").textContent = randomNumber;
      document.getElementById("loadTime").textContent = loadTime.toLocaleString();
      
      // Add an event listener to the slider
      const slider = document.getElementById("slider");
      slider.addEventListener("input", function() {
        // If the slider is used, add the "used" class to the ticket element
        const ticket = document.getElementById("ticket");
        ticket.classList.add("used");
      });
    </script>
  </body>
</html>

