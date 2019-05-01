# Create Your Own Object Chasing Robot w/ TensorFlow, Raspberry Pi, and Intel Neural Compute Stick 2
This project demonstrates how to create your own object chasing robot using machine learning, a Raspberry Pi, and Intel's Neural Compute Stick 2. This guide will hopefully jump start your own real-time object detecting robot.

TODO: insert gif of robot in action

## Table of Contents
* [Project Overview](#project-overview)
* [Hardware List](#hardware-list)
  * [Required Hardware](#required-hardware)
  * [Optional Hardware](#optional-hardware)
* [Hardware Configuration](#hardware-configuration)
  * [Image Capturing Setup](#image-capturing-setup)
  * [Tweak and Test Setup](#tweak-and-test-setup)
  * [Live Deployment Setup](#live-deployment-setup)
* [Train ML Model with TensorFlow](#train-object-detection-model-with-tensorflow)
* [Optimize Model for Intel Neural Compute Stick 2](#optimize-model-for-intel-neural-compute-stick-2)
  * [Install OpenVINO on Dev PC](#install-openvino-on-dev-pc)
* [Deploy the Optimized Model](#deploy-the-optimized-model)
  * [Install Raspberian on Raspberry Pi](#install-raspberian-on-raspberry-pi)
  * [Install OpenVINO on Raspberry Pi](#install-openvino-on-raspberry-pi)
  * [Clone this Repository onto Raspberry Pi](#clone-this-repository-onto-raspberry-pi)
* [Testing](#testing)
* [Deploy the Robot](#deploy-the-robot)
* [References and Acknowledgements](#references-and-acknowledgements)

## Project Overview
This guide will teach you how to: 
* train your own model in TensorFlow using a Transfer Learning technique to save time and money 
* optimize the resulting TensorFlow model to be utilized with Intel's Inference Engine
* implement the 

## Hardware List
this section describes the hardware involved in the project
#### Required Hardware
* **Raspberry Pi 3 B+**
* **MicroSD Card for Raspberry Pi**
* **Intel Neural Compute Stick 2 (NCS2)**
* **USB or Pi Camera** This project uses the [PS3 Eye Camera](https://en.wikipedia.org/wiki/PlayStation_Eye) which can be found on eBay for about $6 USD each.
* **Robot Chassis Kit w/ Motors** This project uses the [Lynxmotion 4WD1 Rover Kit](http://www.lynxmotion.com/c-111-a4wd1-no-electronics.aspx). You can purchase this kit directly from [RobotShop](https://www.robotshop.com) or find a used kit on eBay.
* **Servos x2 w/ Mounting Hardware** This project uses the [Lynxmotion Pan and Tilt Kit](https://www.robotshop.com/en/lynxmotion-pan-and-tilt-kit-aluminium2.html).
* **PWM Controller**
* **Mounting Hardware** Please refer to the [Optional Hardware](#optional-hardware) section for the list of mounting hardware this project uses.
* **Assorted Electrical Components (switches, buttons, wires, etc)** Check out [Adafruit](https://www.adafruit.com/) for great deals and tutorials on anything electrical.
* **Power Delivery Devices (Batteries/AC Adapters)** Please refer to the [Optional Hardware](#optional-hardware) section for the list of power delivery devices this project uses.

#### Optional Hardware
TODO: clean and add links
* **Development PC (Linux, Windows, MacOS)** Development for this project was performed on a Windows 10 platform.
* **Display Monitor w/ HDMI Output** Helpful for debugging and testing within Raspberry Pi environment.
* **Arduino Uno3**
* **Electrical Tape**
* **Small Rig Mounting Arm** TODO: Needs link
* **iFixit Toolkit** TODO: Needs link
* **Velcro Tape (for modular prototype mounting)** TODO: Needs link
* **Breadboards for Prototyping**

## Hardware Configuration

#### Image Capturing Setup

#### Tweak and Test Setup

#### Live Deployment Setup

## Train Object Detection Model with TensorFlow

#### Install the TensorFlow Framework onto Dev PC

#### Label the Captured Images with LabelIMG

#### Convert the Images and Annotations into TFRecord Format

#### Pick an Already Trained Model to Perform Transfer Learning On

#### Deploy the TensorFlow Training Session

##### Using Google Cloud for Machine Learning

#### Extract the Trained Model

## Optimize Model for Intel Neural Compute Stick 2

#### Install OpenVINO on Dev PC

## Configure the Raspberry Pi Environment

## Deploy the Optimized Model

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

## References and Acknowledgements
