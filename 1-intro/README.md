# 1. Overview

The embedded programmable logic controller (PLC) of the Hi6 controller refers to the functions of the PLC that are installed into the controller in a software-like manner. The user can write and operate ladder programs that are commonly used in PLCs.


Ladder programs can be written or edited using the HRLadder, a ladder editing PC software dedicated to the robots of Hyundai Robotics, and downloaded to the Hi6 controller connected via Ethernet. Conversely, the ladder program running on the Hi6 controller can be uploaded to the HRLadder on the PC, and the status, such as the mode of the PLC running on the controller or the values of relays, can be remotely monitored from the HRLadder. 

* You can download the HRLadder from the Hyundai Robotics website (https://www.hyundai-robotics.com) - Customer Support - Application Software screen.
* For the information on how to use the HRLadder, refer to the function manual linked to the Help menu of the HRLadder.
* HRLadder can be used for old controller models ranging from Hi4 to Hi5a. Please note that as the ladder program of the Hi6 controller is different from that of the old model controllers, there is no compatibility between them.


The Hi6 controller’s I/O can be connected to the upper-process PLCs with fieldbus masters or to the devices of lower-level fieldbus slaves, both through a fieldbus or remote I/O device. The functions of the embedded PLC are designed to control the signals of the thus connected I/O using ladder logic.


The functions of the Hi6 controller’s embedded PLC are similar to those of the Hi5a controller’s embedded PLC, and the same HRLadder, in other words, the same ladder editor, is used. Therefore, users who are already familiar with the functions of the Hi5a controller’s embedded PLC can quickly learn from this manual by checking only the different parts of the Hi6 controller.


{% hint style="info" %}
Therefore, users already familiar with the functions of the Hi5a controller’s embedded PLC can quickly learn from this manual by checking only the different parts of the Hi6 controller. You are kindly required to check the link shown below.
[5. Difference in the embedded PLC between Hi5a and Hi6 controllers](../5-diff-hi5a-hi6.md)

{% endhint %}

