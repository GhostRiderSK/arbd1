---
title: 'Bluetooth (HC-05)'
taxonomy:
    category:
        - docs
visible: true
taxanomy:
    category: docs
---

HC-05 is a Bluetooth device used for wireless communication with Bluetooth enabled devices (like smartphones). It communicates with microcontrollers using serial communication (USART).  
**Pin Connections**  

| Bluetooth Pin | Arduino Pin |
| :-: | :-: |
| Rx | D13 |
| Tx | D12 |
### Example :
Interface bluetooth with Arduino and send “Hello world” to the serial monitor with the help of phone app.
```c
#include <SoftwareSerial.h>   // Software Serial Library

//  Connection to HC05
const int Rx = 12; 
const int Tx = 13;

SoftwareSerial hc05(Rx, Tx);

void setup(){
  Serial.begin(115200);
  while(!Serial);
  Serial.println("Serial Started");
  hc05.begin(9600);   // Default data rate for HC05
  hc05.println("Hello, world?");
}

void loop(){
 if(hc05.available()){
  Serial.write(hc05.read()); 
 }
 if(Serial.available()){
  hc05.write(Serial.read());
 }
}
```
### Exercise :
+ Control Leds with a mobile app using bluetooth.