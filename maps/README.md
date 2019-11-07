# Spot Maps

These map PNGs are used for **NativeScript-UpLabs-2019**, instead of setting up an actual maps service (i.e. Google Maps).

- Directory names are the concatenated location _lat_ and _lon_ values, with all non-digit characters removed.
- Inside each directory is a _1x_, _2x_, and _3x_ PNG map of the location.

## Getting the Maps

The process for creating the map images is outlined below.

1. Fetch `wave` data for locations from surfline API.
1. Extract the locations `lat`, and `lon` values from `associated.location`.
1. Store these in `coords` array as `"lat/lon"`;
1. Go to [openstreetmap.org](https://www.openstreetmap.org/#map=14/0.0000/0.0000&layers=H);
1. Open the Chrome Console.
1. Initialise the `getMapAtIndex` function; it's an IIFE.
   ```js
   (function getMapAtIndex(index) {
      const array = [coords...];// hard code the coords array here.
      window.location.href = "https://openstreetmap.org/#map=14/"+array[index]+"&layers=H";
   })(index); // pass in the coords array item index (i.e. location) you want.
   ```
1. Wait for the page to load at your location. Then remove the unwanted _UI_ elements with the `removeUI` IIFE.
   ```js
   (function removeUI() {
     [
       document.getElementById("sidebar"),
       document
         .getElementById("map")
         .querySelector(".leaflet-control-container")
     ].forEach(e => (e.style.display = "none"));
   })();
   ```
1. Now log the index value for the current location minus the `/`. This will be the directory name.
   ```js
   (function logIndexValue(index){
      const array = [coords...];// hard code the coords array here.
      const regex = new RegExp(/\D/, "g");
      console.log(array[index].replace(regex, ""));
   })(index);// the current index.
   ```
1. Copy the output of `logIndexValue` to your clipboard.
1. Now, still in the Chrome Console, take a screen shot by typing `⌘ + Shift + P`. And type `Capture Screenshot`, then `Enter`.
1. Once image is downloded click `Show in Finder`.
1. Open `Get Info` of image.
1. Past the previously coppied location value into the **Tags**, and **Comments** section.
1. Repeat for all locations _(`⌘ + k`, clears the console)_.

## Creating the Map images

To create the _3_ map images of this location follow the below.

1. Open AdobeXD with a Custom Size workspace.
1. Create an Artboard at `W:320 x H:420`.
1. Drag one of the images onto the Artboard.
1. Scale image to `W:882 x H:459`.
1. Align bottom of image with botom of Artboard. And centered horizontally.
1. The OpenStreetMap header should not be visible within the Artboard.
1. Select the Artboad and export it, `File -> Export -> Selected`.
1. Specify this directory and save as `map` for`iOS` @ `1x`.
1. Get the location title from the images **Tag**.
1. Create a new directory with that title.
1. Drag the _3_ new images into this directory.
1. Rename the images `map.1x.png` _(and 2x, 3x)_.
1. Repeat for all the new location you are adding.
