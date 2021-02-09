# Kidney Cell Segmentation
The goal of this project is to identify glomeruli in images of kidney slices.
 
## Dataset:
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
