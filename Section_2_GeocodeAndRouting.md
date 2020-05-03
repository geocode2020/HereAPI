# Geocode, Routing and HERE Places APIs
* Create a New HTML page geocode.html and inside html page write the following code
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
	<meta name="viewport" content="initial-scale=1.0, width=device-width" />
    <title>Title</title>
</head>
<body>

</body>
</html>

```
* in the head section add include all necessary HERE MAPS APIs
```html
    <script src="https://js.api.here.com/v3/3.1/mapsjs-core.js"></script>
    <script src="https://js.api.here.com/v3/3.1/mapsjs-service.js"></script>
    <script src="https://js.api.here.com/v3/3.1/mapsjs-ui.js"></script>
    <link rel="stylesheet" href="https://js.api.here.com/v3/3.1/mapsjs-ui.css" />
    <script src="https://js.api.here.com/v3/3.1/mapsjs-mapevents.js"></script>

```
* in body section add the following div element
```html
<div id="mapContainer" style="width: 800px; height: 600px;"></div>
```
* now add script tag under the div tag
```html
<script>

</script>
```
* inside the script tag add the following code
```javascript
    var platform = new H.service.Platform({
        'apikey':'PUT YOUR API KEY HERE'
    });
    var layers = platform.createDefaultLayers();
    var map = new H.Map(
        document.getElementById('mapContainer'),
        layers.vector.normal.map,
        {
            zoom: 16,
            center:{lat:21.422542, lng:39.826230}
        }
    );
    var ui = new H.ui.UI.createDefault(map,layers);
    ui.getControl('mapsettings').setAlignment('top-left');
    var mapEvents = new H.mapevents.MapEvents(map);
    var behavior = new H.mapevents.Behavior(mapEvents);
    var service = platform.getSearchService();
    service.geocode({q:'Al Haram, Mecca 24231, Saudi Arabia'},(result)=>{
        result.items.forEach((item)=>{
            map.addObject(new H.map.Marker(item.position));
        });
    },alert);

```
* Following is the output
![Alt text](/img/screen8.png)

* following is reverse operation of geocode
```javascript
var service = platform.getSearchService();
service.reverseGeocode({at:'21.422542,39.826230'},(result)=>{
    result.items.forEach((item)=>{
        ui.addBubble(new H.ui.InfoBubble(item.position, {
            content: item.address.label
        }));
    });
},alert);

```
## Routing
* add the following code to find the best rout between two waypoints
```javascript
var router = platform.getRoutingService();
// specify routing parameters
var routingParams = {
    'mode':'fastest;car',
    'waypoint0': 'geo!21.422542,39.826230',
    'waypoint1': 'geo!21.423122,39.856095',
    'representation':'display'
};
// calculate the best route
router.calculateRoute(routingParams, function(result){
    var route, routeShape, startPoint, endPoint, lineString;
    if(result.response.route){
        route = result.response.route[0];
        routeShape = route.shape;
        lineString = new H.geo.LineString();
        routeShape.forEach(function(point){
            var parts = point.split(',');
            lineString.pushLatLngAlt(parts[0],parts[1]);
        });
        startPoint = route.waypoint[0].mappedPosition;
        endPoint = route.waypoint[1].mappedPosition;
        var routeLine = new H.map.Polyline(lineString,{
            style:{strokeColor:'blue', lineWidth:3}
        });
        var startMarker = new H.map.Marker({
            lat: startPoint.latitude,
            lng: startPoint.longitude
        });
        var endMarker = new H.map.Marker({
            lat: endPoint.latitude,
            lng: endPoint.longitude
        });
        map.addObjects([routeLine, startMarker, endMarker]);
        map.getViewModel().setLookAtData({bounds: routeLine.getBoundingBox()});
    }
},function(error){
    alert(error.message);
});
```
* following is the output
![Alt text](/img/screen9.png)

## HERE Places API
* add the following code to find all hospitals and health service facility in Mecca
```javascript
var placesService = platform.getPlacesService();

/* Go to the following link to show all places categories
https://places.ls.hereapi.com/places/v1/categories/places?at=21.422542,39.826230&apiKey={YOUR API KEY}
*/

parameters = {'at':'21.422542,39.826230','cat':'hospital-health-care-facility'};

placesService.explore(parameters,
    function (results) {
        var restGroup = new H.map.Group();
        var items = results.results.items;
        items.forEach(function(item){
            let restPosition = {lat: item.position[0],lng:item.position[1]};
            let data = item.title;
            let restIcon = new H.map.Icon('img/h.png');
            let restMarker = new H.map.Marker(restPosition,{icon:restIcon});
            restMarker.setData(data);
            restGroup.addObject(restMarker);
        });
        map.addObject(restGroup);
    }, function (error) {
        alert(error);
});

map.addEventListener('tap', function (evt) {
    if (evt.target instanceof H.map.Marker) {
        var bubble =  new H.ui.InfoBubble(evt.target.getGeometry(), {
            content: evt.target.getData()
        });
        ui.addBubble(bubble);
    }
}, false);

```

* Following is output of the above code

![Alt text](/img/screen10.png)

