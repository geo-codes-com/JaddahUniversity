# Google Map APIO 

* HERE MAPS API enables GIS Developer to add thier display thier GIS data on top of HERE Maps, mapsjs-data.js enable you to display KML and GeoJSON on HERE Maps API.

* Open Visual Studio Code, Open Your Project Folder and Create a new File use google.html as file name.

* In google.html page press SHIFT + ! to generate the HTML code and change the tite to Google Map API.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> Google Map API </title>
</head>
<body>
    
</body>
</html>
```

* Inside head section include Google MAPS API library.

```html
<script src="https://maps.googleapis.com/maps/api/js?key=YOUR_KEY"></script>
```

* Inside the body section add h1 and div elements and use mapDiv as id for the div element.

```html
<h1> Google MAPS  </h1><hr />
<div id="mapDiv" style="height: 450px;"></div>
```

* Now open script tag and Add Google Map.

```html
    <script>
        var map = new google.maps.Map(
            document.getElementById('mapDiv'),
            {
                center: {lat: 15.1235, lng:32.5662},
                zoom: 9
            }
        );
    </script>
```


* Google Map API enable you to draw different map objects on top of the Google Maps such as points, lines, areas, or collections of objects The Maps JavaScript API calls these objects overlays. Overlays are tied to latitude/longitude coordinates, so they move when you drag or zoom the map

# Add Marker
* A marker identifies a location on a map. By default, a marker uses a standard image. Markers can display custom images, in which case they are usually referred to as "icons." Markers and icons are objects of type Marker. You can set a custom icon within the marker's constructor, or by calling setIcon() on the marker


* Write the following code to add Marker to Google Maps. 

```javascript
var marker = new google.maps.Marker({
	position: {lat: 21.29235, lng: 39.12365},
	title: 'Jeddah City'
});
marker.setMap(map);

```

* to change marker icon add icon property to you

```javascript

 var marker = new google.maps.Marker({
	position: {lat: 21.29235, lng: 39.12365},
	title: 'Jeddah City',
	icon: 'beachflag.png'
});


``` 

* Google map API provide InfoWindow to displays content (usually text or images) in a popup window above the map, at a given location. The info window has a content area and a tapered stem. The tip of the stem is attached to a specified location on the map. the following code will add InfoWindo to the marker

```javascript
const infowindow = new google.maps.InfoWindow({
	content: '<h3> Jeddah </h3><hr> Saudi Arabia ',
});
marker.addListener("click", () => {
	infowindow.open(map, marker);
});

```

# Polylines
* You can draw a line on google map by using polyline object.

```javascript

var lineCoords = [
	{lat: 21.123, lng: 39.123},
	{lat: 21.145, lng: 39.145},
	{lat: 21.165, lng: 39.165},
	{lat: 21.185, lng: 39.145}
];

const polyline = new google.maps.Polyline({
	path: lineCoords,
	strokeColor: "#FF0000",
	strokeOpacity: 1.0,
	strokeWeight: 2
});
polyline.setMap(map);


```

# Polygons
* You can draw a polygon on google map by using polygon object.


```javascript
 var coords = [
	{lat: 21.125, lng: 39.125},
	{lat: 21.145, lng: 39.145},
	{lat: 21.165, lng: 39.165},
	{lat: 21.185, lng: 39.145}
];

const polygon = new google.maps.Polygon({
	path: coords,
	strokeColor: "#FF0000",
	fillColor: "#00FF00",
	strokeOpacity: 1.0,
	strokeWeight: 2
});
polygon.setMap(map);

```

# Layers
* Layers are objects on the map that consist of one or more separate items, but are manipulated as a single unit. Layers generally reflect collections of objects that you add on top of the map to designate a common association. The Maps JavaScript API manages the presentation of objects within layers by rendering their constituent items into one object (typically a tile overlay) and displaying them as the map's viewport changes. Layers may also alter the presentation layer of the map itself, slightly altering the base tiles in a fashion consistent with the layer. 

* The Maps JavaScript API has several types of layers: 
* •	The Google Maps Data layer provides a container for arbitrary geospatial data. You can use the Data layer to store your custom data, or to display GeoJSON data on a Google map.
* •	The Heatmap layer renders geographic data using a Heatmap visualization.
* •	The KML layer renders KML and GeoRSS elements into a Maps JavaScript API tile overlay.
* •	The Traffic layer displays traffic conditions on the map. 
* •	The Transit layer displays the public transport network of your city on the map.
* •	The Bicycling layer object renders a layer of bike paths and/or bicycle-specific overlays into a common layer. This layer is returned by default within the DirectionsRenderer when requesting directions of travel mode BICYCLING.

```javascript

var transitLayer = new google.maps.TransitLayer();
transitLayer.setMap(map);


```

## GeoJSON Layer

* GeoJSON is a common standard for sharing geospatial data on the internet. It is lightweight and easily human-readable, making it ideal for sharing and collaborating. With the Data layer, you can add GeoJSON data to a Google map in just one line of code.

```javascript

map.data.loadGeoJson("states.geojson");


```

# Directions

* You can calculate directions (using a variety of methods of transportation) by using the DirectionsService object. This object communicates with the Google Maps API Directions Service which receives direction requests and returns an efficient path. Travel time is the primary factor which is optimized, but other factors such as distance, number of turns and many more may be taken into account. You may either handle these directions results yourself or use the DirectionsRenderer object to render these results.
* When specifying the origin or destination in a directions request, you can specify a query string (for example, "Chicago, IL" or "Darwin, NSW, Australia"), a LatLng value, or a google.maps.Place object.
* The Directions service can return multi-part directions using a series of waypoints. Directions are displayed as a polyline drawing the route on a map, or additionally as a series of textual description within a <div> element (for example, "Turn right onto the Williamsburg Bridge ramp").


```javascript

var directionsService = new google.maps.DirectionsService();
var directionsRenderer = new google.maps.DirectionsRenderer();
directionsRenderer.setMap(map);
var start = {lat: 21.29123, lng: 39.12123};
var end = {lat: 21.36123, lng: 39.828203};

var params = {
	origin: start,
	destination: end,
	travelMode: 'DRIVING'
};

directionsService.route(params, function(response, status) {
	if (status == 'OK') {
		directionsRenderer.setDirections(response);
	}
});


```