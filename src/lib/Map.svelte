<script context="module"></script>

<script>
  import { onMount, onDestroy } from "svelte";
  import { Map, NavigationControl, Popup, LngLat } from "maplibre-gl";
  import "maplibre-gl/dist/maplibre-gl.css";
  import * as d3 from "d3";
  import jQuery from "jquery";

  import { munis } from "../data/municipis.js";
  import { observable_data } from "../data/observable_data.js";
  export let filtered_data;
  export let colorScale;

  export let selectedParty;
  export let selectedYear;
  export let showOverlay;

  let _f;

  let map;
  let svg;
  let featureElements;

  let projectPoint = function (lon, lat) {
    var point = map.project(new LngLat(lon, lat));
    this.stream.point(point.x, point.y);
  };
  let transform = d3.geoTransform({
    point: projectPoint,
  });
  let path = d3.geoPath().projection(transform);

  let first_update = true;

  $: if (filtered_data.length > 0 && featureElements) {
    

    let arr = filtered_data.map((d) => d.municipality_code);
   
    featureElements
      .transition()
      .duration(450)
      .delay(function (d, i) {
        return i * 2;
      })

      .attr("fill", function (d, i) {
        let codiine = String(d.properties.codiine);
        let pos = arr.indexOf(codiine);
        if (pos > -1) {
          //console.warn(filtered_data[pos].voted_proportion,colorScale(filtered_data[pos].voted_proportion))
          return colorScale(filtered_data[pos].voted_proportion);
        } else {
          return "black";
        }
      });
  }
  else
  {
    if (filtered_data.length == 0)
    {
    featureElements=svg.selectAll("path.municipi");
    featureElements.transition()
      .duration(450)
      .delay(function (d, i) {
        return i * 2;
      })

      .attr("fill",'black')
    }
    
  }

  onMount(() => {
    const data = [];
    console.warn(filtered_data);
    map = new Map({
      container: "map", // container id
      //style: 'mapbox://styles/mapbox/streets-v8',
      style: {
        version: 8,
        sources: {
          geoserver: {
            type: "vector",
            tiles: [
              "https://geospatial.jrc.ec.europa.eu/geoserver/gwc/service/wmts?REQUEST=GetTile&SERVICE=WMTS&VERSION=1.0.0&LAYER=hotspots:gaul_0_simplified&STYLE=&TILEMATRIX=EPSG:900913:{z}&TILEMATRIXSET=EPSG:900913&FORMAT=application/vnd.mapbox-vector-tile&TILECOL={x}&TILEROW={y}",
            ],
          },
        },
        layers: [
          {
            id: "gaul_0_simple",
            source: "geoserver",
            "source-layer": "gaul_0_simplified",
            type: "fill",
            // "minzoom": 4,
            // "maxzoom": 6,
            paint: {
              "fill-color": "#a2a7ab",
              "fill-outline-color": "#87989c",
              "fill-opacity": 1,
            },
          },
        ],
      },
      center: [1.05, 41.4],

      //center: [141.15448379999998, 39.702053　],
      zoom: 4,
      //maxBounds:[[-0.665553,40.45029], [2.276123,42.462188]],
      maxBounds: [
        [-0.37, 40.3],
        [3.6, 42.8],
      ],

      attributionControl: false,
    });

    map.scrollZoom.disable();
    /*  setTimeout(function()
    {
      
story('VOX',2019)
    },3000) */

    map.addControl(new NavigationControl(), "top-right");


    function update() {
      featureElements = svg.selectAll("path.municipi");
      //featureElements.raise();
      featureElements.attr("d", path);
      if (first_update) {
        first_update = false;

    
        svg.on("mouseout", function () {          
          municipi_popup.remove();
        });
      }
    }

    map.on("load", function () {
      let fs = munis.features;

 

      var container = map.getCanvasContainer();

      svg = d3.select(container).append("svg");
      svg
        .style("position", "absolute")
        .style("width", "100%")
        .style("height", "100%")
        .style("top", "0")
        .style("left", "0")
        .style("z-index", "1000")
        .attr("class", "svg_map");

      featureElements = svg
        .selectAll("path.municipi")
        .data(fs)
        .enter()
        .append("path")
        // .classed('region', true)
        .attr("class", function (d) {
          return "municipi code_" + d.properties.municipi;
        })
        .attr("fill", "black")
        .attr("stroke", "gray")      
        .attr("code", function (d) {
          return d.properties.municipi;
        })
        .on("mouseenter", function (d) {
         

          _f = d;
        })
        .on("mouseleave", function (d) {
          
          _f = null;
        });

      update();
    });

    map.on("viewreset", function () {
  
      svg.style("opacity", 0);
      update();
    });
    map.on("movestart", function () {
      svg.classed("hidden", true);
      svg.style("opacity", 0);
    });
    map.on("rotate", function () {
      svg.classed("hidden", true);
      svg.style("opacity", 0);
    });
    map.on("moveend", function () {
      
      svg.classed("hidden", true);
      svg.style("opacity", 0);
      update();
      svg.style("opacity", 1);
      svg.classed("hidden", false);
    });

    let municipi_popup = new Popup({
      closeButton: false,
      closeOnClick: true,
      
      offset: {
        bottom: [0, -20],
        top: [0, 15],
        "top-left": [0, 0], //[linearOffset, (markerHeight - markerRadius - linearOffset) * -1],
        "top-right": [0, 0], //[-linearOffset, (markerHeight - markerRadius - linearOffset) * -1],
      },
    });


    map.on("mousemove", function (e) {
      if (!filtered_data || !_f) {
        
        jQuery(".maplibregl-popup").hide();
        municipi_popup.remove();
    
        return false;
      }

      let binded_data = filtered_data.filter((d) => {
      
        if (
          String(d.municipality_code) ==
          String(_f.target.__data__.properties.codiine)
        ) {
       
          return d;
       
        }
      })[0];

      if (!binded_data) {

        //even if no votes, we popup the name of municipality
        municipi_popup.setHTML(
          "<h3>" + _f.target.__data__.properties.nom_muni + "</h3>"
        );
        var latlng = e.lngLat;
        municipi_popup.addTo(map);
        municipi_popup.setLngLat(latlng);
        return false;
      }
      
      municipi_popup.addTo(map);
      var latlng = e.lngLat;
      var x = e.originalEvent.clientX;
      var y = e.originalEvent.clientY;

      municipi_popup.setLngLat(latlng);
      
      if (binded_data) {
       
        municipi_popup.setHTML(
          '<h3>' +
            _f.target.__data__.properties.nom_muni +
            '</h3><div style="font-size:1.1rem;text-decoration-thickness: .4rem;text-decoration-line: underline;text-decoration-color:'+colorScale(binded_data.voted_proportion)+'">' +
            binded_data.voted_proportion +
            '%</div>'
        );
    
        /*
         "<h3>" +
            _f.target.__data__.properties.nom_muni +
            '</h3><div style="text-decoration: underline;text-decoration-color:'+colorScale(binded_data.voted_proportion)+'>' +
            binded_data.voted_proportion +
            "</div>"
            */
      }
    });
  });

  onDestroy(() => {
    map.remove();
  });

  $: max_voted_features_party = observable_data
    .filter((d2) => d2.main_party == selectedParty && d2.year == selectedYear)
    .sort((a, b) => b.voted_proportion - a.voted_proportion)
    .slice(0, 5);
