# Index

- [Map elements](#Map-elements)
- [View](#View)
- [Layer](#Layer)
- [Overlay](#Overlay)


- [Roster data](#Roster-data)


## Map Elements

- **View**: defines the area where the map will initially displayed, the zoom, the center
- **Layers**: image that you want to see in your map
- **Target Container**: id of the div element to inject the map

```javascript
import { Map, View } from "ol";
import TileLayer from "ol/layer/Tile";
import OSM from "ol/source/OSM";

window.onload = init;

function init() {
  const map = new Map({
    view: new View({
      center: [0, 0],
      zoom: 2,
    }),
    layers: [
      new TileLayer({
        source: new OSM(),
      }),
    ],
    target: "js-map",
  });
}
```

## View
```javascript
var view = new View({
  center: [0, 0],
  zoom: 2,
  minZoom: 1,
  maxZoom: 6,
  rotation: 3,
  ...
});
```

## Layer
A layer provides access to source of geospatial data and then we can visualize them (roster data and vector data)
- roster data: refers to digital image (es: satellite images). This type of data is excellent for visualization of continuos data like elevation or temperature
- vector data: refers to geometric shapes such as points, lines and polygons

**Hierarchy**
- ol/layer/Base~BaseLayer
  - ol/layer/Group~LayerGroup
    - ol/layer/Base~BaseLayer
  - ol/layer/Layer~Layer
    - ol/layer/BaseImage~BaseImageLayer (Server-rendered images that are available for arbitrary extents and resolutions)
    - ol/layer/BaseTile~BaseTileLayer (For layer sources that provide pre-rendered, tiled images in grids that are organized by zoom levels for specific resolutions)
    - ol/layer/BaseVector~BaseVectorLayer (Vector data that is rendered client-side)

- import BaseLayer from 'ol/layer/Base';
  - import LayerGroup from 'ol/layer/Group';
    - import BaseLayer from 'ol/layer/Base';
  - import Layer from 'ol/layer/Layer';
    - import BaseImageLayer from 'ol/layer/BaseImage';
    - import BaseTileLayer from 'ol/layer/BaseTile';
    - import BaseVectorLayer from 'ol/layer/BaseVector';


## Overlay
A overlay is used to visualization of geospatial data in a specific location of the map

```javascript
const popupContainerElement = document.getElementById("popup-coordinates")
const popup = new Overlay({
  element: popupContainerElement,
  position: 'center-left'
});

map.addOverlay(popup);

map.on("click", function(e){
  const clickedCoordinate = e.coordinate;
  popup.setPosition(undefined); //remove popup
  popup.setPosition(clickedCoordinate);
  clickedCoordinate.innerHTML = clickedCoordinate;
})
```

## Roster data
- Tile: if you zoom in, provide you more details
