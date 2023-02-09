<html>
<head>
  <meta charset="UTF-8">
  <title>Check-In System</title>
  <style>
    .check-in-form {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin: 30px;
    }
    .check-in-form input[type="text"] {
  margin-bottom: 10px;
  padding: 10px;
  font-size: 18px;
}

.check-in-form button {
  padding: 10px 20px;
  font-size: 18px;
  background-color: lightblue;
  border: none;
  border-radius: 5px;
}

.check-ins {
  margin: 30px;
}

.check-ins h3 {
  margin-bottom: 10px;
}

.check-ins ul {
  list-style: none;
  padding: 0;
}

.check-ins li {
  margin-bottom: 10px;
  padding: 10px;
  background-color: lightgray;
  border-radius: 5px;
}
    </style>
</head>
<body>
  <div class="check-in-form">
    <input type="text" id="userName" placeholder="Enter your name">
    <button id="checkInBtn">Check-In</button>
  </div>
  <div id="message" class="message"></div>
  <div class="check-ins">
    <h3>Check-Ins</h3>
    <ul id="checkInsList"></ul>
  </div>
  <?php
    // Target location
    $targetLatitude = 56.15386;
    $targetLongitude = 10.20321;
    
    // Check if the check-in form has been submitted
    if (isset($_POST["checkIn"])) {
      // Get user's location
      $userLatitude = $_POST["latitude"];
      $userLongitude = $_POST["longitude"];
      
      // Calculate distance between user's location and target location
      $distance = calculateDistance($userLatitude, $userLongitude, $targetLatitude, $targetLongitude);
      
     // Check if within range
if ($distance <= 100) {
// Store check-in information
$checkIns = json_decode(file_get_contents("check-ins.json"), true);
$checkIns[] = [
"name" => $_POST["name"],
"date" => date("F j, Y"),
"time" => date("g:i a")
];
file_put_contents("check-ins.json", json_encode($checkIns));
        
  // Display success message
    echo "<script>document.querySelector('.message').innerHTML = 'Check-In Successful!';</script>";
    
    // Update check-ins list
    $checkInsList = "";
    foreach ($checkIns as $checkIn) {
      $checkInsList .= "<li>Name: {$checkIn["name"]}<br>Date: {$checkIn["date"]}<br>Time: {$checkIn["time"]}</li>";
    }
    echo "<script>document.querySelector('#checkInsList').innerHTML = '{$checkInsList}';</script>";
  } else {
    // Display failure message
    echo "<script>document.querySelector('.message').innerHTML = 'Check-In Failed: Not within 100m of target location.';</script>";
  }
}
?>

</body>
</html>
