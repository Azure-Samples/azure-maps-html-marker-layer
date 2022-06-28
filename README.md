---
page_type: sample
description: An Azure Maps Web SDK module that provides a layer that renders point data from a data source as HTML elements on the map.
languages:
- javascript
- typescript
products:
- azure
- azure-maps
---

# Azure Maps HTML Marker Layer module

An Azure Maps Web SDK module that provides a layer that renders point data from a data source as HTML elements on the map. This layer works with both GeoJSON based and Vector tile based data sources. 

Only Point features will be rendered and not any points from other feature types.

Note that this is an **experimental library** that attempts to achieve the following:

- Power the creation of HTML markers with a data sources, and thus unlock the benifits of using data sources, usch as clustering, for HTML markers.
- Support larger data sets by dynamically adding/removing items based on the map view, thus increasing potential performance of using HTML markers. 
- Add a way to create fully interactive pie charts as markers on the map.
- Create consistency with how other things are rendered with layers in Azure Maps.

## Getting started

Download the project and copy the `azure-maps-html-marker-layer` JavaScript file from the `dist` folder into your project. 

See the [documentation](https://github.com/Azure-Samples/azure-maps-html-marker-layer/tree/main/docs) for more details on a specific feature or take a look at one of the samples below.

## Samples

[Clustered Pie Chart HTML Markers](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Clustered%20Pie%20Chart%20HTML%20Markers)
<br/>[<img src="https://raw.githubusercontent.com/Azure-Samples/AzureMapsCodeSamples/master/Samples/HTML%20Markers/Clustered%20Pie%20Chart%20HTML%20Markers/screenshot.jpg" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Clustered%20Pie%20Chart%20HTML%20Markers)

[HTML Marker Layer](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20Marker%20Layer)
<br/>[<img src="https://raw.githubusercontent.com/Azure-Samples/AzureMapsCodeSamples/master/Samples/HTML%20Markers/HTML%20Marker%20Layer/screenshot.jpg" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20Marker%20Layer)

[HTML Marker layer and vector tiles](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20Marker%20layer%20and%20vector%20tiles)
<br/>[<img src="https://raw.githubusercontent.com/Azure-Samples/AzureMapsCodeSamples/master/Samples/HTML%20Markers/HTML%20Marker%20layer%20and%20vector%20tiles/screenshot.jpg" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20Marker%20layer%20and%20vector%20tiles)

[HTML marker layer events](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20marker%20layer%20events)
<br/>[<img src="https://github.com/Azure-Samples/AzureMapsCodeSamples/raw/master/Samples/HTML%20Markers/HTML%20Marker%20events/screenshot.gif" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20marker%20layer%20events)

[Pie chart HTML marker options](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Pie%20chart%20HTML%20marker%20options)
<br/>[<img src="https://raw.githubusercontent.com/Azure-Samples/AzureMapsCodeSamples/master/Samples/HTML%20Markers/Pie%20chart%20HTML%20marker%20options/screenshot.jpg" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Pie%20chart%20HTML%20marker%20options)

[Pie Chart HTML Markers](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Pie%20Chart%20HTML%20Markers)
<br/>[<img src="https://raw.githubusercontent.com/Azure-Samples/AzureMapsCodeSamples/master/Samples/HTML%20Markers/Pie%20Chart%20HTML%20Markers/screenshot.jpg" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Pie%20Chart%20HTML%20Markers)

## Alternative solution

If you simply want to be able to cluster HTML Markers, you can leverage a library like [Supercluster](https://github.com/mapbox/supercluster) to achieve this in Azure Maps. Here is an example:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <title></title>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no" />

    <!-- Add references to the Atlas Map control JavaScript and CSS files. -->
    <link href="https://atlas.microsoft.com/sdk/javascript/mapcontrol/2/atlas.min.css" rel="stylesheet" />
    <script src="https://atlas.microsoft.com/sdk/javascript/mapcontrol/2/atlas.min.js"></script>

    <!-- Add a reference to the Supercluster library -->
    <script src="https://unpkg.com/supercluster@7.1.2/dist/supercluster.min.js"></script>

    <script>
        var map, superCluster;

        var earthquakeFeed = "https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_month.geojson";

        function GetMap() {
            //Initialize a map instance.
            map = new atlas.Map('myMap', {
                view: 'Auto',

                authOptions: {
                    authType: 'subscriptionKey',
                    subscriptionKey: '<Your Azure Maps Key>'
                }
            });

            //Wait until the map resources are ready.
            map.events.add('ready', function () {

                //Create a cluster instance.
                superCluster = new Supercluster({
                    radius: 35,
                    maxZoom: 18
                });

                //Add a map move event to re-render the clusters as the map moves. 
                //For added performance, use 'moveend' event instead. Markers will snap into view when the map is done moving rather than constantly being rendered as the map moves.
                map.events.add('move', render);

                //Load data
                fetch(earthquakeFeed).then(r => r.json()).then(r => {
                    //Load data into the super cluster.
                    superCluster.load(r.features);

                    //Render initial state.
                    render();
                });
            });
        }

        function render() {
            //Get the map's camera information. 
            var cam = map.getCamera();

            //Get clusters for the current map's bounding box, and rounding zoom level (super cluster only supports integer zoom levels).
            var points = superCluster.getClusters(cam.bounds, Math.round(cam.zoom));

            //Loop through the clustered points and create HTML markers.
            var markers = [];
            points.forEach(p => {
                var m = new atlas.HtmlMarker({
                    position: p.geometry.coordinates,
                    text: (p.properties.cluster) ? p.properties.point_count_abbreviated : '',
                    color: (p.properties.cluster) ? 'red' : 'DodgerBlue'
                });

                //Copy over id's and properties.
                m.id = p.id;
                m.properties = p.properties;
                
                markers.push(m);
            });

            //Clear the markers that are on the map and add the new set of markers.
            map.markers.clear();
            map.markers.add(markers);
        }
    </script>
    <style>
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
        }

        #myMap {
            width: 100%;
            height: 100%;
        }
    </style>
