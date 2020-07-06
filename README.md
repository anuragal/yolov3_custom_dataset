# Training Custom Dataset on Colab for YoloV3

## Objectives

1. Collect a dataset of 500 images and annotate them. Please select a class for which you can find a YouTube video as well.
2. Download a very small (~10-30sec) video from youtube which shows your class.
3. Use ffmpeg (Links to an external site.) to extract frames from the video.
4. Inter on these images using detect.py file. **Modify** detect.py file if your file names do not match the ones mentioned on GitHub. 
      `python detect.py --conf-thres 0.3 --output output_folder_name`
5. Use ffmpeg (Links to an external site.) to convert the files in your output folder to video
6. Upload the video to YouTube. 
7. Share the link to your GitHub project with the steps as mentioned above
8. Share the link of your YouTube video

## Class: `eyeglasses`

Downloaded [500 pictures](https://github.com/anuragal/yolov3_custom_dataset/tree/master/data/customdata) having eyeglasses in them. Pictures include only eyeglasses, people wearing eyeglasses & animals wearing eyeglasses.

### Example pictures

<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/data/customdata/images/eyeglass001.jpg" height="10%" width="10%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/data/customdata/images/eyeglass002.jpg" height="24%" width="24%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/data/customdata/images/eyeglass004.jpg" height="24%" width="24%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/data/customdata/images/eyeglass504.jpg" height="24%" width="24%" ></a>

## Annotation

Annotated all 500 images using tool [yolo label](https://github.com/developer0hye/Yolo_Label)

## Steps to run on colab

### Directory Structure
    yolov3
      --utils                           # From this repo
        --datasets.py
        --....
        --...
      --data                            # Create of your own
        --customdata                    
          --images/                     # Add all annotated images in this folder
            --img001.jpg
            --img002.jpg
            --...
          --labels/                     # Add all annotated image labels in this folder
            --img001.txt
            --img002.txt
            --...
          custom.data                   # data file
          custom.names                  # your class names
          custom.txt                    # list of name of the images you want your network to be trained on. Currently we are using same file for test/train
        --cfg
          --yolov3-custom.cfg           # Yolo configuration file get it from https://github.com/pjreddie/darknet/blob/master/cfg/yolov3-spp.cfg
      --weights
        --yolov3-spp-ultralytics.pt     # Weights file get it from https://drive.google.com/drive/folders/1LezFG5g3BCW6iYaV89B2i64cqEUZD7e0
        --best.pt                       # This will be created at the time of execution, make sure to save it after execution
        --last.pt                       # This will be created at the time of execution
      --output                          # Create empty folder for saving predicted images
        --
      --predict                         # Add images to be predicted in this folder
        --
      --train.py                        # From this repo
      --test.py                         # From this repo
      --models.py                       # From this repo
      --detect.py                       # From this repo
      
      
      

## Results

### Predicted Images
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/out_put/image-2764.png" height="49%" width="49%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/out_put/image-2771.png" height="49%" width="49%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/out_put/image-2777.png" height="49%" width="49%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/out_put/image-481.png" height="49%" width="49%" ></a>


### Youtube Video

[![](https://github.com/anuragal/yolov3_custom_dataset/blob/master/out_put/youtube.png)](https://www.youtube.com/watch?v=T-Bfob8iY3k)

