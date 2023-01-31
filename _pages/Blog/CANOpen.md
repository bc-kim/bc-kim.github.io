---
permalink: /blog/canopen
title: "Motor control using STM board and CANopen"
layout : single

author_profile: false
classes: wide
sidebar:
  nav: "blog"

---
This page introduces brief information about a method to control the motors using CANopen communication and STM board. In addition, this page briefly explains basic information about CAN and CANOpen communication. The contents written here refers following sites and contents [1-7]. For more details please see the references. The practical demonstration is done using:

- Nucleo F-446 Re board
- MC5004P from Faulhaber
- MCDC3002P from Faulhaber

## CAN vs CANOpen communication
Before explaning the CANopen protocol, we should distinguish CANopen protocol from Controller Area Network (CAN) protocol - CANOpen protocol is a high-level protocol that communicates with other CANOpen device while CAN protocol is a lower level protocol related how to send the message electrically. In terms of [OSI communication  model][osi_layer], that defines 7 distinct layers in communication, the CAN protocol deals with lower layers (physical and data link layer) of OSI model while the CANOpen protocol deals with other five layers of the OSI model. 

Practically, CANprotocol can be thought as a protocol that defines how to send a message physically (i.e., electrically) while CANOpen protocol can be thougt a protocol 

For instance, if we send a message 0x6040, CAN protocol defines how to send this message. On the other hand, CANOpen protocol focus on what a message 0x6040 actually means.

In practical, CANprotocl could be thought as a 

CAN protocol is a lower-layer protocol used for . Since CANOpen communication is based on CAN protocol (which is obvious), we would first walk through the CAN communication here. CANOpen Communication follows in the next section.

## 1. CAN communication

### 1.1 Basic structure of CAN message

Since 
To send or receive CAN message, we have to understand the basic structure of CAN message.  consists of 

### 1.2 CAN settings at cubeMx

### 1.3 Wiring for CAN communication

### 1.4 Initialization of CAN communication
In STM controllers, we first have to initialize the configuration of the CAN. In this state, the code determines which messages the device listens to and which messages it doesn't listen to.

configuration as below. Since our goal is to develop master node rather than slave node, I usually don't make any filter for the CAN communication. So the initialization code is quite simple as below. 

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



## 2. CANOpen Communication

###2.1 CANOpen message basic structure
With given setup for CAN protocol as explained in Chapter 1, we can now send or receive CANOpen messages. The structure consists of CANOpen message has following 

### 2.2 Send CANOpen message
To send CAN message, we have to define two variables: 1) TxHeader and 2) data. TxHeader contains basic information about the CAN message while data contains a specific CAN message. 


```c
// [Example 1.2.1 Send CAN message]
TxHeader.StdId = cobID;
TxHeader.RTR = rtr == 0;
TxHeader.IDE = CAN_ID_STD;
TxHeader.DLC = len;
data[0] = 0x00;
data[1] = 0x01;
data[2] = 0x02;
while(HAL_CAN_GetTxMailboxesFreeLevel(&hcan1) == 0);
  HAL_CAN_AddTxMessage(&hcan1, &TxHeader, data, &TxMailbox);
while(HAL_CAN_IsTxMessagePending(&hcan1, TxMailbox) == 1);
```

### 2.3 Receive CANOpen message

To receive CAN message, I ususally use two different methods. First method is pulling method. 

When we want to receive the CAN message using interrupt method, we should define interrupt function as below. Here, received data is saved in *RxHeader* and *RxData*. 

```c
// [Example 1.3.1 Receive CAN message using interrupt]
void HAL_CAN_RxFifo0MsgPendingCallback(CAN_HandleTypeDef *hcan) // HAL_Can interrupt
{
  if (hcan->Instance == CAN1)
  {
    HAL_CAN_GetRxMessage(&hcan1, CAN_RX_FIFO0, &RxHeader, RxData);
  }
}
```

