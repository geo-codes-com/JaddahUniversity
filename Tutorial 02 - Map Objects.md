# Map Objects
* Here Map API comes with an Object Model, which provide a way to add and organize objects on the map, three main types of objects are markers, geoshape and overlays, let us to see how to add objects to our map.

* Open Visual Studio Code and press SHIFT + ! to generate the basic HTML code, change the title to Map Objects


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Map Objects</title>
</head>
<body>
    
</body>
</html>
```

* Inside the head section include HERE Map APIs (mapsjs-core.js, mapsjs-service.js, mapsjs-ui.js, mapsjs-mapevents.js and mapsjs-ui.css)

```javascript 
<script src="https://js.api.here.com/v3/3.1/mapsjs-core.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-service.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-ui.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-mapevents.js"></script>
<link rel="stylesheet" href="https://js.api.here.com/v3/3.1/mapsjs-ui.css" />
```

* Inside the body section add div element and set the id attribute to mapDiv.

```html
<div id="mapDiv" style="height: 600px;"></div>
```

* After the div element open script tag and add the following code to add here map to your web page.

```html
<script>
	var platform = new H.service.Platform({
		'apikey': 'YOUR API KEY'
	});
	var layersObject = platform.createDefaultLayers();
	var mapObject = new H.Map(
		document.getElementById('mapDiv'),
		layersObject.vector.normal.map,
		{
			zoom: 9,
			center: {lat: 15.1234, lng: 32.1234},
		}
	);
	var ui = new H.ui.UI.createDefault(mapObject, layersObject);
	var mapEvents = new H.mapevents.MapEvents(map);
	var behavior = new H.mapevents.Behavior(mapEvents);
</script>
```

## Add Marker

* Here Provides two types of Marker and DomMarker, write the following code to add a Marker.


```javascript
var markerPosition = {lat: 15.1234, lng: 32.1234};
var markerIcon = new H.map.Icon('marker.png', {size:{w:20, h:20}});
var markerObject = new H.map.Marker(markerPosition, {icon: markerIcon});
mapObject.addObject(markerObject);
```

# Geo Shapes

## Add Polyline
* to add polyline write the following code 


```javascript
var coordinates = [
	{lat: 15, lng: 32},
	{lat: 17, lng: 32},
	{lat: 16, lng: 34}
];
var lineString = new H.geo.LineString();
coordinates.forEach(function(coords){
	lineString.pushPoint(coords);
});
var polylineObject = new H.map.Polyline(lineString);
mapObject.addObject(polylineObject);
```
## Add Circle
* Add the following code to add circle

```javascript
var circleObject = new H.map.Circle({lat: 15.1234, lng: 32.1234}, 80000);
mapObject.addObject(circleObject);
```

## Add Rect
* Add the following code to create a rectangle with custome style.

```javascript
var customStyle = {
  strokeColor: 'blue',
  fillColor: 'rgba(200, 100, 50, 0.5)',
  lineWidth: 8,
  lineCap: 'square',
  lineJoin: 'bevel'
};
var rectObject = new H.map.Rect(new H.geo.Rect(53.5, 12.5, 51.5, 14.5),{ style: customStyle });
mapObject.addObject(rectObject);
```

