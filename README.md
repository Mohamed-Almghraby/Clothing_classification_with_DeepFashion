# Clothing_Classification__with_DeepFashion_Dataset

We propose a method of classifying fashion-wear based on apparels and their patterns using deep learning .
This helps in providing high-level features for clothing and can be used for matching user preferences. 
We obtained an accuracy of 91% using Pretrained models. 
We use Deepfashion  dataset that contain 10 differnt classes. T
he Fashion  training set contains 3,000 examples, and the test set contains 300 examples. The dataset used is at [this repo](https://github.com/alexeygrigorev/clothing-dataset)

# Overview_on_DeepFashion_Dataset

The DeepFashion dataset is a large-scale clothes database,which has several appealing features: Clothing Category and Attribute Prediction,
In-shop Clothes Retrieval Benchmark, Consumer-to-Shop Clothes Retrieval Benchmark, and Fashion Landmark Detection Benchmark,
collected by the Multimedia Lab at the Chinese University of Hong Kong. 
However, for our project, we’ll use only the Category  Prediction dataset because we’re going to work on  classifying clothing in existing images.
For this project, we made our own data subset, reducing the volume of images and category specificity, 
for simplicity and lower computation costs.
We reduced our classification from DeepFashion’s original 46 categories to 10 categories. Then, we selected 100-120 images from each of our simplified categories.

## Dataset Issues
The dataset contains 4000 images. 
The dataset is imbalanced at one category "T-shirt" as you can see from this hitogram 
![Data stastics](/Notebook_img/Data_histo.png)


The dataset contains 10 classes `['outwear','skirt', 'dress','shirt','hat','t-shirt','pants','longsleeve','shoes','shorts']![plot](/Notebook_img/classes.jpg)
so if u look at the data its so small and there a class imbalance at the T-shirt category , so we tried to solve this proplem in the Notebook using Focal loss![plot](/Notebook_img/Focal_loss_1.png)


# DataSet selection
this data set is small and have a class imbalance proplem , as we might see in the real world .
so i try to select data set with proplems so i can try to apply techniques to increse the model performance.
# Model selection
i tried to use two diffrent models , VGG16 , Xception and MobileNet 


# Training Phase
1. I tried sevral preprocessing technique to avoid overfitting and applied two model archticture , so i will explain what happend in 5 steps.
2. i tried to use Transfer learning `VGG-16` which is a pretrained model at imageNet dataset. so there are two approches 

the first one is fast and cheap but no Data Augmentation , the second one high cost and slow but u can apply Data Augmentation 

  so in first Approch:
     Running the convolutional base over our dataset, recording its output to a Numpy array on disk, then using this data as input to a standalone densely-connected classifier .
     This solution is very fast and cheap to run, because it only requires running the convolutional base once for every input image, 
     and the convolutional base is by far the most expensive part of the pipeline. However, for the exact same reason,
     this technique would not allow us to leverage data augmentation at all
     
  In the Second Approch:
     Extending the model we have (conv_base) by adding Dense layers on top, and running the whole thing end-to-end on the input data.
     This allows us to use data augmentation, because every input image is going through the convolutional base every time it is seen by the model. However, 
     for this same reason, this technique is far more expensive than the first one.
     
3. After that i tried to use fine tuning , by in freeaing some layers of the model - it doesnot helpes the performance that much 
4. I tried to use another model called xception it have more layers and skip connections and it applies seprable convolution in feature maps 
5. first by choose a small image size  and with out Data Augmentation it reches a good performance rather than the VGG
6. second by choosing a Larger iamge size and apply Data Augmentation it reaches a higher performance 
7. the Testing Accurasy on the last Xception model achieves `90%` ![Screenshot Capture - 2022-04-17 - 06-29-06](https://user-images.githubusercontent.com/47063541/163700503-8d3b6289-0ef8-4b95-8013-983a0e03ff28.png)
8. in the End i tried to use MobileNetV2 becauese its light weight and the model accursey isnot that far from xception model



# Results
1. The first Approach using VGG-16 achieves accuracy of `98%` on the Training and `85%` on the validation so this model is highly overfitting .
2. The Second approch using Data Augmentation the model achieves accuracy of `80%` on the Training and `80%` on the validation
3. after fine tuning some Layers the model achieves accuracy of `86%` on the Training and `84%` on the validation
4. in the Xception model achieve 94% on the trainng and 87% on the validation 
5. so the Final  xception modela achive 90% on the testing data
6. the MobileNet model achieves accuracy of `98%` on the Training and `8%` on the validation
7. the MobileNet achievees 88% on the test data 

![Screenshot Capture - 2022-04-17 - 07-23-52](https://user-images.githubusercontent.com/47063541/163701674-d4ba1188-2dba-4f2e-b160-e066c8d2852a.png)


