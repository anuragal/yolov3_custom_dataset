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
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/data/customdata/images/eyeglass002.jpg" height="40%" width="40%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/data/customdata/images/eyeglass004.jpg" height="24%" width="24%" ></a>
<a href="url"><img src="https://github.com/anuragal/yolov3_custom_dataset/blob/master/data/customdata/images/eyeglass504.jpg" height="24%" width="24%" ></a>
