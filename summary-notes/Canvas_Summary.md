# Canvas
## Canvas in a nutshell
Canvas is a HTML tag created by Apple (in an attempt to replace SVG) that allows graphics to be drawn in the document through Javascript.

To access the Canvas, you need to include a `<canvas>` tag pair in the HTML file and in the js file you will also need to set a variable (usually ctx) to your canvas tag and assign it ".getContext('2d')".

Canvas also works on the principle of co-ordinates within the browser and by default the co-ordinates of the browser may not align with the Canvas box.  As such, you will need to align these using ".scrollWidth" and ".scrollHeight".  A typical Canvas JS file will contain the following lines:

~~~javascript
var canvas = document.getElementById("my-canvas");
canvas.width = canvas.scrollWidth;
canvas.height = canvas.scrollHeight;
var ctx = canvas.getContext('2d');
~~~

_Note_: The x and y cordinates (0,0) start from the top left corner unlike your typical graph cordinates. 

## Animation in Canvas
Animation in Canvas is made by drawing a series of shapes, erasing them, and then drawing them again a few pixels away from their original position.  This can be done using the setInterval function in JS.  In essense, animation in Canvas is like stop motion.

Rectangles are easiest to make in Canvas. 

~~~javascript
ctx.fillRect(start x, start y, rect width , rect height);
~~~

Other shapes require you to draw the shape and fill it in with color

~~~javascript
ctx.beginPath()
ctx.moveTo(x-cordinate, y-cordinate);
//insert drawing lines 
ctx.fillStyle = this.color;
ctx.closePath();
ctx.fill();
~~~

to clear the canvas use `ctx.clearRect(start x, start y, canvas width , canvas height)`

~~~javascript
ctx.clearRect(0, 0, canvas.width, canvas.height);
~~~

### Canvas examples

See the following examples of graphics/games made in Canvas.

**Bouncing ball** - see canvas bouncing ball example file.  
**Shapes!** - see canvasShapes example file.