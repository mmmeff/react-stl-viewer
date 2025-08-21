# react-19-stl-viewer

React 19 component for visualizing STLs using Three.js.

<p align="center">
    <img src="docs/demo.gif">
</p>

## Install

```shell
npm install --save react-19-stl-viewer
```

or

```shell
yarn add react-19-stl-viewer
```

## Usage

```js
import React from 'react';
import ReactDOM from 'react-dom';
import {StlViewer} from "react-19-stl-viewer";

const url = "https://storage.googleapis.com/ucloud-v3/ccab50f18fb14c91ccca300a.stl"

const style = {
    top: 0,
    left: 0,
    width: '100vw',
    height: '100vh',
}

function App() {
    return (
        <StlViewer
            style={style}
            orbitControls
            shadows
            url={url}
        />
    );
}

ReactDOM.render(<App/>, document.getElementById('root'));
```


## Props

| Prop              |              Type              | Required |                            Notes                            |
|-------------------|:------------------------------:|:--------:|:-----------------------------------------------------------:|
| `url`             |            `string`            |  `true`  |                     url of the Stl file                     |
| `cameraProps`     |         `CameraProps`          | `false`  |                camera properties, see below                 |
| `modelProps`      |          `ModelProps`          | `false`  |               3d model properties, see below                |
| `floorProps`      |          `FloorProps`          | `false`  |                 floor properties, see below                 |
| `shadows`         |           `boolean`            | `false`  |     render shadows projected by the model on the ground     |
| `showAxes`        |           `boolean`            | `false`  |                       show x y z axis                       |
| `orbitControls`   |           `boolean`            | `false`  |                enable camera orbit controls                 |
| `extraHeaders`    |    `Record<string, string>`    | `false`  |          custom headers for making the http query           |
| `onFinishLoading` | `(ev: ModelDimensions) => any` | `false`  |         callback triggered when Stl is fully loaded         |
| `onError`         |     `(err: Error) => any`      | `false`  | callback triggered when an error occurred while loading Stl |
| `canvasId`        |            `string`            | `false`  |    id of the canvas element used for rendering the model    |

The component also accepts ```<div/>``` props

## Interfaces

### CameraProps

| Prop              |          Type          | Required |                                                  Notes                                                   |
|-------------------|:----------------------:|:--------:|:--------------------------------------------------------------------------------------------------------:|
| `ref`             | `{current: CameraRef}` | `false`  |                          reference of the camera for accessing it's properties                           |
| `initialPosition` |    `CameraPosition`    | `false`  | set the position of the camera in geographic coordinates. The origin of coordinates is the object itself |

### CameraRef

| Prop                |                Type                 | Required |                                       Notes                                        |
|---------------------|:-----------------------------------:|:--------:|:----------------------------------------------------------------------------------:|
| `setCameraPosition` | `(position: CameraPosition) => any` |  `true`  | imperatively sets the camera position based on the provided geographic coordinates |

setCameraPosition:

### ModelProps

| Prop            |                      Type                      | Required |                          Notes                          |
|-----------------|:----------------------------------------------:|:--------:|:-------------------------------------------------------:|
| `ref`           |             `{current: ModelRef}`              | `false`  | reference of the 3d model for accessing it's properties |
| `scale`         |                    `number`                    | `false`  |          scale of the 3d model, defaults to 1           |
| `positionX`     |                    `number`                    | `false`  |        x coordinate in the world of the 3d model        |
| `positionY`     |                    `number`                    | `false`  |        y coordinate in the world of the 3d model        |
| `rotationX`     |                    `number`                    | `false`  |             rotation in x axis of the model             |
| `rotationY`     |                    `number`                    | `false`  |             rotation in y axis of the model             |
| `rotationY`     |                    `number`                    | `false`  |             rotation in z axis of the model             |
| `color`         |            `CSSProperties['color']`            | `false`  |        color of the 3d model, defaults to "grey"        |
| `geometryProps` | `(geometry: BufferGeometry) => BufferGeometry` | `false`  |     Perform some processing to the models geometry      | 

### FloorProps

| Prop         |   Type   | Required |                              Notes                               |
|--------------|:--------:|:--------:|:----------------------------------------------------------------:|
| `gridWidth`  | `number` | `false`  | if specified, a grid will be drawn in the floor with this width  |
| `gridLength` | `number` | `false`  | if specified, a grid will be drawn in the floor with this length |

### ModelDimensions

| Prop             |   Type   |                              Notes                               |
|------------------|:--------:|:----------------------------------------------------------------:|
| `boundingRadius` | `number` | the radius of the bounding sphere of the 3d model before scaling |
| `width`          | `number` |                      width of the 3d object                      |
| `height`         | `number` |                     height of the 3d object                      |
| `length`         | `number` |                     length of the 3d object                      |

### CameraPosition

| Prop        |   Type   | Required |                                                                      Notes                                                                       |
|-------------|:--------:|:--------:|:------------------------------------------------------------------------------------------------------------------------------------------------:|
| `latitude`  | `number` | `false`  | camera's position latitude, it should be a number between `- Math.PI / 2` and `Math.PI / 2`, if the number exceeds the limits it will be clamped |
| `longitude` | `number` | `false`  |    camera's position longitude, it should be a number between `- Math.PI` and `Math.PI`, if the number exceeds the limits it will be clamped     |
| `distance`  | `number` | `false`  |      the distance factor between the object and the camera. This is a factor relative to the object size or the grid size if it's specified      |