</script>

<div class="map-wrap">
  {#if selectedParty && showOverlay}
    <div class="map-overlay">
      <div class="story psc_story" style="display: block;">
        <h2>{selectedParty}</h2>
        <div>
          <button
            class="yearbtn"
            class:btn-active={selectedYear === "2015"}
            on:click={() => (selectedYear = "2015")}>2015</button
          >
          <button
            class="yearbtn"
            class:btn-active={selectedYear === "2019"}
            on:click={() => (selectedYear = "2019")}>2019</button
          >
        </div>
        <span>Max voted proportion municipalities</span>
        <ul>
          {#each max_voted_features_party as d}
            <li>
              <span class="party-name" title={d.municipality}
                >{d.municipality}:</span
              >
              <span class="voted-proportion"
                >{d.voted_proportion.toFixed(1)}%</span
              >
            </li>
          {/each}
        </ul>
      </div>
    </div>
  {/if}
  <div class="map" id="map" />
</div>

<style>
  .yearbtn {
    padding: 5px;
  }
  .btn-active {
    background: #888;
  }

  .map-overlay {
    position: absolute;
    z-index: 9999999;
    background: black;
    border: 1px solid white;
    right: 0;
    bottom: 0;

    padding: 10px;
    overflow-y: auto;
    width: 180px;
    border: 1px solid grey;
    font-size: 13px;
  }

  .story ul {
    list-style-type: none;
    padding: 5px;
    display: grid;
    grid-template-columns: 1fr auto;
    row-gap: 10px;
  }

  .story ul li {
    display: contents;
  }
  .story .voted-proportion {
    text-align: right;
  }
  .story .party-name {
    text-align: left;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
  }

  .map-wrap {
    position: relative;
    float: right;
    width: 100%;
    height: 570px;
  }

  .map {
    position: absolute !important;
    width: 100% !important;
    height: 100% !important;
  }

  /* .watermark {
    position: absolute;
    left: 10px;
    bottom: 10px;
    z-index: 999;
  }

  .mapboxgl-popup,
  .maplibregl-popup {
    z-index: 111111111 !important;
  }
  .legendWrapper path.domain,
  .legendWrapper line {
    opacity: 0;
  } */
</style>
