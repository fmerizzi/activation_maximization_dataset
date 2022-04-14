# activation_maximization_dataset
In this repo I explore the activation maximization technique of convnets and produce a dataset of activation maximization filters. The general idea is to optimize an image in such a way that the response of a filter is maximizied. This let us see what each filter is "looking for" during the classification process. 

I decide to produce a new dataset, by computing the activation maximization for every filter in the VGG16 convoluted network, using imagenet pretrained weights. 

The obtianed dataset is made of 4224 images, and its publicly available on kaggle.
[dataset](https://www.kaggle.com/datasets/fastrmerizivic/vgg16-filter-activations)

## studying the filters
Its an interesting task to study the obtained filters, or trying to classify them. 
Simple tests revealed that trying to classify filters (guessing the convoluted layer they belong) is a hard task for traditional convoluted network. we could say that convents struggle to classify their own filters.

but the general question still stands, __what does it mean for a convnet to be good at classifying its own filters?__

Another approach is to study the pixel distributions for the filters. 

for each filter compute a value described as follows:

1) compute the histogram of pixel values for each color channel
2) for each comlumn calculate the abs difference from a uniform distributed image
3) caluclate the mean of all the differences, and then the mean of the 3 color channels

what we obtain is an index measuring the "distance" of the image from a normal distributed image. we normalize in such a way that 0 is a normal distributed image, and 1 is an image where all the pixel have the same value.

I calculate this index for all the 4224 filter, and group the result for convoluted layer, 12 in total. 
We can see that the index vary cinsiderably trough the network. Starting with uniform images and progressivly setting to a distribution described by our index as value of 0.44. 
The following image contains the final results:

![comapring layers](https://github.com/fmerizzi/activation_maximization_dataset/blob/main/images/final_comparison.png)
