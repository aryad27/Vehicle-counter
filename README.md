# Model to count the number of vehicles crossing a line coordinate.
Video analysis is a challenging problem due to a number of factors. Shadows, distracting features, Objects other than vehicles, etc, are some examples that make this model more prone to errors and a major source of inaccuracy. However, to build a model to contend with these challenges, the approach I followed was: 

1) Background Subtraction (BS) is a common and widely used technique for generating a foreground mask (namely, a binary image containing the pixels belonging to moving objects in the scene) by using static cameras.

In OpenCV we have a few algorithms to do this operation –
BackgroundSubtractorMOG – It is a Gaussian Mixture-based Background/Foreground Segmentation Algorithm.

BackgroundSubtractorMOG2 – It is also a Gaussian Mixture-based Background/Foreground Segmentation Algorithm. It provides better adaptability to varying scenes due illumination changes etc.

BackgroundSubtractorKNN – This algorithm implements the K-nearest neighbours background subtraction . Very efficient if the number of foreground pixels is low.
I used BackgroundSubtractorKNN for the project. 

2) Finding Contours:
Contours are defined as the line joining all the points along the boundary of an image that are having the same intensity. There are multiple contours of different areas in an image . In our case, the contour having the maximum area is the desired region. Hence, it is better to have as few contours as possible. 

3) Bounding Rectangles: 
It is a feature of contours. We used straight bounding rectangles to detect objects. Bounding rectangles are important to estimate the vehicle position more accurately than traditional object detecting methods.

4) Vehicle counter: 
Finally, to count the number of vehicles passing through a line whose coordinates were set by us, we introduced a few variables like offset (the lines between which a contour detected will be added to the vehicle counter), A valid contour list was created and all the mid points of the contours detected that fell into the valid contour category, were appended to the valid contour list. Valid contour category was introduced to avoid the small area contours that would have increased the errors in our project. A valid contour within the offset lines implies that a vehicle passed through the main line, thus incrementing the vehicle counter. 
