<html>
<head>
  <meta charset="UTF-8">
  <title>Check-In</title>
</head>
<body>
  <h1>Check-In</h1>
  <input type="text" id="name" placeholder="Enter your name">
  <button id="checkin-button">Check-In</button>
  <div id="result"></div>
  <ul id="checkin-list"></ul>
  
  <script>
    const checkinButton = document.getElementById('checkin-button');
    const resultDiv = document.getElementById('result');
    const checkinList = document.getElementById('checkin-list');
    let checkins = [];
    let previousDate = new Date();
    
    checkinButton.addEventListener('click', function() {
      const name = document.getElementById('name').value;
      if (!name) {
        resultDiv.innerHTML = 'Please enter your name';
        return;
      }
      
      navigator.geolocation.getCurrentPosition(function(position) {
        const latitude = position.coords.latitude;
        const longitude = position.coords.longitude;
        const targetLatitude = 37.7749;
        const targetLongitude = -122.4194;
        const range = 0.5; // in kilometers
        
        const distance = calculateDistance(latitude, longitude, targetLatitude, targetLongitude);
        if (distance <= range) {
          resultDiv.innerHTML = 'Success! You are within range.';
          const date = new Date();
          checkins.push({name, date});
          updateCheckinList();
        } else {
          resultDiv.innerHTML = 'Failure! You are not within range.';
        }
      });
    });
    
    function updateCheckinList() {
      checkinList.innerHTML = '';
      const currentDate = new Date();
      if (currentDate.getDate() != previousDate.getDate()) {
        checkins = [];
        previousDate = currentDate;
      }
      for (let i = 0; i < checkins.length; i++) {
        const checkin = checkins[i];
        const listItem = document.createElement('li');
        listItem.innerHTML = `${checkin.name} checked in on ${checkin.date}`;
        checkinList.appendChild(listItem);
      }
    }
    
    function calculateDistance(lat1, lon1, lat2, lon2) {
      const radius = 6371; // Earth's radius in kilometers
      const dLat = toRadians(lat2-lat1);
      const dLon = toRadians(lon2-lon1);
      const a = 
        Math.sin(dLat/2) * Math.sin(dLat/2) +
        Math.cos(toRadians(lat1)) * Math.cos(toRadians(lat2)) * 
        Math.sin(dLon/2) * Math.sin(dLon/2)
        const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
      const distance = radius * c;
    return distance;
}

function toRadians(degree) {
  return degree * (Math.PI/180);
}
   </script>
</body>
</html>

