<html>
<head>
  <meta charset="UTF-8">
  <title>Check-In</title>
  <!-- Firebase -->
  <script src="https://www.gstatic.com/firebasejs/7.17.1/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/7.17.1/firebase-database.js"></script>
</head>
<body>
  <h1>Check-In</h1>
  <div>
    <label for="name-input">Navn:</label>
    <input type="text" id="name-input">
  </div>
  <button id="check-in-button">Check-In</button>
  <div id="result"></div>
  <ul id="check-in-list"></ul>

  <script>
    // Initialize Firebase
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
      databaseURL: "https://YOUR_PROJECT_ID.firebaseio.com",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_PROJECT_ID.appspot.com",
      messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
      appId: "YOUR_APP_ID"
    };
    firebase.initializeApp(firebaseConfig);
    const database = firebase.database();

    const nameInput = document.querySelector("#name-input");
    const checkInButton = document.querySelector("#check-in-button");
    const result = document.querySelector("#result");
    const checkInList = document.querySelector("#check-in-list");

    let checkIns = [];

    checkInButton.addEventListener("click", function() {
      const currentTime = new Date().getHours() + new Date().getMinutes() / 60;
      if (currentTime < 7.5 || currentTime > 16.25) {
        result.innerHTML = "Hvad laver du på skolen nu? TAG HJEM!";
        return;
      }

      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(function(position) {
          const latitude = position.coords.latitude;
          const longitude = position.coords.longitude;
          const targetLatitude = 56.15867;
          const targetLongitude = 10.21570;
          const margin = 0.001; // 100m i grader
    
    if (
      latitude > targetLatitude - margin &&
      latitude < targetLatitude + margin &&
      longitude > targetLongitude - margin &&
      longitude < targetLongitude + margin
    ) {
      result.innerHTML = "Check-in success!";

      const name = nameInput.value;
      const date = new Date().toLocaleDateString();

      const existingCheckIn = checkIns.find(
        checkIn => checkIn.name === name && checkIn.date === date
      );
      if (existingCheckIn) {
        result.innerHTML = "Du har allerede checket ind i dag.";
        return;
      }

      const time = new Date().toLocaleTimeString();
      const checkIn = { name, date, time };
      checkIns.push(checkIn);

      checkInList.innerHTML += `
        <li>
          Name: ${checkIn.name}<br>
          Date: ${checkIn.date}<br>
          Time: ${checkIn.time}
        </li>
      `;
    } else {
      result.innerHTML = "Check-in failed.";
    }
  });
} else {
     result.innerHTML = "Check-in failed.";
  }
});
} else {
  result.innerHTML = "Geolocation is not supported by your browser.";
}
});
setInterval(function() {
const today = new Date().toLocaleDateString();
if (checkIns.length === 0 || checkIns[0].date !== today) {
checkIns = [];
checkInList.innerHTML = "";
}
}, 86400000); // Resets the check-in list every day (24 hours in milliseconds)
</script>
</body>
</html>
