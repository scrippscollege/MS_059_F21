# Conceptual Visualization

In past years I taught students how to reproduce the charts that you can make in Microsoft Excel using Python and Processing. It worked, but what we wound up doing was making a janky version of Excel. This year I decided to play to Processing's strengths and make *conceptual visualizations* instead.

## Conceptual visualization Examples

Imagine a square window that shows a year of weather patterns in your city. Each cell in a 19x19 grid might have a color indicating  average temperature, another for the temperature range, plus a shape for precipatation. This grid would show a whole year of weather in one small grid and offer unique view of the data.

![](https://www.evernote.com/l/ADMaweu8jJxMQ7Jxpmc_5SbdG3D3ymTqfm8B/image.png)

```# VARIABLES
size(400, 400)
noStroke()
background(0)
ellipseMode(CORNER)
incr = 10

# ANIMATE THIS!

# nested loop
for y in range(0, height, height/incr):
    for x in range(0,width, width/incr):
        # noFill()
        # rect(x,y, width/incr,height/incr)
        fill(random(0,255),random(100,255),random(0,255))
        noStroke()
        ellipse(x,y, random(10,width/incr),height/incr)
```

Animate this image. Could you do it smoothly? 
