# Pie Chart Marker

The `PieChartMarker` class makes it easy to create interactive pie charts are markers on the map.

## PieChartMarker class

Extends: `atlas.HtmlMarker`

Namespace: `atlas`

A class for creating Pie Charts as HTML Markers on a map. 

**Contstructor**

> `PieChartMarker(options?: PieChartMarkerOptions)`

**Methods** 

| Name | Type | Description |
|------|------|-------------|
| `getOptions()` | `PieChartMarkerOptions` | Gets the options of the pie chart marker. |
| `getSlicePercentage(idx: number)` | `` | Gets the percentage value of a slice of the pie based on it's index. |
| `getSliceValue(idx: number)` | `number` | Gets the value of a slice of the pie based on it's index. |
| `getTotalValue()` | `number` | Gets the total value of all slices summed togehter. |
| `setOptions(options: PieChartMarkerOptions)` |  | Sets the options of the pie chart marker. |
| `togglePopup()` | | Toggles the popup attached to the marker. |

**Usage**

```javascript
//Create the pie chart marker and add it to the map.
var marker = new atlas.PieChartMarker({
    position: [0, 0],
    values: [15, 80, 30, 10, 5],
    tooltipCallback: tooltipCallback
});

map.markers.add(marker);

//A callback function for generating the tooltip text to display when a slice of the pie has focus.
function tooltipCallback(marker, sliceIdx) {
    return `${marker.getSlicePercentage(sliceIdx)}%`;
}
```

Optionally, customize the text that appears in the center of the pie chart. This text is rendered inside of a SVG `text` tag.

### PieChartMarkerOptions interface

Options for styling a `PieChartMarker`.

**Properties** 

| Name | Type | Description |
|------|------|-------------|
| `anchor` | `"center"` \| `"top"` \| `"bottom"` \| `"left"` \| `"right"` \| `"top-left"` \| `"top-right"` \| `"bottom-left"` \| `"bottom-right"` | Indicates the marker's location relative to its position on the map. Default: `"center"`|
| `colors` | `string[]` | The colors of each category in the pie chart. Should have a length >= to largest values array in data set. If there are more values than colors specified, random colors will be generated for the new values. Default: `['#d7191c','#fdae61','#ffffbf','#abdda4','#2b83ba']` |
| `draggable` | `boolean` | Indicates if the user can drag the position of the marker using the mouse or touch controls. Default: `false` |
| `fillColor` | `string` | The color to fill the center of a pie chart when inner radius is greated than 0. Default: `transparent` |
| `innerRadius` | `number` | The inner radius of the pie chart in pixels. Default: `0` |
| `pixelOffset` | `atlas.Pixel` | An offset in pixels to move the popup relative to the markers center. Negatives indicate left and up. Default: `[0, 0]` |
| `popup` | `atlas.Popup` | A popup that is attached to the marker. |
| `position` | `atlas.data.Position` | The position of the marker. Default: `[0, 0]` |
| `radius` | `number` | The radius of a pie chart in pixels. Default: `40` |
| `strokeColor` | `string` | The color of the stroke line. Default: `#666666` |
| `strokeWidth` | `number` | The stroke width in pixels. Default: `0` |
| `text` | `string` | Text to display at the center of the pie chart. |
| `textClassName` | `string` | A CSS class name to append to the `text` tag of the SVG pie chart. |
| `tooltipCallback` | `(marker: PieChartMarker, sliceIdx: number) => string` | A callback handler which defines the value of a tooltip for a slice of the pie. |
| `values` | `number[]` | The value of each slice of the pie. |
| `visible` | `boolean` | Specifies if the marker is visible or not. Default: `true` |
