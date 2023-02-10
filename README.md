<html>
  <head>
    <style>
      form {
        width: 500px;
        margin: 0 auto;
        text-align: center;
      }
      
      input[type="text"] {
        padding: 10px;
        font-size: 16px;
        width: 60%;
        margin-bottom: 20px;
      }
      
      input[type="submit"] {
        padding: 10px 20px;
        background-color: green;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
      }
    </style>
  </head>
  <body>
    <h1>Enter Participants</h1>
    <form>
      <input type="text" placeholder="Participant 1" required><br>
      <input type="text" placeholder="Participant 2" required><br>
      <input type="text" placeholder="Participant 3" required><br>
      <input type="text" placeholder="Participant 4" required><br>
      <input type="submit" value="Start Race">
    </form>
  </body>
</html>
