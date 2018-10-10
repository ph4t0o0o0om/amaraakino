
## Bench Demo:(https://bench-lms.herokuapp.com)

# Built-in tools

You can use [`designer.setSelected`] or [`designer.setTools`] for below tools.

1. `line` --- to draw straight lines
2. `pencil` --- to write/draw shapes
3. `dragSingle` --- to drag/ove and especially **resize** last selected shape
4. `dragMultiple` --- to drag/move all shapes
5. `eraser` --- to erase/clear specific portion of shapes
6. `rectangle` --- to draw rectangles
7. `arc` --- to draw circles
8. `bezier` --- to draw bezier curves
9. `quadratic` --- to draw quadratic curves
10. `text` --- to write texts on single or multiple lines, select font families/sizes and more
11. `image` --- add external images
12. `arrow` --- draw arrow lines
13. `marker` --- draw markers
14. `lineWidth` --- set line width
15. `colorsPicker` --- background and foreground colors picker
16. `extraOptions` --- extra options eg. lineCap, lineJoin, globalAlpha, globalCompositeOperation etc.
17. `pdf` --- to import PDF
18. `code` --- to enable/disable code view
19. `undo` --- undo recent shapes

The correct name for `dragSingle` should be: `drag-move-resize last-selected-shape`.

The correct name for `dragMultiple` should be: `drag-move all-shapes`.

nRAR to extract this: [canvas-designer.tar.gz](http://dl.webrtc-experiment.com/canvas-designer.tar.gz)

# Complete Usage

```javascript
var designer = new CanvasDesigner();

websocket.onmessage = function(event) {
    designer.syncData( JSON.parse(event.data) );
};

designer.addSyncListener(function(data) {
    websocket.send(JSON.stringify(data));
});

designer.setSelected('pencil');

designer.setTools({
    pencil: true,
    text: true
});

designer.appendTo(document.documentElement);
```

It is having `designer.destroy()` method as well.

# Use [WebRTC]()!

```javascript
webrtc.onmessage = function(event) {
    designer.syncData( event.data );
};

designer.addSyncListener(function(data) {
    webrtc.send(data);
});
```

# Use Socket.io

```javascript
socket.on('message', function(data) {
    designer.syncData( data );
});

designer.addSyncListener(function(data) {
    socket.emit('message', data);
});
```

# API Reference

## `widgetHtmlURL`

You can place `widget.html` file anywhere on your site.

```javascript
designer.widgetHtmlURL = '/html-files/widget.html';
```

By default `widget.html` is placed in the same directory of `index.html`.

```javascript
// here is default value
designer.widgetHtmlURL = 'widget.html';
```

Remember, `widget.html` is loaded using `<iframe>`.

## `widgetJsURL`

> **Note:** This file is **internally used** by `widget.html`.

You can place `widget.html` file anywhere on your site.

```javascript
designer.widgetJsURL = '/js-files/widget.min.js';
```

By default `widget.min.js` is placed in the same directory of `index.html`.

```javascript
// here is default value
designer.widgetJsURL = 'widget.min.js';
```

Remember, `widget.js` is loaded using `<iframe>`.

## `syncData`

Pass array-of-points that are shared by remote users using socket.io or websockets or XMPP or WebRTC.

```javascript
designer.syncData(arrayOfPoints);
```

## `addSyncListener`

This callback is invoked as soon as something new is drawn. An array-of-points is passed over this function. That array MUST be shared with remote users for collaboration.

```javascript
designer.addSyncListener(function(data) {
    designer.send(JSON.stringify(data));
});
```

## `setSelected`

This method allows you select specific tools.

* See list of [all tools]()

```javascript
designer.setSelected('rectangle');
```

## `setTools`

This method allows you choose between tools that **should be displayed** in the tools-panel.

* See list of [all tools]()

```javascript
designer.setTools({
    line: true,
    arrow: true,
    pencil: true,
    marker: true,
    dragSingle: true,
    dragMultiple: true,
    eraser: true,
    rectangle: true,
    arc: true,
    bezier: true,
    quadratic: true,
    text: true,
    image: true,
    pdf: true,
    zoom: true,
    lineWidth: true,
    colorsPicker: true,
    extraOptions: true,
    code: true,
    undo: true
});
```

# Contributors

1. [Muaz Khan]()
2. [Oleg Aliullov]()
3. [Phantom]()

Please make pull-request to update this list.

# License

[Whiteboard]() is released under [MIT licence]() . Copyright (c) [Muaz Khan]().
