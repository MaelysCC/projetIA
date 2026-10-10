# projetIA

## Part 1
### What is a Convolutional Neural Network (CNN)?

A Convolutional Neural Network, is a type of artificial neural network that is specialized in processing images. It learns to recognize spatial patterns within images by analyzing their pixel values, represented by RGB channels. The imaeges are processed through successive layers that can learn increasingly complex features.

During the training, the CNN makes predictions, and compares them to the correct labels. Based on the error, it then adjusts the filters and other parameters to gradually improve its ability to classify images. 

### What are the convolutional layers

Convolutional layers are components of a Convolutional Neural Network. They are used to extract features from an image. They use small matrices called filters that move across the image, analyzing small regions of pixels at a time.

Each filter produces a feature map, which indicates how strongly the filter responds to certain patterns in different regions of the image. And those filters evolve during the training process, as their weights are adjusted based on the model's prediction error. This allows them to be better at detecting useful patterns.

A convolutional layer can also contain multiple filters, with their own feature map. This means that each of these filters can learn different types of patterns. One could learn edges, another could learn shapes, another could learn textures. And as information passes through the deeper layers, the network can learn increasingly complex pattern like combinations of features.

### What are the pooling layers

Pooling layers process the feature maps produced by convolutional layers, using a small window that moves across each feature map.
Unlike convolutional layers, their goal is not to detect new patterns. 

Instead, MaxPooling takes the highest value within the window at each position and keeps only that value.

Unlike convolutional layers, pooling layers do not aim to detect new patterns. Instead, MaxPooling takes the highest value within each small window of a feature map and keeps only that value.

Pooling layers are usually placed between convolutional layers. This allows the next convolutional layer to work with smaller feature maps, reducing computational cost while still preserving the strongest responses to previously detected patterns. The following convolutional layer can then use this information to learn more complex features.

### What are activation functions
Activation functions are mathematical functions that modify the values produced by a layer of a neural network before passing them to the next one.

They are important because, without them, even a network with many layers would be limited to relatively simple mathematical relationships. Activation functions allow the network to learn more complicated patterns, which is essential when trying to recognize objects in images.

There are several types of activation functions, such as ReLU, Sigmoid, Tanh, Leaky ReLU, Softmax, and GELU.

### What are fully connected layers
Fully connected layers are usually placed near the end of a CNN. Their purpose is to use the features detected by the previous layers to make a final prediction.

In these layers, each neuron is connected to every neuron from the previous layer. This allows the network to combine the different features it has learned to help recognize what is present in the image.