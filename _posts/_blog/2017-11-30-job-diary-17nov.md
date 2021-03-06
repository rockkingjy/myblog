---
layout: post
title:  "Job diary (Nov.)"
date:   2017-11-28 05:16:01 -0300 
categories: blog
tags: ['job']
published: true
comments: true 
excerpted: |
    My job diary here ...
day_quote:
    title: "Quote Day"
    content: |
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. 
        (Mr. Lorem)

# Does not change and does not remove 'script' variables
script: [post.js]
---

* Do not remove this line (it will not be displayed)
{: toc}

# Summary of November
* Tasks I've completed:

Tasks | Achieved Date
----- | --------
Setup nv-caffe and DIGITS on the new GPU server | 11/30
Setup a new GPU server | 11/29
Image data categorization by hand | 11/28
ZED camera data requirement | 11/27 
OpenKAI deteceNet.py change to use camera input, output with bounding box | 11/24
Converter from the Stanford Drone dataset to Kitti format | 11/20
Camera calibration  | 11/17
OpenKai document update | 11/17
Setup and run sample for OpenKAI on Laptop | 11/07
Setup and run sample for OpenKAI on TX2 | 11/06
Prepare a GPU parts list | 11/02


# 2017/11/29~30 Wednesday
* Setup a GPU server
  * Complete.
  * Some tricks: 
  1. The paste for CPU should not too much.
  2. Attention to the fans' air flow directions.
  3. GPUs need double power supplies.
  4. 512G Nvme SSD for op system, normal 3*1T SSD for data treatments, 10T HDD for store data
  5. Ubuntu 16.04, without HDMI input, it will not boot up. So I used a USB to HDMI converter with a HDMI cable to fake a monitor. 

# 2017/11/28 Tuesday
* Setup a GPU server

I've gotten all my parts of GPU server today. So the whole day, I'm trying to assemble it. Half finished. Parts list:

Part | Quantity | Model | Price | Total
---- | -------- | ----- | ----- | -----
GPU 1080Ti | 2 | GEFORCE GTX 1080Ti | JPY 113,378 | JPY 226,756
CPU | 1 | Intel Core i9-7920X X-series Processor LGA2066 12コア/24スレッド | JPY 143,729 | JPY 143,729
M/B | 1 | ROG STRIX X299-E GAMING | JPY 44,980  | JPY 44,980
DDR4 | 2 | CORSAIR DDR4メモリモジュールVENGEANCE LPXシリーズ16GB×4枚キットCMK64GX4M4A2133C13 | JPY 88,734  | JPY 177,468
SSD NVMe | 1 | Samsung SSD 512GB 960 PRO M.2 Type2280 PCIe3.0×4 NVMe1.2 V-NAND搭載 | JPY 40,311 | JPY 40,311
SSD 1TB | 3 | Samsung SSD 1TB 850 EVOベーシックキットV-NAND搭載2.5インチ内蔵型MZ-75E1T0B/IT | JPY 39,717 | JPY 119,151
HDD 10TB | 1 | WD HDD内蔵ハードディスク3.5インチ10TB WD Gold WD101KRYZ SATA3.0 7200rpm 256MB 5年保証 | JPY 60,980 | JPY 60,980
CASE | 1 | Corsair Carbite Air 540 E-ATX対応キューブPCケースCS5326 CC-9011030-WW | JPY 17,101 | JPY 17,101
PSU | 1 | 1600W Power Supply Unit | JPY 40,676 | JPY 40,676
CPU Cooler | 1 | CORE FROZR XL | JPY 13,824  | JPY 13,824
Case FAN | 5 | RDH1238B(38NMB) | JPY 1,809 | JPY 9,045
Camera  | 1 | ロジクール BRIO(ブリオ) RightLight 3(HDR)採用 4K Ultra HDウェブカメラ C1000e  | JPY 22,305 | JPY 22,305
       | | | | JPY 916,326

# 2017/11/27 Monday
* ZED camera data requirement 
  * Have a problem when HDMI and USB keyboard disconnected, the TX2 board could not detect the ZED camera. After one day's work, I found the timing of boot up is changed, so the mounting time for SD card is not enough when the connection status changed. So for the programme of ZED camera data requirement, I add 15 second's delay at the begin if. All the things go well then.

# 2017/11/24 Friday
* ZED camera data requirement 
  * USB3.0 problem solved, it runs normally on the new board.
