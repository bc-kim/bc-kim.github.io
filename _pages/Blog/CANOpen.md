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
Standard CAN frame consists of 8 different types of message fields, which are 1. Start of Frame (SOF), 2. Identifier (ID), 3. Remote Transmission Request (RTR), 4. Control, 5. Data, 6. Cyclic Redundancy Check (CRC), 7. Acknowledgment (ACK), and 8. End of Frame (EOF). 

Since the CAN message structure is complex, sending/reciving CAN frames could be annoying for those who want to use CAN Bus. Therefore, we will not explain 8 message fields here - details are well explained in [[4]][CANOpen_CSS]. It is because, when we write a code to send/receive the CAN message, we don't need to know about these message fields.

Instead of considering 8 message fields, we have to know about

- Communication Object Identifier (COB-ID)
- Remote Transmission Request (RTR)
- Data
- Data length

when writing a code for CAN communication - i.e., the hardwares automatically translate them to CAN message. So we would focus on COB-ID, Data length, and Data, when we write a code for CANOpen.

COB-ID (11 bits) is a identifier consists of two parts: Function code and Node ID. The Function code (4 bits) represents the aim of message - it could be NMT, SYNC, EMCY, TIME, PDO, SDO, and HEARTBEAT. Details of Function code will be explained in the next subsection. The node number (7 bits), on the other side, means the address of the device. Each device has their own node number (which we can change by setting) from 1~127. 

RTR is used to specify whether the message is requesting a message or not. It distinguishes whether the master node is requesting a message or sending a message to other devices. The data contains the content that the message wants to convey while the data length is byte size of the data; the size of data is 0~64 bits while the data length is 4 bits.

### 1.3 Service types of the CANOpen message

As described in the previous subsection, there exists useful service types (NMT, SYNC, EMCY, TIME, PDO, SDO, and HEARTBEAT) in CANOpen protocol. These service types help engineers communicating other device effectively. In this blog, we would cover Network Management (NMT), Service Data Object (SDO) and Process Data Object (PDO) because we can control the motor even with only three service types. 

#### 1.3.1 NMT

NMT, which stands for Network Managements, is used to manage the device state. According to CANOpen protocol, the device has four states as below:

- Initialization
- Pre-Operational
- Operational
- Stopped

When the CANOpen device boots up (i.e., when we apply power to the CANOpen device), the device automatically enters to "Initialization state". After initilization, the device sends a boot-up message and enters to "Pre-operational" state automatically - When we apply power to the CANOpen device, the device automatically enters to "Pre-operational" state after entering to "Initialization state". 

Once the device enters to "Pre-operational" state, the device state can be switched to one of three states (e.g., pre-operational state, operational state, Stopped state). Here, the state can be changed through 3 NMT messages as below:

- Message that switches to Pre-operational state (CS: 0x80)
- Message that switches to operational state (CS: 0x01)
- Message that switches to Stopped state  (CS: 0x02)

When we want to set the device state "Initialization state" again instead of above three states, it can be done by sending 2 NMT messages as below:

- Node Reset Message (CS: 0x81)
- Communication Reset Message (CS: 0x82)

Here, Reset Message (Node) resets all functions while Reset Message (Communication) only resets the communication functions. In summary, there exists total 5 NMT messages that switches the state of the machine. Also, it is notable that, the transition from "Initialization state" to "Pre-operational state" is done automatically. 

With given concept of NMT, the CAN message of NMT is constructed as follow. 

- COB-ID: 0x000
- RTR: 0 (NMT is NOT remote request message)
- Data length: 2 (bytes)
- Data: As below

| Data 1 	| Data 2 	| Data 3 	| Data 4 	| Data 5 	| Data 6 	| Data 7 	| Data 8 	|
|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|
| CS 	| Node ID  	| N/A  	| N/A 	| N/A  	| N/A 	| N/A  	| N/A 	|

