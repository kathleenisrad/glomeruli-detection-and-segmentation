# Glomeruli Detection and Segmentation
The goal of this project is to identify glomeruli in images of kidney slices.  
I used both Faster R-CNN and Mask R-CNN and compare their performances below.  

## Results:
| Model | Epochs Trained | Learning Rate | Weight Decay | Momentum | Step Size | Training Images | Testing Images | mAP | Total Time |
|-------|----------------|---------------|--------------|----------|-----------|-----------------|----------------|-----|------------|
|Faster R-CNN| 10 | 0.0001 | 0.001 | 0.9 | 3 | 1597 |200 | 0.576 | 1hr 50min |
|Mask R-CNN | 1 | 0.001 | 0.1 | 0.9 | 3 | 1597 | 200 | 0.514 |13min 31sec |
 
<br>
<br>

### Faster R-CNN Results:
### <a href="https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/code/02-faster-rcnn-pytorch.ipynb"> > EDA NOTEBOOK < </a>  
Sample image from the training images, that was split into training and testing sets.  
Black boxes are ground truth, white boxes are my model's predictions:  
<img src = "https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/assets/test1.jpg">

Sample image from the testing images (no ground truth):  
<img src="https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/assets/test2.jpg">  
<br>
<br>


### Mask R-CNN Results:
### <a href="https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/code/05-mask-rcnn-pytorch.ipynb"> > EDA NOTEBOOK < </a>  

Sample image from the training images, that was split into training and testing sets.  
Black box is ground truth, grey box is my model's prediction, mask is the aurora colored part:  

<img src = "https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/assets/test3.jpg">


## Dataset:
8 training images and 5 testing images were provided.  

The original images were too large to push onto github. They can be downloaded from here:  
https://www.kaggle.com/c/hubmap-kidney-segmentation/data


## File Structure: 
My folders are organized a little differently than the way the original zip file is organized.  
You will need to move the training and test images to the locations listed below in order for the code to work.  
My code will eventually add additional folders called masks, grey and slices.  

<br>
<pre>[me@home]$ tree main  
<b>main</b>
├── code  
├── CSVs
|   └── <b>ORIGINAL CSVs GO HERE</b> 
├── test  
│   ├── images  
│   │   └── <b>ORIGINAL TEST IMAGES GO HERE</b>  
│   │
│   └── JSONs      
│       └── <b>ORIGINAL TEST JSON FILES GO HERE  </b> 
│       
└── train  
    ├── images  
    │   └── <b>ORIGINAL TRAIN IMAGES GO HERE</b>   
    │    
    └── JSONs     
        └── <b>ORIGINAL TRAIN JSON FILES GO HERE</b>  </pre>


## EDA:
### <a href="https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/code/00-kidney-images-EDA.ipynb"> > EDA NOTEBOOK < </a>  
I performed some exploratory data analysis on the original images to familiarize myself with the dataset.  
The jupyter notebook for EDA is included.   
Each image was gigantic — many were over 1GB, and the largest was a whopping 4GB! — and so my computer wasn’t able to open the images using a traditional image viewer. So instead, I resized each image and plotted them:

<img src = "https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/assets/slices.jpg">  
<br>
Next, I visualized the masks. The masks provided were actually RLE encoded representations, and someone was nice enough to post the function they made to turn the RLE image into a numpy array. I then took this numpy array and turned it into an image:  
<br>
<img src = "https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/assets/masks.jpg">
<br>
<br>
I overlaid these masks on the images to see my target cells:

<img src = "https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/assets/overlay.jpg">

<br>
<br>
Here is a close up of the targets:
<img src = "https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/assets/zoomed.jpg">

<br>

## Preprocessing the images:
### <a href="https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/code/01-preprocessing-kidney-images.ipynb"> > PREPROCESSING NOTEBOOK < </a>  


Steps I took to prepare my images for training:
 - I resized both training and testing to about 50%, then turned them into greyscale in an effort to make their file sizes a bit smaller.  
 - Sliced the resulting images either 16x16 or 32x32, depending on image dimensions.  
   - Example slice:  
       <img src = "https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/assets/examplemaskslice.jpg">  
 - Resized and sliced the masks to match the training images. Then I deleted all the slices from the masks and training images that didn't have any target cells.  
 - Turned each instance in each mask slice into a different color:  
     <img src="https://github.com/kathleenisrad/glomeruli-detection-and-segmentation/blob/main/assets/recoloredmasks.jpg">
 - Made bounding boxes around each instance and recorded the x and y coordinates for each bounding box in a CSV.  
