You need to use a third-party library in an HTML file to display vector tile-based map. Here are some common libraries you can use:

Mapbox
Maplibre: Open-source fork of Mapbox.
OpenLayer


Maplibre
I created a map-maplibre.html file, which you can access via https://www.linuxbabe.com/map-maplibre.html. Note that you need to use your own Maptiler API Key. For how to use Maplibre GL JavaScript library, please check the official Maplibre guides.

<!DOCTYPE html>
<html>
    <head>
         <meta charset="utf-8">
         <title>vector tile map made with Tegola and Maplibre</title>
         <meta name="viewport" content="initial-scale=1,maximum-scale=1,user-scalable=no">
         <script src="https://unpkg.com/maplibre-gl@2.1.9/dist/maplibre-gl.js"></script>
         <link href="https://unpkg.com/maplibre-gl@2.1.9/dist/maplibre-gl.css" rel="stylesheet" />
         <style>
            body { margin: 0; padding: 0; }
            #map { position: absolute; top: 0; bottom: 0; width: 100%; }
         </style>
   </head>
   <body>
        <div id="map"></div>
        <script>
                var map = new maplibregl.Map({
                container: 'map',
                style:
                        'https://api.maptiler.com/maps/streets/style.json?key=5Wt1JU7PRdrMRzbqkJvG',
                zoom: 5,
                center: [0.8, 53.5]
        });     


        map.on('load', function () {
                  // Add a new vector tile source with ID 'linuxbabe'.
                  map.addSource('linuxbabe', {
                         'type': 'vector',
                         'tiles': [
                              'https://vector-tile.linuxbabe.com/maps/osm/{z}/{x}/{y}.pbf'
                          ],
                          'minzoom': 6,
                          'maxzoom': 14
                    });
                    map.addLayer(
                       {
                            'id': 'default', // Layer ID
                            'type': 'line',
                            'source': 'linuxbabe', // ID of the tile source created above
                               // Source has several layers. We visualize the one with name 'sequence'.
                            'source-layer': 'sequence',
                            'layout': {
                                      'line-cap': 'round',
                                      'line-join': 'round'
                             },
                            'paint': {
                                       'line-opacity': 0.6,
                                       'line-color': 'rgb(53, 175, 109)',
                                       'line-width': 2
                             }
                      },
                   );
                });

                map.addControl(new maplibregl.NavigationControl());
        </script>
        </body>
</html>
Here’s how it looks:


The first example is from the Tegola tutorial...
... the second one is from the tileserver tutorial
... the second one doesn't use a maptiler key...??



Display Map with MapLibre GL
Maplibre GL is an open-source fork of Mapbox GL. Demo: https://www.linuxbabe.com/maps/maplibre-streets.html

* [ ] try running both locally in a browser
... ?? maybe is just want to do create-react-app and put this directly in the index file...??
HTML code:

<!DOCTYPE html>
<html>
    <head>
         <meta charset="utf-8">
         <title>vector tile map made with Tegola and Maplibre</title>
         <meta name="viewport" content="initial-scale=1,maximum-scale=1,user-scalable=no">
         <script src="https://unpkg.com/maplibre-gl@2.1.9/dist/maplibre-gl.js"></script>
         <link href="https://unpkg.com/maplibre-gl@2.1.9/dist/maplibre-gl.css" rel="stylesheet" />
         <style>
            body { margin: 0; padding: 0; }
            #map { position: absolute; top: 0; bottom: 0; width: 100%; }
         </style>
   </head>
   <body>
        <div id="map"></div>
        <script>
                var map = new maplibregl.Map({
                container: 'map',
                style:
                        'https://www.linuxbabe.com/maps/mapbox-street-style.json',
                zoom: 5.43,
                center: [-3.9, 54.5]
        });     


        map.on('load', function () {
                  // Add a new vector tile source with ID 'linuxbabe'.
                  map.addSource('linuxbabe', {
                         'type': 'vector',
                         'tiles': [
                              'https://tileserver.linuxbabe.com/data/v3/{z}/{x}/{y}.pbf'
                          ],
                          'minzoom': 6,
                          'maxzoom': 14
                    });
                    map.addLayer(
                       {
                            'id': 'default', // Layer ID
                            'type': 'line',
                            'source': 'linuxbabe', // ID of the tile source created above
                               // Source has several layers. We visualize the one with name 'sequence'.
                            'source-layer': 'sequence',
                            'layout': {
                                      'line-cap': 'round',
                                      'line-join': 'round'
                             },
                            'paint': {
                                       'line-opacity': 0.6,
                                       'line-color': 'rgb(53, 175, 109)',
                                       'line-width': 2
                             }
                      },
                   );
                });

                map.addControl(new maplibregl.NavigationControl());

                //set max zoom level (0-24)
                map.setMaxZoom(19);
        </script>
        </body>
</html>

* [ ] When I put it the url `https://linuxbabe.com/maps/maptiler-3d-gl-style.json` the json files comes up in the broswer.  Make a local url in my local app that makes a similar json page appear except using the url localhost:XXX
    * [ ] substitute the url that tie to tileserver.XXX ... replace with tileserver.drifter.live
    * [ ] subsstitue the url that tie to linuxbabe.com ... replace with localhost:xxxx

    * [x] download source for maptiler basic inside of http directory
    * [ ] try putting a path in for the url

    * [ ] localhost:8001 returns the json data for the basic style
    * [ ] put the url for drifter.live into the sources for openmaptiles in this json
    * [ ] put the url for the newly defined fonts from the nginx file in the for glyphs
    *so I'm still putting my local style url in the node http app and then I'm putting the url for the drifter.live tileserver style in inside of that local file*

* [ ] 127.0.0.1:8000/map-style returns the json file that is being run on 8001
* [ ] make the style json return just like digital ocean is doing books (instead of the stringify json just put my json object inside of ``)
    * [x] now should show json when I navigate to localhost:8001/map-stylebe the same on 8001 except using new switch case statement
    * [ ] show the same json WHEN I navigate to localhost:8000/map-style

    * find out WHAT this position is in WHAT json?
    `Error: Bad control character in string literal in JSON at position 18680`


"For security reasons, browsers restrict cross-origin HTTP requests initiated from scripts..."

"... only accepts requests from same origin... unless the response from the other origins includees the right CORS headers"

??WHAT are the "right" CORS headers?

I'm not sure if I messed it up or what but now there are 2 server blocks in my nginx config file:


