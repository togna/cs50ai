# GTSRB Neural Network

## Overview

This project trains and evaluates a neural network to recognize traffic signs based on the [German Traffic Sign Recognition Benchmark dataset](https://benchmark.ini.rub.de/gtsrb_news.html).

## Process and Analysis

The first thing I tried was a single-layer network consisting only of the flattened inputs and output layer on a small subset of the data. The accuracy was 99.7% but loss was 0.4306, so while most images in the test set were correctly categorized, but the few images that were incorrectly predicted were off significantly. It seemed like a great start, but after running on the full dataset the accuracy was reduced to 78.29% and loss up to 40.4114. That meant it was time to add more layers and see if we could improve the results.

Adding a 3x3 32-filter convolutional layer increased accuracy to 90.09% and decreased loss to 1.069, a huge step in the right direction! Adding a 2x2 max pooling layer sped up training, but also surprisingly increased accuracy to 93.28% and decreased loss to 0.5625, showing that there may have been some overfitting without the pooling.  

Adding a hidden layer with 128 nodes actually slightly decreased accuracy to 92.61% and loss to 0.5783, which was unexpected. I reran the same exact experiment again yielded 91.08% accuracy and 0.6729 loss, showing that there is some variability between runs. It's hard to draw conclusions from just one run and I would benefit from doing each run multiple times and looking at an average. Still, adding the hidden layer seems to have provided no benefit.  

Next, I tried adding a 50% dropout to the hidden layer in case there was overfitting happening there. This absolutely ruined accuracy, bringing it down to an abysmal 5.4% and increasing loss to 3.5023. I think it's likely some nodes were not being trained since I was only doing 10 epochs, so I tried decreasing the dropout to 10%. This got accuracy back up to 90.14% and loss down to 0.4007. Reducing the number of nodes in the hidden layer to 64 again tanked accuracy down to 38.09% and increased loss to 2.0093. Adding an identical second hidden layer helped get accuracy back up to 67.5% and loss down to 1.0866. Doubling the size of both hidden layers boosted accuracy to 92.62% and reduced loss to 0.3353.  

Finally, I tried removing the hidden layers completely and adding another round of convolution and pooling. Accuracy was 93.16% and loss 0.3879, showing no real benefits for these additional layers. In one final attempt, I removed the additional convolutional and pooling layers and added back in the hidden layers, this time with a 20% dropout. Results were comparable with 86.76% accuracy and 0.4673 loss. It seemed like the best loss value came with 2 hidden layers using 10% dropout, so I tried that one more time and got an accuracy of 77.51% and loss of 0.7152, showing that variability is very high.  

The high variability with the hidden layers was unexpected, so I went back to zero hidden layers with just one convolution and pooling layer. This brought accuracy back up to 93.28% and loss to 0.7255. In an effort to reduce the loss, I added back one 128-node hidden layer with 10% dropout, as that seemed to be the sweet spot in prior testing. In this final test, I observed 93.88% accuracy and 0.2935 loss. This was the lowest loss thus far, and this configuration seemed to consistently deliver low loss, so it was submitted.