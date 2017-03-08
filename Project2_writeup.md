## Data Set Summary & Exploration
### 1. Overview
The following document describes the Jupyter notebook 
that implements my traffic sign classifier. 
[This](https://github.com/JPWILSON/JPWILSON-Self-Driving-Car-Project2-/blob/master/Traffic_Sign_Classifier.ipynb) is a link to my notebook. 
* My training set has 26 099 images
* My testing set has 12630
* My validation set has 8700, or, 25% of the original training set.
* The shape of each image is: (32, 32, 3). That is, a height and width of 32px each, and 3 color channels. 
* The number of unique classes is 43. That is, 43 different sign classifications are possible. 

### 2. Visualization

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
### 4. Optimizer details
I made use of the Adam optimizer, but only because David mentioned in the project description that it was more efficient. 

### 5. Results
I made several runs, fine tuning the hyperparameters. 
I increased the number of epochs iteratively and found the accuracy increasing with each one, unitl with 16 epochs, the accuracy started to decrease. I determined that, with the batch soze of 
128 and learn rate (rate) of 0.00096, I got a validation accuracy of 0.962 for epoch 14. I then changed back down to 14 epochs, which led to a drop in accuracy, but after re-running a few times, both Epoch 13 and 14 achived identical validation accuracies of 0.958, which is not as high as an earlier training version, but is still higher than the required 93%. 

## Testing on new images
### 1. Traffic Signs chosen 
The instructions were to find at least 5 signs, so I just did some googling and found 6 signs. All in color. I made sure they were as 'head-on' as possible. I manually cropped the images, made sure the signs were in the centre of the screen (although I assume from my understanding during the lectures, that the convnet architecture is translation invariant, so I may come back and use images that are not centered). 

The six signs were plotted in the notebook. They were: 
* 12 Priority Road
* 17 No entry
* 18 General Caution
* 39 Keep Left
* 40 Roundabout
* 4 Speed Limit 70km/h

### 2. Predictions
I obtained an accuracy of 83.33%. That is, my model got five of the signs correct, and two of them wrong. 
The incorrectly labeled sign was: 
 
* 39 Keep Left, it was incorrectly labeled by my classifier as 40, the roundabout. I think that, had I implemented grayscale, this would be resolved. The 5 top_k predictions did however include the correct label, as seen in the notebook.   


