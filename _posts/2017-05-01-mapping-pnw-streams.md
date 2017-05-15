---
layout: post
title: "Mapping Streams in The Pacific Northwest"
categories: 
tags: [Web Design]
image:
  feature: mapbox-map.png
  teaser: mapbox-map.png
  credit: 
  creditlink: ""
mapbox: true
---

This is a repost from my old website, originally posted on 8/9/2014.

I like visualizing river networks because they often explain why the topography looks the way it does. The <a href="http://nhd.usgs.gov/" target='_blank'>National Hydrography Dataset</a> is a geodatabase of all the catalogued streams in the US and includes useful stream attributes such as stream name and estimated annual flow. This second attribute is cool because I can use it to change the symbology of the river so larger streams get darker line colors and wider line widths, while smaller streams get lighter line colors and narrower line widths. Using flow directly is difficult when mapping the whole Columbia River Basin since the Columbia River has such large flow volumes relative to the other streams (~265,000 cfs at the mouth). Basically, the histogram of flows throughout the region is heavily right skewed to the point where good symbology is near impossible. To make the data usable I took the fifth root of flows. While the results are still not normal, they are MUCH better, and as you can see on the map, streams like the Willamette, Deschutes and Snake pop out when they should.
<div id='map-one' class='map'> </div>
<script>
L.mapbox.accessToken = 'pk.eyJ1IjoibXBzYXJpczAxIiwiYSI6ImNBNDRSUkUifQ.o5l8AZp3bO52Lb52G1rBcQ';
  L.mapbox.map('map-one', 'mapbox.outdoors,mpsaris01.y9hn0zfr', {
				minZoom: 6,
				maxZoom: 10}).setView([45.359, -118], 6);
</script>
Once I finished the symbology, I moved on to creating the map. I wanted to show the streams on top of the terrain but I didn't want to create my own base-layer. Instead, I used TileMill to symbolize my streams with no baselayer, exported them to MBTiles which I could then upload to Mapbox and display on top of their terrain basemap with roads and labels turned off. <a href="https://www.mapbox.com/foundations/an-open-platform/#mbtiles" target='_blank'>MBTiles</a> are a lot cooler than I originally realized because they can store mouse-over data and other information inside the tiles. It was therefore very easy to include stream name and estimated annual flows as a popup for each stream. I limited the zoom extents of the map to a range of six to ten since the size of the MBTiles grows exponentially for each additional zoom level. At this zoom range and spatial extent the MBTiles already took up 96 Mb! 

So there you have it. All the major streams in the Pacific Northwest! Some of the stream names are blank. That's because they are unnamed. I'm going to have fun poking around the region looking at streams that are named. It seems like you could make a fun little trivia quiz out of this. Whatever you end up using this for, I hope you enjoy it. I'm going to be thinking about how I can add some more data to the map and make it more interactive. Feel free to email me with any cool ideas.
