# Fire_Risk
This project aims at using a ResNet 18 Model to train and test the Fire Risk dataset.

THE DATASET:
The original Fire Risk dataset was created aiming at predicting the level of risk for the Forest Fire to occur at a particular landscape just by looking at the picture of the landscape. 

First, the used the Wildfire Hazard Potential(WHP) map from the USDA Forest Service, which already classified the lans based on vegetation, fuel and weather models. Then they use National Agriculture Imagery Program(NAIP) images to get the high resolution aerial images of those exact locations and cropped a 270x270 pixel image as from the aerial photos centered at the centroid.

These series of 270x270 make the Fire Risk dataset, divided into 7 classes('High','Low','Water','Very_high','Very_Low','Moderate','Non-Burnable'). Each image occurs along with it's labels 'pairs of two'.

THE MODEL:
We use the outline of a ResNet50 Model (shown in the PyTorch video tutorial) and alter it to fit the ResNet18 model. We First declare a class 'block' to define all the convolutional layer blocks in ResNet architecture. In case of ResNet50, each block uses a 'bottleneck' apporoach, to first reduce the dimensions , perform feature extraction and then restoring the dimensions, each of these done by a convolution layer. 

This approach is very much helpful in reducing the loss of data in deeper networks. In case of ResNet18, we don't use all those, we keep it simple, as we do not have a deep network to train.Every block uses only 2 convolutional layers insetad of 3, repeated twice. 

The ResNet class remains mostly the same. It is used to create all the layers before and after the blocks. It also calls another function called 'make_layers' to actually make the layers in the ResNet block.
The actual ResNet architecture comes in these layers. Here is where we do the layer skipping idea and identity downsampling.

THE TRAINING:
Eventhough the paper suggests a transfer learning approach by using the Pre-Trained ResNet18 model on the imagenet dataset, we try to do the training first from scratch then compare the results with the transfer learning approach.

We use the normal training apporach of forward,loss,backward,optimization,weight updation. We define all this in a single function and then call this function through a loop multiple times.

THE RESULTS:
Since we have used the resized 224x224 images instead of the original 270x270 images, our training maybe a little inefficient on predicting for real life data and making decisions from them. This was done to stick to the standard ResNet18 model which expects a 224x224 images. According to the paper, the maximum accuracy that the models were able to achieve was 65.29% ( by transfer learning approach). By using ResNet50 the accuaracy was around 63.20%. 
Our ResNet18 model acieves a maximum accuracy of 59.30%. Eventhough the validation accuracy is fluctuating, we see a steady decrease in the fluctuation loss, which is evident from the graphs given.

FUTURE GOALS:
To compare this result with using 270x270 pixel images(as suggested in the paper) as input. And also with the pre-trained ResNet18 model on the ImageNet dataset.

REFERENCES:
1) ResNet Youtube Tutorials: https://www.youtube.com/watch?v=DkNIBBBvcPs
2) https://github.com/NaveenPaluru/OCT-NRSD
3) Fire_Risk Research Paper sent by Mam.(Uploaded here)


