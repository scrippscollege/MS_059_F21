# Bridget Riley

![](https://www.evernote.com/l/ADMII6ECvflGUJ4oCBZq5b6xw8l1M7nl314B/image.png)

```size(500, 500)
background(255)
fill(0)
noStroke()

w=width
slotx=100

for y in range(0,30):
    x=-width+(y%2)*20
    print(x,y)
    while (x < 1e3):
        d = pow(abs(atan(x-slotx))/1.57,w)
        ellipse(lerp(slotx,x,d),20*y,min(20,40*d),20)
        x += 40
        # print(x)
```
