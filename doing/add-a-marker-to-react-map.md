# As a user, I see my own marker at the center of the map

I'm thinking I want to use a phoenix live view function component

... But no matter what, I should still want to interact with the React map to get the marker added

... it should correspond with the user dropdown... or simply the current user object that is stored in cookies

... I want location in there

... I want language in there

... I want the ...

* [ ] make a react component that returns a random number

vvvv Rando component is imported in app.js
vvvv Ranod component is created in js/components/
vvvv Rando component is called to be used in drifter_live_web/live/rando_live_component

* [ ] put the rando live component into Map live view

* generate a random number as per that REF
const randomNumber = Math.random() * 180 - 90

* [ ] add the marker to the map in the map component without anything external
... in the example, they use map.current...

I have access to this also...??

WHEN I add this to the top of app.css

@import './maplibre-gl.css';

... the markers stay in place like they should

* [ ] WHEN I restart the server, that line should be removed and the markers will be messed up again

There is something that writes the css to the file... ??WHAT is it?
---> there is assets.setup which is set to an array.  I guess this does all the setup steps in the array in order...??

... This is triggered by the setup method which has deps.get, ecto.setup, and assets.setup as its last step in the array

