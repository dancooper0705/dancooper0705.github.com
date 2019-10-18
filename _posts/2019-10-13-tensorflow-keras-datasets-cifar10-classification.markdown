---
layout: post
title: "tensorflow-keras-datasets-cifar10-classification"
date:  2019-10-13 12:00:00  +0800
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
![alt text](/assets/2019-10-13-tensorflow-keras-datasets-cifar10-classification-figure-4.png)

## source
```python
import numpy as np
import matplotlib.pyplot as plt
import tensorflow as tf
import tensorflow.keras as keras

class_names = ['airplane', 'automobile', 'bird', 'cat', 'deer', 'dog', 'frog', 'horse', 'ship', 'truck']

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
    (train_images, train_labels), (test_images, test_labels) = keras.datasets.cifar10.load_data()
    train_images = train_images / 255.0
    test_images = test_images / 255.0
    train_images_data = train_images.reshape(train_images.shape[0], 32*32*3)
    test_images_data = test_images.reshape(test_images.shape[0], 32*32*3)
    train_labels = train_labels.reshape(len(train_labels))
    test_labels = test_labels.reshape(len(test_labels))
    '''
    print('type(tain_lables): ' + str(type(train_labels)))
    print('train_images.shape: ' + str(train_images.shape))
    print('train_labels.shape: ' + str(train_labels.shape))
    print('test_images.shape: ' + str(test_images.shape))
    print('train_images_data.shape: ' + str(train_images_data.shape))
    print('test_images_data.shape: ' + str(test_images_data.shape))
    print('train_images: ' + str(train_images))
    print('train_labels: ' + str(train_labels))
    print('test_images: ' + str(test_images))
    '''

def learn_train_images():
    global model
    inputs = keras.Input(shape=(32*32*3,), name='img')
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

def save_model_as_image():
    keras.utils.plot_model(model, 'model_with_shape_info.png', show_shapes=True)

def main():
    download_images()
    learn_train_images()
    save_model_as_image()
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
2019-10-13 10:22:32.230260: I tensorflow/core/platform/cpu_feature_guard.cc:142] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2019-10-13 10:22:32.240660: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x7f8e0d673210 executing computations on platform Host. Devices:
2019-10-13 10:22:32.240672: I tensorflow/compiler/xla/service/service.cc:175]   StreamExecutor device (0): Host, Default Version
Model: "mnist_model"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
img (InputLayer)             [(None, 3072)]            0         
_________________________________________________________________
dense (Dense)                (None, 64)                196672    
_________________________________________________________________
dense_1 (Dense)              (None, 64)                4160      
_________________________________________________________________
dense_2 (Dense)              (None, 10)                650       
=================================================================
Total params: 201,482
Trainable params: 201,482
Non-trainable params: 0
_________________________________________________________________
Train on 40000 samples, validate on 10000 samples
Epoch 1/5
40000/40000 [==============================] - 8s 201us/sample - loss: 1.9575 - accuracy: 0.2751 - val_loss: 1.9360 - val_accuracy: 0.2759
Epoch 2/5
40000/40000 [==============================] - 8s 195us/sample - loss: 1.8635 - accuracy: 0.3169 - val_loss: 1.8657 - val_accuracy: 0.3192
Epoch 3/5
40000/40000 [==============================] - 8s 193us/sample - loss: 1.8384 - accuracy: 0.3300 - val_loss: 1.8205 - val_accuracy: 0.3412
Epoch 4/5
40000/40000 [==============================] - 8s 191us/sample - loss: 1.8234 - accuracy: 0.3364 - val_loss: 1.8472 - val_accuracy: 0.3291
Epoch 5/5
40000/40000 [==============================] - 8s 191us/sample - loss: 1.8065 - accuracy: 0.3422 - val_loss: 1.8488 - val_accuracy: 0.3312
10000/1 - 0s - loss: 1.6584 - accuracy: 0.3297
Test loss: 1.8290688621520996
Test accuracy: 0.3297
[0.02208202 0.04227012 0.02013903 0.3350343  0.01797167 0.44402105
 0.01911547 0.04697036 0.0417988  0.01059717]
 5
 3
 (3072,)
 (1, 3072)
 [[0.02208201 0.04227009 0.02013901 0.33503434 0.01797166 0.44402108
   0.01911546 0.04697033 0.04179878 0.01059716]]
```
### the first 25 train images and its label
![alt text](/assets/2019-10-13-tensorflow-keras-datasets-cifar10-classification-figure-1.png)

### the first 15 test images and inference result
![alt text](/assets/2019-10-13-tensorflow-keras-datasets-cifar10-classification-figure-2.png)

### only the fist test image and inference result
![alt text](/assets/2019-10-13-tensorflow-keras-datasets-cifar10-classification-figure-3.png)

## reference
[https://www.tensorflow.org/tutorials/keras/classification](https://www.tensorflow.org/tutorials/keras/classification)
[https://www.tensorflow.org/guide/keras/functional](https://www.tensorflow.org/guide/keras/functional)
