---
permalink: /blog/canopen
title: "Motor control using STM board and CANopen"
layout : single

author_profile: false
classes: wide
sidebar:
  nav: "blog"

---
This page introduces brief information about a method to control the motor using CANopen communication and Nucleo F-446 RE board. 

## 1. CAN Communication
Before explaning the CANopen protocol, we should know distinguish CANopen protocol from Controller Area Network (CAN) protocol. CAN protocol is a lower-layer protocol used for 

### 1.1 Initialization of CAN communication
To establish CAN communication, we should first initialize the CAN configuration as below. Since our goal is to develop master node rather than slave node, I usually don't make any filter for the CAN communication. So the initialization code is quite simple as below. 

```c
  // [[ 1. Init CAN ]]
  CAN_FilterTypeDef sFilterConfig;
  sFilterConfig.FilterBank = 0;
  sFilterConfig.FilterMode = CAN_FILTERMODE_IDMASK;
  sFilterConfig.FilterScale = CAN_FILTERSCALE_16BIT;
  sFilterConfig.FilterIdHigh = 0x0000;
  sFilterConfig.FilterIdLow = 0x0000;
  sFilterConfig.FilterMaskIdHigh = 0x0000;
  sFilterConfig.FilterMaskIdLow = 0x0000;
  sFilterConfig.FilterFIFOAssignment = CAN_RX_FIFO0;
  sFilterConfig.FilterActivation = ENABLE;
  sFilterConfig.SlaveStartFilterBank = 14;

  if (HAL_CAN_ConfigFilter(&hcan1, &sFilterConfig) != HAL_OK)
  {
    Error_Handler();
  }
  HAL_CAN_ActivateNotification(&hcan1, CAN_IT_RX_FIFO0_MSG_PENDING);
  if (HAL_CAN_Start(&hcan1) != HAL_OK)
  {
    Error_Handler();
  }
```

After 
### 1.2 Send CAN message

### 1.3 Receive CAN message

## 2. CANOpen Communication

Since we can now send and receive CAN messages, now we can build higher level communication using CANOpen rules. Among many functions related to CANOpen protocol, following three protocol should be considered in practical cases. 
 - NMT
 - SDO
 - PDO

### 2.1 NMT



CAN communication is one of well used protocol used to communicate between the electric devices. 

Controlling the motor requires in-depth understanding on the working principle of the motor. Also, the motor requires high electric power, therefore, additional circuit is required to operate the motor. For this reason, an electric circuit called `motor driver' has been dedicated to controlling the motor. In this way, we can control the motor in a real-time without burdening the main controller. 

When controlling the motor using the motor driver, it is important to follow the communication protocol for the motor driver. [CANOpen][cia_link] protocol is one of the well used communication protocol for the motor control. It is because this protocol provides researchers a variety of features to reliably control the motor in real time. *I have experience controlling 4 motors with 1Khz control loop using CANOpen (Details are [here][mycanopen_link].). I am also confident in constructing robot system using a high-level controller (ROS) and low-level controller(STM) with this CANOpen protocol.* Details of how I constructed the high-level and low-level controller is described in below.


Among several rules 
###1.1 NMT

###1.2 SDO

###1.3 PDO

