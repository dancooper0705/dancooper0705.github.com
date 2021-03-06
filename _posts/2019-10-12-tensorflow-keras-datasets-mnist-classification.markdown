---
layout: post
title: "tensorflow-keras-datasets-mnist-classification"
date:  2019-10-12 18:00:00  +0800
categories: [dev]
tags: [tensorflow, keras]
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

## tensorflow keras model
![alt text](/assets/2019-10-12-tensorflow-keras-datasets-mnist-classification-figure-4.png)

## source
```python
import numpy as np
import matplotlib.pyplot as plt
import tensorflow as tf
import tensorflow.keras as keras

class_names = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']

train_images = None
train_labels = None
test_image = None
test_labels = None
model = None
train_images_data = None
test_images_data = None

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
    global test_images_data
    global train_images_data
    fashion_mnist = tf.keras.datasets.fashion_mnist
    (train_images, train_labels), (test_images, test_labels) = keras.datasets.mnist.load_data()
    train_images = train_images / 255.0
    test_images = test_images / 255.0
    train_images_data = train_images.reshape(train_images.shape[0], 784)
    test_images_data = test_images.reshape(test_images.shape[0], 784)
    print('train_images.shape: ' + str(train_images.shape))
    print('test_images.shape: ' + str(test_images.shape))
    print('train_images_data.shape: ' + str(train_images_data.shape))
    print('test_images_data.shape: ' + str(test_images_data.shape))

def learn_train_images():
    global model
    inputs = keras.Input(shape=(784,), name='img')
    x = keras.layers.Dense(64, activation='relu')(inputs)
    x = keras.layers.Dense(64, activation='relu')(x)
    outputs = keras.layers.Dense(10, activation='softmax')(x)
    model = keras.Model(inputs=inputs, outputs=outputs, name='mnist_model')
    model.summary()
    model.compile(optimizer='adam',
            loss='sparse_categorical_crossentropy',
            metrics=['accuracy'])
    model.fit(train_images_data, train_labels, epochs=5, validation_split=0.2, steps_per_epoch=train_images_data.shape[0]//10)
    test_scores = model.evaluate(test_images_data,  test_labels, verbose=2)
    print('Test loss:', test_scores[0])
    print('Test accuracy:', test_scores[1])

def predict_all_test_images():
    predictions = model.predict(test_images_data)
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
    img = test_images_data[0]
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
2019-10-12 18:22:12.410700: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2019-10-12 18:22:12.421261: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x7fcc2034e2f0 executing computations on platform Host. Devices:
2019-10-12 18:22:12.421274: I tensorflow/compiler/xla/service/service.cc:175]   StreamExecutor device (0): Host, Default Version
train_images.shape: (60000, 28, 28)
test_images.shape: (10000, 28, 28)
train_images_data.shape: (60000, 784)
test_images_data.shape: (10000, 784)
Model: "mnist_model"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
img (InputLayer)             [(None, 784)]             0         
_________________________________________________________________
dense (Dense)                (None, 64)                50240     
_________________________________________________________________
dense_1 (Dense)              (None, 64)                4160      
_________________________________________________________________
dense_2 (Dense)              (None, 10)                650       
=================================================================
Total params: 55,050
Trainable params: 55,050
Non-trainable params: 0
_________________________________________________________________
Train on 48000 samples, validate on 12000 samples
Epoch 1/5
48000/48000 [==============================] - 8s 172us/sample - loss: 0.2559 - accuracy: 0.9231 - val_loss: 0.1398 - val_accuracy: 0.9578
Epoch 2/5
48000/48000 [==============================] - 8s 169us/sample - loss: 0.1230 - accuracy: 0.9628 - val_loss: 0.1145 - val_accuracy: 0.9672
Epoch 3/5
48000/48000 [==============================] - 8s 167us/sample - loss: 0.0918 - accuracy: 0.9722 - val_loss: 0.1065 - val_accuracy: 0.9688
Epoch 4/5
48000/48000 [==============================] - 8s 164us/sample - loss: 0.0724 - accuracy: 0.9772 - val_loss: 0.1294 - val_accuracy: 0.9635
Epoch 5/5
48000/48000 [==============================] - 8s 163us/sample - loss: 0.0593 - accuracy: 0.9811 - val_loss: 0.1153 - val_accuracy: 0.9704
10000/1 - 0s - loss: 0.0501 - accuracy: 0.9708

Test loss: 0.09991136973106768
Test accuracy: 0.9708
[2.0496465e-12 3.9963290e-09 7.8489097e-07 1.7835089e-06 1.5911729e-14
4.6289467e-10 1.1751793e-21 9.9999726e-01 1.3774022e-11 8.3155776e-08]
7
7
(784,)
(1, 784)
[[2.0496426e-12 3.9963290e-09 7.8488870e-07 1.7835038e-06 1.5911790e-14
4.6289467e-10 1.1751793e-21 9.9999726e-01 1.3773969e-11 8.3155776e-08]]
```
### the first 25 train images and its label
![alt text](/assets/2019-10-12-tensorflow-keras-datasets-mnist-classification-figure-1.png)

### the first 15 test images and inference result
![alt text](/assets/2019-10-12-tensorflow-keras-datasets-mnist-classification-figure-2.png)

### only the fist test image and inference result
![alt text](/assets/2019-10-12-tensorflow-keras-datasets-mnist-classification-figure-3.png)

## reference
[https://www.tensorflow.org/tutorials/keras/classification](https://www.tensorflow.org/tutorials/keras/classification)
[https://www.tensorflow.org/guide/keras/functional](https://www.tensorflow.org/guide/keras/functional)
