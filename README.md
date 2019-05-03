# Porky: The Real-Time Object Detecting Robot
The goal of this project is to demonstrate how to create a real-time object detection autonomous robot with relatively inexpensive components. By training your own Machine Learning model and pairing Intel's Neural Compute Stick 2 with a Raspberry Pi 3 B+, you'll be able jumpstart your next real-time object detection project! 

TODO: pictures and gif of robot in action

## Table of Contents
* [Project Overview](#project-overview)
* [Update History](#update-history)
* [Hardware List](#hardware-list)
  * [Required Hardware](#required-hardware)
  * [Optional Hardware](#optional-hardware)
* [Hardware Configuration](#hardware-configuration)
  * [Image Capturing Setup](#image-capturing-setup)
  * [Tweak and Test Setup](#tweak-and-test-setup)
  * [Live Deployment Setup](#live-deployment-setup)
* [Train Object Detection Model with TensorFlow](#train-object-detection-model-with-tensorflow)
* [Optimize Model for Intel Neural Compute Stick 2](#optimize-model-for-intel-neural-compute-stick-2)
  * [Install OpenVINO on Dev PC](#install-openvino-on-dev-pc)
* [Deploy the Optimized Model](#deploy-the-optimized-model)
  * [Install Raspberian on Raspberry Pi](#install-raspberian-on-raspberry-pi)
  * [Install OpenVINO on Raspberry Pi](#install-openvino-on-raspberry-pi)
  * [Clone this Repository](#clone-this-repository)
* [Testing](#testing)
* [Deploy the Robot](#deploy-the-robot)
* [Feedback Statement](#feedback-statement)
* [References and Acknowledgements](#references-and-acknowledgements)

## Update History
**2019/05/09:** Initial Release

## Project Overview
This guide will teach you how to: 
* Train your own model in TensorFlow using a Transfer Learning technique to save time and money 
* Optimize the resulting TensorFlow model to be utilized with Intel's Inference Engine
* Implement the optimized model into a Python script
* Deploy the program with real-time performance and feedback loops

## Hardware List
While some of the hardware in this section is described as 'Required' or 'Optional', this is only if you want to follow this guide step-by-step. This does not mean you are restricted to these components if you want to swap, subtract, or add components. However, for the best initial results (if your intention is to follow this guide), I highly suggest acquiring the components within the 'Required Hardware' section at the very least. This will enable you to train a Machine Learning model and perform Real-Time Object Detection. My personal favorite sites for finding components for robotic projects are [Adafruit](https://www.adafruit.com/), [RobotShop](https://www.robotshop.com/), and [eBay](https://www.ebay.com/) (useful for scoring great deals on used parts). The possibilities are endless!

#### Required Hardware
* **Raspberry Pi 3 B+** w/ MicroSD Card and a way to power the device (battery or AC wall adapter)
* **[Intel Neural Compute Stick 2 (NCS2)](https://software.intel.com/en-us/neural-compute-stick/where-to-buy)**
* **USB or Pi Camera** This project uses the [PS3 Eye Camera](https://en.wikipedia.org/wiki/PlayStation_Eye) which can be found on eBay for about $6 USD each.

#### Optional Hardware
TODO: clean and add links
* **Development PC (Linux, Windows, MacOS)** Development for this project was performed on a Windows 10 platform.
* **Display Monitor w/ HDMI Output** Helpful for debugging and testing within Raspberry Pi environment.
* **Robot Chassis Kit w/ Motors** This project uses the [Lynxmotion 4WD1 Rover Kit](http://www.lynxmotion.com/c-111-a4wd1-no-electronics.aspx). You can purchase this kit directly from [RobotShop](https://www.robotshop.com) or find a used kit on eBay.
* **Servos x2 w/ Mounting Hardware** This project uses the [Lynxmotion Pan and Tilt Kit](https://www.robotshop.com/en/lynxmotion-pan-and-tilt-kit-aluminium2.html).
* **PWM/Servo Controller** This project uses this [one](https://www.amazon.com/Channel-Driver-interface-PCA9685-arduino-Raspberry/dp/B01D9VNXEQ/ref=sr_1_fkmrnull_1?keywords=ficbox+pwm%2Fservo&qid=1556889116&s=gateway&sr=8-1-fkmrnull) from Amazon.
* **Motor Controller** This project uses the [Sabertooth 2X12 Regenerative Dual Channel Motor Controller](http://www.lynxmotion.com/p-562-sabertooth-2x12-regenerative-dual-channel-motor-controller.aspx) which can be found at [RobotShop](https://www.robotshop.com).
* **Li-Po Battery** To power the motor controller. This project uses a 3S 11.1V 6000 mAh LiPo battery with an XT60 Plug. Search on Amazon or eBay for deals. **These batteries are known to cause fires, so please be aware of the risks and proper handling procedures.** 
* **Balance Charger/Discharger** To charge/discharge your Li-Po Battery safely. I use the [SKYRC iMAX B6 Mini](https://www.amazon.com/SKYRC-Professional-Balance-Discharger-Batteries/dp/B00YAASVGQ/ref=pd_sbs_21_5/144-5415705-1628207?_encoding=UTF8&pd_rd_i=B00YAASVGQ&pd_rd_r=cf5ae83e-6daa-11e9-8254-d7002cb5b05b&pd_rd_w=JfidM&pd_rd_wg=07fLG&pf_rd_p=588939de-d3f8-42f1-a3d8-d556eae5797d&pf_rd_r=HTGJGSAZSPKNNAG7NR62&psc=1&refRID=HTGJGSAZSPKNNAG7NR62). Note: this charger requires the charging unit itself and a wall adapter/power supply, ensure you're purchasing both.
* **Portable Powerbank** Be aware that not all portable chargers are compatible for Raspberry Pi projects. This project uses this [RAVPower Portable Charger](https://www.amazon.com/Portable-RAVPower-26800mAh-Double-Speed-Recharging/dp/B07793KSV4/ref=sr_1_3?keywords=ravpower+usb+c+portable+charger&qid=1556890740&s=industrial&sr=1-3-catcorr).
* **Electrical Tape**
* **Mounting Arm** For holding the Pan and Tilt Kit, this project uses the [VideoSecu 1/4" Security Camera Mount](https://www.amazon.com/VideoSecu-Security-Adjustable-Universal-Mounting/dp/B000IDCDZY/ref=sr_1_fkmrnull_1?crid=15XODHE8DCCAT&keywords=videosecu+1%2F4%22+x+20+thread+swivel+security+camera+mount&qid=1556890057&s=gateway&sprefix=videosecu+1%2F4%22+x%2Caps%2C215&sr=8-1-fkmrnull) and the [SMALLRIG Super Clamp w/ 1/4" and 3/8" Thread](https://www.amazon.com/Smallrig-Thread-Cameras-Umbrellas-Shelves/dp/B0062U2M4E/ref=sr_1_fkmrnull_3?crid=1QMJ6ZJIAWL7&keywords=smallrig+super+clamp+w%2F1%2F4+and+3%2F8&qid=1556890140&s=electronics&sprefix=smallrig+super+clamp%2Caps%2C1424&sr=1-3-fkmrnull).
* **iFixit Toolkit** I use the [iFixit Pro Tech Toolkit](https://www.amazon.com/iFixit-Pro-Tech-Toolkit-Electronics/dp/B01GF0KV6G/ref=sr_1_2?keywords=ifixit&qid=1556889807&s=gateway&sr=8-2) (highly recommended if you do a lot of tinkering).
* **Velcro Tape (for modular prototype mounting)** I used a [2" Adhesive Black Hook and Loop Tape](https://www.amazon.com/Strenco-Adhesive-Black-Hook-Loop/dp/B00H3R9S1K/ref=sr_1_3?crid=2S3OQ9CVTVMCF&keywords=adhesive+black+hook+and+loop+tape&qid=1556890301&s=industrial&sprefix=adhesive+black+hook+an%2Celectronics%2C406&sr=1-3).
* **Assorted Electrical Components (switches, buttons, wires, breadboards, etc)** Check out [Adafruit](https://www.adafruit.com/) for great deals on electrical components.

## Hardware Configuration
The wiring diagrams contained within this section were created with [Fritzing](http://fritzing.org/home/), a fantastic open-source tool.

#### Image Capturing Setup
To train your own Machine Learning model, you will need to gather the data to train and validate your model on. The idea for this project was to train the model based on images captured with an identical camera that was eventually going to be deployed live.

This setup consists of:
* **Raspberry Pi 3 B+** w/ MicroSD Card and a way to power the device (battery or AC wall adapter)
* **PS3 Eye USB Camera** TODO: provide a link to ebay search
* **Portable Powerbank** TODO: update this name and link
* **Mini Button** TODO: provide a link to adafruit buttons
* **Breadboard** TODO: provide a link to adafruit breadboards
* **2 Female to Male Wires** TODO: provide a link to adafruit wires

Please see the [Capture Images with the Image Capturing Setup](#capture-images-with-the-capturing-setup) section to capture your own images for your dataset using this hardware configuration.

#### Tweak and Test Setup
This hardware configuration serves the purpose for testing your hardware components (motors, servos, etc) and software integrations (debugging, testing, sandbox). This setup is geared towards using AC wall adapters to save batteries and keeping moving components as stationary as possible. Having a proper testing setup can potentially save lots of frustration and money. It is strongly suggested to test your own project before deploying it into the wild.

#### Live Deployment Setup
After performing adequate hardware and software tests, you'll be ready to release your autonomous robot without its leash. This section will show you how to configure your robot to be deployed live. 

## Train Object Detection Model with TensorFlow
The goal of this section is to use TensorFlow to train your custom model using Transfer Learning. While creating your own Machine Learning model can be extremely rewarding, that process typically involves much configuration, troubleshooting, and training/validating time. A very costly process. However, with Transfer Learning, you can minimize all three fronts by choosing an already proven model to customize with your own dataset.

#### Create Your Dataset

###### Capture Images with the [Image Capturing Setup](#image-capturing-setup)

###### Label the Captured Images with LabelIMG

#### Install the TensorFlow Framework onto Dev PC

#### Convert the Images and Annotations into TFRecord Format

#### Pick an Already Trained Model and Use Transfer Learning

#### Deploy the TensorFlow Training Session

##### Using Google Cloud for Machine Learning

#### Extract the Trained Model

## Optimize Model for Intel Neural Compute Stick 2

#### Install OpenVINO on Dev PC

## Deploy the Optimized Model

#### Install Raspberian on Raspberry Pi

#### Install OpenVINO on Raspberry Pi

#### Clone this Repository

## Testing
During the lifecycle of your robot project, it's a good idea to develop and maintain some sort of testing strategy. In this section, I will break down how to use the provided testing scripts and their purpose.
#### Hardware Specific Tests
###### Test the Camera
###### Test the Motors
###### Test the Servos

#### Unit Tests
###### Test the ML Model
###### Test the Camera Process
###### Test the Detection Process

#### Integration Tests
###### Test Detection with Pan and Tilt
###### Test Detection with Pan and Follow

## Deploy the Robot

## Feedback Statement
I tried my best to detail all of the processes I used to get this project off the ground, but I may have missed some key steps along the way or you may have experienced some frustrations trying to follow along. With that being said, please don't hesitate to drop me any comments, questions or concerns. I promise to do my best to address your issues.

TODO: add contact links

## References and Acknowledgements
**[leswright1977/Rpi3_NCS2](https://github.com/leswright1977/RPi3_NCS2):** leswright1977's bottle-chasing robot introduced me to the Intel NCS2 and its ability to integrate machine learning models for real-time applications.

**[PINTO0309](https://github.com/PINTO0309):** PINTO0309's [MobileNet-SSD-RealSense](https://github.com/PINTO0309/MobileNet-SSD-RealSense) project provided a ton of inspiration for this project especially for the use of hardware choices and multiprocessing in Python to optimize performance.

**[OpenCV Docs](https://docs.opencv.org/):** The official documentation for OpenCV. Necessary for gaining a strong foundation of using OpenCV to build your application.

**[Adafruit Pixy Pet Robot](https://learn.adafruit.com/pixy-pet-robot-color-vision-follower-using-pixycam/overview):** Adafruit's guide on creating color vision following robot using a Pixy CMUCam-5 vision system and Zumo robot platform. This guide was very helpful for learning how to integrate a PID (Proportional-Integral-Deravitive) control feedback loop for the motion mechanisms.
