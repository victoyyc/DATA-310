[Output 1](https://www.youtube.com/watch?v=5ADnyHWZ00s)

[Output 2](https://www.youtube.com/watch?v=UzeeedOY124)

#### 1. Was your social distance detector effective at detecting potential violations?
THe detector was effective when people in the video are the same horizontal level, but no so mcuh when the frame contains people in various distance to the camera. 
My firts output shows a couple holding hands, who are much closer to the camera than the others. They are clearly not properly distanced, but they
 are assigned green boxes. I think this might be because the couple are walking toward the camera and their image appears to be much larger than the others, 
 interrupting the calibration. I then used another video clip where people are not walking toward the camera but from one side of the frame to another, 
 so that the individuals' size do not vary that much. This time the detector became more effective. 
 
#### 2. Are you able to describe how the distance detector is applying its calculations of either being safe or noting a violation?
It appears that the script analyze the video frame by frame. It establishes a calibration as standard for measuring the social distancing. It then identifies each individual from the frame and check if their distance to 
one another is large enough. It then copies that frame of image, drawing red/green boxes around each individual according to their social distancing status and output the frames as a video. The script also record and output the time used to process each frame.

#### 3. Do you think this approach would be effective for estimating new infections in real time? How would you implement such an approach in response to the COVID-19 pandemic we are currently experiencing?
I think it can be a good way to detect violations of social distancing, but since the health status of each individual is unknown, it cannot directly tell if one has been infected.
The detector might be useful in tracking close-contacts of a known patient when paired with some facial recognition techniques. The detector can store the videos, and when a new cas
of infection appear, facial recognition programs can run through the output videos and see who has been closely contacted by the infected individual. However, as it invlves recognition of individual identity, 
there would be a series of ethical issue to be considered before we can actually implement such detection method.

#### 4. What limitations or improvements might you include in order to improve your proposed design?
As shown in question #1, the current dectector does not work well with perspective. When individuals in the frame are in different scales, the dectector cannot measure the distance as effectively.
Secondly, as in the couple' case, it is possible that they are from the same household, which social distancing between the two not necessary. I think it would be great if the detector can be
improved so that it identifies families and couples who are likely from the same household and do not identify them as violations.
