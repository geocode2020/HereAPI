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
* following is output of our code
![Alt text](/images/screen1.png)