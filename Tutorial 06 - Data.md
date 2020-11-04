# Data 

* HERE MAPS API enables GIS Developer to add thier display thier GIS data on top of HERE Maps, mapsjs-data.js enable you to display KML and GeoJSON on HERE Maps API.

* Open Visual Studio Code, Open Your Project Folder and Create a new File use data.html as file name.

* In data.html page press SHIFT + ! to generate the HTML code and change the tite to GIS DATA.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> GIS Data </title>
</head>
<body>
    
</body>
</html>
```

* Inside head section include HERE MAPS API libraries.

```html
<script src="https://js.api.here.com/v3/3.1/mapsjs-core.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-service.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-ui.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-mapevents.js"></script>
<link rel="stylesheet" href="https://js.api.here.com/v3/3.1/mapsjs-ui.css" />
```

* Inside the body section add h1 and div elements and use mapDiv as id for the div element.

```html
<h1> GeoJSON Data </h1><hr />
<div id="mapDiv" style="height: 450px;"></div>
```

* Now open script tag and Add Here Map, UI controls and Map Events.

```html
<script>
	var platform = new H.service.Platform({
		'apikey': 'YOUR API KEY'
	});
	var layers = platform.createDefaultLayers();
	var map = new H.Map(
		document.getElementById('mapDiv'),
		layers.vector.normal.map,
		{
			zoom: 6,
			center: {lat: 15.1234, lng: 32.1234}
		}
	);
	var ui = new H.ui.UI.createDefault(map, layers);
	var mapEvents = new H.mapevents.MapEvents(map);
	var behavior = new H.mapevents.Behavior(mapEvents);

</script>
```


* To display your data on HERE Maps API, we should include mapsjs-data.js library in Our web page. inside head section add the following instruction


```html
<script src="https://js.api.here.com/v3/3.1/mapsjs-data.js"></script>

```

* We want to display states layer on HERE Maps, and we will use POP_2018 for Symbology. let us to create symbols classes. 

```javascript
var class1 = {fillColor: 'rgba(255, 255, 255, 0.5)', lineWidth: 0.5, strokeColor: 'white'};
var class2 = {fillColor: 'rgba(200, 221, 240, 0.5)', lineWidth: 0.5, strokeColor: 'white'};
var class3 = {fillColor: 'rgba(115, 179, 216, 0.5)', lineWidth: 0.5, strokeColor: 'white'};
var class4 = {fillColor: 'rgba(40, 121, 185, 0.5)', lineWidth: 0.5, strokeColor: 'white'};
var class5 = {fillColor: 'rgba(8, 48, 107, 0.5)', lineWidth: 0.5, strokeColor: 'white'};
```

* We will create an object from Reader class to display the data.

```javascript

var states = new H.data.geojson.Reader('states.geojson',{
	disableLegacyMode: true,
	style: function(mapObject){
		if(mapObject.getData().POP_2018 <= 1045398){
			mapObject.setStyle(class1);
		}else if(mapObject.getData().POP_2018 <= 1527364){
			mapObject.setStyle(class2);
		}else if(mapObject.getData().POP_2018 <= 2150446){
			mapObject.setStyle(class3);
		}else if(mapObject.getData().POP_2018 <= 2503956){
			mapObject.setStyle(class4);
		}else if(mapObject.getData().POP_2018 <= 7993851){
			mapObject.setStyle(class5);
		}
	}
});
states.parse();
map.addLayer(states.getLayer());

``` 

* Now let us add event to show InfoBubble when usser click on features.

```javascript

states.getLayer().getProvider().addEventListener('tap', (evt) => {
	var coords = map.screenToGeo(
		evt.currentPointer.viewportX,
		evt.currentPointer.viewportY
	);
	var postion = {lat: coords.lat , lng: coords.lng};
	var dat = evt.target.getData();
	var bubble = new H.ui.InfoBubble(postion, {
		content: '<b>NAME:</b><br>' + dat['State_En'] + '<br>' +
		'<b>Population 2008 :</b><br>' + dat['POP_2008'] + '<br>' +
		'<b>Population 2008 :</b><br>' + dat['POP_2018'] + '<br>'+
		'<b>Area :</b><br>' + dat['Area'] + '<br>'
	});
	ui.addBubble(bubble);
},false);


```
