---
layout: post
title:  "Job diary (Dec.)"
date:   2017-12-01 05:16:01 -0300 
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

# Summary of December

# 2017/12/14～15 Thursday~Friday
* Batch inference - done.

To run multiple images through a googlenet at the same time. Never done by anybody before. I've chaged the codes of [jetson-inference](https://github.com/dusty-nv/jetson-inference): imageNet.cpp, imageNet.cu, imagenet-console.cpp etc.

[Code](https://github.com/rockkingjy/jetson-inference-batch)

# 2017/12/13 Wednesday
* Build a drone by myself
  * Important parts:
  Name | Company
 ----- | --------
 Controler   | PIXFALCON
 GPS/Compass | Holybro
 Transmitter | Futaba FMR-02
 Telemetry Transmitter USB | LAB
 4 motors | LAB
 4 becs | LAB
  * Motors order should be as pictures presented.
  * Search "missionplanner motor direction" on google for the pins' number.
  {% imager drone1.jpg|left %}
  {% imager drone2.jpg|left %}
  {% imager drone3.jpg|left %}
  {% imager drone4.jpg|left %}
  {% imager drone_pins_direction.jpg|center %}

# 2017/12/12 Tuesday
* Set a new TX1 from the begining to test for the problem of suddenly shutdown when running googlenet. Procedure:
  1. Setup all the components, connect the TX1 like the following:
  {% imager tx1_setup1.jpg|left %}
  {% imager tx1_setup2.jpg|left %}
  2. Run JetPack, following the instructions. 
  3. Install the OS on TX1 through lan directly by host computer.
  4. After OS has installed on TX1, connect the TX1 to the same inner net, ifconfig to check the ip address, run JetPack again to install CUDA TensorRT etc.
* With the original carrier board, it runs normally with googlenet.

# 2017/12/11 Monday
* Batch inference 
* Problem of suddenly shutdown on TX2+Auvedia carrier board when running googlenet.

# 2017/12/07~08 Thursday~Friday
* Quartery meeting
  * 中泽佑树 Nakazawa Yoki: 机械设计，工具管理，UGV设计。
  * 宫川 Kohei Miyakawa: Production Team, manual of products, how to glue because of waterproof. Sticker, Uniforms, Flags, etc. Future, for improve production efficiency. Build drone.
  * 福田勇也 Fukuda Yuya: ROV
  * 酒井贵之 Takayuki Sakai:Make the UGV, UAV; Demonstration; 
  * 大久保博之 Ookubo Hiroyuki: PCB， electricity hardware, layout of PCB. Issue from noise.
  * 伊豆拓将 Izu Takumasa: Prototype of Drone; get information from Operators and feed back to designer. Require actual data.
  * Sassa: Skyhopper~3000USD / DVL-1~500USD
  * Mario: Reconstruction, SLAM, 
  * Glenn: To create an unmanned vehicle system robotics and AI to help people. AI+Drone.

# 2017/12/06 Wednesday
* Read the Tensorflow code for running a CNN. 
* Solve the problem of mysubmission.py in the project of google tensorflow command recogonition.

# 2017/12/05 Tuesday
* ZED camera data aquisition
Update ZED camera, create the folder and log file automatically. Problems:
  * Problem of computer bootup without HDMI connected still exists. The problem is, sometimes it can not mount the SD card. And I do not know why. The changement I've done:
  1. I've changed to cpp to mount it, not bash. 
  2. I've delayed the programme to run after bootup. But, sometimes the system itself do the mount itself, but to another path, not the one I've signified. 
  * Problem of cut off electricity suddenly, and the SD card could not be recognized again. This problem sometimes happens, I still do not know why. Maybe the reason is, it still writing into the sd card when I cut off the electricity.

# 2017/12/04 Monday
* Field Test Experiment
First time to go out for the field test experiment. I just wanna see how those things used in real life. But it just a test. They have tested the following functions:
  * Go and return function by Randy
  To control the vehicle to go far away and let it return automatically. Seems work all right.
  * 3D reconstruction by Mario
  He used a Lidar to get the point cloud of the field, and try to reconstruct it in 3d. But seems failed because the noise. The reason of the noise is unclear.
  * The function of running the small car with man on it. 
  It runs quite well on the flat land, but when it goes to the field with up and downs, it stucked quite frequently. That's a big problem.
  * Using the webpage to control the vehicle through WIFI by Ali.
  Seems work quite well, but he hasn't test the distance it can be. Normally Wifi is not good for long distance, that's the key weekness of Wifi.
  * RTK gpu, to do the accurate location.
  They use RTK to let the vehicle to run in a straight line for about 200 meters. Succeed finally after a long adjustements. That seems quite good.
  * Video transmission test by Glenn and Sassa
  They planned to get the test on a Drone, but they encountered the problem of signal noise. So they quite the fly. Then they try distance of the video transmission module on earth, seems about 50 meters.
 * Summary of the test
 I have to admit that it's not quite a impressive field test. But that's what happened everyday before do something really impressive. I think of several points that may make the test better or effective:
   * It seems no plan before the test, no preparation of potential risk of failure.
   * Some test seems do not need to go for that far away(one hours by car) to do it.
   * No summary meeting after the test, how to get the most out of the test?

# 2017/12/01 Friday
* Auto Drone Station
Think, search, communicate to gather the information of Auto Drone station.

* Charging Mechanism

[Skysense Charging Pad and Droneport](http://www.skysense.co)

[edronic](http://www.edronic.com)

[H3dynamics Drone box](https://www.h3dynamics.com/products/drone-box/)

[Identified Technologies](https://www.identifiedtech.com/blog/uav-surveying/autonomous-mapping-boomerang-drone-and-docking-charging-station/)

* Landing Navigation

Precision real-time Landing(Image recognition, LiDAR, other sensors)

[MarkOne Precision Landing Tutorial](https://irlock.readme.io/v2.0/docs)

[Precision Landing and Loiter with IR-LOCK](http://ardupilot.org/copter/docs/precision-landing-with-irlock.html)

* Visual Tracking

[ZhiHu](https://www.zhihu.com/question/26493945)

[YOLO](https://pjreddie.com/darknet/yolo/)

* PID Control

* Prototypes

[World's First Home w/ Drone Charging Station](https://www.youtube.com/watch?v=061Qhkr7XCE)

{% endpost #9D9D9D %}
