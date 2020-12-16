# HTML Marker Layer

The HTML marker layer lets you connect a data source to a layer that renders HTML markers for points, similar to how other rendering layers work within the map.

## HtmlMarkerLayer class

Implements: `atlas.layer.Layer`

Namespace: `atlas.layer`

A layer that renders point data from a data source as HTML elements on the map.

**Contstructor**

> `HtmlMarkerLayer(source?: string | atlas.source.Source, id?: string, options?: HtmlMarkerLayerOptions)`

**Methods**

| Name | Type | Description |
|------|------|-------------|
| `getId()` | `string` | Gets the id of the layer. |
| `getMap()` | `atlas.Map` | Gets the map that the layer is currently added to, or null. |
| `getOptions()` | `HtmlMarkerLayerOptions` | Gets the options of the Html Marker layer. |
| `getSource()` | `string` \| `atlas.source.Source` | Gets the source provided when creating the layer. |
| `setOptions(options: HtmlMarkerLayerOptions)` | | Sets the options of the Html marker layer. |
| `update()` | | Force the layer to refresh and update. |

**Events**

| Name | Type | Description |
|------|------|-------------|
| `click` | `TargetedEvent` | Fired when a pointing device is pressed and released at the same point on the map. |
| `contextmenu` | `TargetedEvent` | Fired when the right button of the mouse is clicked. |
| `dblclick` | `TargetedEvent` | Fired when a pointing device is clicked twice at the same point on the map. |
| `drag` | `TargetedEvent` | Fired repeatedly during a "drag to pan" interaction on the map, popup, or HTML marker. |
| `dragstart` | `TargetedEvent` | Fired when a "drag to pan" interaction starts on the map, popup, or HTML marker. |
| `dragend` | `TargetedEvent` | Fired when a "drag to pan" interaction ends on the map, popup, or HTML marker. |
| `keydown` | `TargetedEvent` | Fired when a key is pressed down. |
| `keypress` | `TargetedEvent` | Fired when a key that produces a typable character (an ANSI key) is pressed. |
| `keyup` | `TargetedEvent` | Fired when a key is released. |
| `mousedown` | `TargetedEvent` | Fired when a pointing device is pressed within the map or when on top of an element. |
| `mouseenter` | `TargetedEvent` | Fired when a pointing device is initially moved over the map or an element. |
| `mouseleave` | `TargetedEvent` | Fired when a pointing device is moved out the map or an element. |
| `mousemove` | `TargetedEvent` | Fired when a pointing device is moved within the map or an element. |
| `mouseout` | `TargetedEvent` | Fired when a point device leaves the map's canvas our leaves an element. |
| `mouseover` | `TargetedEvent` | Fired when a pointing device is moved over the map or an element. |
| `mouseup` | `TargetedEvent` | Fired when a pointing device is released within the map or when on top of an element. |

**Usage**

```javascript
//Create a HTML marker layer and connect a data source to it.
var markerLayer = new atlas.layer.HtmlMarkerLayer(datasource, null, {
    //Specify a callback to create custom markers.
    markerCallback: function (id, position, properties) {

        //Check to see if marker is a cluster.
        if (properties.cluster) {
            //Cluster markers will be purple in color and display the abbreviated count of points in the cluster.
            var cluster = new atlas.HtmlMarker({
                position: position,
                color: 'purple',
                text: properties.point_count_abbreviated
            });
    
            return cluster;
        } 

        //Individual markers will be red.
        return new atlas.HtmlMarker({
            position: position,
            color: 'red'
        });
    }
});

//Optionally add events.
 map.events.add('click', markerLayer, markerClicked); 

//Add the marker layer to the map.
map.layers.add(markerLayer);

//Sample event handler. The event argument is a TargetedEvent object with the target being an HTML marker.
function markerClicked(e) {
    var marker = e.target;

    if (marker.properties.cluster) {
        //Marker represents a cluster.
    } else {
        //Marker represents an individual point.
    }
}
```

### HtmlMarkerLayerOptions interface

Options for the HTML Marker Layer class.

**Properties** 

| Name | Type | Description |
|------|------|-------------|
| `filter` | `atlas.Expression` | An expression specifying conditions on source features. Only features that match the filter are displayed. Default: `['==', ['geometry-type'], 'Point']` |
| `markerCallback` | `(id: string, position: atlas.data.Position, properties: any) => atlas.HtmlMarker` | A callback function that generates a HtmlMarker for a given data point. The `id` and `properties` values will be added to the marker as properties within the layer after being created by this callback function. |
| `maxZoom` | `number` | An integer specifying the maximum zoom level to render the layer at. This value is exclusive, i.e. the layer will be visible at `maxZoom > zoom >= minZoom`. Default `24`. |
| `minZoom` | `number` | An integer specifying the minimum zoom level to render the layer at. This value is inclusive, i.e. the layer will be visible at `maxZoom > zoom >= minZoom`. Default: `0`. |
| `source` | `string` \| `atlas.source.Source` | The id or instance of a data source which the layer will render. |
| `sourceLayer` | `string` | Required when the source of the layer is a VectorTileSource. A vector source can have multiple layers within it, this identifies which one to render in this layer. |
| `updateWhileMoving` | `boolean` | Specifies if the layer should update while the map is moving. When set to false, rendering in the map view will occur after the map has finished moving. New data is not rendered until the moveend event fires. When set to true, the layer will constantly re-render as the map is moving which ensures new data is always rendered right away, but may reduce overall performance. Default: `false` |
| `visible` | `boolean` | Specifies if the layer is visible or not. Default `true`. |