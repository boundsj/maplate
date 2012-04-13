maplate :: a demonstration and skeleton project for today's common opensource mapping client libraries

#### Overview
In a simple HTML file, link to leaflet.js and associated libraries wax.leaflet and cartodb.leaflet. This 
will allow us to display map tiles (show a map in the browser) from various tile servers and also
draw arbitrary points and shapes on the map based on geo data stored in a geospatial db (like cartodb).

#### Components and Terms
Tile Server - This is a host computer that holds the map tiles that make up the map you want to render. 
Various organizations host tile servers like Stamen, OSM, MapQuest, MapBox, etc..

leaflet.js - javascript library that renders map tiles from a tile server in the browser

wax.leaflet.js - javascript library from MapBox that essentially adds functionality to leaflet
so that MapBox tiles and Interactivity are available

cartodb.leaflet.js - javascript library from CartoDB that adds functionality to leaflet so that
points and shapes from cartodb can be displayed on a leaflet rendered map

Tile URL - This is a scheme for communicating from the client to the tile server which tiles you 
want. The OSM standard is: http://[abc].tile.openstreetmap.org/zoom/x/y.png
Several organizations use this format including Stamen and Mapnik
This [wiki page](http://wiki.openstreetmap.org/wiki/Slippy_map_tilenames#Tile_servers) explains more 
details about the URL schemes and how tile servers work.
Note that MapBox uses a different scheme, it looks like this: 
http://a.tiles.mapbox.com/v3/user.tilesetname.jsonp


#### Make a Map!
The template.html file has javascript with 4 recipes. At the top of the file you can uncomment one
function (recipe) at a time and refresh this template.html file in your browser to see how they look.
 Here is an explanation of each recipe:

Recipe 1:
This function simply displays tiles from MapQuest using leafet.
You can change the tile server url to show tiles from other places (make sure to give proper attribution!). For 
example, let's use Stamen's watercolor map tiles:

  $ var baseUrl = 'http://{s}.tile.stamen.com/watercolor/{z}/{x}/{y}.jpg',
  $   attrib = 'Map tiles by <a href="http://stamen.com">Stamen Design</a>, ' +
  $     'under <a href="http://creativecommons.org/licenses/by/3.0">CC BY 3.0</a>. ' +
  $     'Data by <a href="http://openstreetmap.org">OpenStreetMap</a>, ' +
  $     'under <a href="http://creativecommons.org/licenses/by-sa/3.0">CC BY SA</a>.'

Note: you can find the url for Stamen and other tile servers [here](http://geocommons.com/overlays/217943) at geocommons

This first recipe uses leaflet with the "typical" tileserver format.
Typical in this case is really the Open Streetmap tile format with server/{z}/{x}/{y}.jpg. The
z / x / y describe zoom, lat, and lon and are substituted out automatically for you by the 
leaflet library when you load the map, when you scroll around, and when you zoom. Basically,
every time you manipulate the map, leaflet goes back to the tile server and requests new
tiles based on the lat / lon you are viewing and the zoom level. Next, we'll look at 
an example using MapBox tiles.

Recipe 2:
This uses wax to grab tiles from mapbox. The mechanics work
similarly but, because mapbox does not use the exact same algorithm and url scheme
for serving tiles, wax is used to handle tile interaction like mapbox likes and
normailze it for leaflet so leaflet can work like it normally does.

Recipe 3:
This is similar to Recipe 2, except now we are using wax to grab not just the basemap tiles
but also transparent (except for points) tiles that overlay on top of the basemap - points on a map!
This is interesting because we are not using leaflet to insert individual markers in the layer. 
The cartodb/wax stack is actually rendering speical tiles that live on top of our base map layer. 
We could theoretically show many thousands of points in just a few seconds because the the dots
are coming as tiles (not individual geojson).

Recipe 4:
This is just like Recipe 3, except that we are not using wax to load the base layer tiles - we are using
leaflet instead. This let's us grab tiles from a non-mapbox tile server (like Stamen in this case).