Here, CS stands for Command Specifier which has different values (0x01, 0x02, 0x80, 0x81, 0x82 as described above) according to 5 NMT messages. Also, if we want to send NMT message for all devices at the CAN Bus, we can set Node ID as 0x00 to conduct this process. 

For example, if we want to switch the state of CANOpen device (that has Nide ID as 0x01) to Pre-operational state, we can do it by sending a CAN message as 

| COB-ID 	| Data 1 	| Data 2 	| Data 3 	| Data 4 	| Data 5 	| Data 6 	| Data 7 	| Data 8 	|
|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|
| 0x000 	| 0x80  	| 0x01  	| N/A 	| N/A  	| N/A 	| N/A  	| N/A 	| N/A  	|

Also, if we want to switch the state of all devices at the CAN Bus to Operational state, it can be done by sending a CAN message as 

| COB-ID 	| Data 1 	| Data 2 	| Data 3 	| Data 4 	| Data 5 	| Data 6 	| Data 7 	| Data 8 	|
|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|:-------:	|
| 0x000 	| 0x01  	| 0x00  	| N/A 	| N/A  	| N/A 	| N/A  	| N/A 	| N/A  	|

#### 1.3.2 SDO
When communicating with CANOpen devices, we have to know  *Object dictionary* - it is a data structure that contains all communication parmeters (it contains not only  motor control commands such as target/current velocity but also other data such as device manufacturer, interface data). Since Object dictionary of CANOpen devices can be usually found in their data sheet, so please see data sheet for more examples of Object dictionary. 

SDO, which stands for Service Data Object, is a protocol to read from or write to Object dictionary. 


#### 1.3.3 PDO
Since SDO deals with a single object dictionary per single message frame, a communication using SDO may be seem inefficient - because we need some overhead when using SDO (such as index and subindex). 

Alternative way to deal with this issue is a method of using PDO - in most of cases, PDO is used to transfer desired/current motor values (e.g., motor position, velocity, torque) in a real-time manner.

PDO can be categorized into TxPDO and RxPDO. 
For PDO communication, we have to first map object to PDO entry. When using Faulhaber motor driver, PDO mapping can be done by using motion manager. (It can be downloaded here)

## 2. Implementation 

Before writing a code for CANOpen communication, we have to configure the CAN bus using STM cubeMX. In cubeMX, we deal with hardware layer of the CAN bus. 
### 2.1 Wiring for CAN communication
As a first step, we have to construct CAN-Bus that connects our MCU board (i.e., Nucleo F-446RE) and motor driver. The wiring of CAN communication is simple (it is one big advantage of the CANOpen communication). Only thing we should do is to connect two wires. Please refer to [here][CAN_Wiring] for more detailed wiring method.

### 2.2 CAN settings at cubeMx
Since we are using STM boards, we first have to use cubeMx in order to configure basic settings for the CAN communication.


### 2.3 Initialization of CAN communication (in STM codes)
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

### 2.4 Send CANOpen message
To send CAN message, we have to define two variables: 1) TxHeader and 2) data. TxHeader contains basic information about the CAN message while data contains a specific CAN message. 

Below is a simple code that sends a CAN message. 
```c
// [Example 1.2.1 Send CAN message]
uint8_t codID;
uint8_t txData[8];
uint8_t Node;
uint8_t len;

Node = 0x01;
txData = {
    0x00,
};
cobID = 0x000; // Changes according to the message 
txData[0] = 0x01; // Changes according to the message 
txData[1] = Node; // Changes according to the message 
len = 2;  // Changes according to the message.

TxHeader.StdId = cobID;
TxHeader.RTR = 0;
TxHeader.IDE = CAN_ID_STD;
TxHeader.DLC = len;
data[0] = 0x00;
data[1] = 0x01;
data[2] = 0x02;
while(HAL_CAN_GetTxMailboxesFreeLevel(&hcan1) == 0);
  HAL_CAN_AddTxMessage(&hcan1, &TxHeader, data, &TxMailbox);
while(HAL_CAN_IsTxMessagePending(&hcan1, TxMailbox) == 1);
```

