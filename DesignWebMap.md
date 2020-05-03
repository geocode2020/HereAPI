# Create Web Map using HERE API for JavaScript
* Open Your IDE for Example Visual Studio Code, WebStorm or even simple IDE like Notepad++
* Create a New HTML Page and write the following code in your HTML page
```
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
```
<script src="https://js.api.here.com/v3/3.1/mapsjs-core.js"></script>
<script src="https://js.api.here.com/v3/3.1/mapsjs-service.js"></script>

```
* to make our web page suitable with different screen size add the following code in the head section.
```
<meta name="viewport" content="initial-scale=1.0, width=device-width" />
```
* Inside the body section add the following code
```
<div id="mapContainer" style="width: 800px; height: 600px;"></div>
```
* Now we are going to write script to add HERE maps in our HTML page
```
<script>

</script>

```
* inside the script tag write the following javascript code
```javascript
var platform = new H.service.Platform({
	'apikey':'PUT YOUR API KEY HERE'
});

```