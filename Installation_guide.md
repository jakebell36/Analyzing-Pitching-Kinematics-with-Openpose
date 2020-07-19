# Installation Guide
Point Loma Nazarene University Summer Research 2020

## Overview:

This document contains instructions on how to set up:
  * Openpose
  * Jupyter notebooks through Anaconda
  * How to set up a dual boot to run Ubuntu alongside a Windows system
  
## Openpose Installation:


### Original sources of information:

***Note:*** 
   * All of these installations were done on a Windows computer, so some of these commands may not work on other operating systems. If that happens, check out the Links to the original sources for commands for your specific operating system
   * If you are experiencing problems while installing, follow the original information links for help troubleshooting and more in-depth instructions


1. Prerequisites for Openpose:
   * https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/prerequisites.md

1. Guide of how to set up OpenPose: 
   * https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/installation.md



### Openpose Installation via Youtube video:

**I recommend that you follow this youtube video to install Openpose**
   * https://www.youtube.com/watch?v=QC9GTb6Wsb4&t=1s 
   * you can check my installation instructions if you get confused during the video

### Openpose Installation via my instructions:

1. Install git, I picked the default options in the installer for it
   * https://git-scm.com/download/win (windows install link)
   
1. Clone the Openpose github repository by running this command in your Command Prompt. I did it in the Anaconda Prompt. (If you don't have Anaconda downloaded, skip to the Anaconda Installation, follow those instructions, then come back here)
   * git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
   *Here is an example of the git clone command:
   
   ![Openpose Clone Photo](/pics/anaconda_openpose_clone.jpg)


1. Install Microsoft Visual Studio 2019
   * https://visualstudio.microsoft.com/downloads/
   * Make sure to enable all C++ related flags when selecting the components to install, as stated in the installation document
   
1. Install CMake GUI (an open source development tool)
   * Website: https://cmake.org/download/
      * For windows 64 bit, download the most recent version of CMake, it ends in the extension .msi
      * Mine was: cmake-3.17.3-win64-x64.msi
      
1. **For nvidia GPU version ONLY**
   * Install the latest versions of CUDA and cuDNN from nvidia
      * There is troubleshooting resources in the ***"Prerequisites for OPenpose"*** link
   * If you have a Mac computer, you can use AMD graphics cards, the instructions are located in the official openpose github
      
1. Use CMake to configure openpose
   * This part can be a little complicated, so I recommend that you either watch the youtube video, or go to the Original Information link for ***"Guide of How to Set up Openpose"***
   * Follow the steps under “Installation” in the link, you will already have the prerequisites installed
      * But, if you do not have a graphics card, make sure to set the check box **"GPU_MODE"** to **"CPU_ONLY"** while configuing Openpose

1. Use Visual Studio 2019 to "build" our newly-configured openpose
   * Navigate to the folder where you have openpose downloaded, go to the openpose/build/OpenPose.sln file, and double click on it
      * It should open the file in Visual Studio
   * Now, on the top bar of the screen, there should be a box with the name **"Debug"**. Click on the box and set the value from **"Debug"** to **"Release"**
   * Then, click on the green triangle to start the process of building (it might take a few minutes)
   
1. When Visual Studio is done, go to the folder where you downloaded openpose, and Copy all the files from ***openpose/build/bin*** and Paste them into ***openpose/build/x64/Release*** 
   * The file ***"OpenPoseDemo.exe"*** should be in the **Release** folder
   * Now, you can run openpose by calling the OpenPoseDemo.exe from the command prompt (I use the Windows Powershell Prompt)


## Anaconda Installation to run Jupyter Notebooks

1. Here a link on how to install Anaconda
   * https://docs.anaconda.com/anaconda/install/windows/

1. Now that you have anaconda installed, we will set up our own Anaconda environment to install the requirements on. Run the below commands in the Anaconda prompt to create an Anaconda environment named ***"openpose_env"***
   * conda create --name openpose_env python=3.5
      * press "y" when it asks if you want to proceed
   * conda activate openpose_env
      * this command makes openpose_env your current environment
      
1. Now we will install the prerequisites for jupyter notebooks to run properly, so run these commands in the prompt:
   * conda install -c anaconda numpy
   * conda install -c anaconda pandas
   * conda install -c conda-forge matplotlib
   * pip install pypiwin32
   * python -m ipykernel install --user

1. Now, type "jupyter notebook" in the prompt to open up Jupyter Notebooks
   * A tab for jupyter notebooks will open up in your browser
   * Navigate to where you have ***“openpose_keypoint_analysis.ipynb”*** downloaded
   * Now you can open the file ***“openpose_keypoint_analysis.ipynb”***


## Ubuntu dual-boot Install for Windows Machine

### Background/Why is there a guide for a Dual-Boot here?

Well, since I could not figure out how to do 3D reconstruction in Openpose on Windows, I decided to try to do it on Ubuntu, a linux operating system. Since openpose had more support for linux than windows, I figured it would be easier to set up 3D reconstruction.
I got the dual-boot to work (after a lot of troubleshooting), but I could not get Openpose set up in Linux, and since I was running low on time, I decided to revert back to Windows and only focus on 2D processing.

Even though I ended up using Openpose through Windows, I still have the documentation on how to set up a dual-boot, so here it is.

### Installation steps:

Youtube video guide on how to set up a dual boot:
   * https://www.youtube.com/watch?v=u5QyjHIYwTQ

### Installation Extra Steps:

The youtube video did not completely work for me, I had to follow these extra steps to get the dual boot working completely.


#### Change Storage System from RST to ACHI

Since my intel drivers were RST (Rapid Storage Technology), Ubuntu could not install from my USB-drive, so I had to convert my storage system from RST/RAID to ACHI	
   * Reference: https://discourse.ubuntu.com/t/ubuntu-installation-on-computers-with-intel-r-rst-enabled/15347/30
   
##### Here are the steps on how to do this:

1. For Windows dell xps, open Windows Powershell as admin and run the following command: **bcdedit /set safeboot minimal**

1. Now, restart the computer, and when the Dell Logo pops up on screen, press the ***F2*** button to get to the BIOS System Setup Menu

1. From the BIOS System Setup Menu, select System Configuration, and under SATA Operation, change from RAID to ACHI

1.  Apply the changes and Exit the BIOS System Setup menu

1. Boot back into windows and go back to the Windows Powershell as Admin, and run the following command: ***bcdedit /deletevalue safeboot***

1.  Now, restart your computer once more and it should be complete



#### Turn off Windows BitLocker Encryption

Bitlocker encrypts your drives in windows, but it also makes ubuntu unable to access the drives, so we must disable it

   * Reference : https://discourse.ubuntu.com/t/ubuntu-installation-on-computers-running-windows-and-bitlocker-turned-on/15338
   
* NOTICE: Back up your data to an external source before doing this, since it could potentially lead to data loss, so please be careful

1. On Windows, open Settings > type “Manage Bitlocker” in the search bar

1. Select the option “Turn off Bitlocker”

1. Select “Turn off Bitlocker” in the pop-up as well, and it will begin decrypting your drive

1. Once it is done, Bitlocker has been disabled, and Ubuntu should be able to run
