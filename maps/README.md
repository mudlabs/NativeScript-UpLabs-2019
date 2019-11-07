# Spot Maps

These map PNGs are used for **NativeScript-UpLabs-2019**, instead of setting up an actual maps service like Google Maps. Because the private KEYs could not be secured in a Playground app.

- Directory names are the concatenated location _lat_ and _lon_ values, with all non-digit characters removed.
- Inside each directory is a _1x_, _1.5x_, _2x_, _3x_, and _4x_ PNG of the location.

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
1. Now log the index value for the current location minus the non-digit characters. This will be the directory name for this maps images.
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

1. Get the location title from the images **Tag**.
1. Create a new directory with that title here.
1. Open AdobeXD with a Custom Size workspace.
1. Create an Artboard at `W:320 x H:420`.
1. Drag the image onto the Artboard.
1. Using the `ExportX` plugin, adjust the image _size_ and _position_.
1. Using the `EportX` plugin, export the images to the correct directory.
1. Repeat for all the new location you are adding.
