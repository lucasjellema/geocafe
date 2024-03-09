# Geo Cafe - exploring geo data and tools & technologies for working with it

In the Geo Cafe we look at tools for visualizing geo data - including Datawrapper anm Google MyMaps, for creating and manipulating geo data - such as geojson.io, mapshaper and mapwarper - and at a tool for doing most of that as well as analyzing geo data: QGIS. We discuss geo data formats and public geo datasets. We end with a look at Leaflet, a JavaScript library for integrating real world interactive maps in web applications.

## 1. Datawrapper - Chloropleth map

Using CSV file with geo-related data, create chloropleth map

DataWrapper is a free online service for visualizing data. 19 chart types are available as well as many resources explaining how to tell stories with data. Three types of maps can be created, next to 16 other types of visualizations. 

To create a map, go to [app.datawrapper.de/create/map] and select Choropleth map.

![](images/datawrapper-chloropleth-step1.png)
The first question that Datawrapper will ask you after you've decided on a choropleth map, is: "What type of map do you want to create?" 
![](images/datawrapper-chloropleth-step2.png)

Enter "netherlands" in the search field. From the list of maps, select "Netherlands » Provinces (2016)". Then click on Proceed.

Note: Data Wrapper has over 3000 predefined maps with the boundaries of different administrative units. The world, continents, countries, states and more. 

You can now upload the file `dutch-provinces.csv` from the repo or paste contents from this file into the text area, as is shown here:
![](images/datawrapper-chloropleth-paste-data.png)

Click on the icon with the arrow point to the right. The pasted data is merged into the table and if possible matched with the (names of the) provinces (and thereby to the geographical areas on the map that each of these provinces occupies).   

Either your data can be automagically matched with the definitions of the administrative units in the map you select, or you need to specify explicitly how that mapping can take place. This is done on the "Match" tab. 

![](images/datawrapper-chloropleth-math.png)

The field Matching Key indicates the property from the predefined set of administrative units in the selected map you want to match with. With "Select column for Name", you specify which of the fields in the CSV file is to be matched with the key. Finally, the field selected in "Select column for Value" os the field or property used to determine the value to use for coloring each matched administrative unit. Here I am using the randomly generated *Preference* field. You can also select *Area in km2* to get a more meaningful map.  


In this next step - Visualize - you can finetune the appearance of the map. What color palette to use, what value range to support. What are titles and labels. Should the map be zoomable to users? What should be the size of the map in published form?   

![](images/datawrapper-chloropleth-visualize2.png)

Under Annotate, you can define meta-data for the map, specify if tool tips are shown and define labels - for example names of the provinces to be shown in the map. You can add annotations to the map. 
![](images/datawrapper-chloropleth-annotate.png)

On the tab Layout are more settings that determine what the map will look like when published. One interesting option to switch on or off: Data Download. Do you make the raw data available from which the chart was built. It is good form to do so.

![](images/datawrapper-chloropleth-layout.png)

The next step - Publish & Embed - is where the map can be exported as static (i.e. non-interactie) image (to do with as you see fit) or to publish the image for others to see and for you to embed in your website, articles, applications etc. 
![](images/datawrapper-chrloropleth-publish-embed.png) 

When you press "Publish Now", and you are not yet signed in to Data Wrapper, you will be asked to enter an email address to have a link to the visualization sent to. With that link, you can get various embed links/scripts to include the chloropleth visualization in your own website, Medium articles, Powerpoint slide decks etc. After receiving the email, you can click on the link. At this point if you do not have an account already you have to create one (for free). Once you have an account, you get the public URL and the embed snippets to include the map in your own website, blog article or application.

### Recreate the Map for Area instead of Preference

Repeat the steps and this time create a map that colors the provinces based on their area.

The result for me looks like this:
![](images/datawrapp-erchlorpleth-byarea.png)

I have an interesting observation: Gelderland has the biggest area - a well known fact - but Friesland is shaded the darkest blue. This has to do with the source of the data - and the definition of the area. Friesland encompasses large bodies of water, including a substantial part of the Waddenzee. That is not land mass but should it be included in area? I asked ChatGPT to generate the CSV data for me and this is what it did.


## 2. Datawrapper - Locator Map

In this exercise you will create a Locator Map in Data Wrapper to show data on the Conclusion office locations. You will start from the "raw" GeoJSON file that Data Wrapper can turn into a set of locations on a map.

Again, go to the Data Wrapper website. Click on Products. Click on Maps. Select Locator Map.
![](images/datawrapper-locatormap.png)

Click on the button for creating a new Locator Map

![](images/datawrapper-locatormap2.png)
The first page of a four step wizard appears. You can define the markers manually, or upload the GeoJSON data from which to build the map. Or paste it in. 

Open the file `datafiles\conclusion-offices-geojson.json` and copy the contents into the clipboard.

In Data Wrapper, click on the radio button to import the data.

A text area appears. Click on it and paste the data from the clipboard.

Acknowledge the warning. (22 locations is not that many)

