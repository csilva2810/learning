# Browser Rendering Optimization

## How to achieve 60fps
When any change occurs in the browser the browser will paint/render new frames for this change. Usually this frame change occurs 60 times per second, which means that we have 16ms (1000ms/60f ) to render each frame. But the browser needs some amount of this 16ms to do some house keeping work. Which means that in the end of the day we will have about 10ms per frame.

## Browser rendering pipeline
Here is what the browser does to render a page.

1. DOM (Parse HTML)
2. Recalculate Styles (CSS)
3. Combine the DOM with the calculated styles generating a *Render Tree*
4. Calculate the spaces that elements will take on the screen (Layout/Reflow) 
5. Transform the elements from vectors to pixels to fill the screen (Raster/Paint)
6. Render different layers for different sections of the page (Composite Layers)

### Render Tree
The render tree will contain only nodes that will really be rendered on the page. If the styles set some element to `display: none`, this element will not be on the render tree.

### Raster/Paint
The raster is the process of paint the elements on screen. This process will call browsers APIs like `drawRoundedRectangle` or `drawBitmap` to paint the elements.

### Composite layers
This is part of the paint process

### Layout
As we saw, layout is the process of calculate where the elements will be painted on the screen. It’s important to know that every change to elements geometry causes a layout recalculation. Geometry would be properties like *width*, *height*, *padding*, *margins*.
It’s a good practice avoiding changing geometry properties because they will cause a *Reflow* which means that all the elements on the page will be repainted.

### Anatomy of a frame
*Javascript > Style > Layout > Paint > Composite*
Usually Javascript will be used to trigger changes on the elements that will cause the subsequents tasks to run.

### Different rendering pipeline triggers
#### Geometry properties change. 
The browser will have to run all the pipeline again because *Layout* was affected. 
Pipeline: *Style > Layout > Paint > Composite*

#### Paint properties change.
 When we change painting properties like *background-color* and *color*, the browser will skip the layout phase.
Pipeline: *Style > Paint > Composite*

#### Compositing properties change.
If the change only compositing properties like *transform* and *opacity* the browser skip Layout and Paint .
Pipeline: *Style > Composite*
This is the best-performing version of the pipeline.

## RAIL
#####

## Request Animation Frame
#####

## References
[Rendering Performance  |  Web Fundamentals  |  Google Developers](https://developers.google.com/web/fundamentals/performance/rendering#3_js_css_style_composite)
[Browser Rendering Optimization](https://www.udacity.com/course/browser-rendering-optimization--ud860)