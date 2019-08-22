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

In order to supply the network, it was also needed to build a loader responsible for loading the images on the fly, since the dataset is too large to fit as needed. Furthermore, it is needed some preprocessing and some feature engineering, for example, constructing a matrix mask with the size of the image and filled with 0's and 1's using the bounding boxes information detailed on the dataset. 
