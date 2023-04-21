<script>
    import { LayerCake, Svg } from 'layercake';
    import { scaleOrdinal, scaleBand } from 'd3-scale';
  
    import ForceLayout from './CirclePackForce.svelte';
  
    import data from '../../data/circleData.json';
  
    const xKey = 'Type';
    const rKey = 'pages';
    const zKey = 'Type';
  
    let groupBy = 'true';

    const seriesColors = ['#ccc', '#000', '#3C787E', '#726DA8'];

    let manyBodyStrength = 3;
    let xStrength = 0.1
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
    label {
    cursor: pointer;
    }
    input {
    margin-right: 7px;
    }
</style>

<div class="input-container">
    <label><input type="radio" bind:group={groupBy} value="true"/>Group by category</label>
    <label><input type="radio" bind:group={groupBy} value="false"/>Clump together</label>
    </div>

    <div class="chart-container">
    <LayerCake
    data={data}
    x={xKey}
    r={rKey}
    z={zKey}
    xScale={scaleBand()}
    rRange={[3, 12]}
    zScale={scaleOrdinal()}
    zRange={seriesColors}
    >
    <Svg>
        <ForceLayout
        {manyBodyStrength}
        {xStrength}
        groupBy={JSON.parse(groupBy)}
        nodeStroke='#000'
        />
    </Svg>
    </LayerCake>
</div>