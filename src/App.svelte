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

  //import * from './images/';

  let w;
  
//   let table = document.querySelector('table');
// table.onwheel = function(e) {
//   if (e.deltaY < 0) {
//     table.style.fontSize = parseInt(getComputedStyle(table).fontSize) + 1 + 'px';
//   } else if (e.deltaY > 0) {
//     table.style.fontSize = parseInt(getComputedStyle(table).fontSize) - 1 + 'px';
//   }
//   e.preventDefault();
// };


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
    
    <table class="taula-imatges">
      <tr >
        <td><img src="./public/images/001.jpeg" alt="1" width="400" height="50"></td>
        <td><img src="./public/images/002.jpeg" alt="2" width="400" height="50"></td>
        <td><img src="./public/images/003.jpeg" alt="3" width="400" height="50"></td>
        <td><img src="./public/images/004.jpeg" alt="4" width="400" height="50"></td>
        <td><img src="./public/images/005.jpg" alt="5" width="400" height="50"></td>
        <td><img src="./public/images/006.jpg" alt="6" width="400" height="50"></td>
        <td><img src="./public/images/007.1.jpg" alt="7" width="200" height="50">
          <img src="./public/images/007.2.jpeg" alt="7.2" width="200" height="50"></td>
        <td><img src="./public/images/008.jpg" alt="8" width="400" height="50"></td>
        <td><img src="./public/images/009.jpeg" alt="9" width="400" height="50"></td>
        <td><img src="./public/images/010.jpeg" alt="10" width="400" height="50"></td>
      </tr>
      <tr>
        <td><img src="./public/images/011.jpg" alt="11" width="400" height="50"></td>
        <td><img src="./public/images/012.jpeg" alt="12" width="400" height="50"></td>
        <td><img src="./public/images/013.1.jpeg" alt="13" width="200" height="50">
          <img src="./public/images/013.2.jpg" alt="13.2" width="200" height="50"></td>
        <td><img src="./public/images/014.jpeg" alt="14" width="400" height="50"></td>
        <td><img src="./public/images/015.jpeg" alt="15" width="400" height="50"></td>
        <td><img src="./public/images/016.jpeg" alt="16" width="400" height="50"></td>
        <td><img src="./public/images/017.jpg" alt="17" width="400" height="50"></td>
        <td><img src="./public/images/018.jpeg" alt="18" width="400" height="50"></td>
        <td><img src="./public/images/019.jpeg" alt="19" width="400" height="50"></td>
        <td><img src="./public/images/020.jpeg" alt="20" width="400" height="50"></td>
      </tr>
      <tr>
        <td><img src="./public/images/021.jpeg" alt="21" width="400" height="50"></td>
        <td><img src="./public/images/022.jpeg" alt="22" width="400" height="50"></td>
        <td><img src="./public/images/023.jpeg" alt="23" width="400" height="50"></td>
        <td><img src="./public/images/024.jpeg" alt="24" width="400" height="50"></td>
        <td><img src="./public/images/025.jpg" alt="25" width="400" height="50"></td>
        <td><img src="./public/images/026.jpg" alt="26" width="400" height="50"></td>
        <td><img src="./public/images/027.jpg" alt="27" width="400" height="50"></td>
        <td><img src="./public/images/028.jpg" alt="28" width="400" height="50"></td>
        <td><img src="./public/images/029.jpeg" alt="29" width="400" height="50"></td>
        <td><img src="./public/images/030.jpg" alt="30" width="400" height="50"></td>
      </tr>
      <tr>
        <td><img src="./public/images/031.jpeg" alt="31" width="400" height="50"></td>
        <td><img src="./public/images/032.jpg" alt="32" width="400" height="50"></td>
        <td><img src="./public/images/033.jpg" alt="33" width="400" height="50"></td>
        <td><img src="./public/images/034.jpg" alt="34" width="400" height="50"></td>
        <td><img src="./public/images/035.jpeg" alt="35" width="400" height="50"></td>
        <td><img src="./public/images/036.jpg" alt="36" width="400" height="50"></td>
        <td><img src="./public/images/037.jpeg" alt="37" width="400" height="50"></td>
        <td><img src="./public/images/038.jpeg" alt="38" width="400" height="50"></td>
        <td><img src="./public/images/039.jpg" alt="39" width="400" height="50"></td>
        <td><img src="./public/images/040.jpeg" alt="40" width="400" height="50"></td>
      </tr>
      <tr>
        <td><img src="./public/images/041.jpeg" alt="41" width="400" height="50"></td>
        <td><img src="./public/images/042.jpg" alt="42" width="400" height="50"></td>
        <td><img src="./public/images/043.jpg" alt="43" width="400" height="50"></td>
        <td><img src="./public/images/044.jpg" alt="44" width="400" height="50"></td>
        <td><img src="./public/images/045.jpg" alt="45" width="400" height="50"></td>
        <td><img src="./public/images/046.jpeg" alt="46" width="400" height="50"></td>
        <td><img src="./public/images/047.jpeg" alt="47" width="400" height="50"></td>
        <td><img src="./public/images/048.jpg" alt="48" width="400" height="50"></td>
        <td><img src="./public/images/049.jpg" alt="49" width="400" height="50"></td>
        <td><img src="./public/images/050.jpg" alt="50" width="400" height="50"></td>
      </tr>
      <tr>
        <td><img src="./public/images/051.jpg" alt="51" width="400" height="50"></td>
        <td><img src="./public/images/052.jpg" alt="52" width="400" height="50"></td>
        <td><img src="./public/images/053.jpg" alt="53" width="400" height="50"></td>
        <td><img src="./public/images/054.jpg" alt="54" width="400" height="50"></td>
        <td><img src="./public/images/055.jpg" alt="55" width="400" height="50"></td>
        <td><img src="./public/images/055.jpg" alt="56" width="400" height="50"></td>
        <td><img src="./public/images/057.jpg" alt="57" width="400" height="50"></td>
        <td><img src="./public/images/058.jpg" alt="58" width="400" height="50"></td>
        <td><img src="./public/images/059.jpg" alt="59" width="400" height="50"></td>
        <td><img src="./public/images/060.jpg" alt="60" width="400" height="50"></td>
      </tr>
    </table>
    
    <br>
    <p>First rellevant thing is to compare motivation vs tiredness to answer the question if tiredness played an important role.</p>

    <div class="radials">
      <div class="rad-chart1" >
        <h3>Tiredness</h3> 
        <RadarT></RadarT> 
      </div>
      <div class="rad-chart2" >
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

    <br>
    <br>
    <h2>Will I achieve my goal?</h2>
    
    <table class="taula">
      <tr>
        <td class="taula-1">Previous</td>
      </tr>
      <tr>
        <td class="taula-2">Total pages 2022: <b>4000</b> <sub class="taula-3">11 p/d</sub></td>
        <td class="taula-2"> Total books 2022: <b>12</b></td>
      </tr>
      <tr>
        <td class="taula-1">Actual</td>
      </tr>
      <tr>
        <td class="taula-2">Total pages 2023: <b>398</b> <sub class="taula-3">6 p/d</sub></td>
        <td class="taula-2"> Current books 2023: <b>3</b></td>
      </tr>
      <tr>
        <td class="taula-1">Expectations</td>
      </tr>
      <tr>
        <td class="taula-2">Expected pages 2023: <b>6000</b> </td>
        <td class="taula-2">Expected books 2023: <b>18</b></td>
      </tr>
      <tr>
        <td class="taula-1">Can it be achieve?</td>
      </tr>
      <tr>
        <td class="taula-2"><span class="highlighted">There's still a chance, but I need to increase the rythm</span></td>
      </tr>
    </table>
 

</main>

<style>
  .highlighted 
  {
    font-size: 1.4rem;
    color: goldenrod;
  }
  .rad-chart1 {
    width: 400;
  }
  .rad-chart2 {
    width: 400;
  }
  .radials {
    width: 100%;
  }
  .taula-1 {
    color: white;
    font-weight: bold;
    text-align: left;
  }
  .taula-2 {
    color: white;
  }
  .taula-3 {
    color: rgb(199, 197, 197);
  }
  .taula {
    margin-left: auto;
    margin-right: auto;
    font-size: 25px;
  }
  td {
    padding-top: 10px;
  padding-bottom: 20px;
  }
  .taula-imatges {
    margin-left: 10px;
    margin-right: auto;
  }
  img {
    max-width: 100%;
    max-height: 100%;
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
  :root 
  {
    color:white;
  }
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