Since we can now send and receive CAN messages, we can use CANOpen to communicate with other CANOpen devices (e.g. motor driver). Among many functions in CANOpen protocol, I have used following three protocols:
 - Network Management (NMT)
 - Service Data Object (SDO)
 - Process Data Object (PDO)

In this blog, I would briefly explain above three protocols and how to implement them in actual STM codes. For more details on NMT, SDO, and PDO, please see reference listed below.


### 2.1 NMT
When we aim to communicate with motor driver, we first have to know about NMT. Briefly, NMT defines the network state of the device - the CANOpen device 

- Initilization
- Pre-operational
- 

For this reason, when we first want to 

{% capture fig_img %}
![Foo]({{ "/assets/images/Researches/SliderTendonLinearActuator/Fig1.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Fig. 1 Soft wearable robot application using the Slider-Tendon Linear Actuator. The proposed actuator provides adaptability and usability to the soft wearable robot by including functions such as fast-connection, under-actuation mechanism, and stroke amplification.</figcaption>
</figure>

```c
// Start_Remote_node //

// Enter_Pre_operation // 

// Stop_Remote_node //

// Reset_node //

// Reset_Communication //
if (CAN_NMT(Start_Remote_node, Node[i], Delay) == Operational)
{
  CAN_Device_Control(Shut_down, Node[i]);
  HAL_Delay(Delay);
  CAN_Device_Control(Switch_on, Node[i]);
  HAL_Delay(Delay);
  CAN_Device_Control(Enable_operation, Node[i]);
}

```

CAN communication is one of well used protocol used to communicate between the electric devices. 

Controlling the motor requires in-depth understanding on the working principle of the motor. Also, the motor requires high electric power, therefore, additional circuit is required to operate the motor. For this reason, an electric circuit called `motor driver' has been dedicated to controlling the motor. In this way, we can control the motor in a real-time without burdening the main controller. 

When controlling the motor using the motor driver, it is important to follow the communication protocol for the motor driver. CANOpen protocol is one of the well used communication protocol for the motor control. It is because this protocol provides researchers a variety of features to reliably control the motor in real time. *I have experience controlling 4 motors with 1Khz control loop using CANOpen (Details are here.). I am also confident in constructing robot system using a high-level controller (ROS) and low-level controller(STM) with this CANOpen protocol.* Details of how I constructed the high-level and low-level controller is described in below.

### 2.2 SDO
CANopen devices have their object dictionary 

defines all the information 

```c 
  CAN_Device_Control(Shut_down, Node[i]);
  HAL_Delay(Delay);
  CAN_Device_Control(Switch_on, Node[i]);
  HAL_Delay(Delay);
  CAN_Device_Control(Enable_operation, Node[i]);
```

### 2.3 PDO
Since SDO deals with a single object dictionary per single message frame, a communication using SDO may be seem inefficient - because we need some overhead when using SDO (such as index and subindex). 

Alternative way to deal with this issue is a method of using PDO - in most of cases, PDO is used to transfer desired/current motor values (e.g., motor position, velocity, torque) in a real-time manner.

PDO can be categorized into TxPDO and RxPDO. 
For PDO communication, we have to first map object to PDO entry. When using Faulhaber motor driver, PDO mapping can be done by using motion manager. (It can be downloaded here)

For example, if we mapped "current position" to PDO-1, the 

```c

```

Also, if we mapped "target velocity" to PDO-1, we can change the motor velocity by sending PDO message as 

```c

```


[1] [Overal view of CAN & CANOpen][CAN_cia] 

[2] [CAN description from NI][CAN_NI] 

[3] [CANOpen description from NI][CANOpen_NI]

[CAN_cia]: https://www.can-cia.org
[CAN_NI]: https://www.ni.com/en-us/innovations/white-papers/06/controller-area-network--can--overview.html
[CANOpen_NI]: https://www.ni.com/en-us/innovations/white-papers/13/the-basics-of-canopen.html
[osi_layer]: https://en.wikipedia.org/wiki/OSI_model