# Analyzing-Pitching-Kinematics-with-Openpose
PLNU Summer Research 2020 - Analyzing Pitching Kinematics with Openpose

Overview:
Hi! This document is a brief overview of what I have learned/coded/attempted over the course of my Summer Research. 

To summarize, by using OpenPose, an open-source software package, as well as some of my own python code, I have been able to analyze video of pitchers and gain some significant insights.

In this “Summer Research 2020” google drive folder, under “Written Documents”, are documents describing what articles I read, what tools I used, how to install those tools, and what I accomplished in my research.

Under “Final Product”

My Experience:
I spent a lot of time trying to figure out the installation of Openpose so that I could use its 3D reconstruction capabilities. Unfortunately, I was not able to figure out how to correctly set up Openpose’s 3D reconstruction module. So, as a result of not figuring out how to do 3D reconstruction, I simply chose to just stick to analyzing 2D videos. 


Description of Program:
My Program, “json_keypoint_analysis_multi_video”, works with multi-angle videos of a pitcher throwing a ball. It takes in a folder containing multiple videos that have already been processed by OpenPose. 

Here is what the openpose software does: 
The Openpose software first examines the video to find where the subject is in each frame. 
Then, it estimates where, and in what position the subject’s skeleton would be in that frame. 
Then, Openpose outputs a series of text-based .JSON files, where each file represents one frame, and contains the x,y position and confidence level of each keypoint used to build the skeleton.

Here is an example of one .JSON file and how it is organized.
 
Here is what my program does with the OpenPose output:
Set up the variables necessary for calculations by asking the user
Read in the .JSON files from the user-specified folder to create Position dataframes for each video
Use the Position dataframes to calculate a Velocity dataframe for each video
Use the Velocity dataframes to calculate an Acceleration dataframe for each video
Use values from all of the dataframes to form a Throwing Arm dataframe
Calculate the angle of the throwing arm for each frame
Plot the results in meaningful ways

How to use my program (with pictures!):
First, install Openpose and get it working. Check out the google doc “Openpose & Ubuntu Install”, it contains the Instructions on how to set up Openpose, and build it with CMake and Visual Studio 2019. It also contains links to the OpenPose Github and to a video tutorial.
Once you have Openpose all set up, go to the Windows Powershell Prompt, the keyboard shortcut is the windows sign + x + a. (This is for Windows systems only, other systems will have to look on the OpenPose Github under openpose/doc/installation.md for instructions)
In the Windows Powershell Prompt, navigate to the directory where you have openpose set up. Look up online on how to change directories if you don’t know how to.
When you set up Openpose with CMake, you generated a “build” file. Copy the command in the picture below, but with some changes.
Where the command says “build_GPU”, change it to whatever your build file is named. 
Where it says “--video “C:\Users…” “, change the path to wherever you have  your raw video stored
To get the path to the video easily, navigate to the file location in File Explorer, and click on “Copy Path”, then paste the path
Where it says “--write_json  ‘C:\Users…’ “, change the path to the location where you want to save the .JSON output folder, and at the end have it be the name you want the folder to be saved as
Now that you have the right command, press the Enter key and run the program
If you want to run your program using a Graphics Card or eGPU, the setup for that configuration is specified in the “Openpose & Ubuntu Install” google doc.
Run that command, with the proper arguments, for every video you want to be processed.
Once you have processed all of your videos through openpose, you are ready to work with the main program. 
Open “openpose_keypoint_analysis_multi_video.ipynb”  in Jupyter notebooks
If you do not have Jupyter notebooks installed, I have a guide on how to set it up through Anaconda.

Some ways that my program can be improved:
Find ways to better handle “0” values or extreme values from Openpose
“0” values happens when a certain part of the body is obscured from view for a camera angle
Extreme values happen sometimes when openpose does not identify the subject’s skeleton correctly in some frames
Velocity and Acceleration would be calculated more smoothly by averaging the values of the frames before it and after it, instead of setting it equal to its own calculation (although this would make the first and last frames unusable)
Find more relationships in the data between the throwing arm angle and velocity of the arm through the video
When angle changes most, how does the velocity change?
Try to identify the 6 stages of Pitching a Ball in the data for each video
The 6 Phases are: 1.) Wind up 2.) Stride 3.) Cocking 4.) Acceleration 5.) Deceleration 6.) Follow Through 
Try to input videos of one pitcher doing multiple pitches from one angle
Then you would be able to measure the consistency of pitching
You could make a dataframe for the pitcher’s average and measure successive pitches against it
What is the standard deviation of velocity and angle
Flag pitches that are outliers for review
How does the pitcher’s pitch change when he is tired?
Maybe put the code in a .py file for easier 1-click processing, instead of a jupyter notebook
Another useful measurement: Stride ankle distance 
It is important that the stride ankle lands at a distance of approximately 87% of the pitcher’s height away from the other leg, changes in this distance affect the stress levels on the shoulders during a pitch.
Source: https://www.physio-pedia.com/Throwing_Biomechanics#cite_note-Baseball_Biomechanics-10
Maybe this would be another good measurement to obtain from the position dataframes

