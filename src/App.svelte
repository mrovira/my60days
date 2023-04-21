<script>
  
  import { LayerCake } from 'layercake';
  //const multilineColors1 = ['#18307b', '#eedd00','#eb6109','#fdb94d','#ed5975','#aaa','#00ff7f','#4488cc','#ee0000','#912c45','#63be21'];
  //const multilineColors2 = ['#008837','#a6dba0','#c2a5cf','#7b3294'];
  import RadarT from "./lib/radar/myRadarT.svelte";
  import RadarM from "./lib/radar/myRadarM.svelte";
  //import MyBeeswarm from './lib/beeswarm/myBeeswarm.svelte';
  import MyChart from './lib/LineArea/myChart.svelte';
  import MyBeeswarmForce from './lib/beeswarnFroce/myBeeswarmForce.svelte';
  import MyCricle from './lib/circleForce/myCricle.svelte';
  //import dataRadar from '../../data/radar.json';
  let w;
  
</script>

<main>
  <header>
  
    <h1>60 days of reading 📚</h1>
    <p>By Marina Rovira Boix</p>
  
  </header>
    <h2>How has my progress been?</h2>
    <p>This project aims to explore a little bit my reading habits within 60 days to check if I will achieve my goal in Goodreads of 18 book read this year 2023. For that, din these 60 days, I have tracked my progress reading, including the number of pages, the time, motivation and tiredness in the moment.</p>
    <br>
    
    <h2>Pictures?</h2>
    

    <p>First rellevant thing is to compare motivation vs tiredness to answer the question if tiredness played an important role.</p>

    <div class="radials">
      <div class="rad-chart1">
        <h3>Tiredness</h3> 
        <RadarT></RadarT> 
      </div>
      <div class="rad-chart2">
        <h3>Motivation</h3> 
        <RadarM></RadarM>
      </div>
    </div>

    <p>While the day I was tired the most was Thursday, the one I was most motivated was Sunday, duh... are we surprised was on the weekend?! 😜</p>
    <p>It seems that tiredness HAS an impact. Antoher example is Wednesday, tiredness is low and motivation is high (yet). And others days but Sunday and Wednesday, are more or less at same rate.
      One curious things is that you can follow my week starting well on Monday, then decreasing in motivation, and recovering it on the weekend. 
    </p>
    <p>And we can conclude that <span class="highlighted">Thursday</span> is the <span class="highlighted">worst day</span>  of my weeks, deal with that Mondays!</p>
    
    <br>
    <p>At some point I started adding the type of book I was reading. In the presentation of the project I wanted to know to know if I have a tendency in a particular kind of book.
      But first, let's take a glimpse on the kind per day.
    </p>

    <div class="bee">
      <br>

    <MyBeeswarmForce></MyBeeswarmForce>

    <br>
    </div>
    

    <p>We can already see that the color showing the most is green, which represents essay. And if we check the number of pages we can confirm <span class="highlighted">Essay</span> is the type I read the <span class="highlighted">most</span></p>

    <MyCricle></MyCricle>
    <br>
    <p>To finish with the stats, here is the timeline of the pages read during these 60 days.</p>
    <MyChart></MyChart>

    <h2>Will I achieve my goal?</h2>
    

 

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
  .rad-chart1 {
    width: 50%;
  }
  .rad-chart2 {
    width: 50%;
  }
  .radials {
    width: 100%;
  }
  /* .bee {
    background-color: white;
  } */
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
    
    background: #3F93F4;
  }
  :global(.maplibregl-popup-content) 
  {
    border: 1.5px solid white
  }
  :global(.mapboxgl-popup-anchor-bottom .mapboxgl-popup-tip, .maplibregl-popup-anchor-bottom .maplibregl-popup-tip) {
    border-top-color: #3F93F4;
  }
</style>
