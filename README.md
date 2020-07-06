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
    yolov3_custom_dataset
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
      
### Data folder
Add all annotated images into `/data/customdata/images` folder & add all labels into `/data/customdata/labels` folder

#### custom.data
For single class object detection add `classes=1`. Add paths of corresponding folders.

      classes=1
      train=data/customdata/custom.txt
      valid=data/customdata/custom.txt
      names=data/customdata/custom.names

If `train` and `test` data are different then provide seperate paths for them

#### custom.names
Custom object class

    eyeglasses

#### custom.txt
List of all the images in below format. Doble check the paths

    ./data/customdata/images/eyeglass001.jpg
    ./data/customdata/images/eyeglass002.jpg
    ./data/customdata/images/eyeglass003.png

### cfg folder
Download [yolov3-spp.cfg](https://github.com/pjreddie/darknet/blob/master/cfg/yolov3-spp.cfg) file and rename it to `yolov3-custom.cfg`. Make following changes to your file (search and change on all places)

      classes = 1
      filters = 18                  # 18 = (4+1+1)*3
      burn_in = 100 
      max_batches = 5000 
      steps = 4000, 4500
      
### Weights Folder
Download `yolov3-spp-ultralytics.pt` from [location](https://drive.google.com/drive/folders/1LezFG5g3BCW6iYaV89B2i64cqEUZD7e0) and put it in this folder. While model execution `best.pt` and `last.pt` will be added into this folder. Make sure to save `best.pt` as this will be used to predict the objects in image files later

### Predict & Output folder
`Predict`: Input Images to be predicted
`Output`: Predicted images by the model

#### Images for prediction

1. Download a very small (~10-30sec) video from youtube which shows your class.
2. Use [ffmpeg](https://en.wikibooks.org/wiki/FFMPEG_An_Intermediate_Guide/image_sequence) to extract frames from the video.
3. Add all images into `Predict` folder

#### Once predicted
1. Use [ffmpeg](https://en.wikibooks.org/wiki/FFMPEG_An_Intermediate_Guide/image_sequence) to convert the image files from `output` folder to video

### Utils folder & rest of .py files
Copy these from the repo as it is

## Execution

1. Clone the repo
```
    git clone https://github.com/anuragal/yolov3_custom_dataset.git
```
2. Mount google drive for downloading weights folder (Weights cannot be added to git as git has max limit of 100 MB for file size)
```
    from google.colab import drive
    drive.mount('/content/gdrive')
```
3. Copy `yolov3-spp-ultralytics.pt` from gdrive to `yolo/weights/` folder Or directly access from google drive
4. Execute below command fot running the model
```python
    !python /content/yolov3_custom_dataset/train.py --data /content/yolov3_custom_dataset/data/customdata/custom.data --cache --epochs 300 --weights '/content/gdrive/My Drive/yolo/weights/yolov3-spp-ultralytics.pt' --cfg /content/yolov3_custom_dataset/data/cfg/yolov3-custom.cfg
```
   This will add `best.pt` and `last.pt` to `weights` folder

5. Predict
```python
    !python detect.py --conf-thres 0.5 --output '/content/yolov3_custom_dataset/output/' --weights '/content/yolov3_custom_dataset/weights/best.pt' --source '/content/yolov3_custom_dataset/predict/' --cfg /content/yolov3_custom_dataset/data/cfg/yolov3-custom.cfg
```
6. Show one of the images
```python
    from IPython.display import Image 
    Image(filename='/content/gdrive/My Drive/yolo/out_put/image-067.png', width=600)
```
## Results

### Predicted Images
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/out_put/image-2764.png" height="49%" width="49%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/out_put/image-2771.png" height="49%" width="49%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/out_put/image-2777.png" height="49%" width="49%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/out_put/image-481.png" height="49%" width="49%" ></a>


### Youtube Video
[![](https://github.com/anuragal/yolov3_custom_dataset/blob/master/out_put/youtube.png)](https://www.youtube.com/watch?v=T-Bfob8iY3k)