### 2.5 Receive CANOpen message

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


### 2.6 NMT
Code at the below shows NMT communication related to 1. Start_remote_node, 2. Enter_pre_operation, 3. Stop_remote_node, 4. Reset_node, and 5. Reset_communication. 

```c
  uint8_t codID;
  uint8_t txData[8];
  uint8_t Node;
  
  Node = 0x01;
  txData = {
      0x00,
  };
  // Start_Remote_node:
    cobID = 0x000;
    txData[0] = 0x01;
    txData[1] = Node;
    TxHeader.StdId = cobID;
    TxHeader.RTR = 0;
    TxHeader.IDE = CAN_ID_STD;
    TxHeader.DLC = 2;
    while(HAL_CAN_GetTxMailboxesFreeLevel(&hcan1) == 0);
      HAL_CAN_AddTxMessage(&hcan1, &TxHeader, &txData, &TxMailbox);
    while(HAL_CAN_IsTxMessagePending(&hcan1, TxMailbox) == 1);
    
  // Enter_Pre_operation:
    cobID = 0x000;
    txData[0] = 0x80;
    txData[1] = Node;
    TxHeader.StdId = cobID;
    TxHeader.RTR = 0;
    TxHeader.IDE = CAN_ID_STD;
    TxHeader.DLC = 2;
    while(HAL_CAN_GetTxMailboxesFreeLevel(&hcan1) == 0);
      HAL_CAN_AddTxMessage(&hcan1, &TxHeader, &txData, &TxMailbox);
    while(HAL_CAN_IsTxMessagePending(&hcan1, TxMailbox) == 1);
    
  // Stop_Remote_node:
    cobID = 0x000;
    txData[0] = 0x02;
    txData[1] = Node;
    TxHeader.StdId = cobID;
    TxHeader.RTR = 0;
    TxHeader.IDE = CAN_ID_STD;
    TxHeader.DLC = 2;
    while(HAL_CAN_GetTxMailboxesFreeLevel(&hcan1) == 0);
      HAL_CAN_AddTxMessage(&hcan1, &TxHeader, &txData, &TxMailbox);
    while(HAL_CAN_IsTxMessagePending(&hcan1, TxMailbox) == 1);
    
  // Reset_node:
    cobID = 0x000;
    txData[0] = 0x81;
    txData[1] = Node;
    TxHeader.StdId = cobID;
    TxHeader.RTR = 0;
    TxHeader.IDE = CAN_ID_STD;
    TxHeader.DLC = 2;
    while(HAL_CAN_GetTxMailboxesFreeLevel(&hcan1) == 0);
      HAL_CAN_AddTxMessage(&hcan1, &TxHeader, &txData, &TxMailbox);
    while(HAL_CAN_IsTxMessagePending(&hcan1, TxMailbox) == 1);
    
  // Reset_Communication:
    cobID = 0x000;
    txData[0] = 0x82;
    txData[1] = Node;
    TxHeader.StdId = cobID;
    TxHeader.RTR = 0;
    TxHeader.IDE = CAN_ID_STD;
    TxHeader.DLC = 2;
    while(HAL_CAN_GetTxMailboxesFreeLevel(&hcan1) == 0);
      HAL_CAN_AddTxMessage(&hcan1, &TxHeader, &txData, &TxMailbox);
    while(HAL_CAN_IsTxMessagePending(&hcan1, TxMailbox) == 1);
    
```
### 2.7 SDO

### 2.8 PDO


For example, if we mapped "current position" to PDO-1, the 

```c

```

Also, if we mapped "target velocity" to PDO-1, we can change the motor velocity by sending PDO message as 

```c

```

### 2.9 Overall code - example
With the concept of NMT, SDO and PDO, this page also introduce a simple code that control the motor position. 

```d

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
[CAN_Wiring]: https://www.csselectronics.com/pages/can-bus-simple-intro-tutorial