<script>
  import * as d3 from "d3";
  import { onMount } from "svelte";
  import tallyDataRaw from "../data/fiveyears_tally.json";
  let figureEl;

  let tallyData = tallyDataRaw.map((d) => ({
    id: d.main_party,
    label: d.main_party,
    losses: d.lost,
    gains: d.gained,
    no_change: d.no_change,
  }));
export let w;
 // console.log({tallyData})

  onMount(() => {
    const tooltip = d3.select('body') 
      .append('div')
      .attr('class','tooltip')
      .style('position', 'absolute')
      .style('z-index', '1')
      .style('visibility', 'hidden')
      .style('border-radius', '4px')
      .style('color', '#fff');

    const margin = { top: 50, right: 10, bottom: 10, left: 60 };
    
    const width = 700 - margin.left - margin.right;
    const height = 500 - margin.top - margin.bottom;
    const y = d3.scaleBand().rangeRound([0, height]).padding(0.3);
    const x = d3.scaleLinear().rangeRound([0, width]);
    const legendLabels = new Map();
    legendLabels.set("losses", "Losses");
    legendLabels.set("no_change", "Hold");
    legendLabels.set("gains", "Gains");
    const color = d3
      .scaleOrdinal()
      .range(["#C4140A","#a8a2a2", "#0ABAC4"])
      .domain(Array.from(legendLabels.keys()));
    const xAxis = d3.axisTop().scale(x);
    const yAxis = d3.axisLeft().scale(y);
    const svg = d3
      .select(figureEl)
      .append("svg")
      .attr("width", width + margin.left + margin.right)
      .attr("height", height + margin.top + margin.bottom)
      .attr("id", "d3-plot")
      .append("g")
      .attr("transform", "translate(" + margin.left + "," + margin.top + ")");
    const data = tallyData.map((originalDatum) => {
      const d = Object.assign({}, originalDatum);
      let x0 = -1 * d["losses"];
      let idx = 0;
      d.boxes = color.domain().map(function (name) {
        return {
          name: name,
          x0: x0,
          x1: (x0 += +d[name]),
          n: +d[name],
        };
      });
      return d;
    });
    //console.log("data"+{data})
    //console.log(data.length)
    const minValue = d3.min(data, (d) => d.boxes[0].x0);
    const maxValue = d3.max(data, (d) => d.boxes[d.boxes.length - 1].x1);
    console.log(minValue)
    console.log(maxValue)
    const absoluteExtremeValue = Math.max(
      Math.abs(minValue),
      Math.abs(maxValue)
    );
    x.domain([-absoluteExtremeValue, absoluteExtremeValue]).nice();
    y.domain(data.map((d) => d.label));
    svg.append("g").attr("class", "x axis").call(xAxis);
    svg.append("g").attr("class", "y axis").call(yAxis);
    const vakken = svg
      .selectAll(".question")
      .data(data)
      .enter()
      .append("g")
      .attr("class", "bar")
      .attr("transform", (d) => `translate(0,${y(d.label)})`);
    const bars = vakken
      .selectAll("rect")
      .data((d) => d.boxes)
      .enter()
      .append("g")
      .attr("class", "subbar");
    bars
      .append("rect")
      .attr("height", y.bandwidth())
      .attr("x", (d) => x(d.x0))
      .attr("width", (d) => x(d.x1) - x(d.x0))
      .style("fill", (d) => color(d.name))
      // .on("mouseover", function(e,d,i) {
      //   console.log(arguments)
      //   let tooltipWidth = tooltip.node().offsetWidth;
      //   let tooltipHeight = tooltip.node().offsetHeight;
      //   tooltip
      //     .style("left", e.pageX - tooltipWidth/2 +'px')
      //     .style("top", e.pageY-tooltipHeight - 10+'px')
      //     .style('background', 'rgba(0,0,0,0.8)')
      //     .style('visibility', 'visible')
      //     .html( (d) => 
      //       {
      //         console.log(d)
      //       return `<b>Loss</b>: ${d.losses} <br/>
      //                         <b>Hold</b>: ${d.no_change} <br/>
      //                         <b>Gain</b>: ${d.gains}`
      //       });
      //   d3.select(this).attr("fill", "steelblue");})
      // .on('mousemove', function (e) {
      //   let tooltipWidth = tooltip.node().offsetWidth;
      //   let tooltipHeight = tooltip.node().offsetHeight;
      //   tooltip
      //     .style("left", e.pageX - tooltipWidth/2 +'px')
      //     .style("top", e.pageY-tooltipHeight - 10+'px')
      // })
      // .on("mouseout", function(e,d) {
      //   tooltip
      //     .style('visibility', 'hidden')
      //   d3.select(this).attr("fill", "purple");});
    bars
      .append("text")
      .attr("x", (d) => x(d.x0))
      .attr("y", y.bandwidth() / 2)
      .attr("dy", "0.5em")
      .attr("dx", "0.5em")
      .style("font", "10px sans-serif")
      .style("text-anchor", "begin")
      .style("fill", "#ffffff")
      .style("font-weight", "bold")
      .text((d) => (d.n !== 0 && d.x1 - d.x0 > 3 ? d.n : ""));
    // vakken
    //   .insert("rect", ":first-child")
    //   .attr("height", y.bandwidth())
    //   .attr("x", "1")
    //   .attr("width", width)
    //   .attr("fill-opacity", "0")
    //   // .style("fill", "#F5F5F5")
    //   .attr("class", (d, index) => (index % 2 == 0 ? "even" : "uneven"));
    svg
      .append("g")
      .attr("class", "y axis")
      .append("line")
      .attr("x1", x(0))
      .attr("x2", x(0))
      .attr("y2", height);
    const startp = svg.append("g").attr("class", "legendbox");
    // this is not nice, we should calculate the bounding box and use that
    const legend_tabs = [0, 120, 200, 375, 450];


    const legend = startp
      .selectAll(".legend")
      .data(color.domain().slice())
      .enter()
      .append("g")
      .attr("class", "legend")
      .attr("transform", (d, i) => `translate(${legend_tabs[i]},-45)`);
    
    legend
      .append("rect")
      .attr("x", 0)
      .attr("width", 18)
      .attr("height", 18)
      .style("fill", color);
      
    legend
      .append("text")
      .attr("x", 22)
      .attr("y", 9)
      .attr("dy", ".35em")
      .style("text-anchor", "begin")
      .style("font", "10px sans-serif")
      .text((d) => legendLabels.get(d))
      .style("fill", "white");
    svg
      .selectAll(".axis path")
      .style("fill", "none")
      .style("stroke", "#000")
      .style("shape-rendering", "crispEdges");
    svg
      .selectAll(".axis line")
      .style("fill", "none")
      .style("stroke", "#000")
      .style("shape-rendering", "crispEdges");
  
    setTimeout(() => {
      const movesize = width / 2 - startp.node().getBBox().width / 2;
      svg.selectAll(".legendbox").attr("transform", `translate(${movesize},0)`);
      svg.selectAll(".legendbox text").style('fill','white')
    }, 0);
  });
</script>
<div class="chart-container" bind:this={figureEl} />
<style>
.chart-container {
    
    width: 100%;
    height: 100%;
  }
  .legend text 
  {
    fill: white;
  }
</style>
