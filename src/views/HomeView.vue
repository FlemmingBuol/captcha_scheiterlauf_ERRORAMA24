<template>
<header>
<img src="@/assets/post_logo.png" alt="">
</header>
<Captchastate class="Captchastate"/>
</template>

<script>
// @ is an alias to /src
import Captchastate from '@/components/Captchastate.vue';

export default{
  components: { 
    Captchastate
  }
}

</script><style>
@import url('https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400;1,700&display=swap');
.Captchastate {
  font-family: "Space Mono", sans-serif;
  font-weight: 600;
  font-style: normal;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
input {width: 100%;
  height: 30px;  border-radius: 5px;
  margin: auto;
}
button {
  width: 100%;
  height:30px;
  border-radius: 5px;

}
.tilestate {
  font-size: 2em;
  text-align: center;
}
.questionstate {
  font-size: 2em;
  text-align: center;
}
.dotstate {
  font-size: 2em;
  text-align: center;
}
header {
  flex: auto;
  margin: 0%;
background-color:#FFCC00 ;
height: 100px;
}
body {
  margin: 0
}
header img {
    width: 100px; /* Set the width as desired */
    height: auto; /* Maintain aspect ratio */

  }
</style>