# activation_maximization_dataset
In this repo I explore the activation maximization technique of convnets and produce a dataset of activation maximization filters

- Using the VGG16 network with pretrained weights from imagenet 
- produce a full dataset of all activation from all the filters of all the layers

### In the following image the final result are reported
An index measuring the distance from a uniform random distribution image is calculated for every filter. 1 represent an image with all the pixel of the same value, zero represent an image with a uniform distribution of pixels. The results are grouped for convoluted layer, for all 12 layers.
![comapring layers](https://github.com/fmerizzi/activation_maximization_dataset/blob/main/images/final_comparison.png)
