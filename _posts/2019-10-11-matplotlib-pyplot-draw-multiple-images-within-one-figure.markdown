---
layout: post
title: "matplotlib-pyplot-draw-multiple-images-within-one-figure"
date:  2019-10-11 18:00:00  +0800
categories: [dev]
tags: [python, matplotlib, image]
---

## what is matplotlib
A python package for 2D plotting

## what is matplotlib.pyplot
A python module providing matlab-like plotting functions

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
bash-3.2$ pip3 list
matplotlib           3.1.1  
tensorflow           2.0.0  
```

## source
```python
import tensorflow as tf
import matplotlib.pyplot as plt

def main():
    fashion_mnist = tf.keras.datasets.fashion_mnist
    (train_images, train_labels), (test_images, test_labels) = fashion_mnist.load_data()
    class_names = ['T-shirt/top', 'Trouser', 'Pullover', 'Dress', 'Coat',
                   'Sandal', 'Shirt', 'Sneaker', 'Bag', 'Ankle boot']
    #print(train_images)
    #print(train_labels)
    #print(test_images)
    #print(test_labels)
    plt.figure(figsize=(6.4,4.8))
    for i in range(100):
        plt.subplot(10,10,i+1)
        plt.xticks([])
        plt.yticks([])
        plt.grid(False)
        plt.imshow(train_images[i], cmap=plt.cm.binary)
    plt.show()

if __name__ == "__main__":
    main()
```

## output
![alt text](/assets/2019-10-11-matplotlib-pyplot-draw-multiple-images-within-one-figure.png)
