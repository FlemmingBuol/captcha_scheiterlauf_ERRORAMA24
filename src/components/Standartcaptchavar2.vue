<template>
    <div class="p5state">
    <div>
      <div class ="Canvasstyling" ref="sketchWindow"></div>
    </div>
    <div class="InputandButtons">
      <input type="text" v-model="inputValue" placeholder="Enter text">
      <button @click="redirectToError">I'm not a robot</button>
    </div>
</div>
  </template>
  
  <script>
  import p5 from 'p5'; // Import 'p5' library
  
  export default {
    name: 'Standartcaptcha',
    data() {
      return {
        inputValue: '', // Initialize inputValue data property
        fonts: [
          require('@/assets/Barriecito/Barriecito-Regular.ttf'),
          require('@/assets/DM_Serif_Display/DMSerifDisplay-Italic.ttf'),
          require('@/assets/Roboto/Roboto-Regular.ttf')
        ]
      };
    },
    mounted() {
      const container = this.$refs.sketchWindow;
  
      new p5(sketch => {
        let letters = []; // Array to store unique letters
        let circleX, circleY, circleRadius; // Variables for circle position and radius
  
        sketch.setup = () => {
          const canvas = sketch.createCanvas(500, 300).parent(container);
          sketch.background(250);
          sketch.textAlign(sketch.CENTER, sketch.CENTER); // Align text to center
  
          // Generate random circle position and radius
          circleX = sketch.width / 2 + sketch.random(-40, 40);
          circleY = sketch.height / 2 + sketch.random(-40, 40);
          circleRadius = sketch.random(100, 300);
  
          sketch.push();
          sketch.fill(160); // Set fill color to white
          sketch.circle(circleX, circleY, circleRadius); // Draw circle with random position and radius
          sketch.pop();
  
          // Generate unique letters
          const uniqueLetters = new Set(); // Using a Set to ensure uniqueness
          while (uniqueLetters.size < 5) {
            const randomCharCode = sketch.floor(sketch.random(0, 65536)); // Random ASCII code for lowercase letters
            const randomLetter = String.fromCharCode(randomCharCode); // Convert ASCII code to letter
            uniqueLetters.add(randomLetter); // Add unique letter to the set
          }
  
          // Assign fonts and sizes to each letter
          const uniqueLettersArray = Array.from(uniqueLetters); // Convert set to array
          for (let i = 0; i < uniqueLettersArray.length; i++) {
            const letter = uniqueLettersArray[i];
            const x = (i + 1) * (sketch.width / (uniqueLettersArray.length + 1)); // Equally distribute letters horizontally
            const y = sketch.height / 2 + sketch.random(-20, 20); // Center vertically
            const fontIndex = Math.floor(Math.random() * this.fonts.length); // Randomly select a font
            const selectedFont = sketch.loadFont(this.fonts[fontIndex]); // Load the selected font
            const fontSize = 80 + sketch.random(-40, 40);
            letters.push({ letter, x, y, font: selectedFont, fontSize });
          }
  
          // Draw random lines across the canvas
          const numLines = sketch.random(2, 5); // Random number of lines between 2 and 5
          for (let i = 0; i < numLines; i++) {
            const startX = sketch.random(sketch.width);
            const startY = sketch.random(sketch.height);
            const endX = sketch.random(sketch.width);
            const endY = sketch.random(sketch.height);
            sketch.line(startX, startY, endX, endY);
          }
  
          sketch.noLoop()
          sketch.redraw()
        };
  
        sketch.draw = () => {
          // Draw letters
          for (let i = 0; i < letters.length; i++) {
            const { letter, x, y, font, fontSize } = letters[i];
            sketch.textSize(fontSize);
            sketch.textFont(font); // Set font for the current letter
            // Set font size for the current letter
            sketch.text(letter, x, y);
          }
  
          // Apply Perlin noise to shift pixels slightly
          for (let x = 0; x < 500; x++) {
            for (let y = 0; y < 300; y++) {
              const noiseVal = sketch.noise(x * 0.02, y * 0.02);
              const shiftX = (noiseVal - 0.5) * 10;
              const shiftY = (noiseVal - 0.5) * 5;
              const pixelColor = sketch.get(x, y);
              sketch.set(x + shiftX, y + shiftY, pixelColor);
            }
          }
  
          sketch.updatePixels();
        };
      });
    },
    methods: {
      redirectToError() {
        // Redirect to /error route
        this.$router.push('/error');
      }
    }
  }
  </script>
  
  <style>
  .Canvasstyling {
  border: 2px;
  border-radius: 3px;
  border-color: black;
  }
  </style>