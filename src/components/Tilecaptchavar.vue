<template>
    <div class="tilestate">
    <div class="burger">
      <div class="image-gallery">
        <img v-for="(image, index) in images"
             :key="index"
             :src="image"
             :alt="'Image ' + (index + 1)"
             @click="toggleImage(index)"
             :style="{ opacity: isSelected(index) ? 0.5 : 1 }" />
      </div>
    </div>
    Wähle die Kacheln aus, auf denen <span id="randomWord">{{ randomWord }}</span> zu sehen sind.
    <div class="InputandButtons">
     
      <button @click="redirectToError">Ich bin kein Roboter</button>
    </div>
</div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        wordsArray: ["Flaschen", "Gabeln", "Äpfel", "Autos", "Katzen"],
        randomWord: "",
        images: [],
        selectedImages: [], // Array to store selected image indices
      };
    },
    mounted() {
      this.chooseRandomWord();
      this.loadImagesFromDirectory();
    },
    methods: {
      chooseRandomWord() {
          const randomIndex = Math.floor(Math.random() * this.wordsArray.length);
          this.randomWord = this.wordsArray[randomIndex];
        },
        redirectToError() {
          // Redirect to /error route
          this.$router.push('/error');
        },
      loadImagesFromDirectory() {
        // Import images from the assets directory
        const imageContext = require.context('@/assets/2', false, /\.(png|jpe?g|gif|svg)$/);
        this.images = imageContext.keys().map(key => imageContext(key));
      },
      toggleImage(index) {
        // Toggle the selected state of the image at the given index
        if (this.isSelected(index)) {
          this.selectedImages = this.selectedImages.filter(i => i !== index);
        } else {
          this.selectedImages.push(index);
        }
      },
      isSelected(index) {
        // Check if the image at the given index is selected
        return this.selectedImages.includes(index);
      },
      redirectToError() {
        // Redirect to /error route
        this.$router.push('/error');
      }
    },
  };
  </script>
  
  <style scoped>
  .image-gallery {
    display: flex;
  flex-wrap: wrap;
  justify-content: center;
  width: 600px;
  box-sizing: border-box; 
  margin: auto; /* Include padding and border in the element's total width */
  }
  
  .image-gallery img {
    flex: 0 0 calc(25% - 10px);
    max-width: calc(25% - 10px);
    max-height: calc(25vw - 10px);
    object-fit: cover;
    margin: 2px;
    border-radius: 3px;
  }
  
  </style>