![](images/datawrapper-locatormap-warning.png)
DataWrapper processes the data, lists the entries (as markers) and shows it on a map:

![](images/datawrapper-locatormap-markers.png)

Adjust center and scale to bring the data into focus. Labels and icons are the default. You can update them for every marker. 

Enter a title for the map chart. Click on Proceed.
![](images/datawrapper-locatormap-maprefinement.png)
In this step, we can refine the map – show geographic details, (province) borders, roads? Show an inset (The Netherlands on a globe)? A scale indication?
Make the refinements you fancy. Or none to just quickly create the map.

Next step: set some map attributes (description, data source and URL, by line or author) and define the keys for the legend that clarifies the markers if you have defined different icon types or colors.

Then go to Publish and Embed like before to complete the definition of the map and make it available to external publication. 
![](images/datawrapper-locatormap-publish.png)


### Adding More Visual Clues to the Locator Map

We will now improve on the results from the previous step. We could manually change the appearance of each marker, but that is a lot of work. Instead, let's use the meta-data already present in the GeoJSON document. If we can provide that data to Data Wrapper [in the prescribed way](https://academy.datawrapper.de/article/177-how-to-style-your-markers-before-importing-them-to-datawrapper), it will be able to derive icon, color, size, label etc. from it .   

Follow the instructions in [this article](https://technology.amis.nl/data-analytics/prepare-custom-map-data-with-mapshaper-and-present-with-datawrapper/) to use **Mapshaper** to get a better prepared data file that is converted by Data Wrapper into a much nicer looking map. 

The result will look something like this:
![](images/datawrapper-locatormap-conclusion-offices.png)



## 3. Google MyMaps, Mapshaper & GeoJSON.io


## 4. Browse Public Geo Datasets

Check out websites

GISCO - the Geographic Information System of the COmmission - localise, analyse, visualise: https://ec.europa.eu/eurostat/web/gisco/geodata/reference-data . Within Eurostat, GISCO is responsible for meeting the European Commission's geographical information needs at 3 levels: the European Union, its member countries, and its regions.

The PDOK Viewer - Dutch open government data with current geo-information: Bij PDOK vind je open datasets van de overheid met actuele geo-informatie. Deze datasets zijn benaderbaar via geo webservices en beschikbaar als downloads. https://app.pdok.nl/viewer

UNdata - https://data.un.org/ - a world of information - data sets from United Nations on population, refugees, economy, education, labor, trade, energy, crime, health, science, environment, communication, transport and tourism.

Natural Earth is a public domain map dataset available at 1:10m, 1:50m, and 1:110 million scales. Featuring tightly integrated vector and raster data, with Natural Earth you can make a variety of visually pleasing, well-crafted maps with cartography or GIS software. Both vector (Shapefiles) and raster (TIFF) files.   https://www.naturalearthdata.com/
Some examples: countries, regions, cities, parks, administrative units. And: Coastline, rivers, reefs, bathymetry (deepness). Raster: elevation, bathymetry, gray-tone, relief, natural earth.

Copernicus - Satellite imagery available as raster (WMS/WMTS) - https://www.copernicus.eu/en/accessing-data-where-and-how/copernicus-services-catalogue -  

Worldbank Data Catalog - https://datacatalog.worldbank.org/home 

NASA EarthData - https://www.earthdata.nasa.gov/

GADM maps and data - provides maps and spatial data for all countries and their sub-divisions. https://gadm.org/data.html (GeoJSON, Shapefile,KMZ data files with boundaries of administrative units)



Download a particular data set
Check and Shape (and combine?) with mapshaper? 
Visualize in Datawrapper or MyMaps



## 5. QGIS - first steps



## 6. Playing with FotoMapp

Trying out https://lucasjellema.github.io/foto-map/ 

Upload images
Click to create markers
Click on marker - inspect popup
Paste GeoJSON

Copy GeoJSON (and paste in geojson.io or in Datawrapper)
Copy as Image

Filter by date
Clustering of closely located markers
Consolidate markers (check out the caroussel in the popup)

Edit mode:
Click to add marker
Drag Marker
Edit Marker/Site/Tooltip


Add custom map layer of tiled map service, for example of WARP-ed images/maps such as https://mapwarper.net/maps/tile/80272/{z}/{x}/{y}.png




## 7. First steps with Leaflet - integrating a map in a web application

If you want to integrate real world maps into your applications and provide interaction, zoom control, multiple layers and other fineries, you can do no better than use Leaflet. Leaflet is a well established, very popular and very easy to use JavaScript library for creating such maps inside your application, from the data manaed by your application and well interated with the events taking place inside your application.

We will now take a few quick first steps with Leaflet. Even if you are not a web application developer - of a developer of any kind - you can probably follow along.
For slightly more detail, check [Leaflet's Quick Start Documentation](https://leafletjs.com/examples/quick-start/)

Open the web site JSFiddle at https://jsfiddle.net/.
![](images/jsfiddle1.png)

Paste the following HTML, CSS and JavaScript fragments in the designated areas.

### HTML - the structure and markup of the web page:
```
<!DOCTYPE html>
<html lang="en">

  <head>
    <base target="_top">
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Quick Start - Leaflet</title>

    <link rel="shortcut icon" type="image/x-icon" href="docs/images/favicon.ico" />

    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY=" crossorigin="" />
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js" integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo=" crossorigin=""></script>

  </head>

  <body>
    <div id="map" style="width: 600px; height: 400px;"></div>
  </body>

</html>
```

### CSS: the styles (colors, sizes, fonts) of the objects in the page
```
	html,
	body {
	  height: 100%;
	  margin: 0;
	}

	.leaflet-container {
	  height: 400px;
	  width: 600px;
	  max-width: 100%;
	  max-height: 100%;
	}
```

### JavaScript: the code to actually create and initialize the map
```
const map = L.map('map').setView([52.07941, 5.14144], 13);

const tiles = L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
  maxZoom: 19,
  attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
}).addTo(map);
```    

![](images/jsfiddle-leaflet1.png)

Now press the Run button in the upperleft hand corner. You should see a map - based on an OpenStreetMap baselayer, centered on Utrecht. It has no markers yet. You can pan and zoom. 

![](images/jsfiddle-leaflet3-firstmap.png)


### Add Markers

Add a single marker for Utrecht Central Station. You can find the coordinates in several ways. Using geojson.io is probably the easiest (click and inspect the geojson data). Using Google Maps also works: right mouse click on the right location and at the top of the context menu are the coordinates (latitude, longitude); if you click on that first menu option, the coordinates are copied to the clipboard, ready to be pasted elsewhere.

Add this line at the end of the code section in the script panel in JSFiddle:

```
const marker = L.marker([52.08973650799466, 5.1098320811113505]).addTo(map);
```
and press Run. You should see the marker on the map:

![](images/jsfiddle-marker-leaflet.png)

The geo-coordinates of the marker are easily recognized in this statement:  52.08973650799466 (latitude), 5.1098320811113505 (longitude)


To allow users to get some useful information about a marker, we can add a popup to it: a balloon text that opens when the marker is clicked. Add this line to the end of the JavaScript section:
```
marker.bindPopup(`<b>Utrecht Central Station<\/b><br>3511 CA Utrecht. Zie: <a href="https:\/\/www.ns.nl\/uitgelicht\/bestemmingen\/utrecht">Reisinformatie van NS<\/a>.`).openPopup();
```

And press Run again. When you now click on the marker, a popup appears:

![](images/jsfiddle-leaflet-markerpopup.png)

Leaflet supports GeoJSON. We can easily add markers for all point features in a GeoJSON document.

In order to add all Conclusion office locations, add this next snippet of code, again at the bottom of the JavaScript section. It will load the GeoJSON document with Conclusion offices from a GitHub repository. Once the document is retrieved, the contents is used to create a new GeoJSON layer that is then added to the map.

```
const geojsonUrl = "https://raw.githubusercontent.com/lucasjellema/visualization-netherlands-and-conclusion-locations/main/conclusion-offices-geojson.json"
// Fetch the GeoJSON file
fetch(geojsonUrl)
  .then(response => {
    // Check if the request was successful
    if (!response.ok) {
        throw new Error('Network response was not ok');
    }
    return response.json(); // Parse the response body as JSON
  })
  .then(geojsonData => {
    // Create a GeoJSON layer and add it to the map
    L.geoJSON(geojsonData, {
      // Optionally, specify a style or onEachFeature function here
      // For example, to set the style of polygons:
      style: function (feature) {
        return {color: feature.properties.color};
      },
      // To add popups to features:
      onEachFeature: function (feature, layer) {
        if (feature.properties && feature.properties.popupContent) {
          layer.bindPopup(feature.properties.popupContent);
        }
      }
    }).addTo(map);
  })
  .catch(error => {
    console.error('Error fetching the GeoJSON data:', error);
  });
```

Press Run. The map - when propertly zoomed out - should now show markers for all offices locations of the Conclusion ecosystem - inside The Netherlands. 

![](images/jsfiddle-leaflet-addgeojson.png)


### Bonus: Add WARPed Map

If you have created a WARPed map from a custom image - or you reuse someone else's handywork - you can include that layer easily in the Leaflet map. You need the url for the tiled map for this. For maps on MapWarper, this URL should be something like  https://mapwarper.net/maps/tile/xxx/{z}/{x}/{y}.png where xxx is the identification of the map.

For example to add the warped map for the plan of Galgenwaard Stadium (home of FC Utrecht) we can use URL:  https://mapwarper.net/maps/tile/80272/{z}/{x}/{y}.png

Add this next line of code - using your own URL - to the JavaScript section:

```
L.tileLayer('https://mapwarper.net/maps/tile/80272/{z}/{x}/{y}.png', {attribution: '&copy; <a href="https://www.https://mapwarper.net">mapwarper.net</a> '}).addTo(map);
```

Press Run.

Your custom warped map is now included:

![](images/jsfiddle-leaflet-custommap-tilelayer.png)