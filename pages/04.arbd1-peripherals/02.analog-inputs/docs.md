---
title: 'Analog Inputs'
taxonomy:
    category:
        - docs
visible: true
taxanomy:
    category:
        - docs
---

The signals from most of the sensors that measure surrounding temperature, pressure, humidity etc. are analog in nature. Their output voltage varies with change in surrounding parameters which tells us about the change in that particular parameter.  
On the other hand, the controllers are digital in nature. So, in order to fulfill this gap, ADC (Analog to Digital converter) works as a bridge between analog signals and digital signals.  
ADC divides the total range i.e (Max value - Min value) in sections. When the analog value lies in a section ADC converts the analog value to the assigned value of that section which can be manipulated by the controller for further calculations.  
!! If there is a 10-bit ADC and input range is (0-5)V. Then the total range is divided into 2<sup>10</sup> i.e 1024 numbers.  
To convert any ADC value ‘X’ into analog voltage ‘Y’.  
**Y = ( X * 5 )/1024 V**  