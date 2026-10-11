# projetIA

## Step 1: Introduction to CNNs
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

## Step 3: Build your own CNN Model

### How many parameters does our model have:

To calculate the number of parameters in our model, we first need to identify the different types of layers it contains.

Our CNN consists of:
- 4 convolutional layers (Conv2D), with 32, 64, 128, and 256 filters respectively.
- 4 MaxPooling layers, each using a 2 × 2 window.
- 1 Flatten layer, which transforms the feature maps into a one-dimensional array.
- 2 fully connected layers (Dense), containing 128 and 1 neuron respectively.
- 1 Dropout layer, with a dropout rate of 50%.

The formulas to calculate the parameters for each layers are the following.

#### Convolutional layers:

$$P = (K_h\times K_w \times C_{in} + 1) \times F$$
Where:

- $K_h$ and $K_w$ are the height and width of each filter.
- $C_{in}$ is the number of input channels.
- $F$ is the number of filters.
- The additional 1 represents the bias associated with each filter.

##### First convolutional layer:
- Filter size: 3x3
- Input channels: 3 (Since it's RGB)
- Numbers of filters: 32

$$P1 = (3 \times 3 \times 3 + 1) \times 32 = 896$$

##### Second convolutional layer:
- Filter size: 3x3
- Input channels: 32 (From the previous layer)
- Numbers of filters: 64

$$P1 = (3 \times 3 \times 32 + 1) \times 64 = 18496$$

##### Third convolutional layer:
- Filter size: 3x3
- Input channels: 64
- Numbers of filters: 128

$$P1 = (3 \times 3 \times 64 + 1) \times 128 = 73856$$

##### Fourth convolutional layer:
- Filter size: 3x3
- Input channels: 128
- Numbers of filters: 256

$$P1 = (3 \times 3 \times 128 + 1) \times 256 = 295168$$

#### Maxpooling and Flatten layers:
These layers have 0 trainable parameters. MaxPooling reduces the size of feature maps, Flatten reorganizes them into a one-dimensional array.

#### Fully connected layers:

$$P = (N_{in} + 1) \times N_{out}$$

Where:

- $N_{in}$ is the number of input values.
- $N_{out}$ is the number of neurons.
- The additional 1 represents the bias associated with each neuron.

##### First Dense layer (128 neurons):

After the final MaxPooling layer, the feature maps have dimensions of $7 \times 7 \times 256$.

The Flatten layer therefore produces:

$$N_{in} = 7 \times 7 \times 256 = 12,544$$

$$P = (12,544 + 1) \times 128 = 1,605,760$$

##### Second Dense layer (1 neuron):

$$P = (128 + 1) \times 1 = 129$$

#### Total number of parameters:

$$P_{total} = P_{Conv2D} + P_{Dense1} + P_{Dense2}$$

$$P_{total} = 388,416 + 1,605,760 + 129$$

$$\boxed{P_{total} = 1,994,305}$$

#### Choice of optimizer and loss function

We chose Adam as our optimizer because it automatically adjusts the learning rate for each parameter during training, allowing the model to learn efficiently.

We chose binary cross-entropy as our loss function because we are dealing with a binary classification problem (cats and dogs). It measures the difference between the predicted probabilities and the actual labels, penalizing incorrect predictions.

Finally, we use accuracy as our evaluation metric, which represents the proportion of images correctly classified by our CNN.

## Step 4: Train the model

We trained our CNN for 10 epochs, using a batch size of 100 images
During training, accuracy increased from approximately 53% to 76%, while validation accuracy increased from 60% to 73%. Both training and validation loss also decreased throughout the process.

We can observe a small gap between training and validation accuracy during the final epochs, suggesting early signs of overfitting. However, since validation accuracy continues increasing and validation loss continues decreasing, the model does not appear to be significantly overfitting yet.

Overall, the model is learning useful features, although its accuracy leaves room for improvement.

## Step 5: Evaluate the Model on the test set

We evaluated our CNN on the test set containing 400 images.
The results were:
- Accuracy: 73.5%
- Precision: 73.5%
- Recall: 73.5%
- F1-score: 73.5%

Overall, the CNN has learned to distinguish cats from dogs, but its performance leaves room for improvement.

## Step 6: Attempt to improve the model

### Data augmentation:
We applied random rotations, shifts, zooms, and horizontal flips to the training images to increase their diversity.

After 10 epochs, the augmented CNN achieved a maximum validation accuracy of 65.7%, compared to 72.7% for the baseline model.

Data augmentation therefore did not improve performance in this experiment, with a decrease of 7 percentage points. One possible explanation is that the transformations made training more difficult, and the model may require additional epochs to benefit from them.

### Dropout
We added a Dropout layer with a rate of 0.5 to reduce overfitting by randomly deactivating 50% of its inputs during training.

After 10 epochs, the model achieved a maximum validation accuracy of 67.2%, compared to 72.7% for the baseline.

Dropout therefore did not improve performance in this experiment. Since our baseline model showed limited signs of overfitting, the additional regularization may have slowed down learning.

### Batch normalization
We added Batch Normalization layers after each convolutional layer to stabilize the training process.

After 10 epochs, the model achieved a maximum validation accuracy of 53.5%, compared to 72.7% for the baseline model.

Despite reaching approximately 86.4% training accuracy, validation accuracy remained close to 50%. This suggests a significant generalization problem, potentially caused by overfitting or differences between the Batch Normalization statistics used during training and validation.

### Conclusion
Overall, none of the three techniques improved our CNN's performance. The baseline model remained the best-performing configuration, achieving 72.7% validation accuracy.

However, this does not mean these techniques are ineffective. Their performance depends on the model architecture, the dataset, and the training conditions. Since we only trained each model for 10 epochs, further experimentation could produce different results.
