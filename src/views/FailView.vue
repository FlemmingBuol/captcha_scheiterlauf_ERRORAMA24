<template>
<ErrorState/>


</template>

<script>

import ErrorState from '@/components/Errorstate.vue';
export default {
    name: 'FailView.vue',
  components: {
    ErrorState
  }
}


</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400;1,700&display=swap');
.errorstate{
  font-family: "Space Mono", sans-serif;
  font-weight: 600;
  font-style: italic;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 2em;
  text-align: center;

}

</style>