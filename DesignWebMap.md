# Create Web Map using HERE API for JavaScript
* Open Your IDE for Example Visual Studio Code, WebStorm or even simple IDE like Notepad++
* Create a New HTML Page and write the following code in your HTML page
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

</body>
</html>
```
* Now let us to include HERE MAP API for JavaScript in Our HTML Page, inside head tag add the following code.
```html
<script src="https://js.api.here.com/v3/3.1/mapsjs-core.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-service.js"></script>

```
* to make our web page suitable with different screen size add the following code in the head section.
```html
<meta name="viewport" content="initial-scale=1.0, width=device-width" />
```
* Inside the body section add the following code
```html
<div id="mapContainer" style="width: 800px; height: 600px;"></div>
```
* Now we are going to create script to add HERE maps, under the <div> tag add the following code
```html
<script>

</script>

```
* inside the script tag write the following javascript code
```javascript
var platform = new H.service.Platform({
        'apikey':'PUT YOUR API KER HERE'
    });
    var layers = platform.createDefaultLayers();
    var map = new H.Map(
        document.getElementById('mapContainer'),
        layers.vector.normal.map,
        {
            zoom: 9,
            center:{lat:21.422542, lng:39.826230}
        }
    );
```
* following is full code
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="initial-scale=1.0, width=device-width" />
    <title>Title</title>
    <script src="https://js.api.here.com/v3/3.1/mapsjs-core.js"></script>
    <script src="https://js.api.here.com/v3/3.1/mapsjs-service.js"></script>
</head>
<body>
<div id="mapContainer" style="width: 800px; height: 600px;"></div>
<script>
    var platform = new H.service.Platform({
        'apikey':'PUT YOUR API KER HERE'
    });
    var layers = platform.createDefaultLayers();
    var map = new H.Map(
        document.getElementById('mapContainer'),
        layers.vector.normal.map,
        {
            zoom: 9,
            center:{lat:21.422542, lng:39.826230}
        }
    );
</script>
</body>
</html>
```
* The following screenshot shows the output
![Alt text](/images/screen1.png)

## Add UI Controls
* In the head section include the following javascript and css modules
```html
    <script src="https://js.api.here.com/v3/3.1/mapsjs-ui.js"></script>
    <link rel="stylesheet" href="https://js.api.here.com/v3/3.1/mapsjs-ui.css" />
```
* inside the script tag add the following code
```javascript
var ui = new H.ui.UI.createDefault(map,layers);
```
* The following screenshot shows the output
![Alt text](/images/screen2.png)

* We can change the position of UI control, for example add the following code to change the position of MapSettings UI control
```javascript
ui.getControl('mapsettings').setAlignment('top-left');
```

### Add InfoBubble
* Write the following code to add InfoBubble inside the script tag
```javascript
var bubble = new H.ui.InfoBubble(
    {lat:21.422542,lng:39.826230},
    {content:'<b>MAKKA</b>'}
);
ui.addBubble(bubble);

```
* The following Screenshot shows the InfoBubble
![Alt text](/images/screen4.png)

## Map Events and Interaction
* to Add Map Events and Interactions, in the head section include the following modules
```html
<script src="https://js.api.here.com/v3/3.1/mapsjs-mapevents.js"></script>
```
* write the following code inside the script tag
```javascript
var ui = new H.ui.UI.createDefault(map,layers);
ui.getControl('mapsettings').setAlignment('top-left');
var mapEvents = new H.mapevents.MapEvents(map);
var behavior = new H.mapevents.Behavior(mapEvents);

```
* Write the following code to add Onclick Events, the event handler shows click location coordinates in InfoBubble
```javascript
map.addEventListener('tap',function(evt){
    var coords = map.screenToGeo(
        evt.currentPointer.viewportX,
        evt.currentPointer.viewportY
    );
    let bubble = new H.ui.InfoBubble(
        {lat: coords.lat , lng: coords.lng},
        {content: coords.lat + ', ' + coords.lng}
    );
    ui.addBubble(bubble);
});

```

* The following figure shows the output
![Alt text](/images/screen5.png)

