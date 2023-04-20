<!--
  @component
  Generates an SVG bar chart.
 -->
 <script>
    import { getContext,createEventDispatcher } from 'svelte';
  
    const { data, xGet, yGet, xScale, yScale } = getContext('LayerCake');
    const dispatch = createEventDispatcher();
    
    function handleMousemove(feature,e) {
			console.info(arguments)
			return function handleMousemoveFn(e) {
				console.info(e,this)
				
				// When the element gets raised, it flashes 0,0 for a second so skip that
				if (e.layerX !== 0 && e.layerY !== 0) {
					dispatch("mousemove", { e });
				}
			};
		}
  
    /** @type {String} [fill='#00bbff'] - The shape's fill color. This is technically optional because it comes with a default value but you'll likely want to replace it with your own color. */
    export let fill = '#00bbff';
  </script>
  
  <g class="bar-group">
    {#each $data as d, i}
      <rect
        class='group-rect'
        data-id="{i}"
        x="{$xScale.range()[0]}"
        y="{$yGet(d)}"
        height={$yScale.bandwidth()}
        width="{$xGet(d)}"
        {fill}
        on:mouseover={(e) => dispatch("mousemove", { e, props: d })}
        on:mousemove={(e) => handleMousemove(e, d)}
      ></rect>
    {/each}
  </g>