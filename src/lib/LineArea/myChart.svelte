<script>
    import { LayerCake, Svg } from 'layercake';
  
    import Line from './Line.svelte';
    import Area from './Area.svelte';
    import AxisX from './AxisX.svelte';
    import AxisY from './AxisY.svelte';
  
    // This example loads csv data as json using @rollup/plugin-dsv
    import data from '../../data/lineAreaData.json';
  
    const xKey = 'day';
    const yKey = 'pages';
  
    data.forEach(d => {
      d[yKey] = +d[yKey];
    });
  </script>
  
  <style>
    /*
      The wrapper div needs to have an explicit width and height in CSS.
      It can also be a flexbox child or CSS grid element.
      The point being it needs dimensions since the <LayerCake> element will
      expand to fill it.
    */
    .chart-container {
      width: 100%;
      height: 250px;
    }
  </style>
  
  <div class="chart-container">
    <LayerCake
      padding={{ top: 8, right: 10, bottom: 20, left: 25 }}
      x={xKey}
      y={yKey}
      yNice={4}
      yDomain={[0, null]}
      data={data}
    >
      <Svg>
        <AxisX/>
        <AxisY
          ticks={4}
        />
        <Line/>
        <Area/>
      </Svg>
    </LayerCake>
  </div>