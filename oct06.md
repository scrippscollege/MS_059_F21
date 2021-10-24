## MS059 10/06
# iterating with data files

---

## the idea: 
# run an expensive operation once and save the results to a data file


---
## code, section by section
# imports

```
import csv, os
from os.path import expanduser
from colorthief import ColorThief
```

---
# paths

```
# GET THE PATHS

# If you didn't change the Default location
home = expanduser("~/Documents/Processing/") 
sketchpath = "colorthief_csv/"
datadir = home +sketchpath +"data/"
print("path to data folder: " +datadir)
```

---
# variables

```
# SET THE VARIABLES
# Set the display window width to a multiple of the number of frames
size(1100, 240)
noStroke()
background(0)

framedir = 'frames/'
datafile = framedir[:-1] +'_data.csv'
datafilepath = datadir +datafile
q=10
```

---
# create the data file

```
# Create the data file!
imgs = []
for filename in os.listdir(datadir + framedir):
    if filename.endswith(".jpg"):
        f = framedir + filename

        # Ooooh, a DICTIONARY
        # Generate the Metadata and put it in there
        color_thief = ColorThief(f)
        rgb = color_thief.get_color(quality=q)
        # palette = color_thief.get_palette(color_count=7,quality=q);
        d = {'path':f,
            'r':rgb[0],
            'g':rgb[1],
            'b':rgb[2]
            }
        print(d)
        imgs.append(d)
    else:
        continue

```

---
# put the frames in order

```
# PUT THE FRAMES IN ORDER
# Sort  the dictionary by the 'path' key!
imgsplus = sorted(imgs, key=lambda k: k['path']) 

```

---
# save the metadata

```
# save the metadata for the next time!
with open(datafilepath, 'wb') as csv_file:
    fieldnames = ['path','r','g','b',]
    imgswriter = csv.DictWriter(csv_file, fieldnames=fieldnames)
    imgswriter.writeheader()
    
    for img in imgsplus:
        imgswriter.writerow({'path':img['path'],
                            'r':int(img['r']),
                            'g':int(img['g']),
                            'b':int(img['b']),
                            })
```

---
# draw the viz

```
l = len(imgsplus)
w = float(width/l)
# print(imgsplus)
    

for i,frame in enumerate(imgsplus):
    x = int(i*w)
    fill(int(frame['r']),
         int(frame['g']),
         int(frame['b']))
    rect(x,0,x+w,height)
   
```