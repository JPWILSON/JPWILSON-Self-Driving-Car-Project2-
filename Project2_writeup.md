## Data Set Summary & Exploration
### 1. Abstract
The following document describes the LeNet-5 classifier I implemented for German Traffic sign classification.
[This](https://github.com/JPWILSON/JPWILSON-Self-Driving-Car-Project2-/blob/master/Traffic_Sign_Classifier.ipynb) is a link to my notebook.

### 2. Input Data Description
* My training set has 26 099 images
* My testing set has 12630
* My validation set has 8700, or, 25% of the original training set.
* The shape of each image is: (32, 32, 3). That is, a height and width of 32px each, and 3 color channels. 
* The number of unique classes is 43. That is, 43 different sign classifications are possible. 

### 3. Visualization
A histogram displaying the distribution of the various labels among the data set is plotted. It shows that there is quite an uneven distribution. That is, there are many of certain signs and very few examples of other signs. This means that the model may generalize certain signs (that there are many more of them to learn from) a lot better than other signs. 

In addition, a random sign is plotted, as well as its label, just to make sure that everything is working correctly. 

## Model Acrhitecture and Testing

### 1. Image processing
A grayscale method is included, but, as I have a high enough accuracy, I will not grayscale the pictures. 
May do this at a later stage, but conceptually, it doesn't really make sense to me on a fundamental level. I understand that the grayscale allows for a 
clearer highlighting of edges (and also that it increases the performance (and is even recommended and used Sermanet & LeCun's paper on traffic signsin http://yann.lecun.com/exdb/publis/pdf/sermanet-ijcnn-11.pdf)). It just seems incorrect that traffic signs (that make use of color for conveying meaning (otherwise they would all be blue&white/ red& white, etc) should be reduced to grayscale.)
I think the computer can also gain meaning from the color, in the same way humans do, even if not in this particular example. 

### 2. Training, Validation and Testing 
I normalised the the data.

### 3. Model Architecture
I did not add any dropout, or implement any other changes, I simply made use of LeNet-5, and have listed the layers in the notebook. If I get ahead of schedule I will revisit this and add further architecture to improve the network. 
A description of the architecture is as follows: 

## Implement the LeNet-5 neural network architecture.
I will just use the LeNet-5 Architecture as outlined in the lessons for now...
Not sure if required, but it is described below: 

**Input**
The LeNet architecture accepts a 32x32xC image as input, where C is the number of color channels. Since MNIST images are grayscale, C is 1 in this case.

**Architecture**

**Layer 1: Convolutional.** The output shape should be 28x28x6.

**Activation.** Your choice of activation function.

**Pooling. **The output shape should be 14x14x6.

**Layer 2: Convolutional. **The output shape should be 10x10x16.

**Activation.** Your choice of activation function.

**Pooling.** The output shape should be 5x5x16.

**Flatten.** Flatten the output shape of the final pooling layer such 
that it's 1D instead of 3D. The easiest way to do is by using tf.contrib.layers.flatten, 
which is already imported for you.

**Layer 3: Fully Connected.** This should have 120 outputs.

**Activation.** Your choice of activation function.

**Layer 4: Fully Connected.** This should have 84 outputs.

**Activation.** Your choice of activation function.

**Layer 5: Fully Connected (Logits).** This should have 10 outputs.

#### Output:
Return the result of the 2nd fully connected layer.

### 4. Optimizer details
I made use of the Adaptive Moment Estimation (Adam) optimizer, which computes adaptive learning rates, and stores exponentially
decaying average of past squared gradients. Fundamentally, this is just a way to ensure that a false minimum is not 
mistakenly interpreted, by making use of momentum. Stochastic gradient descent encounters this problem, and that is why Adam is chosen over it. 

### 5. Results
**Validation**
I made several runs, fine tuning the hyperparameters. 
I increased the number of epochs iteratively and found the accuracy increasing with each one, unitl with 16 epochs, the accuracy started to decrease. I determined that, with the batch soze of 
128 and learn rate (rate) of 0.00096, I got a validation accuracy of 0.962 for epoch 14. I then changed back down to 14 epochs, which led to a drop in accuracy, but after re-running a few times, I got Epoch 14's validation accuracy to 0.959, which is just under the higher accuracy I had gotten earlier and therefore not the optimum, but is still higher than the required 93% and therefore sufficient. 

**Test Set**
Running my model on the test set, I obtained an accuracy of 98.329%. 

## Testing on new images
### 1. New Data: Description of Traffic Signs Chosen 
The instructions were to find at least 5 signs, so I just did some googling and found 6 signs. 

The six signs were plotted in the notebook. They were, in order of plotting: 
* 12 Priority Road
* 17 No entry
* 18 General Caution
* 39 Keep Left
* 40 Roundabout
* 4 Speed Limit 70km/h

Notable attributes/ qualities of the images of signs: 
* All in color. 
* The constrast for many of the signs (4) was high, having in 3 of them a white background (and one, yellow - 70km/h sign). 
* The brightness for all of the signs is high.
* I looked for images of signs that were as 'head-on' as possible. 
* I manually cropped the images, made sure the signs were in the centre of the screen (although I assume from my understanding during the lectures, that the convnet architecture is translation invariant, so I may come back and use images that are not centered). 
* Two of the signs are similar in that they are both blue, and both have a white, left pointing arrow ('roundabout' and 'keep left'). This may cause the classifier to have some trouble differentiating between them. 


### 2. Predictions
Running my model on the newly inputted signs, the model calssified four of the 6 signs correctly. 
That is, my model incorrectly labeled the "18-General Caution" "39 Keep Left" signs 
as "26 Traffic Signals" and "38 Keep right" respectively.

This result is inconsistent when compared to the 96% validation accuracy and 98.329 testing accuracy of the model.

The top five softmax predictions show almost ~100% for each of the images, and negligable certainty for the remaining four predictions, except in the case of the general caution image, where there is a 4.2% probabilty for the correct sign. The bar chart is therefore not useful except in this case, although included. The printed out top 5 probabilites can be read and in some cases are so close to zero it requires 29 zeros from the decimal to see the value. 
What is troubling is that the bar chart shows this certainty for the wrong sign (Keep Left) and doesn't have the correct sign in its tops 5 predictions. 

It must be noted that I had initially gotten 100% accuracy, and mistakenly restested while plotting the softmax probs and this dropped the accuracy. I then retrained the model but again got only 66% accuracy. Clearly my model needs some work. 

**Concluding on the testing of the new images**, comparing the accuracy of my model's performance on the new data to the validation and test set accuracy, it is not possible to accurately rate it. This is because I should be testing on a lot more than just 6 images. At best, it can be said that the model classifies new signs correclty "4 out of 6 times".



