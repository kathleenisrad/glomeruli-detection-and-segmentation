# Glomeruli Detection and Segmentation
The goal of this project is to identify glomeruli in images of kidney slices.  
I used both Faster R-CNN and Mask R-CNN and compare their performances below.  
 
## Dataset:
8 training images and 5 testing images were provided.  

The original images were too large to push onto github. They can be downloaded from here:  
https://www.kaggle.com/c/hubmap-kidney-segmentation/data


## File Structure 
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
