<script>
  import BarChartLayer from "./lib/BarChartLayer.svelte";
  import MultiLineLayer from "./lib/MultiLineLayer/MultiLineLayer.svelte"; 
  import MapSection from "./lib/MapSection.svelte";
  import dataVotes from "./data/fiveyears_votes.json"
  import dataVotesLeftRight from "./data/political_alignment.json"
  const multilineColors1 = ['#18307b', '#eedd00','#eb6109','#fdb94d','#ed5975','#aaa','#00ff7f','#4488cc','#ee0000','#912c45','#63be21'];
  const multilineColors2 = ['#008837','#a6dba0','#c2a5cf','#7b3294'];
  let w;
  
</script>

<main>
  <header>
  
    <h1>Catalunya Municipal Elections</h1>
    <p>By Marina Rovira Boix, Joseph Ricafort, Pere Roca Ristol</p>
  
  </header>
  <section bind:clientWidth={w}>
    <h2>Introduction</h2>
    <p>The next 28th of May, people from 947 municipalities are summoned to the polls to choose which party will be elected for each of the country's councils. </p>
    <br>

    <p>The municipal elections, which are held every four years, are the ones that have the most impact on a day-to-day basis, because they serve to choose the representatives who will have the responsibility of adopting the policies most linked to the citizenry. The parties face them not only with the desire to take on the maximum number of mayors and representatives possible, but also as a platform to consolidate their local power.</p>
    <br>
    
    <p>This project aims to explore a little bit the results of the recent years elections. We have used the last 5 years of information for all the municipalities.
      Although the data is fine, there was the need to include a new column about to which main party in Spanish/Catalan government all the little municipal parties are related to. 
      This is due to, in the municipalities, usually the main parties have a party there, but in some towns, the name is not a clear relation.
    </p>
 
    <h2>Exploration</h2>
    
    
 
    <p>With that said, let’s progress to discuss the data. </p>
    <p>First, in the chart below, there’s an evolution for the last 5 years of elections for each party. The exploration is done using the general names, rather than all the municipal parties.</p>
    <p>Let’s consider this 4 groups for the parties:</p>

      <dl>
        <dt><b>Right:</b> VOX, Ciutadans, PP</dt>
        <dt><b>Moderate right:</b> JxCat, CIU</dt>
        <dt><b>Moderate left:</b> ERC, PSC, PACMA</dt>
        <dt><b>Left:</b> CUP, Podem</dt>
      </dl>

    <MultiLineLayer inputData={dataVotesLeftRight}  colors={multilineColors2}/> 



    <p>From this graph, we can conclude that in the vast majority of Catalonia, people vote more for left-wing parties. However, the correct matches have increased a bit.</p>
    <p>If we take a look at the evolution of each match, the graph is as follows.</p>
    
  
     <MultiLineLayer inputData={dataVotes} colors={multilineColors1}/> 


    <p>We can see a party that has dropped a lot, which is the <span class="highlighted">PSC</span>, considered moderate left and the current party elected in Spain alongside <span class="highlighted">Podemos</span>, which has dropped a little but is always between 200,000 and 300,000 votes.</p>
    <p>The <span class="highlighted">Others</span> category is also increased, which includes all the municipal parties that could not be related to the main ones. These are just local groups that exist only for municipal elections, usually with people from that place who want to lead change but not be associated with a major party. The main reason is usually the association with the ideals of one of the elders.</p>

    <br>

    <p>A curious case in the correct parties section is <span class="highlighted">Vox</span> & <span class="highlighted">Ciutadans</span>, both recently created (in the last 20 years) while others like <span class="highlighted">PP</span> or <span class="highlighted">PSOE</span> have been around since the 70s. They were new in 2003 and both are in 0 votes, but they got about 23,000 votes. 
      <span class="highlighted">Ciutadans</span> has always won more votes than <span class="highlighted">VOX</span>. However, they are having an internal crisis at the moment, so this could change in the future. What we can detect from the graph is that while both are increasing votes, the <span class="highlighted">PP</span> (which is the other one on the right) is decreasing its numbers.</p>
    <p>Hopefully this means that the people who vote well stay on the right, but the total number of people who vote for them does not increase.</p>

    <br>

    <p>Finally, but not least, there is a notable increase in <span class="highlighted">JxCat</span> and <span class="highlighted">ERC</span>, although one moderate left and the other moderate right, they are, along with the <span class="highlighted">CUP</span>, the three parties that defend the independence of Catalonia.
       Last year all three together got 43% of the total votes.</p>
    <p>We can better see the gains and losses of councilors between 2015 and 2019.</p>
 
    <BarChartLayer bind:clientWidth={w} {w}/>

  
</section>
  
  <section class="maps">
    <p>After the exploratory analysis, below you’ll find a map that provides a deeper inside in the municipality's results.</p>
    <br>
    <p>The 2015 and 2019 results can be explored in more detail. There are stories that are easily seen in the face of the drastic increase (ERC/JxCAT) or decrease (PP/CUP) of votes.
      For cases like the PSC where the increase is more general, winning votes distributed among many municipalities, it allows us to see in more detail which these municipalities are.
    </p>
    <MapSection />
  </section>
  <section class="stats-analyis">
    <h2>Stats Analysis</h2>
    
    <p>Preliminary analysis of the stats was done using R and Observable</p>
    <a href="https://observablehq.com/d/7eb01f000c28ad2e">Observable notebook</a><br>
    <a href="https://rpubs.com/josephricafort/catalunyaelections">R stats</a>
    <br>
    <p>Finally, we want to thank Anton Bardera and Matt Osborn for their help with the development of this project </p>
  </section>
</main>

<style>
  .highlighted 
  {
    font-size: 1.4rem;
    color: goldenrod;
  }
  .bar-chart {
    
    width: 100%;
  }
 /*  :global(.layercake-container line)
  {
    border-left: 1px dotted goldenrod;
  } */
  :global(.layercake-container .tooltip)
  {
    background-color: black;
  }
  :global(.axis .tick-mark) {
    font-size: .725em;
    
    color:white;
    
    
    text-shadow:unset!important;
  }
  :global(.layercake-container .key-item .name,.layercake-container text) {
    font-size: .725em;
    
    color:white;
    fill:white;
    text-shadow:unset!important;
  }
  section {
    padding: 10px;
    margin: 10px;
    color: white;
  }
  :root 
  {
    color:white;
  }
  section,
  header {
    max-width: 700px;
    margin: 0 auto;
  }
  :global(.legendbox text) 
  {
    fill: white;
  }
  :global(body) 
  {
    
    background: black;
  }
  :global(.maplibregl-popup-content) 
  {
    border: 1.5px solid white
  }
  :global(.mapboxgl-popup-anchor-bottom .mapboxgl-popup-tip, .maplibregl-popup-anchor-bottom .maplibregl-popup-tip) {
    border-top-color: black;
  }
</style>
