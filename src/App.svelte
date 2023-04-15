<script>
  import { LayerCake, Svg } from 'layercake';
  import { scaleLinear } from 'd3-scale';
  import MyRadar from 'src\components\myRadar.svelte';
  import data from 'src\data\data.json';
  import * as d3 from 'd3';

  const options = {
    width: 500,
    height: 500,
    padding: 50,
    xKey: 'day_of_the_week',
    yKeys: ['tiredness', 'motivation'],
    yKeyLabels: ['Tiredness', 'Motivation'],
    yKeyColors: ['#ff0000', '#00ff00'],
    yKeyMin: 0,
    yKeyMax: 10,
    xLabel: 'Day of the Week'
  };

  /*name,fastball,change,slider,cutter,curve
  Allison,10,0,4,8,5
  */
</script>

<div>
 <h1>60 days of reading.... or not</h1>

 <div> 
   <section id=requadre1>
     <h2>Reading progress</h2>
 <!--    <table>
       <tr>
         <td><img src="./images/001.jpeg" alt="1"/></td>
         <td><img src="./images/002.jpeg" alt="2"/></td>
         <td><img src="./images/003.jpeg" alt="3"/></td>
         <td><img src="./images/004.jpeg" alt="4"/></td>
         <td><img src="./images/005.jpeg" alt="5"/></td>
         <td><img src="./images/006.jpeg" alt="6"/></td>
       </tr>
     </table>-->
      <div class="row">
        <div class="column">
          <img src="src\images\001.jpeg" alt="1"/>
          <img src="src\images\011.jpg" alt="1"/>
        </div>
        <div class="column">
          <img src="src\images\002.jpeg" alt="2"/>
        </div>
        <div class="column">
          <img src="src\images\003.jpeg" alt="3"/>
        </div>
        <div class="column">
          <img src="src\images\004.jpeg" alt="4"/>
        </div>
        <div class="column">
          <img src="src\images\005.jpg" alt="5"/>
        </div>
        <div class="column">
          <img src="src\images\006.jpg" alt="6"/>
        </div>
        <div class="column">
          <img src="src\images\007.1.jpg" alt="7.1"/>
          <img src="src\images\007.2.jpeg" alt="7.2"/>
        </div>
        <div class="column">
          <img src="src\images\008.jpg" alt="8"/>
        </div>
        <div class="column">
          <img src="src\images\009.jpeg" alt="9"/>
        </div>
        <div class="column">
          <img src="src\images\010.jpeg" alt="10"/>
        </div>
      </div>
   </section>	
 </div>

</div>



<style>

 #requadre1 {
   background-color: white;
   color: #3F93F4;
   text-align: left;
   vertical-align: top;
   border-radius: 15px;
 }
.row {
  display: flex;
  flex-wrap: wrap;
  padding: 0 4px;
}

/* Create four equal columns that sits next to each other */
.column {
  flex: 50%;
  max-width: 10%;
  padding: 0 4px;
}

.column img {
  margin-top: 8px;
  vertical-align: middle;
  width: 100%;
}
</style>
<!--
  In app.svelte, you should import the MyRadarChart component that you created in MyRadarChart.svelte, 
  as well as any other dependencies that you need. 
  You should also define any options that you want to pass to the component, such as the width and height of the chart.

In MyRadarChart.svelte, you should define the logic and structure of the component, 
including any data processing or rendering that you need to do. 
You should also specify any props that the component expects, such as the data and options.
-->