</head>
<body onload="GetMap()">
    <div id="myMap"></div>
</body>
</html>
```

## Related Projects

* [Azure Maps Web SDK Open modules](https://github.com/microsoft/Maps/blob/master/AzureMaps.md#open-web-sdk-modules) - A collection of open source modules that extend the Azure Maps Web SDK.
* [Azure Maps Web SDK Samples](https://github.com/Azure-Samples/AzureMapsCodeSamples)
* [Azure Maps Gov Cloud Web SDK Samples](https://github.com/Azure-Samples/AzureMapsGovCloudCodeSamples)
* [Azure Maps & Azure Active Directory Samples](https://github.com/Azure-Samples/Azure-Maps-AzureAD-Samples)
* [List of open-source Azure Maps projects](https://github.com/microsoft/Maps/blob/master/AzureMaps.md)

## Additional Resources

* [Azure Maps (main site)](https://azure.com/maps)
* [Azure Maps Documentation](https://docs.microsoft.com/azure/azure-maps/index)
* [Azure Maps Blog](https://azure.microsoft.com/blog/topics/azure-maps/)
* [Microsoft Q&A](https://docs.microsoft.com/answers/topics/azure-maps.html)
* [Azure Maps feedback](https://feedback.azure.com/forums/909172-azure-maps)

## Contributing

We welcome contributions. Feel free to submit code samples, file issues and pull requests on the repo and we'll address them as we can. 
Learn more about how you can help on our [Contribution Rules & Guidelines](https://github.com/Azure-Samples/azure-maps-html-marker-layer/blob/main/CONTRIBUTING.md). 

You can reach out to us anytime with questions and suggestions using our communities below:
* [Microsoft Q&A](https://docs.microsoft.com/answers/topics/azure-maps.html)
* [Azure Maps feedback](https://feedback.azure.com/forums/909172-azure-maps)

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). 
For more information, see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or 
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## License

MIT
 
See [License](https://github.com/Azure-Samples/azure-maps-html-marker-layer/blob/main/LICENSE.md) for full license text.
