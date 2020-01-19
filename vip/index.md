---
layout: page
title: 
excerpt: 
modified:

---


![center-aligned-image](https://shangyblog-1256840873.cos.ap-beijing.myqcloud.com/20200119changdao.jpeg){: .align-center}


<html>
<head>
<script>

function startTime() {
  
  var pretime = new Date(2015,6,27,3,0,0);
  var nowtime = new Date();

  var delta = Math.floor((nowtime - pretime)/1000);

  var days = Math.floor(delta / 86400);
  delta -= days * 86400;

  var hours = Math.floor(delta / 3600) % 24;
  delta -= hours * 3600;

  var minutes = Math.floor(delta / 60) % 60;
  delta -= minutes * 60;

  var seconds = delta % 60;  // in theory the modulus is not required
  
  var update_days = days+30


  var info = "I have fallen in love with Xin for " + update_days + " days " + hours + " hours " + minutes + " minutes " + seconds + " seconds."

  info = info.fontsize("16")
  info = info.fontcolor("#FF69B4")
  info = info.bold()
  document.getElementById('time').innerHTML = info

  t = setTimeout(function() {
    startTime()
  }, 500);
}


startTime();


</script>
</head>
<body onload="startTime();">

<!-- <div align="center">
</div>

 -->
<div id="time" align="center">

</div>

</body>

</html>
