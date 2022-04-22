# activation_maximization_dataset
In this repo I explore the activation maximization technique of convnets and produce a dataset of activation maximization filters. The general idea is to optimize an image in such a way that the response of a filter is maximized. This let us see what each filter is "looking for" in the image during the classification process. 

I decide to produce a new dataset, by computing the activation maximization for every filter in the VGG16 convoluted network, using imagenet pretrained weights. 

The obtianed dataset is made of 4224 images, and its publicly available on kaggle.

[VGG16 filter activations dataset](https://www.kaggle.com/datasets/fastrmerizivic/vgg16-filter-activations)

## files summary

1) computing_filter_activations.ipynb, compute the maximum activations
2) how-random-are-you.ipynb, calculate our index for all the filters

## some sample filters from the dataset

![](https://github.com/fmerizzi/activation_maximization_dataset/blob/main/images/filter-114.png)
![](https://github.com/fmerizzi/activation_maximization_dataset/blob/main/images/filter-124.png)
![](https://github.com/fmerizzi/activation_maximization_dataset/blob/main/images/filter-21.png)
![](https://github.com/fmerizzi/activation_maximization_dataset/blob/main/images/filter-22.png)
![](https://github.com/fmerizzi/activation_maximization_dataset/blob/main/images/filter-25.png)


## studying the filters
Its an interesting task to study the obtained filters, or trying to classify them. 
Simple tests revealed that trying to classify filters (guessing the convoluted layer they belong to) is a hard task for traditional convoluted network. we could say that convents struggle to classify their own filters.

but the general question still stands, __what does it mean for a convnet to be good at classifying its own filters?__

Another approach is to study the pixel distributions for the filter's activation maximization. 

for each filter we compute a value described as follows:

1) compute the histogram of pixel values for each color channel
2) for each comlumn calculate the absolute difference from a uniform distributed image (straigth histogram)
3) caluclate the mean of all the differences, and then the mean for the 3 color channels

what we obtain is an index measuring the "distance" of the image from a normal distributed image. we normalize in such a way that 0 is a normal distributed image, and 1 is an image where all the pixel have the same value.

I calculate this index for all the 4224 filter, and group the result for convoluted layer, 12 in total. 
We can see that the index vary considerably troughout the network. Starting with uniform images and progressivly setting to a distribution described by our index as value of ~0.46. 

The following image contains the final results, with all the filters for the 13 layers. Each group of layers have the same color, the number of filters also vary in the layers. 

![comapring layers](https://github.com/fmerizzi/activation_maximization_dataset/blob/main/images/final_comparison.png)
