> 当元素存在 scale 属性时，在拖拽位置和改变大小的时候，需要考虑当前 scale 的值来计算偏移量，否则鼠标的移动和组件的拖拽会不匹配。该 fork 解决了这个问题

<p align="center"><img src="https://rawgit.com/mauricius/vue-draggable-resizable/v1/docs/resources/logo.png" alt="logo"></p>
<h1 align="center">VueDraggableResizable 2</h1>

[![Latest Version on NPM](https://img.shields.io/npm/v/vue-draggable-resizable.svg?style=flat-square)](https://npmjs.com/package/vue-draggable-resizable)
[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![npm](https://img.shields.io/npm/dt/vue-draggable-resizable.svg?style=flat-square)](https://www.npmjs.com/package/vue-draggable-resizable)

> Vue2 Component for draggable and resizable elements.

If you are looking for the version 1 of the component, it is available on the [v1 branch](https://github.com/mauricius/vue-draggable-resizable/tree/v1).

## Table of Contents

- [Features](#features)
- [Live Playground](#live-playground)
- [Install and basic usage](#install-and-basic-usage)
  - [Props](#props)
  - [Events](#events)
  - [Styling](#styling)
- [Contributing](#contributing)
- [License](#license)

### Features

- No dependencies
- Use draggable, resizable or both
- Define handles for resizing
- Restrict size and movement to parent element or custom selector
- Snap element to custom grid
- Restrict drag to vertical or horizontal axis
- Maintain aspect ratio
- Touch enabled
- Use your own classes
- Provide your own markup for handles

### Live Playground

For examples of the component go to the [live playground](https://mauricius.github.io/vue-draggable-resizable/)

Alternatively you can run the playground on your own computer:

- Clone this repository
- `npm install`
- `npm run storybook`
- Visit [http://localhost:9001/](http://localhost:9001/)

---

## Install and basic usage

```bash
$ npm install --save vue-draggable-resizable
```

Register the component

```js
import Vue from 'vue'
import VueDraggableResizable from 'vue-draggable-resizable'

// optionally import default styles
import 'vue-draggable-resizable/dist/VueDraggableResizable.css'

Vue.component('vue-draggable-resizable', VueDraggableResizable)
```

You may now use the component in your markup

```vue
<template>
  <div
    style="height: 500px; width: 500px; border: 1px solid red; position: relative;"
  >
    <vue-draggable-resizable
      :w="100"
      :h="100"
      @dragging="onDrag"
      @resizing="onResize"
      :parent="true"
    >
      <p>
        Hello! I'm a flexible component. You can drag me around and you can
        resize me.<br />
        X: {{ x }} / Y: {{ y }} - Width: {{ width }} / Height: {{ height }}
      </p>
    </vue-draggable-resizable>
  </div>
</template>

<script>
import VueDraggableResizable from 'vue-draggable-resizable'

export default {
  data: function() {
    return {
      width: 0,
      height: 0,
      x: 0,
      y: 0
    }
  },
  methods: {
    onResize: function(x, y, width, height) {
      this.x = x
      this.y = y
      this.width = width
      this.height = height
    },
    onDrag: function(x, y) {
      this.x = x
      this.y = y
    }
  }
}
</script>
```

### Props

#### className

Type: `String`<br>
Required: `false`<br>
Default: `vdr`

Used to set the custom `class` of a draggable-resizable component.

```html
<vue-draggable-resizable class-name="my-class"></vue-draggable-resizable>
```

#### classNameDraggable

Type: `String`<br>
Required: `false`<br>
Default: `draggable`

Used to set the custom `class` of a draggable-resizable component when `draggable` is enable.

```html
<vue-draggable-resizable
  class-name-draggable="my-draggable-class"
></vue-draggable-resizable>
```

#### classNameResizable

Type: `String`<br>
Required: `false`<br>
Default: `resizable`

Used to set the custom `class` of a draggable-resizable component when `resizable` is enable.

```html
<vue-draggable-resizable
  class-name-resizable="my-resizable-class"
></vue-draggable-resizable>
```

#### classNameDragging

Type: `String`<br>
Required: `false`<br>
Default: `dragging`

Used to set the custom `class` of a draggable-resizable component when is dragging.

```html
<vue-draggable-resizable
  class-name-dragging="my-dragging-class"
></vue-draggable-resizable>
```

#### classNameResizing

Type: `String`<br>
Required: `false`<br>
Default: `resizing`

Used to set the custom `class` of a draggable-resizable component when is resizing.

```html
<vue-draggable-resizable
  class-name-resizing="my-resizing-class"
></vue-draggable-resizable>
```

#### classNameActive

Type: `String`<br>
Required: `false`<br>
Default: `active`

Used to set the custom `class` of a draggable-resizable component when is active.

```html
<vue-draggable-resizable
  class-name-active="my-active-class"
></vue-draggable-resizable>
```

#### classNameHandle

Type: `String`<br>
Required: `false`<br>
Default: `handle`

Used to set the custom common `class` of each handle element. This way you can style each handle individually using the selector `<your class>-<handle code>`, where `handle code` identifies one of the handles provided by the `handle` prop.

So for example, this component:

```html
<vue-draggable-resizable
  class-name-handle="my-handle-class"
></vue-draggable-resizable>
```

renders the following:

```html
<div ...>
  <div class="my-handle-class my-handle-class-tl"></div>
  <div class="my-handle-class my-handle-class-tm"></div>
  <div class="my-handle-class my-handle-class-tr"></div>
  [...]
</div>
```

#### disableUserSelect

Type: `Boolean`<br>
Required: `false`<br>
Default: `true`

By default, the component adds the style declaration `'user-select:none'` to itself to prevent text selection during drag. You can disable this behaviour by setting this prop to `false`.

```html
<vue-draggable-resizable :disable-user-select="false"></vue-draggable-resizable>
```

#### enableNativeDrag

Type: `Boolean`<br>
Required: `false`<br>
Default: `false`

By default, the browser's native drag and drop funcionality (usually used for images and some other elements) is disabled, as it may conflict with the one provided by the component. If you need, for whatever reason, to have this functionality back you can set this prop to `true`.

```html
<vue-draggable-resizable :enable-native-drag="true"></vue-draggable-resizable>
```

#### active

Type: `Boolean`<br>
Required: `false`<br>
Default: `false`

Determines if the component should be active or not. The prop reacts to changes and also can be used with the `sync`[modifier](https://vuejs.org/v2/guide/components.html#sync-Modifier) to keep the state in sync with the parent. You can use along with the `preventDeactivation` prop in order to fully control the active behavior from outside the component.

```html
<vue-draggable-resizable :active="true"></vue-draggable-resizable>
```

#### preventDeactivation

Type: `Boolean`<br>
Required: `false`<br>
Default: `false`

Determines if the component should be deactivated when the user clicks/taps outside it.

```html
<vue-draggable-resizable :prevent-deactivation="true"></vue-draggable-resizable>
```

#### draggable

Type: `Boolean`<br>
Required: `false`<br>
Default: `true`

Defines it the component should be draggable or not.

```html
<vue-draggable-resizable :draggable="false"></vue-draggable-resizable>
```

#### resizable

Type: `Boolean`<br>
Required: `false`<br>
Default: `true`

Defines it the component should be resizable or not.

```html
<vue-draggable-resizable :resizable="false"></vue-draggable-resizable>
```

#### w

Type: `Number`<br>
Required: `false`<br>
Default: `200`

Define the initial width of the element.

```html
<vue-draggable-resizable :w="200"></vue-draggable-resizable>
```

#### h

Type: `Number`<br>
Required: `false`<br>
Default: `200`

Define the initial height of the element.

```html
<vue-draggable-resizable :h="200"></vue-draggable-resizable>
```

#### minWidth

Type: `Number`<br>
Required: `false`<br>
Default: `50`

Define the minimal width of the element.

```html
<vue-draggable-resizable :min-width="50"></vue-draggable-resizable>
```

#### minHeight

Type: `Number`<br>
Required: `false`<br>
Default: `50`

Define the minimal height of the element.

```html
<vue-draggable-resizable :min-height="50"></vue-draggable-resizable>
```

#### maxWidth

Type: `Number`<br>
Required: `false`<br>
Default: `null`

Define the maximum width of the element.

```html
<vue-draggable-resizable :max-width="400"></vue-draggable-resizable>
```

#### maxHeight

Type: `Number`<br>
Required: `false`<br>
Default: `null`

Define the maximum height of the element.

```html
<vue-draggable-resizable :max-height="50"></vue-draggable-resizable>
```

#### x

Type: `Number`<br>
Required: `false`<br>
Default: `0`

Define the initial x position of the element.

```html
<vue-draggable-resizable :x="0"></vue-draggable-resizable>
```

#### y

Type: `Number`<br>
Required: `false`<br>
Default: `0`

Define the initial y position of the element.

```html
<vue-draggable-resizable :y="0"></vue-draggable-resizable>
```

#### z

Type: `Number|String`<br>
Required: `false`<br>
Default: `auto`

Define the zIndex of the element.

```html
<vue-draggable-resizable :z="999"></vue-draggable-resizable>
```

#### handles

Type: `Array`<br>
Required: `false`<br>
Default: `['tl', 'tm', 'tr', 'mr', 'br', 'bm', 'bl', 'ml']`

Define the array of handles to restrict the element resizing:

- `tl` - Top left
- `tm` - Top middle
- `tr` - Top right
- `mr` - Middle right
- `br` - Bottom right
- `bm` - Bottom middle
- `bl` - Bottom left
- `ml` - Middle left

```html
<vue-draggable-resizable
  :handles="['tm','bm','ml','mr']"
></vue-draggable-resizable>
```

#### axis

Type: `String`<br>
Required: `false`<br>
Default: `both`

Define the axis on which the element is draggable. Available values are `x`, `y` or `both`.

```html
<vue-draggable-resizable axis="x"></vue-draggable-resizable>
```

#### grid

Type: `Array`<br>
Required: `false`<br>
Default: `[1,1]`

Define the grid on which the element is snapped.

```html
<vue-draggable-resizable :grid="[1,1]"></vue-draggable-resizable>
```

#### parent

Type: `Boolean | String`<br>
Required: `false`<br>
Default: `false`

Restricts the movement and the dimensions of the component to the parent (if `true` is provided), or to an element identified by a valid CSS selector.

```html
<vue-draggable-resizable :parent="true"></vue-draggable-resizable>
```

```html
<vue-draggable-resizable :parent=".selector"></vue-draggable-resizable>
```

#### dragHandle

Type: `String`<br>
Required: `false`

Defines the selector that should be used to drag the component.

```html
<vue-draggable-resizable drag-handle=".drag"></vue-draggable-resizable>
```

#### dragCancel

Type: `String`<br>
Required: `false`

Defines a selector that should be used to prevent drag initialization.

```html
<vue-draggable-resizable drag-cancel=".drag"></vue-draggable-resizable>
```

#### lockAspectRatio

Type: `Boolean`<br>
Required: `false`<br>
Default: `false`

The `lockAspectRatio` property is used to lock aspect ratio. This property doesn't play well with `grid`, so make sure to use only one at a time.

```html
<vue-draggable-resizable :lock-aspect-ratio="true"></vue-draggable-resizable>
```

#### onDragStart

Type: `Function`<br>
Required: `false`<br>
Default: `null`

Called when dragging starts (element is clicked or touched). If `false` is returned by any handler, the action will cancel. You can use this function to prevent bubbling of events.

```html
<vue-draggable-resizable
  :onDragStart="onDragStartCallback"
></vue-draggable-resizable>
```

```js
function onDragStartCallback(ev){
   ...
   // return false; — for cancel
}
```

#### onResizeStart

Type: `Function`<br>
Required: `false`<br>
Default: `null`

Called when resizing starts (handle is clicked or touched). If `false` is returned by any handler, the action will cancel.

```html
<vue-draggable-resizable
  :onResizeStart="onResizeStartCallback"
></vue-draggable-resizable>
```

```js

function onResizeStartCallback(handle, ev){
   ...
   // return false; — for cancel
}
```

---

### Events

#### activated

Parameters: `-`

Called whenever the component gets clicked, in order to show handles.

```html
<vue-draggable-resizable @activated="onActivated"></vue-draggable-resizable>
```

#### deactivated

Parameters: `-`

Called whenever the user clicks anywhere outside the component, in order to deactivate it.

```html
<vue-draggable-resizable @deactivated="onDeactivated"></vue-draggable-resizable>
```

#### resizing

Parameters:

- `left` the X position of the element
- `top` the Y position of the element
- `width` the width of the element
- `height` the height of the element

Called whenever the component gets resized.

```html
<vue-draggable-resizable @resizing="onResizing"></vue-draggable-resizable>
```

#### resizestop

Parameters:

- `left` the X position of the element
- `top` the Y position of the element
- `width` the width of the element
- `height` the height of the element

Called whenever the component stops getting resized.

```html
<vue-draggable-resizable @resizestop="onResizstop"></vue-draggable-resizable>
```

#### dragging

Parameters:

- `left` the X position of the element
- `top` the Y position of the element

Called whenever the component gets dragged.

```html
<vue-draggable-resizable @dragging="onDragging"></vue-draggable-resizable>
```

#### dragstop

Parameters:

- `left` the X position of the element
- `top` the Y position of the element

Called whenever the component stops getting dragged.

```html
<vue-draggable-resizable @dragstop="onDragstop"></vue-draggable-resizable>
```

---

### Styling

You can style the component using appropriate class names passed as props to the component. Moreover you can replace the default styles for the handles, provided in the source file `vue-draggable-resizable.css`, but you should take care to define position and size for them. The default classes for handles are `handle` and `handle-tl`, `handle-br` and so on.

The component also provides [named slots](https://vuejs.org/v2/guide/components-slots.html#Named-Slots) for each handle, so you can use your markup inside each one.

## Thanks

Thanks to @kirillmurashov for his work on [vue-drag-resize](https://github.com/kirillmurashov/vue-drag-resize) component.

## Security

If you discover any security related issues, please email maurizio.bonani@gmail.com instead of using the issue tracker.

## Contributing

Any contribution to the code or any part of the documentation and any idea and/or suggestion are very welcome.

```bash
# serve with hot reload at localhost:8080
npm run serve

# distribution build
npm run build

# build the storybook docs into gh-pages
npm run gh-pages:build

# run unit tests
npm run unit

# run storybook at localhost:9001
npm run storybook
```

## License

The MIT License (MIT). Please see [License File](LICENSE) for more information.
