# Build a Near Real-time multi-device processing System

After a whole cycle of designing & implementing & testing a near real-time multi-device processing system for almost 3 years, here I summarize some interesting design related  stuff.

## System Introduction
The system will be deployed in a field. It processes data from multiple devices in near real-time, and notifies the user if detecting abnormal situation. 
The user need to control/monitor/view it remotely.
The user can run the system with Simulated/Recorded data for testing/validating purpose before deploying to the field.

[Architecture Design Diagram]: https://github.com/yan2liu/ArchitectureDesignNotes/blob/master/SystemDiagram.jpg "Architecture Design Diagram"

## To build this system, we face a few challenging questions:
* How to synchronize all the device with the server?
A [GPS based NTP Network Time Server](https://timemachinescorp.com/product/gps-time-server-tm1000a/) is installed in the network. All the devices & server are configured as NTP client to it.

* How to integrate a high-volume raw data device?
Add a small computing device like Intel NUC to connect directly to the device with USB 2.0 to preprocess data before dropping the data to the server through ethernet

## Design Ideas


Comparing with a lot of systems, which deploy in shop/office/AWS,  these are the non-normal consideration, but same criical for the system's sucess:* Highway vibration
* Weather condition: clear, fog, rain, snow, thunderstorm, humidity, temperature
* Device generated heat & power assumption.
* Cost for installation
