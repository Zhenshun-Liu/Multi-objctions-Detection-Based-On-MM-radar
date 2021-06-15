# Multi-obictions detection based on mm-radar
*I am a undergraduate student from China University of Geoscience, and my graduation project in bachelor period is human-pose estimation based on mm-radar. After went through the references named "You Only Look Once" always applied in objects detection of images, I was inspired by the YOLO algorithm and wanted to tranform it into which could be used in objects detection on mm-radar's data.*
## Storage Pattern of Processed Radar Data
In order to transform the YOLO algorithm successfully, I have to make sure that the storage pattern of processed radar data, containing the range, velocity and angle of objects, is similar to the image's. If you think carefully, you would find that pixels representing an object in the image always get together. So, I have to store the precessed mm-radar data in that way, which is suitable for YOLO algorithm to do objections detection.</br>
<div align=center>
<img src="/Picture/1.png" />
</div></br>
The storage pattern of processed radar data as the picture beyond, among range, velocity and angle, the amount of angle has to be from small to large(or from large to small). Because in this way, all the points representing one object get together in one demension. As for range and velocity, they both have the pattern from small to large based on the arrangement rule of angle, but the range has the higher priority than the velocity.
## Neural Network Of YOLO
<div align=center>
<img src="/Picture/2.png" />
</div></br>
In this project, 121 radar data points are divided into 11 Bounding Boxes. Each Bounding Box has 11 radar data points. After the convolution layer and full connection layer, the data volume with length of 11 and depth of 4 is obtained. Each data point in the output layer contains the information of whether each Bounding Box of the input radar data contains the target.
<div align=center>
<img src="/Picture/3.png" />
</div></br>
Here is the detail of output layer. Each output layer data point consists of four predictions: X, W, C (confidence) and P (category). X is the center coordinate of the bounding box relative to the bounding box in the cell. W is the width of the bounding box relative to the input radar data.
## Loss Function
<div align=center>
<img src="/Picture/4.png" />
</div></br>
## Generation of radar YOLO algorithm train data set
In order to train the Yolo neural network for radar data, it is necessary to mark the targets in radar data correctly. Therefore, when acquiring radar data, it is necessary to record the distance and angle between the target and the radar, and express them in the form of output layer data.
