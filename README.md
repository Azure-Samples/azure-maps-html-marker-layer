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

Note that HTML markers will only render in a single "world" of the map. When zoomed out a lot, it is possible the map will show copies of the world. Most layers will 

## Getting started

Download the project and copy the `azure-maps-html-marker-layer` JavaScript file from the `dist` folder into your project. 

See the [documentation](https://github.com/Azure-Samples/azure-maps-html-marker-layer/tree/main/docs) for more details on a specific feature or take a look at one of the samples below.

## Samples

[Clustered Pie Chart HTML Markers](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Clustered%20Pie%20Chart%20HTML%20Markers)
<br/>[<img src="https://github.com/Azure-Samples/AzureMapsCodeSamples/raw/master/AzureMapsCodeSamples/SiteResources/screenshots/Clustered-Pie-Chart-HTML-Markers.jpg" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Clustered%20Pie%20Chart%20HTML%20Markers)

[HTML Marker Layer](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20Marker%20Layer)
<br/>[<img src="https://github.com/Azure-Samples/AzureMapsCodeSamples/raw/master/AzureMapsCodeSamples/SiteResources/screenshots/HTML-Marker-Layer.jpg" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20Marker%20Layer)

[HTML Marker layer and vector tiles](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20Marker%20layer%20and%20vector%20tiles)
<br/>[<img src="https://github.com/Azure-Samples/AzureMapsCodeSamples/raw/master/AzureMapsCodeSamples/SiteResources/screenshots/HTML-Marker-layer-and-vector-tiles.jpg" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20Marker%20layer%20and%20vector%20tiles)

[HTML marker layer events](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20marker%20layer%20events)
<br/>[<img src="https://github.com/Azure-Samples/AzureMapsCodeSamples/raw/master/AzureMapsCodeSamples/SiteResources/screenshots/HTML-marker-layer-events.gif" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=HTML%20marker%20layer%20events)

[Pie chart HTML marker options](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Pie%20chart%20HTML%20marker%20options)
<br/>[<img src="https://github.com/Azure-Samples/AzureMapsCodeSamples/raw/master/AzureMapsCodeSamples/SiteResources/screenshots/Pie-chart-HTML-marker-options.jpg" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Pie%20chart%20HTML%20marker%20options)

[Pie Chart HTML Markers](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Pie%20Chart%20HTML%20Markers)
<br/>[<img src="https://github.com/Azure-Samples/AzureMapsCodeSamples/raw/master/AzureMapsCodeSamples/SiteResources/screenshots/Pie-Chart-HTML-Markers.jpg" height="200px">](https://azuremapscodesamples.azurewebsites.net/index.html?sample=Pie%20Chart%20HTML%20Markers)

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
