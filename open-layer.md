# Index

- [Key concept](#Key-concept)
- [View](#View)
- [Layer](#Layer)
- [Overlay](#Overlay)
- [Interaction](#Interaction)





## Key concept

- **View**: represents a simple 2D view of the map. This is the object to act upon to change the center, resolution, and rotation of the map.
- **Layers**: base class from which all layer types are derived
- **Overlay**: an element to be displayed over the map and attached to a single map location.
- **Interaction**: allow to interact with the map thanks user actions that change the state of the map (similar to controls, but are not associated with a DOM element)
- **Controls**: allow to interact with the map thanks to ui widget

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

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## View
- Defines the area where the map will initially displayed, the zoom, the center ecc.. </br>
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

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Layer
- A layer provides access to source of geospatial data and then we can visualize them (roster data and vector data)
  - roster data: refers to digital image (es: satellite images). This type of data is excellent for visualization of continuos data like elevation or temperature
  - vector data: refers to geometric shapes such as points, lines and polygons

**Hierarchy**
- import BaseLayer from 'ol/layer/Base';
  - import LayerGroup from 'ol/layer/Group';
    - import BaseLayer from 'ol/layer/Base';
  - import Layer from 'ol/layer/Layer';
    - import BaseImageLayer from 'ol/layer/BaseImage';
    - import BaseTileLayer from 'ol/layer/BaseTile';
    - import BaseVectorLayer from 'ol/layer/BaseVector';


<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Overlay
An element to be displayed over the map and attached to a single map location </br>
A overlay is used to visualization of geospatial data in a specific location of the map
```html
<div id='popup-container'>
  <div id='popup-coordinates'></div>
</div>
<div id='js-map'></div>
```
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


<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Interaction
- Define interaction </br>
- Define condition (optional) </br>
- Define fires event (it's the event that occurs when the interaction is finished) </br>

#### active keyboard
```javascript
function init() {
  const map = new Map({
    keyboardEventTarget: document
  });
}
```

#### Interaction
Superclass for interactions class </br>
```javascript
import { ... } from 'ol/interaction';
```

#### DragRotate (it's an example)
```javascript
const dragRotateInteraction = new DragRotate({
  condition: ol.events.condition.altKeyOnly ;
})

map.addInteraction(dragRotateInteraction)
```

#### Draw (it's an example)
```javascript
const drawInteraction = new Draw({
  condition: ol.events.condition.altKeyOnly ;
})

map.addInteraction(dragRotateInteraction)

drawInteraction.on('drawend', function(e){
  let parser = new GeoJSON();
  // let drawnFeatures = parser.writeFeatures([e.feature]);
  let drawnFeatures = parser.writeFeaturesObject([e.feature]);
  console.log(drawnFeatures);
})
```

<!------------------------------------------------------------------------------------------------------------------>
<!-----------------------------------------------> </br><hr></br> <!----------------------------------------------->
<!------------------------------------------------------------------------------------------------------------------>

## Controls

#### add controls (besides the default controls)
```javascript
function init() {
  const fullScreenControl = new FullScreen();
  const mousePositionControl = new MousePosition();

  const map = new Map({
    controls: ol.control.defaults().extend([
      fullScreenControl,
       mousePositionControl
    ])
  });
}
```