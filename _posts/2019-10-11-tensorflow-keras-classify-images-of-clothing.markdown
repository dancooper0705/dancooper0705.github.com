---
layout: post
title: "tensorflow-keras-classify-images-of-clothing"
date:  2019-10-11 19:00:00  +0800
categories: [dev]
tags: [python, tensorflow, keras]
---

## what is tensorflow
A python package which implement neural network machine learning

## what is keras
A python package which runs marchin leanring. Its nerual network backend could be tensorflow.

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
numpy                1.17.2
matplotlib           3.1.1
tensorflow           2.0.0
```

## source
```python
import numpy as np
import matplotlib.pyplot as plt
import tensorflow as tf
import tensorflow.keras as keras

class_names = ['T-shirt/top', 'Trouser', 'Pullover', 'Dress', 'Coat',
               'Sandal', 'Shirt', 'Sneaker', 'Bag', 'Ankle boot']

train_images = None
train_labels = None
test_image = None
test_labels = None
model = None

def plot_train_images():
    plt.figure(figsize=(10,10))
    for i in range(25):
        plt.subplot(5,5,i+1)
        plt.xticks([])
        plt.yticks([])
        plt.grid(False)
        plt.imshow(train_images[i], cmap=plt.cm.binary)
        plt.xlabel(class_names[train_labels[i]])
    plt.tight_layout()
    plt.show()

def download_images():
    global test_images
    global test_labels
    global train_images
    global train_labels
    fashion_mnist = tf.keras.datasets.fashion_mnist
    (train_images, train_labels), (test_images, test_labels) = fashion_mnist.load_data()
    train_images = train_images / 255.0
    test_images = test_images / 255.0

def learn_train_images():
    global model
    model = keras.Sequential()
    model.add(keras.layers.Flatten(input_shape=(28, 28)))
    model.add(keras.layers.Dense(128, activation='relu'))
    model.add(keras.layers.Dense(10, activation='softmax'))
    model.summary()
    model.compile(optimizer='adam',
            loss='sparse_categorical_crossentropy',
            metrics=['accuracy'])
    model.fit(train_images, train_labels, epochs=5)
    test_scores = model.evaluate(test_images,  test_labels, verbose=2)
    print('Test loss:', test_scores[0])
    print('Test accuracy:', test_scores[1])

def predict_all_test_images():
    predictions = model.predict(test_images)
    print(predictions[0])
    print(np.argmax(predictions[0]))
    print(test_labels[0])
    # Plot the first X test images, their predicted labels, and the true labels.
    # Color correct predictions in blue and incorrect predictions in red.
    num_rows = 5
    num_cols = 3
    num_images = num_rows*num_cols
    plt.figure(figsize=(2*2*num_cols, 2*num_rows))
    for i in range(num_images):
        plt.subplot(num_rows, 2*num_cols, 2*i+1)
        plot_image(i, predictions[i], test_labels, test_images)
        plt.subplot(num_rows, 2*num_cols, 2*i+2)
        plot_value_array(i, predictions[i], test_labels)
    plt.tight_layout()
    plt.show()

def predict_single_test_images():
    img = test_images[0]
    print(img.shape)
    # Add the image to a batch where it's the only member.
    img = (np.expand_dims(img,0))
    print(img.shape)
    predictions = model.predict(img)
    print(predictions)
    i = 0
    plt.figure(figsize=(6,3))
    plt.subplot(1,2,1)
    plot_image(i, predictions[0], test_labels, test_images)
    plt.subplot(1,2,2)
    plot_value_array(i, predictions[0], test_labels)
    plt.show()

def main():
    download_images()
    learn_train_images()
    plot_train_images()
    predict_all_test_images()
    predict_single_test_images()

def plot_image(i, predictions_array, true_label, img):
  predictions_array, true_label, img = predictions_array, true_label[i], img[i]
  plt.grid(False)
  plt.xticks([])
  plt.yticks([])

  plt.imshow(img, cmap=plt.cm.binary)

  predicted_label = np.argmax(predictions_array)
  if predicted_label == true_label:
    color = 'blue'
  else:
    color = 'red'

  plt.xlabel("{} {:2.0f}% ({})".format(class_names[predicted_label],
                                100*np.max(predictions_array),
                                class_names[true_label]),
                                color=color)

def plot_value_array(i, predictions_array, true_label):
  predictions_array, true_label = predictions_array, true_label[i]
  plt.grid(False)
  plt.xticks(range(10))
  plt.yticks([])
  thisplot = plt.bar(range(10), predictions_array, color="#777777")
  plt.ylim([0, 1])
  predicted_label = np.argmax(predictions_array)

  thisplot[predicted_label].set_color('red')
  thisplot[true_label].set_color('blue')

if __name__ == "__main__":
    main()
```

## output
```bash
2019-10-12 19:32:40.993094: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2019-10-12 19:32:41.003973: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x7fc4c651af20 executing computations on platform Host. Devices:
2019-10-12 19:32:41.003986: I tensorflow/compiler/xla/service/service.cc:175]   StreamExecutor device (0): Host, Default Version
Model: "sequential"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
flatten (Flatten)            (None, 784)               0         
_________________________________________________________________
dense (Dense)                (None, 128)               100480    
_________________________________________________________________
dense_1 (Dense)              (None, 10)                1290      
=================================================================
Total params: 101,770
Trainable params: 101,770
Non-trainable params: 0
_________________________________________________________________
Train on 60000 samples
Epoch 1/5
60000/60000 [==============================] - 3s 44us/sample - loss: 0.4990 - accuracy: 0.8257
Epoch 2/5
60000/60000 [==============================] - 2s 38us/sample - loss: 0.3745 - accuracy: 0.8651
Epoch 3/5
60000/60000 [==============================] - 2s 38us/sample - loss: 0.3355 - accuracy: 0.8778
Epoch 4/5
60000/60000 [==============================] - 2s 38us/sample - loss: 0.3117 - accuracy: 0.8859
Epoch 5/5
60000/60000 [==============================] - 2s 38us/sample - loss: 0.2946 - accuracy: 0.8917
10000/1 - 0s - loss: 0.2992 - accuracy: 0.8783
Test loss: 0.37171216771602633
Test accuracy: 0.8672
[4.5444303e-06 2.8985139e-06 2.4740308e-05 5.0351861e-07 6.3307103e-05
 5.4802161e-01 2.8345596e-05 1.9788887e-01 4.0743238e-04 2.5355774e-01]
 5
 9
 (28, 28)
 (1, 28, 28)
 [[4.5444367e-06 2.8985210e-06 2.4740297e-05 5.0351741e-07 6.3307132e-05
   5.4802138e-01 2.8345637e-05 1.9788916e-01 4.0743258e-04 2.5355771e-01]]
```

### the first 25 train images and its label
![the first 25 train images](/assets/2019-10-11-tensorflow-keras-classify-images-of-clothing-figure-1.png)

### the first 15 test images and inference result
![the first 25 test images](/assets/2019-10-11-tensorflow-keras-classify-images-of-clothing-figure-2.png)

### only the fist test image and inference result
![only the first train image](/assets/2019-10-11-tensorflow-keras-classify-images-of-clothing-figure-3.png)

## reference
[https://www.tensorflow.org/tutorials/keras/classification](https://www.tensorflow.org/tutorials/keras/classification)
