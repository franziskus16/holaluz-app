<template>
    <article>
        <section>
            <h1>Holaluz charts</h1>
            <div>
                <div class="d-flex flex-row justify-content-center">
                    <div class="d-flex flex-row ml-3">
                        <div class="align-self-center chart1"></div> 
                        <div class="align-self-center ml-3">1 PRECIO</div>
                    </div>
                    <div class="d-flex flex-row ml-3">
                        <div class="align-self-center chart2"></div> 
                        <div class="align-self-center ml-3">2 PRECIOS</div>
                    </div>
                    <div class="d-flex flex-row ml-3">
                        <div class="align-self-center chart3"></div> 
                        <div class="align-self-center ml-3">3.0a</div>
                    </div>
                </div>
              <div class="chart"></div>
            </div>
        </section>
    </article>    
</template>
<script>
                                                     
 const datos =   {
                    "unprecio": [
                      {
                        "0-23": 0.123
                      }
                    ],
                    "dosprecios": [
                      {
                        "0-13": 0.079
                      },
                      {
                        "14-23": 0.155
                      }
                    ],
                    "3.0a": [
                      {"0-7": 0.055},
                      {"8-12": 0.082},
                      {"13-16": 0.190},
                      {"17-20": 0.078},
                      {"21-23": 0.045}
                    ]
                  }
                  
import * as d3 from 'd3'; 

  export default {
    data() {
      return {
          unprecio: [],
          dosprecios: [],
          threeZeroA: []
      }
    },
    mounted() {
      this.unprecio = this.setupDataSet(datos.unprecio);
      this.dosprecios = this.setupDataSet(datos.dosprecios);  
      this.threeZeroA = this.setupDataSet(datos["3.0a"]);  
      this.printChart(this.unprecio, this.dosprecios, this.threeZeroA);
    },
    methods:{
      setupDataSet: function(vector) {
          var dataset = [];
          var n = vector.length;
          for (var i = 0; i < n; i++) {
            let obj = vector[i];
            let k = Object.keys(obj)[0];
            let v = Object.values(obj)[0];
            let z = k.split('-', 2);
            let start = z[0];
            let end = z[1];

            for (var y = 0; y <= end - start; y++){
                dataset.push({"y": Number(v).toFixed(3) });
            }
          }
         return dataset;
      },
      
      printChart: function(dataset1, dataset2, dataset3) {
        
        // 2. Use the margin convention practice 
        var margin = {top: 50, right: 50, bottom: 50, left: 50}
        , width = 650 - margin.left - margin.right // Use the window's width 
        , height = 400 - margin.top - margin.bottom; // Use the window's height

        // The number of datapoints
        var n = 23;

        // 5. X scale will use the index of our data
        var xScale = d3.scaleLinear()
            .domain([0, n]) // input
            .range([0, width]); // output

        // 6. Y scale will use the randomly generate number 
        var yScale = d3.scaleLinear()
            .domain([0, 1]) // input 
            .range([height, 0]); // output 

        // 7. d3's line generator
        var line = d3.line()
            .x(function(d, i) { return xScale(i); }) // set the x values for the line generator
            .y(function(d) { return yScale(d.y); }) // set the y values for the line generator 
            .curve(d3.curveMonotoneX) // apply smoothing to the line

        // 1. Add the SVG to the page and employ #2
        var svg = d3.select(".chart").append("svg")
            .attr("width", width + margin.left + margin.right)
            .attr("height", height + margin.top + margin.bottom)
            .append("g")
            .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

        // 3. Call the x axis in a group tag
        svg.append("g")
            .attr("class", "x axis")
            .attr("transform", "translate(0," + height + ")")
            .call(d3.axisBottom(xScale)); // Create an axis component with d3.axisBottom

        // 4. Call the y axis in a group tag
        svg.append("g")
            .attr("class", "y axis")
            .call(d3.axisLeft(yScale)); // Create an axis component with d3.axisLeft

        // 9. Append the path, bind the data, and call the line generator 
        svg.append("path")
            .datum(dataset1) // 10. Binds data to the line 
            .attr("class", "line") // Assign a class for styling 
            .attr("d", line); // 11. Calls the line generator 
            // 9. Append the path, bind the data, and call the line generator 
        svg.append("path")
            .datum(dataset2) // 10. Binds data to the line 
            .attr("class", "line2") // Assign a class for styling 
            .attr("d", line); // 11. Calls the line generator 
            // 9. Append the path, bind the data, and call the line generator 
        svg.append("path")
            .datum(dataset3) // 10. Binds data to the line 
            .attr("class", "line3") // Assign a class for styling 
            .attr("d", line); // 11. Calls the line generator 

        }
        }
    }

</script>
<style>
.chart1 {
    width:10px;
    height:10px;
    background-color:#e5027b;
}
.chart2 {
    width:10px;
    height:10px;
    background-color:#ef5d26;
}
.chart3 {
    width:10px;
    height:10px;
    background-color:#edbd4e;
}
.line {
    fill: none;
    stroke: #e5027b;
    stroke-width: 3;
}
.line2 {
    fill: none;
    stroke: #ef5d26;
    stroke-width: 3;
}
.line3 {
    fill: none;
    stroke: #edbd4e;
    stroke-width: 3;
}

.legend {
    font-size: 12px;
}
rect {
    stroke-width: 2;
}
  
.overlay {
  fill: none;
  pointer-events: all;
}

</style>