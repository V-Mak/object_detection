# object_detection



https://github.com/V-Mak/object_detection/assets/111484051/30dada46-6f42-417d-a990-d33558007247




## Introduction:
The goal of this project is to detect and count vehicles in a traffic video using computer vision techniques. The main steps are:
1.	Detect vehicles in each video frame using a deep learning model
2.	Track detected vehicles across frames
3.	Count vehicles crossing a defined line
OpenCV, ultralytics, and supervision libraries are utilized for the project implementation.

## Object Detection:-
YOLOv8 object detection model from ultralytics is used to detect vehicles.
* The model is loaded and instantiated. YOLOv8 is a real-time detector capable of identifying common objects.
`model = YOLO("yolov8x.pt")`
* Input video stream is captured using OpenCV and each frame is passed through the model to get bounding box predictions.
*	The output detections are converted to a Detections format containing boxes, scores and class IDs.
*	Classes are filtered to only vehicles types like cars, trucks etc.

## Object Tracking:-
ByteTrack algorithm is used to track detected vehicles across frames based on bounding box overlap.
•	ByteTrack maintains object trajectories and assigns each tracked object a unique ID.
•	New detections are matched to existing tracks using IoU matching. Matched detections get the track ID.
•	Unmatched detections are assigned a new track ID and stored.



## Line Counting:-
A LineCounter class increments count when tracked vehicles cross a defined line.
*	Line start and end points are initialized as x/y coordinates.
*	It checks bounding box intersections with the line to detect crosses.
*	The line_count variable gets incremented when a tracked vehicle crosses the line.

## Output:-
*	Output video is saved using VideoSink to overlay tracking labels and line count.
*	Annotators from supervision library are used to draw bounding boxes and text.

## Challenges:-
*	Initially faced attribute errors when trying to increment line_count.
*	Fixed by defining it as a class variable instead of local integer.
*	However issue persisted due to dependency mismatches.
*	Creating fresh virtual environment and reinstalling packages resolved the errors.

## Results:-
*	YOLOv8 achieves high detection recall, identifying nearly all vehicles in the video stream.
*	ByteTrack is able to successfully track vehicles over extended periods despite occlusion and scale changes.
*	The line counter accurately counts vehicles crossing the defined boundary.
*	The final output video has clean labeled boxes around each tracked vehicle along with real-time count.

## Conclusion:-
The project demonstrates how YOLO, ByteTrack and other libraries can be integrated to build a vehicle tracking and counting system. The implementation covers core concepts like deep learning inference, object tracking, and line intersection. Managing dependencies and environments is also an important lesson learned.
