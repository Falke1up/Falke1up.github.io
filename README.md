<html>
  <head>
    <title>Guess the Number Game</title>
  </head>
  <body>
    <h1>Guess the Number Game</h1>
    <p>Guess a number between 1 and 10:</p>
    <input type="text" id="guess" name="guess">
    <button onclick="checkGuess()">Submit</button>
    <p id="result"></p>

    <script>
      // Generate a random number between 1 and 10
      const randomNumber = Math.floor(Math.random() * 10) + 1;

      function checkGuess() {
        // Get the player's guess
        const guess = parseInt(document.getElementById("guess").value);

        // Check if the guess is correct
        if (guess === randomNumber) {
          document.getElementById("result").innerHTML = "Congratulations! You guessed the correct number.";
        } else {
          document.getElementById("result").innerHTML = "Sorry, that's not the correct number. Please try again.";
        }
      }
    </script>
  </body>
</html>
