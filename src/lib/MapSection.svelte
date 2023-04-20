<script>
  import Map from "./Map.svelte";
  import * as d3 from "d3";
  import BasicStats from "./BasicStats.svelte";
  import { observable_data } from "../data/observable_data.js";

  const years = [...new Set(observable_data.map((d) => d.year))].sort(
    (a, b) => a - b
  );
  const main_parties = [...new Set(observable_data.map((d) => d.main_party))];
  const storyParties = main_parties.filter((d) => {
    return (
      ["psc", "vox", "jxc", "erc", "cs", "pp", "cup"].indexOf(d.toLowerCase()) >
      -1
    );
  });
  $: selected_schema = "interpolateTurbo";
  let no_data=false;
  

  let selectedYear = "2015";
  let selectedParty = "ERC";

  const createColorScale = (selected_schema, min, max) =>
    d3.scaleSequential(d3[selected_schema]).domain([min, max]);

  $: filtered_data = observable_data.filter(
    (d) => d.year == parseInt(selectedYear) && d.main_party == selectedParty
  );


  $: no_data=filtered_data.length==0;
  $: f = filtered_data
    .filter((d) => d.voted_proportion > 0)
    .map((d) => d.voted_proportion);

    function someFunc() {
	console.log(my_value);
}



  function get_stats()
  {
    if (f.length>0)
    return {
      min: d3.min(f),
      max: d3.max(f),
      avg: d3.mean(f).toFixed(3)
    };
    else
    return {
      min: 0,
      max: 0,
      avg: 0
    };
  }

  $: stats= get_stats(f);
 /*  $: stats = {
    min: d3.min(f),
    max: d3.max(f),
    avg: d3.mean(f).toFixed(3)
  }; */

  $: colorScale = createColorScale(selected_schema, stats.min, stats.max);
</script>

<div class="forms">
  <select bind:value={selectedYear}>
    <option disabled selected value="">Select a year</option>
    {#each years as year}
      <option value={year.toString()}>{year}</option>
    {/each}
  </select>

  {#if selectedYear}
    <select bind:value={selectedParty}>
      <option disabled selected value="">Select a party</option>
      {#each main_parties as party}
        <option value={party}>{party}</option>
      {/each}
    </select>
  {/if}
</div>
{#if selectedParty && selectedYear && selected_schema && !no_data}
  <BasicStats {filtered_data} {colorScale} {stats} {no_data}/>
{/if}
{#if no_data}
  <div class="no_data">No data for {selectedParty} on {selectedYear}</div>
{/if}

<div class="story-buttons">
  {#each storyParties as party}
    <button
      class:btn-active={party === selectedParty}
      on:click={() => {
        selectedParty = party;
        selectedYear = "2015";
      }}>{party}</button
    >
  {/each}
</div>

<Map
  {filtered_data}
  
  {colorScale}
  {selectedParty}
  
  showOverlay={storyParties.includes(selectedParty)}
  bind:selectedYear
/>

<style>
  .story-buttons {
    margin: 15px 0;
    display: flex;
    justify-content: center;
    column-gap: 5px;
  }
  .btn-active {
    background: #888;
  }
  :global(.next_year) {
    margin-top: 5px;
    color: orange;
    cursor: pointer;
  }
  .forms {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 10px;
    padding: 10px;
  }
  :global(.maplibregl-control-container) {
    z-index: 99999999;
  }

  :global(.maplibregl-control-container, .maplibregl-ctrl-top-right) {
    z-index: 99999;
  }
  :global(.scale_container path.domain),
  :global(.scale_container line) {
    opacity: 0;
  }

  :global(.mapboxgl-popup-content)
  {
    background-color: black;
  }
  :global(.mapboxgl-popup),
  :global(.maplibregl-popup) {
    color: white !important;
    
    z-index: 111111111 !important;
  }
  :global(.maplibregl-ctrl-bottom-right) {
    z-index: 99999;
    background: #242424;
  }
</style>
