---
layout: post
title: "python-convert-rgb-pixel-into-grayscale"
date:  2019-10-11 14:00:00  +0800
categories: [dev]
tags: [python, image]
---

## environment
macOS High Sierra
```bash
bash-3.2$ sw_vers
ProductName:    Mac OS X
ProductVersion: 10.13.6
BuildVersion:   17G4015
```

## python version
```bash
bash-3.2$ python3 --version
Python 3.7.3
```

## python module version
```bash
bash-3.2$ pip3 list | grep -E "(numpy|scipy|Pillow)"
numpy                1.17.2 
Pillow               6.2.0  
scipy                1.3.1
```

## convert with Pillow
### source
```python
import PIL
import PIL.Image
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.image as mpimg

def main():
    img = PIL.Image.open('1200.png').convert('L')
    data = np.array(list(img.tobytes())).reshape(512,512)
    print('shape: ' + str(data.shape))
    print(data)
    plt.imshow(data, cmap=plt.get_cmap('gray'))
    plt.show()

if __name__ == "__main__":
    main()

```

### output
```bash
bash-3.2$ python3 a.py
shape: (512, 512)
[[145 135 137 ... 209 209 224]
 [138 126 126 ... 196 194 210]
 [137 126 129 ... 195 196 209]
 ...
 [131 125 128 ...  97  99 106]
 [132 123 129 ... 103 103 108]
 [140 132 136 ... 111 112 119]]
```

## convert by formula
### source
```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.image as mpimg

def rgb2gray(rgb):
    return np.dot(rgb[...,:3], [0.2989, 0.5870, 0.1140])

def main():
    img = mpimg.imread('1200.png')
    data = rgb2gray(img)
    print('shape: ' + str(data.shape))
    print(data)
    plt.imshow(data, cmap=plt.get_cmap('gray'), vmin=0, vmax=1)
    plt.show()

if __name__ == "__main__":
    main()
```
### output
```bash
bash-3.2$ python3 a.py
hape: (512, 512)
[[0.57021414 0.53213218 0.53750356 ... 0.82117374 0.82262393 0.88107883]
 [0.54357571 0.49598982 0.49716198 ... 0.76889962 0.76408433 0.82398942]
 [0.53848238 0.49684159 0.50828512 ... 0.76630158 0.77216237 0.82305295]
 ...
 [0.51597611 0.49172392 0.50574708 ... 0.38243412 0.39089256 0.41818942]
 [0.51783101 0.48336785 0.50943257 ... 0.40480667 0.40423295 0.42392353]
 [0.5523965  0.51865846 0.53668748 ... 0.43911883 0.44293098 0.46818629]]
```
