html>
<head>
  <meta charset="UTF-8">
  <title>Check-In System</title>
</head>
<body>
  <h1>Check-In System</h1>
  <input type="text" id="userName" placeholder="Enter your name">
  <button id="checkInBtn">Check-In</button>
  <div id="message">
    <!-- Message will be displayed here -->
  </div>
  <ul id="checkInList">
    <!-- Check-in information will be displayed here -->
  </ul>
  <script>
    // Get current date and time
    const currentDate = new Date();
    let previousDate = new Date();
    
    // Get check-in button and message div
    const checkInBtn = document.getElementById("checkInBtn");
    const messageDiv = document.getElementById("message");
    
    // Check-in information array
    let checkIns = [];
    
    // Target location
    const targetLocation = {
      lat: 56.15386,
      lng: 10.20321
    };
    
    // Check if user is within 100m of target location
    const isWithinRange = (userLocation) => {
      return (
        Math.abs(userLocation.lat - targetLocation.lat) < 0.001 &&
        Math.abs(userLocation.lng - targetLocation.lng) < 0.001
      );
    };
    
    // Check if current date is different from previous date
    const isNewDay = () => {
      return (
        currentDate.getDate() !== previousDate.getDate() ||
        currentDate.getMonth() !== previousDate.getMonth() ||
        currentDate.getFullYear() !== previousDate.getFullYear()
      );
    };
    
    // Reset check-in information
    const resetCheckIns = () => {
      checkIns = [];
      document.getElementById("checkInList").innerHTML = "";
    };
    
    // Display check-in information
    const displayCheckIns = () => {
      let checkInList = document.getElementById("checkInList");
      checkInList.innerHTML = "";
      
      checkIns.forEach(checkIn => {
        let checkInItem = document.createElement("li");
        checkInItem.innerHTML = `Name: ${checkIn.name} Date: ${checkIn.date} Time: ${checkIn.time}`;
        checkInList.appendChild(checkInItem);
      });
    };
    
    // Get user location and check if they are within range
    const checkIn = () => {
      // Get user name
      const userName = document.getElementById("userName").value;
      
      // Get user location
      navigator.geolocation.getCurrentPosition(
        position => {
          const userLocation = {
            lat: position.coords.latitude,
            lng: position.coords.longitude
          };
          
          // Check if user is within range
          if (isWithinRange(userLocation)) {
            // Display success message
messageDiv.innerHTML = "Check-In Successful!";

// Store check-in information
checkIns.push({
name: userName,
date: currentDate.toDateString(),
time: currentDate.toLocaleTimeString()
});
        
        // Display check-in information
        displayCheckIns();
      } else {
        // Display failure message
        messageDiv.innerHTML = "Check-In Failed: Not within range.";
      }
    },
    error => {
      messageDiv.innerHTML = "Check-In Failed: Could not retrieve location.";
    }
  );
};

// Check if it's a new day and reset check-ins if necessary
if (isNewDay()) {
  previousDate = currentDate;
  resetCheckIns();
}

// Add event listener to check-in button
checkInBtn.addEventListener("click", checkIn);
  </script>
</body>
</html>
