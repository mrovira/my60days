<script>
  import { onMount } from 'svelte';
  import { LayerCake, Svg } from 'layercake';
  import { scaleLinear } from 'd3-scale';
  import Radar from 'src\components\Radar.svelte';
  import AxisRadial from 'src\components\AxisRadial.svelte';

  export let data;
  export let options;

  let chart;

  onMount(() => {
    const el = document.getElementById('radar-chart');
    chart = new Radar(el, options);
    chart.setData(data);
  });
</script>

<div id="radar-chart"></div>

<!--
  <script>
  import { onMount } from 'svelte';
  import { RadarChart, scaleLinear } from 'layercake.graphics';

  export let data;
  export let options;
  
  let container;

  onMount(() => {
    const xScale = scaleLinear(options.xKey, data, [0, 2 * Math.PI]);
    const yScale = scaleLinear(options.yKeys[0], data, [0, options.height/2]);
    
    const chart = new RadarChart(container, {
      xScale,
      yScale,
      data,
      width: options.width,
      height: options.height,
      padding: options.padding,
      xLabel: options.xLabel,
      yLabels: options.yKeyLabels,
      yColors: options.yKeyColors,
      yMin: options.yKeyMin,
      yMax: options.yKeyMax
    });

    chart.draw();
  });
</script>

<div bind:this={container} />

-->


<!--
  In this example, app.svelte imports MyRadarChart, data, and d3, and defines the options object. 
  It passes data and options as props to MyRadarChart.

MyRadarChart.svelte imports the required components and defines the data and options props using the export keyword. 
It also defines a container variable using the let keyword and binds it to the div element in the template using 
the bind:this directive. Finally, it uses the onMount lifecycle function to create a new RadarChart instance and 
draw the chart using the provided data and options.
-->