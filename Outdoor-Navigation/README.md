# Navigation for the blind
An algorithm that detects and outlines sidewalks or driving lanes. These outlines can be used to help the blind navigate. The programs gives real time voice feed backs to the blind. \

## Getting started
Both the python files have to be ran simultaneously. The detection.py file will append it's results into a text file. The output.py file will read the results and say it out loud for the blind.

## Running the algorithm
Both files detection.py and out.py have to be run simultaneously. The file detection.py is running its algorithm over a mp4 video and it is challenge.mp4. Same algorithm can be used for a live video feed from a camera.
## Working of Algorithm
The algorithm use the results from hough lines probabilistic and creates 2 linear lines to the driving lanes. Implemetation suggests that the 2 linear lines will intersect if the driving lanes curve or turn. \

Perform edge detection over the frames from challenge.mp4 \
![GitHub Logo](/Outdoor-Navigation/Results/edgeDetection.jpg)

Cut out reigon of interest. \
![GitHub Logo](/Results/ROI.jpg)

Perform hough lines probabilistic over ROI frames. \
![GitHub Logo](/Results/houghLines.jpg)

Average out 2 linear lines using the results from hough lines probabilistic. \
![GitHub Logo](/Results/linearLines.jpg)

Perform quadratic regression on hough line results to outline the lanes. \
![GitHub Logo](/Results/polyReg.jpg)

Final results - \
![GitHub Logo](/Results/detections.jpg)

