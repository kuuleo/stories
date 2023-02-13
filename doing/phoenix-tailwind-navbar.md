# REF https://tailwind-elements.com/docs/standard/navigation/navbar/#

The error I'm getting I'm guessing is because Map is not all defined...

* [ ] make sure all the imports are available in the map component and follow the errors in the Phoenix console.


I got the style.json file in the react app... now I just have to get the react app into the phoenix app

??HOW is maplibre in the react app?
---> it's maplibre-gl... and the version in package.json is 2.4


* [ ] user icon for the user profile dropdown
* [ ] make an icon helper
* [ ] REF says to create the svg's file in the assets/static/images file...
...?? has it changed and now they use priv instead... There isn't a file static inside of assets but there is a static directory inside of priv...
... * [ ] check and see

... still getting the error that the path is undefined
... * [x] try putting the same thing into the priv directory
```

```
vvvv now the error went away but only after I change from Drifter to DrifterWeb in the icons_helper... and i have both priv...icons and assets...icons.svg file
* [x] remove the assets one and see if it still works
---> yeah error is still gone

* [x] continue the REF and first just see if his svgs show up
* [ ] ... if they do then add the tabler icon for user circle
GROOVE and continue adding to that file

??HOW did I get the drifter logo to be the height that it currently is?
* [ ] match the tabler icons to this size also
