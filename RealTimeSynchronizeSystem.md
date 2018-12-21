# Build a Near Real-time Multi-device Processing System

After a whole cycle of designing & implementing & testing a near real-time multi-device processing system for almost 3 years, here I summarize some interesting design related stuff.

## System Introduction
The system will be deployed in a field. It processes data from multiple devices in near real-time, and notifies the user if detecting abnormal situation. 
The user need to control/monitor/view it remotely.
The user can run the system with Simulated/Recorded data for testing/validating purpose before deploying to the field.

![Architecture Design Diagram](./SystemDiagram.jpg?raw=true)

## To build this system, a few challenging questions were faced:
* How to synchronize all the device with the server?
A [GPS based NTP Network Time Server](https://timemachinescorp.com/product/gps-time-server-tm1000a/) is installed in the network. All the devices & server are configured as NTP client to it.

* How to integrate a high-volume raw data device?
Add a small computing device like Intel NUC to connect directly to the device with USB 2.0 to preprocess data before dropping the data to the server through ethernet.

## Design Ideas & Implementation
* Loosely-coupled modules by asynchronized message system to achieve testability.

All devices capture data, and wrap data in standard message, and drop to the Queue.
[RabbitMQ](https://www.rabbitmq.com/) or [ActiveMQ](http://activemq.apache.org/) are both widely used message broker with nice Admin web management console. RabbitMQ have been use more often recently years than ActiveMQ.
Real-time messages can be recorded & replay during test.

* Standardized message format for all the devices to communicate to server for interoperability.

More than 10 years ago, XML was often used for standardized information communication among different system. I think it is still widely used by big institutes. XML schema is well defined for communication's data type  & format & meaning.  But, the message  size is too big.

Considering the data volume & multiple program languages (Java & C++) used among devices, [Google Protobuf](https://developers.google.com/protocol-buffers/) and [Apache Thrift](https://thrift.apache.org/) were evaluated. They both define message format, then generate message data model code in Java & C++. Protobuf performance is better than Thrift. Thrfit is better in support complicate data structure. We need map in the message, Protobuf did not support it at that time.

* By external running model related settings in configuration properties, allow the system to switch between simulation/real-time model. This achieves better usability & code reusability.

[Spring Boot framework](https://spring.io/guides/gs/spring-boot/) itself is a very good example for less code by configuration. As web application built with Spring Boot, all the system configuration should be pushed to [the application.properties](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html)

* Web interface communicate to server by RESTful Web service & Web Socket with JSON data.

Front-end builds with JavaScript framework like AngularJS (was 1.X version at that time). Both AngularJS and Polmer has tool to create seeding project. 

JSON is the most-widely used data format between web interface & web server since it is naturally/well-supported by JavaScript & WS Framework. JSON is very flexible. To allow user dynamically create JSON with certain format, I more enjoy the [JSON schema supported JavaScript library](https://github.com/json-editor/json-editor).  

For real-time data high frequency & low-latency communication from server to front end, web socket instead of RESTful Web service is used. Both user & server can stop the live data feeding. Javascript Web Socket API is well documented [here](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket).  [Spring Framework](https://docs.spring.io/spring/docs/5.0.0.BUILD-SNAPSHOT/spring-framework-reference/html/websocket.html) also supports web socket in the backend.

Live data needs to show as time series chart on the front-end with [dygraph JS library](https://github.com/danvk/dygraphs). It is simple & fit this purpose. A comparison of different chart JS libaries to be added in my Git Blog later.


### Comparing with a lot of systems, which deploy in shop/office/AWS,  these are the non-normal consideration, but same criical for the system's sucess:

* Highway vibration
* Weather condition: clear, fog, rain, snow, thunderstorm, humidity, temperature
* Device generated heat & power assumption.
* Cost for installation



