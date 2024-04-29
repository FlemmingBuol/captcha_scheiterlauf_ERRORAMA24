<template>
 <div class="questionstate">
 <div>
      <span id="randomWord">{{ randomWord }}</span>
  </div>
  <div class="InputandButtons">
      <input type="text" v-model="inputValue" placeholder="Beantworte die Frage">
      <button @click="redirectToError">Ich bin kein Roboter</button>
  </div>
</div>
</template>

<script>
export default {
  name: "Questioncaptcha",
  data() {
      return {
          wordsArray: ["Hat ein Mensch diese Fragen geschrieben?","Wie viele Schraubenzieher besitzt du?","Was bin ich?","Wo sind wir hier?","Was ist dein Lieblingswein?", "Wieso stehst du nie für dich ein?", "Wann machst du am liebsten Pause?", "Wärst du lieber ein Roboter?", "Auffällig warst du doch schon immer, oder?"],
          randomWord: ""
      };
  },
  created() {
      this.setRandomWord();
  },
  methods: {
      setRandomWord() {
          const randomIndex = Math.floor(Math.random() * this.wordsArray.length);
          this.randomWord = this.wordsArray[randomIndex];
      },
      redirectToError() {
          // Redirect to /error route
          this.$router.push('/error');
      }
  }
}
</script>
