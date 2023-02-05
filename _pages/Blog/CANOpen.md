---
permalink: /blog/canopen
title: "Motor control using STM board and CANopen"
layout : single

author_profile: false
classes: wide
sidebar:
  nav: "blog"

---
CAN communication is one of well used protocol used to communicate between the electric devices. When we want to control the motor, it requires in-depth understanding on the working principle of the motor. Also, the motor requires high electric power, therefore, additional circuit is required to operate the motor. For this reason, an electric circuit called `motor driver' has been dedicated to controlling the motor. In this way, we can control the motor in a real-time without burdening the main controller. 

For more effecient way to control the motor in a real-time, motor drivers were designed using several communication protocols. CANOpen protocol is one of the well used communication protocol for the motor control. It is because this protocol provides researchers a variety of features to reliably control the motor in real time. This page introduces brief information about a method to control the motors using CANopen communication and STM board. In addition, this page briefly explains basic information about CAN and CANOpen communication. The contents written here refers following sites and contents [1-7]. For more details please see the references. The practical demonstration is conducted using:

- Nucleo F-446 Re board
- MC5004P from Faulhaber
- MCDC3002P from Faulhaber

 
## 1. Basic information of CAN & CANOpen

### 1.1 Difference between CAN and CANOpen communication
Before explaning the CANopen protocol, we should distinguish CANopen protocol from Controller Area Network (CAN) protocol - CANOpen protocol is a high-level protocol that communicates with other CANOpen device while CAN protocol is a lower level protocol related how to send the message electrically. In terms of [OSI communication  model][osi_layer], that defines 7 distinct layers in communication, the CAN protocol deals with lower layers (physical and data link layer) of OSI model while the CANOpen protocol deals with other five layers of the OSI model. 

Practically, CAN is related to a method of sending/receivng bit messages physically (i.e., electrically). On the other hand, CANOpen can be thought as a protocol that defines meaning of each messages. For instance, if we send a message 0x6040, CAN defines how to send this message. On the other hand, CANOpen protocol focus on an actual meaning of 0x6040.


### 1.2 Structure of CAN and CANOpen message
Standard CAN frame consists of 8 different types of message fields, which are 1) Start of Frame (SOF, 1bit), 2) Identifier (ID, 11 bits), 3) Remote Transmission Request (RTR, 1 bit), 4) Control (6 bits), 5) Data (0-64 bits), 6) Cyclic Redundancy Check (CRC, 16 bits), 7) Acknowledgment (ACK, 2 bits), and 8) End of Frame (EOF, 7 bits). 

Since the CAN message structure is complex (but it is important for reliable communication), sending/reciving CAN frames can be annoying for those who want to use CAN Bus. Therefore, we will not explain 8 message fields here - details are well explained in [[4]][CANOpen_CSS]. It is because, when we write a code to send/receive the CAN message, we don't need to know about these message fields.

Instead of considering 8 message fields, we have to know about


1) Communication Object Identifier (COB-ID)
2) Remote Transmission Request (RTR)
3) Data length
4) Data

 
when writing a code for CAN communication - i.e., the hardwares automatically translate them to CAN message. So we would focus on COB-ID, Data length, and Data, when we write a code for CANOpen.

COB-ID (11 bits) is a identifier consists of two parts: Function code and Node ID. The Function code (4 bits) represents the aim of message - it could be NMT, SYNC, EMCY, TIME, PDO, SDO, and HEARTBEAT. Details of Function code will be explained in the next subsection. The node number (7 bits), on the other side, means the address of the device. Each device has their own node number (which we can change by setting) from 1~127. 

RTR is used to specify whether the message is requesting a message or not. It distinguishes whether the master node is requesting a message or sending a message to other devices. The data length is exact byte size of the data.

### 1.3 Service types of the CANOpen message

As we showed in the previous subsection, there exists useful service types (NMT, SYNC, EMCY, TIME, PDO, SDO, and HEARTBEAT) in CANOpen protocol. These service types help us communicating other device effectively. In this blog, we would cover NMT, PDO, and SDO because we can control the motor even with only three service types. 

#### 1.3.1 NMT
NMT stands for Network managements. 

 - Network Management (NMT)
 - Service Data Object (SDO)
 - Process Data Object (PDO)

In this blog, I would briefly explain above three protocols and how to implement them in actual STM codes. For more details on NMT, SDO, and PDO, please see reference listed below.


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


### 2.2 SDO
CANopen devices have their object dictionary 

defines all the information 

```c 

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

## 3. Implementation 

Before writing a code for CANOpen communication, we have to configure the CAN bus using STM cubeMX. In cubeMX, we deal with hardware layer of the CAN bus. 
### 3.1 Wiring for CAN communication
As a first step, we have to construct CAN-Bus that connects our MCU board (i.e., Nucleo F-446RE) and motor driver. 

### 3.2 CAN settings at cubeMx

Since we are using STM boards, we first have to use cubeMx in order to configure basic settings for the CAN communication.


### 3.3 Initialization of CAN communication (in STM codes)
Before writing a code for CANOpen communication, we have to configure the CAN in STM. 

In this state, the code determines which messages the device listens to and which messages it doesn't listen to. When we want to get all the messages in the bus (Since we usually develop master node rather than slave node, not using any filter for the CAN communication is common.), the filter can be written as below: 

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

### 3.3 Send CAN message

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


### 
```c
// Start_Remote_node //

// Enter_Pre_operation // 

// Stop_Remote_node //

// Reset_node //

// Reset_Communication //


```


[1] [Overal view of CAN & CANOpen][CAN_cia] 

[2] [CAN description from NI][CAN_NI] 

[3] [CANOpen description from NI][CANOpen_NI]

[4] [CAN and CANOpen intro from CSS][CANOpen_CSS]

[CAN_cia]: https://www.can-cia.org
[CAN_NI]: https://www.ni.com/en-us/innovations/white-papers/06/controller-area-network--can--overview.html
[CANOpen_NI]: https://www.ni.com/en-us/innovations/white-papers/13/the-basics-of-canopen.html
[osi_layer]: https://en.wikipedia.org/wiki/OSI_model
[CANOpen_CSS]: https://www.csselectronics.com/pages/can-bus-intros-tutorials