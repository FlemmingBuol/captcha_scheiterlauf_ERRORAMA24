<template>
 <div class="errorstate">
 <div>
    <span id="randomWord">{{ randomWord }}</span>
  </div>
  <div>
    Neuer Versuch in {{ countdown }}
  </div>
</div>
</template>

<script>
export default {
  name: 'Errorstate',
  data() {
    return {
      wordsArray: ["Versuchen Sie es noch einmal", "Fehler! Fehler! Fehler!", "Falsche Antwort, wieder einmal", "Versuchst du es überhaupt?", "Damit kann ich nichts anfangen", "Also doch ein Roboter", "Juckt mich nicht", "Knapp daneben", "Wenns beim ersten Mal nicht klappt, try, try again"],
      randomWord: "",
      countdown: 5,
      timer: null
    };
  },
  methods: {
    setRandomWord() {
      const randomIndex = Math.floor(Math.random() * this.wordsArray.length);
      this.randomWord = this.wordsArray[randomIndex];
    }
  },
  mounted() {
    this.setRandomWord(); // Set initial random word
    this.timer = setInterval(() => {
      if (this.countdown > 0) {
        this.countdown--;
      } else {
        clearInterval(this.timer);
        this.$router.push('/'); // Assuming '/homeview' is the route for Homeview
      }
    }, 1000); // Update countdown every second
  },
  beforeDestroy() {
    clearInterval(this.timer);
  }
};
</script>
