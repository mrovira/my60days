<script>
    import { LayerCake, Svg } from 'layercake';
    import { scaleLinear } from 'd3-scale';
  
    import Radar from './RadarM.svelte';
    import AxisRadial from './AxisRadial.svelte';
  
    // This example loads csv data as json using @rollup/plugin-dsv
    //import data from '../../data/radar.json';
    import data from "../../data/motivationRadar.json"

  

    const seriesKey = 'concept';
    const xKey = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'];
  
    const seriesNames = Object.keys(data[0]).filter(d => d !== seriesKey);
  
    data.forEach(d => {
      seriesNames.forEach(name => {
        d[name] = +d[name];
      });
    });

    //console.log(seriesNames)
  </script>
  
  <style>
    /*
      The wrapper div needs to have an explicit width and height in CSS.
      It can also be a flexbox child or CSS grid element.
      The point being it needs dimensions since the <LayerCake> element will
      expand to fill it.
    */
    .chart-container {
      width:100%;
      height: 250px;
    }
  </style>
  
  <div class="chart-container">
    <LayerCake
      padding={{ top: 30, right: 0, bottom: 7, left: 0 }}
      x={xKey}
      xDomain={[0, 10]}
      xRange={({ height }) => [0, height / 2]}
      data={data}
    >
      <Svg>
        <AxisRadial/>
        <Radar/>
      </Svg>
    </LayerCake>
  </div>