maplate :: a demonstration and skeleton project for today's common opensource mapping client libraries

#### Overview
In a simple HTML file, link to leaflet.js and associated libraries wax.leaflet and cartodb.leaflet. This 
will allow us to display map tiles (show a map in the browser) from various tile servers and also
draw arbitrary points and shapes on the map based on geo data stored in a geospatial db (like cartodb).


#### Components
Tile Server - This is a host computer that holds the map tiles that make up the map you want to render

leaflet.js - javascript library that renders map tiles from a tile server in the browser

wax.leaflet.js - javascript library from MapBox that essentially adds functionality to leaflet
so that MapBox tiles and Interactivity are available

cartodb.leaflet.js - javascript library from CartoDB that adds functionality to leaflet so that
points and shapes from cartodb can be displayed on a leaflet rendered map


#### Make a Map!
Out of the box, the template.html file in this repo will display a map from MapQuest. You can change
the tile server url to show tiles from other places (make sure to give proper attribution!). For 
example, let's use Stamen's watercolor map tiles:

  $ var baseUrl = 'http://{s}.tile.stamen.com/watercolor/{z}/{x}/{y}.jpg',
  $   attrib = 'Map tiles by <a href="http://stamen.com">Stamen Design</a>, ' +
  $     'under <a href="http://creativecommons.org/licenses/by/3.0">CC BY 3.0</a>. ' +
  $     'Data by <a href="http://openstreetmap.org">OpenStreetMap</a>, ' +
  $     'under <a href="http://creativecommons.org/licenses/by-sa/3.0">CC BY SA</a>.'


You will notice that the template.html file has several "methods" of displaying tiles. The
first one (the one we just experimented with) uses leaflet with the "typical" tileserver format.
Typical in this case is really the Open Streetmap tile format with server/{z}/{x}/{y}.jpg. The
z / x / y describe zoom, lat, and lon and are substituted out automatically for you by the 
leaflet library when you load the map, when you scroll around, and when you zoom. Basically,
every time you manipulate the map, leaflet goes back to the tile server and requests new
tiles based on the lat / lon you are viewing and the zoom level. 

The second method (commented out) uses wax to grab tiles from mapbox. The mechanics work
similarly but, because mapbox does not use the exact same algorithm and url scheme
for serving tiles, wax is used to handle tile interaction like mapbox likes and
normailze it for leaflet so leaflet can work like it normally does. You can comment out
method 1 and uncomment method 2 to see tiles coming from mapbox.