* OpenKAI deteceNet.py change to use camera input, output with bounding box
  * Done, [[Codes](https://github.com/rockkingjy/OpenKAI/tree/master/python)].
  * Ths speed still needs to be enhanced. 
  * The frame of camera:
  ```
  ret, frame = cap.read()
  ```
  is exactly inverse of reading from the png picture, so needs to be inversed:
  ```
  image = frame[:,:,::-1] 
  ```
  If not, it will infect the result of DNN object testing.
  

# 2017/11/23 Thursday
Holiday, finally successfully set my blog([Codes](https://github.com/rockkingjy/myblog)) under the help of [William Canin](https://github.com/williamcanin)! 

# 2017/11/22 Wednesday
* ZED camera data requirement 
  * Solve the boot time running problem yesterday, that because the linux haven’t mount the SD card before I click it, so needs to mount it manually. [[Codes](https://github.com/rockkingjy/ZedDataCollection)]
  * Change the default carrier board to [Auvidea carrier board](https://auvidea.com)->Support->Firmware->Firmware for Jetson TX2 based carrier boards, meet some problems on USB not working, because the firmware needs to be changed. 
  * Install JetPack, download “ChangesTX2J140_Kernel” from the website, do as the readme.txt told me(Remember to replace ALL the files, not only the first three files).
* When run JetPack to flash the TX2 board, some key points:
  * Change the default carrier board to [Auvidea carrier board](https://auvidea.com)->Support->Firmware->Firmware for Jetson TX2 based carrier boards, if you use Auvidea. 
  * Connect the minusb port of TX2 to usb of the computer, internet port to computer by a internet/usb converter;
  * Change “opencv4tegra" to no-action, because openKai do not support the opencv version here;
  * To flash TX2, do the following: power on->hold the reset key-> press the recovery key->the the internet port light flash, release all->check on the computer by $lsusb, a Nvidia device appears->continue the flashing.
  * After flashing the TX2, it will login to Ubuntu, some times the computer will automatically detect the IP address of TX2, just close it and re-run JetPack, to make no-action “flash os image to target” item.
  * To install OpenKai and everything: first install ZED driver, then run the script from Mario: [[Codes](https://github.com/rockkingjy/Tips/blob/master/Install-OpenKAI-TX1-after-ZED.sh)]

# 2017/11/21 Tuesday
* Image categorization
  * Write a script for check the results of the removal results of out-sourcing.
* ZED camera data requirement
  * Avoid the duplication of image names: if(duplicate){create another folder}
  * To run on TX2;
  * To run on power on TX2 automatically, refering: [[Link](http://cosmolinux.no-ip.org/raconetlinux2/boot.html)]. Still have some problems on running the program at boot time.

# 2017/11/20 Monday
* Image categorization
  * Try to transfer some data to Baidu Yun, but too slow(~20kB/s). Try again the multcloud, also failed. Reason not clear, maybe need to pay for them, $8 monthly. Try to transfer directly though QQ.
* Converter from the Stanford Drone dataset to Kitti format
  * Modified the Stanford drone data set to kitty format codes.
* ZED camera data requirement 
  * Coding for the zed depth camera data requirement: [[Codes](https://github.com/rockkingjy/ZedDataCollection)]

# 2017/11/18~19 Weekends
* Image categorization
  * The data transfer to the company in China failed, because of the Great Wall. I’ve found [multcloud](https://www.multcloud.com) which could transfer data from google drive to Baidu Yun directly. But the data should not be too large. I divided the original data(~27GB) to less than 2GB for each file and now it works fine. (Later, I found it’s not quite stable, on Sunday it stopped.)
  * In order to save time, I’ve written a python script to change the name of images to numbers, so that after the company in China do the human-hand removal and classification, they could just send me a text file with the number of the images. 

# 2017/11/17 Friday
* Camera calibration
  * Clean the files for camera calibration, code uploaded: [[Codes](https://github.com/rockkingjy/cameraCalibration)]
* OpenKai document
  * Update the openKai document, push for merge: [[Codes](https://github.com/rockkingjy/OpenKAI_docs)]
* Connverter from the Stanford Drone dataset to Kitti format
  * Done the converter from the Stanford Drone dataset to Kitti format, code uploaded: [[Code](https://github.com/rockkingjy/sdd2kitti)]

{% label Attention|20px %}: The compress of the large file should be separated into small pieces, for each pieces should be around 2GB, then the compress will work, else, it fails.

# 2017/11/16 Thursday
* Image categorization
  * Communicate with the Chinese image categorization company about the removal of the duplicated data and the classification. Write an instruction “readme.txt” file for them to proceed.
  * Building/ Cloud/ Night/ ordinary road/ Rock/ sea road/ Ship/ these categories are not seen in the categories in Places.
* Camera calibration
  * Kai said it’s difficult to calibrate camera with opencv. Try to understand [how to calibrate the camera using opencv](https://docs.opencv.org/2.4/doc/tutorials/calib3d/camera_calibration/camera_calibration.html)
  * My modified codes and explanations: [[Codes](https://github.com/rockkingjy/cameraCalibration)]
  * For the OpenKAI, I added a .kiss file called “cameracalibration.kiss”, and some camera calibration parameter names in the /openkai/src/_camera.cpp, and it succeeded. Problem solved.

# 2017/11/15 Wednesday
* Image categorization
  * Check the category names.
  * Communicate with the company.
  * Upload the data for the company to classify.
* ZED camera data requirement
  * Read the [document](https://www.stereolabs.com/documentation/overview/getting-started/introduction.html) to understand how to use Zed and programme it.
* Camera calibration
  * Read the [document](https://en.wikipedia.org/wiki/Distortion_%28optics%29) to understand the details.
* Mario's problem of Image Sementation
  * The DL training model for segmentation of Mario’s building picture is not so good, because the training data is not fit for this task.

# 2017/11/14 Tuesday
* Meeting, some explanation from Kai of the project.
  * OpenCV calibration programme - talk with Kai and Mario tomorrow
  * Stanford drone dataset to kitti format
  * DNNzed - Collect the zed data for training, and to convert the RGB image to depth image.
  * DNNavoidance - To train on the dataset to avoid the buildings etc.
  * DNNlanding - To avoid dangerously landing like to avoid of landing on the human’s head, water etc.
  * DNNodometry - Regression, Calculate the distance displaced.
  * DNNnavigation - Regression, Input: pic, Output: 3d location data.
  * DNNfollow - The project is from the Japanese government, Kai is working on it, to follow the savage animal.

# 2017/11/13 Monday
* Image categorization
  * Read the paper of [Places](http://places2.csail.mit.edu/index.html), it depicts the evaluation of image classification datasets just as I discussed it last week.

# 2017/11/10 Friday
* Image categorization
  * A big problem that I found when I do the classification is the duplication of the pictures when they are extracted from the video. How to remove the redundant similar pictures? Needs a program to get the similarity of two pictures, I’ve tried the [Link](https://www.pyimagesearch.com/2014/09/15/python-compare-two-images/), the problem is: too slow!
  * For some pictures that contain lots of things, what should I do? In the human case, one can only focus on some area that tell something. Attention model.
  * Lots of studies were on the segmentation of figures out of a picture. For example flag out the people or car. But my task here is to recognize the background, like mountain, forest, building, lake, sea, bay or even night. How to figure out the large vague background.

# 2017/11/09 Thursday
* Image categorization
  * Try to find some company special for the classification: http://huicuiapi.com - 1w张图片分类300RMB，1w张图片去重复等200RMB，1w框600RMB
10w图片分类3days分类，3days质检，1week交货; 在交付数据之前会把所有标注数据都看一遍，以保证标注质量，交付之后未通过客户验收的数据，一律不计入费用。有发票。

# 2017/11/08 Wednesday
* Image categorization
  * Aerial Image categorization for DNNavoid, that means to categorize all the randomized images to different folders. 
  * The first step should determine the name and structure of the folders fit for the task.
  * How to classify the image quicker?
  * Write a python program classifypictures.py to make it easier to classify.

{% label Some points maybe need to be taken into consideration|20px %}:
* The name of the categories.

There are 16 categories now, I don't know whether they were named with some deeper considerations, here are some of my considerations:

  * The categories should be clear and easily identified by human beings, similar to the mathematical term "orthognal", any two of them should not be connected to each other. For example, "road" and "water" are quite clear for us human beings to identified; but "beach", "bay" and "coast" maybe not that clear; "water" seems to include "river"; "mountain" somtimes overlaped with "forest"; "suburb“ could contain lots of things; and "night" is quite a bit of special category that it could be overlaped with any other categories.
  * Take the consideration of the limited time, the categories should be highly related to the task, which should be quite clear(while I am not now). The categories like ImageNet is too large for us to create, so we have to focus on the precise task.

I've checked that, ImageNet took the WordNet hierarchy to create the categories, and CIFAR-100 and some others are also quite clear. Maybe we could try to learn something from them.
* The quality of the pictures for each categories.

  * As I did the categorization myself, I found that, some pictures that I could not figure out what they are. Then I put them into a special folder called "undecided". And some pictures are not quite typically belong to one of the category, that puzzled me a lot.
  * Should the pictures of the categories be "typical"? That is a question. Maybe the "typicality" could help the DNN to extract out the hidden features.

* There are around 65000 pics. At first it took me around 10 seconds to classify a pic. Then I wrote a small programme by python, that speeds up to 3~5 seconds to classify a pic. Even with this speed, it will take around 65000*3~5s/60s/60min/8h=7day~11days non-stop works to finish it. That pains, but that's necessary.

# 2017/11/07 Tuesday

Because of the installation of the wrong version of CUDA, and I need to familiar with ALL the installation details, so I decided to reinstall Ubuntu from the beginning.

* Create a bootable USB stick on macOS

Download ubuntu-16.04.1-desktop-amd64.iso 

Create the bootable USB according to the link:
https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-macos#6

Attention: ubuntu-16.04.3-desktop-amd64.iso always cause error!

* Install Ubuntu16.04.1

Reinstall by reboot and F12, choose UEFI OPTIONS usb boot;

After login to Ubuntu, double click the icon on the desktop to reinstall ubuntu;

Restart from the hard disk;

Attention: If choose from the LEGACY OPTIONS, it will cause the problem of unable to login to ubuntu and go to grub!

* Install Nvidia GPU driver

Connect to internet

System Settings->Software & Updates->Additional Drivers->Using Nvidia binary driver->restart
```
nvidia-smi
```
Attention: Kai told me when install CUDA, do NOT install the display driver come with it, it will cause error.

* Some prerequisites installation:
Follow the procedures from: http://docs.openkai.xyz/x86build.html
* Install CUDA8.0
Attention: Should be CUDA8.0, CUDA9.0 will cause some error later.

Follow the “CUDA_Quick_Start_Guid.pdf”, install with the deb file(more easier).

Test with the examples in /NVIDIA_CUDA-8.0_Samples;

To change the PATH permanently:
```
sudo echo -e "export PATH=/usr/local/cuda-8.0/bin:\$PATH\nexport LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:\$LD_LIBRARY_PATH" >> ~/.bashrc
CUDA version check: nvcc --version
```
* Install cuDNN7.0 on ubuntu: 
Follow the “CUDNN Installation Guide”, install with the deb file(more easier). 
Test with the examples;

cuDNN version check:
```
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
```
* Install TensorRT2.1 on ubuntu:

Attention: Should be TensorRT2.1, TensorRT3.0 is not stable.

Follow the Quick Start Instructions, install with the deb file(more easier). 

* Install OpenCV3.1

Follow the OpenKAI document and OpenCV document.

* Install ZED driver

Download ZED_SDK_Linux_Ubuntu16_CUDA8_V2.2.0.run from the site https://www.stereolabs.com/developers/downloads/

Install follow the OpenKAI document.

* Install Pangolin and ORB_SLAM2 GPU version

Follow the OpenKAI document.

* Install jetson-inference

Change the CMakeLists.txt to:
```
arch=compute_61,code=sm_61
```
* Install OpenKAI

Follow the OpenKAI document.

* Install Eclipse and run the project

If error：undefined reference to uuid_unparse@@uuid_1.0 

Add “uuid" to Properties for OpenKAI->C/C++ Build/Setttings/Gcc C++ Linker/Libraries

If error: error while loading shared libraires: libjetson-inference.so

Carefully check the path to libjetson-inference.so is right in the file /etc/ld.so.conf (for my case I just mistake x86_64 by x86-64) and do
```
sudo ldconfig
```
A very good webpage for explain:
https://lonesysadmin.net/2013/02/22/error-while-loading-shared-libraries-cannot-open-shared-object-file/

2017/11/06
* Get the Alienware laptop.

# 2017/11/01~02
* Get the NVIDIA JETSON TX2, Mario helped me to install ubuntu and installed openKAI on TX2;
* Create the parts list for the new GPU Server.

{% endpost #9D9D9D %}
