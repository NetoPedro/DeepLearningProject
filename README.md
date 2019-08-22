# DeepLearningProject

How to reproduce: 
```
Run all the cells on the jupyter notebook. 
```
Dependencies: 
- Python 
- Pytorch
- Scikit-Image 
- Scikit-Learn

## Project Description

This project was the final project of the course CS-E4890 - Deep Learning at Aalto University, Finland. The main goal was to implement some of the acquired knowledge during the course, try to push even further to new grounds and even try novel ideas.  

My goal for this project was to not only classify X-ray images as pneumonia or not pneumonia but also to detect opacities that are the cause of a positive classification. To achieve this goal with good enough results a few techniques were considered, and the pros and cons compared.  

The first idea was to try an object detection algorithm like [RetinaNet](https://arxiv.org/abs/1708.02002), [R-CNN](https://arxiv.org/abs/1311.2524) or even the improved version [Faster R-CNN](https://arxiv.org/abs/1506.01497). Nevertheless, I wanted to train the model just by using a CPU, ao I started to consider some simpler model for image segmentation. Hence, I came across the [U-Net](https://arxiv.org/abs/1505.04597), a this became the chosen approach.  It was not as fast as I would like on the CPU, but much faster than the other options, especially with some tweaks. 

In order to supply the network, it was also needed to build a loader responsible for loading the images on the fly, since the dataset is too large to fit as needed. Furthermore, it is needed some preprocessing and some feature engineering, for example, constructing a matrix mask with the size of the image and filled with 0's and 1's using the bounding boxes information detailed on the dataset. This implementation did not use any form of data augmentation, nevertheless, the positive effects of those techniques are well known and considered for a future version. 

A quick to the dataset distribution as also shown that only approximately 1 out of 3 images consisted of examples of pneumonia, this associated with a bounding box. There is also some information about the with and height of the opacities described in those examples.

This U-Net implementation is somewhat different from the original, in the first place, skip connections between blocks with the same resolution of the downsampler and upsampler do not exist here (although the may be added in future versions of the model).  Secondly, after some experimentation, it was found that replacing a convolutional upsampler with a Nearest Upsampler led to faster computations and lower false positives on the bounding boxes.  Instead of a reLU activation, LeakyReLU was used after convolutions as well as batch normalization (Instance normalization in this case since the batch size was 1). 

The optimization process required a combination of 2 loss functions. 


