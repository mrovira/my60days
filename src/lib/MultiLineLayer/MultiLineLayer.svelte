<script>
    import { onMount } from "svelte";
    // import fiveYearsNorm from "../../data/fiveyears_norm.json"
    import dataCouncilors from "../../data/fiveyears_councilors.json"

    import { LayerCake, ScaledSvg, Html, flatten } from 'layercake';
    import { scaleOrdinal } from 'd3-scale';
    import { timeParse, timeFormat } from 'd3-time-format';
    import { format, precisionFixed } from 'd3-format';
  
    import MultiLine from './MultiLine.svelte';
    import AxisX from './AxisX.html.svelte';
    import AxisY from './AxisY.html.svelte';
    import GroupLabels from './GroupLabels.html.svelte';
    import Key from './Key.html.svelte';
    import SharedTooltip from './SharedTooltip.percent-range.html.svelte';
  
    // This example loads csv data as json using @rollup/plugin-dsv
    //import data from './fruit.csv';
    // const data = [
    //     {month:"2015-04-01",apples: 3840,bananas:1920,cherries:960,dates:400},
    //     {month:"2015-03-01",apples: 1600,bananas:1440,cherries:960,dates:400},
    //     {month:"2015-02-01",apples: 640,bananas:960,cherries:640,dates:400},
    //     {month:"2015-01-01",apples: 320,bananas:480,cherries:640,dates:400}
    // ];

    /* --------------------------------------------
     * Set what is our x key to separate it from the other series
     */
    export let inputData;
    export let colors;

    let eVarSel;
    let elecVars = ["votes_sum", "councilors_mean"];

     let data = inputData;

    const xKey = 'year';
    const yKey = 'councilors_mean';
    const zKey = 'main_party';
  
    const seriesNames = Object.keys(data[0]).filter(d => d !== xKey);
    const seriesColors = colors;//['#18307b', '#eedd00','#eb6109','#fdb94d','#ed5975','#aaa','#00ff7f','#4488cc','#ee0000','#912c45','#63be21'];
  
    //const parseDate = timeParse('%Y-%m-%d');
    const parseDate = timeParse('%d-%m-%Y');
  
    /* --------------------------------------------
     * Create a "long" format that is a grouped series of data points
     * Layer Cake uses this data structure and the key names
     * set in xKey, yKey and zKey to map your data into each scale.
     */
    const dataLong = seriesNames.map(key => {
      return {
        [zKey]: key,
        values: data.map(d => {
          // Put this in a conditional so that we don't recast the data on second render
          d[xKey] = typeof d[xKey] === 'string' ? parseDate(d[xKey]) : d[xKey];
          //d[xKey] = typeof d[xKey] === 'string' ? +d[xKey] : d[xKey];
          return {
            [yKey]: +d[key],
            [xKey]: d[xKey],
            [zKey]: key
          };
        })
      };
    });
  
    const formatTickX = timeFormat('%Y');
    //const formatTickX = d => d;
    const formatTickY = d => format(`.${precisionFixed(d)}s`)(d);
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
      height: 350px;
      margin-top: 100px;
    }
  
 
  </style>
  
  <div class="chart-container">
    <!-- <div>
      {#each elecVars as eVar, i}
        <label>
          <input type="radio" bind:group={elecVars} name="elecVars" bind:value={eVarSel}/>
          {eVar}
        </label>
      {/each}
    </div> -->
    <LayerCake
      ssr={true}
      percentRange={true}
      padding={{ top: 7, right: 10, bottom: 20, left: 25 }}
      x={xKey}
      y={yKey}
      z={zKey}
      zScale={scaleOrdinal()}
      zRange={seriesColors}
      flatData={flatten(dataLong, 'values')}
      yDomain={[0, null]}
      data={dataLong}
    >
      <Html>
        <AxisX
          gridlines={false}
          ticks={data.map(d => d[xKey]).sort((a, b) => a - b)}
          snapTicks={true}
          tickMarks={true}
          formatTick={formatTickX}
        />
        <AxisY
          baseline={true}
          formatTick={formatTickY}
        />
      </Html>
  
      <ScaledSvg>
        <MultiLine/>
      </ScaledSvg>
  
      <Html>
<!--          <GroupLabels/>  -->
        <SharedTooltip
          formatTitle={formatTickX}
          dataset={data}
        />
      </Html>
      <Html pointerEvents={false}>
        <Key
          align='end'
          shape='circle'
       />
      </Html>  
    </LayerCake>
  </div>
