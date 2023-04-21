<script>
    import { LayerCake, Svg, Html } from 'layercake';
    import { format } from 'd3-format';
    import { scaleOrdinal } from 'd3-scale';
  
    import Key from './Key.html.svelte';
    import AxisX from './AxisX.svelte';
    import Beeswarm from './Beeswarm.svelte';
  
    // This example loads csv data as json using @rollup/plugin-dsv
    import data from '../../data/beeData.json';
  
    const xKey = 'day';
    const zKey = 'Type';
    const titleKey = 'book';
  
    const r = 4;
  
    const seriesNames = new Set();
    const seriesColors = ['#ccc', '#fc0', '#000'];
  
    const dataTransformed = data.map(d => {
      seriesNames.add(d[zKey]);
      return {
        [titleKey]: d[titleKey],
        [xKey]: +d[xKey],
        [zKey]: d[zKey]
      };
    });
  
    const addCommas = format(',');
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
  
  <div class='chart-container'>
    <LayerCake
      padding={{bottom: 15}}
      x={xKey}
      z={zKey}
      zScale={scaleOrdinal()}
      zRange={seriesColors}
      data={dataTransformed}
      let:width
    >
  
      <Svg>
        <AxisX
          baseline={true}
          formatTick={addCommas}
          tickMarks={true}
        />
        <!-- The Beeswarm component transforms the data and nests our original fields under `data` so access the `titleKey` under that -->
        <Beeswarm
          r={width < 400 ? r / 1.6 : r}
          spacing={1}
          getTitle={d => d.data[titleKey] }
        />
      </Svg>
  
      <Html pointerEvents={false}>
        <Key
          align='end'
          shape='circle'
          lookup={{
            USA: 'U.S.'
          }}
        />
      </Html>
  
    </LayerCake>
  </div>