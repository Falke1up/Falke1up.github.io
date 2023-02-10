<!DOCTYPE html>
<html>
  <head>
    <style>
      .race-track {
        width: 500px;
        height: 200px;
        border: 1px solid black;
        position: relative;
        margin: 0 auto;
      }
      
      .duck {
        width: 50px;
        height: 50px;
        position: absolute;
        bottom: 0;
        left: 0;
        background-image: url('duck.png');
        background-size: contain;
        animation: swim 5s linear infinite;
      }
      
      @keyframes swim {
        from {
          left: 0;
        }
        to {
          left: 450px;
        }
      }
    </style>
  </head>
  <body>
    <h1>Duck Racing</h1>
    <div class="race-track">
      <div class="duck" style="left: 10%"></div>
      <div class="duck" style="left: 20%"></div>
      <div class="duck" style="left: 30%"></div>
      <div class="duck" style="left: 40%"></div>
    </div>
  </body>
</html>
