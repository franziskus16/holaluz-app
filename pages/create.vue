<template>
    <article>
        <section>
            <h1>Holaluz price charts</h1>
            <div>
              <div class="chart"></div>
                <!-- <ul>
                    <li v-for="prices in prices" class="item"></li>
                </ul> -->
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
                    ],
                    "pepe": [
                      30, 86, 168, 281, 303, 365
                    ]
                  }
                  
import * as d3 from 'd3'; 

  export default {
    data() {
      return {
        sampleData: [30, 86, 168, 281, 303, 365],
      }
    },
    mounted() {
      this.printChart();
    },
    methods:{
      printChart: function() {
        
          // let listOfObjects = Object.keys(this.prices.pepe).map((key) => {
          //     return this.prices.pepe[key];
          // }).bind(this);
        console.log(datos);
        
         // set the dimensions and margins of the graph
var margin = {top: 10, right: 30, bottom: 30, left: 60},
    width = 460 - margin.left - margin.right,
    height = 400 - margin.top - margin.bottom;

// append the svg object to the body of the page
var svg = d3.select("#my_dataviz")
  .append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform",
          "translate(" + margin.left + "," + margin.top + ")");

//Read the data
d3.csv("https://raw.githubusercontent.com/holtzy/D3-graph-gallery/master/DATA/iris.csv", function(data) {

  // Add X axis
  var x = d3.scaleLinear()
    .domain([4, 8])
    .range([ 0, width ]);
  svg.append("g")
    .attr("transform", "translate(0," + height + ")")
    .call(d3.axisBottom(x));

  // Add Y axis
  var y = d3.scaleLinear()
    .domain([0, 9])
    .range([ height, 0]);
  svg.append("g")
    .call(d3.axisLeft(y));

  // Color scale: give me a specie name, I return a color
  var color = d3.scaleOrdinal()
    .domain(["setosa", "versicolor", "virginica" ])
    .range([ "#440154ff", "#21908dff", "#fde725ff"])

  // Add dots
  svg.append('g')
    .selectAll("dot")
    .data(data)
    .enter()
    .append("circle")
      .attr("cx", function (d) { return x(d.Sepal_Length); } )
      .attr("cy", function (d) { return y(d.Petal_Length); } )
      .attr("r", 5)
      .style("fill", function (d) { return color(d.Species) } )

})
        // d3.select(".chart")
        //   .selectAll("div")
        //   .data(this.sampleData)
        //     .enter()
        //     .append("div")
        //     .style("width", function(d) { return d + 'px' })
        //     .text(function(d) { return '$ ' + d; });
      }
    }

  }

</script>
<style>
.chart div {
  font: 10px sans-serif;
  background-color: steelblue;
  text-align: right;
  padding: 3px;
  margin: 1px;
  color: white;
}
</style>