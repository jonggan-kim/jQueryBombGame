# jQueryBombGame
Bomb game using jQuery

<img width=400 src = "./img_bomb/failed.png">
<img width=400 src = "./img_bomb/success.png">


<!DOCTYPE html>
<html>

<head>
  <title>jQuery Bomb Game</title>
  <style>
    #box {
      width: 400px;
      margin-left: 30px;
    }

    .box1 {
      border-radius: 10px;
      border: 2px solid #73ad21;
      background-color: #73ad21;
      padding: 10px;
      margin: 10px;
      width: 400px;
      height: 20px;
      color: white;
      text-align: center;
    }

    .box2 {
      width: 80px;
      height: 60px;
      background-color: greenyellow;
      /* margin-top: 10px; */
      margin: 10px;

      padding: 10px;
      border-radius: 10px;
      border: 2px solid grey;
      float: left;
    }

    .box3 {
      float: both clear;
    }

    #msg {
      background-color: rgb(10, 125, 163);
      margin-top: 10px;
      margin-left: 10px;
      padding: 50px;
      width: 320px;
      height: 20px;
      border-radius: 10px;
      border: 2px solid black;
      text-align: center;
      font-size: large;
      color: aqua
    }

    #btn1 {
      margin-top: 320px;
      margin-left: -230px;
      background-color: yellow;
      border-radius: 5px;
      padding: 5px;
    }
  </style>
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
  <script>
    var num = [0, 0, 0, 0, 0, 0, 0, 0, 1];
    var flag = false;
    var cnt
    // shuffle Bomb location
    function shuffle() {
      for (var i = 0; i < num.length; i++)
        var idx1 = Math.floor(Math.random() * 9);
      var idx2 = Math.floor(Math.random() * 9);

      if (idx1 != idx2) {
        var temp = num[idx1];
        num[idx1] = num[idx2];
        num[idx2] = temp;
      }
    }
    $(document).ready(function () {
      $('#btn1').click(function () {
        // bomb loation decision
        cnt = 0;
        flag = false;
        $("#msg").text("")
        shuffle();

        // show ? image
        for (i = 0; i <= 9; i++) {
          var htmlStr =
            "<img width='50' src='./img_bomb/q.png' class='imgBox' id='img" +
            i +
            "'>";
          $('#div' + i).html(htmlStr);
        }
      });
      //make click event on the dynamically generated image
      $('.box2').on('click', '.imgBox', function (event) {
        if (flag == true) return;
        //check which location image is clicked
        var id = $(this).attr('id').replace('img', '') - 1;
        // console.log(id);
        //check if num array element is 0 or 1
        //show heart image for 0, otherwise show bomb image
        if ($(this).attr('src') == './img_bomb/q.png') {
          if (num[id] == 0) {
            $(this).attr('src', './img_bomb/heart.png');
            flag = false;
            cnt++;
            if (cnt == 8) {
              $(".imgBox").attr("src", "./img_bomb/heart.png")
              $("#msg").text("Success");
              flag = true;
            }

          } else {
            $(this).attr('src', './img_bomb/bomb.png');
            flag = true;
            $("#msg").text("Failed")
          }
        }
      });
    });
  </script>
</head>

<body>
  <div class="box1">jQuery Bomb Game</div>
  <div id="box">
    <div class="box2" id="div1"></div>
    <div class="box2" id="div2"></div>
    <div class="box2" id="div3"></div>
    <div class="box3"></div>
    <div class="box2" id="div4"></div>
    <div class="box2" id="div5"></div>
    <div class="box2" id="div6"></div>
    <div class="box3"></div>
    <div class="box2" id="div7"></div>
    <div class="box2" id="div8"></div>
    <div class="box2" id="div9"></div>
    <div class="box3"></div>
  </div>
  <input type="button" value="Shuffle Bomb" id="btn1" />
  <div id="msg"></div>
  <!-- <div class="box2"></div>
    <div class="box3"></div> -->
</body>

</html>
