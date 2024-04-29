<template>
    
    <div class="dotstate">
        <div id="bubbleChart"></div>
      Welche Nummer wird angezeigt?
      <div class="InputandButtons">
        <input type="number" min="0" max="9" v-model="inputValue" >
        <button @click="redirectToError">Ich bin kein Roboter</button>
      </div>
    
    </div>
  </template>
  
  <script>
  import * as d3 from 'd3';
  
  export default {
    name: "Dotcaptcha",
    data() {
      return {
        inputValue: ''
      };
    },
    methods: {
      redirectToError() {
        // Redirect to /error route
        this.$router.push('/error');
      },
      drawBubbleChart() {
        // D3.js script to generate packed bubble chart
        const diameter = 600;
  
        const bubble = d3.pack()
          .size([diameter, diameter])
          .padding(1.5);
  
        const svg = d3.select("#bubbleChart")
          .append("svg")
          .attr("width", diameter)
          .attr("height", diameter)
          .attr("class", "bubble");
  
        const numberOfBubbles = Math.floor(Math.random() * (550 - 500) + 500); // Generate a random number of bubbles between 500 and 550
        const nodes = d3.range(numberOfBubbles).map(() => ({radius: Math.random() * 14 + 1}));
  
        const root = d3.hierarchy({children: nodes})
          .sum(function (d) { return d.radius; });
  
        bubble(root);
  
        const color = d3.scaleSequential(d3.interpolateLab("red", "green"));  
        const node = svg.selectAll(".node")
          .data(root.children)
          .enter().append("g")
          .attr("class", "node")
          .attr("transform", function (d) {
            return "translate(" + d.x + "," + d.y + ")";
          });
  
        node.append("circle")
          .attr("r", function (d) {
            return d.r;
          })
          .style("fill", function () {
            return color(Math.floor(Math.random() * 10)); // Randomly select a color from the color scale
          });
      }
    },
    mounted() {
      this.drawBubbleChart(); // Call the method to draw bubble chart on component mount
    }
  };
  </script>
  
  <style scoped>
  .bubble {
    font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
    text-align: center;
  }
  .node circle {
    fill: #ccc;
    stroke: #fff;
  }
  </style>
  

  //const color = d3.scaleSequential(d3.interpolateLab("red", "green"));
