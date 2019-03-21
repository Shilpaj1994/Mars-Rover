## Project: Search and Sample Return
### 

---

**The goals / steps of this project are the following:**  

**Training / Calibration**  

* Download the simulator and take data in "Training Mode"
* Test out the functions in the Jupyter Notebook provided
* Add functions to detect obstacles and samples of interest (golden rocks)
* Fill in the `process_image()` function with the appropriate image processing steps (perspective transform, color threshold etc.) to get from raw images to a map.  The `output_image` you create in this step should demonstrate that your mapping pipeline works.
* Use `moviepy` to process the images in your saved dataset with the `process_image()` function.  Include the video you produce as part of your submission.

**Autonomous Navigation / Mapping**

* Fill in the `perception_step()` function within the `perception.py` script with the appropriate image processing functions to create a map and update `Rover()` data (similar to what you did with `process_image()` in the notebook). 
* Fill in the `decision_step()` function within the `decision.py` script with conditional statements that take into consideration the outputs of the `perception_step()` in deciding how to issue throttle, brake and steering commands. 
* Iterate on your perception and decision function until your rover does a reasonable (need to define metric) job of navigating and mapping.  

[//]: # "Image References"

[image1]: ./misc/rover_image.jpg
[image2]: ./calibration_images/example_grid1.jpg
[image3]: ./calibration_images/example_rock1.jpg

## [Rubric](https://review.udacity.com/#!/rubrics/916/view) Points
The rubrics consists of 3 sections:

-  Writeup
- Notebook Analysis
- Autonomous Navigation and Mapping

1. The writeup is included in the repository
2. Notebook content can be found in `./code/Rover_Lab_Notebook.ipynb`
3. The code for autonomous navigation and mapping in `.py` files in `./code/`directory

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it!

---

### Notebook Analysis
#### 1. Run the functions provided in the notebook on test images (first with the test data provided, next on data you have recorded). Add/modify functions to allow for color selection of obstacles and rock samples.

- The code for following is in `./code/Rover_Lab_Notebook.ipynb` notebook.

- First, thresholding is done to find the navigable terrain, obstacles and rocks

  > Code for Thresholding is in cell 6  

- Using Perspective transform, we got bird's eye view on which thresholding is done to get a binary image of navigable terrain

  > Code for Bird's eye view is in cell 5

- Using coordinate transformation, we obtained world coordinates of the navigable terrain.

  > Code for coordinate transformation is in cell 8

- Using world coordinates, we calculated the angle at which the rover should be steered

![1](D:\RoboND-Rover-Project-master\writeup_contents\1.png)

![6](D:\RoboND-Rover-Project-master\writeup_contents\6.png)



![4](D:\RoboND-Rover-Project-master\writeup_contents\4.png)

![5](D:\RoboND-Rover-Project-master\writeup_contents\5.png)

#### 1. Populate the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Run `process_image()` on your test data using the `moviepy` functions provided to create video output of your result. 
<video src="D:\RoboND-Rover-Project-master\writeup_contents\test_mapping.mp4"></video>



---

### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.

- The `perception_step()` from the notebook cannot be used directly since we have to map at least 40% of the map with more than 60% fidelity
- Also, to map the covered area with precision, we have to take into account the obstacles map.
- In the notebook, the perception step only covers the navigable terrain part
- For the project, we have to follow the pipeline for navigable terrain, obstacle and the rock so that at every instance of time we will know where navigable area, obstacles and rocks are with respect to the rover.
- Using this information, we can collect the rocks while covering the map.


#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**

#### Simulator Settings

> Screen:  1680 x 1050
>
> Graphics Quality: Fantastic

- First approach I took was to only use navigable terrain and the rock information
- It worked in terms of covering area but the fidelity was below 50%
- Later, I included the obstacle region which increased the fidelity by around 10%
- Using roll and pitch information before updating the Rover states increased it by another 10%

- The pipeline might fail sometimes when the rover gets stuck in certain region of the map

<video src="D:\RoboND-Rover-Project-master\writeup_contents\2019-03-21-1052-20.mp4"></video>

### Future Improvements

- Collecting Rocks
- Avoid looping in certain part of the map by using coordinates of the rover
- Increasing fidelity by changing perspective transform
- Making pipeline more robust by introducing change in speed near obstacles