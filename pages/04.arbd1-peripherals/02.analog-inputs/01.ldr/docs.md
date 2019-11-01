---
title: LDR
media_order: hatchnhack_ldr_schematic.png
taxonomy:
    category:
        - docs
visible: true
taxanomy:
    category: docs
---

An LDR is a component that has a (variable) resistance that changes with the light intensity that falls upon it. This allows them to be used in light sensing circuits.
Variation in resistance with changing light intensity. LDR is connected with pin “A0” of Arduino pin.  
![hatchnhack_ldr_schematic](hatchnhack_ldr_schematic.png?classes=caption "ARBD1 LDR")
As per shown in Figure LDR is connected in such a way that it forms a voltage divider with a 1k resistor(why?). With a change in LDR resistance value, the voltage at A0 will change and thus indicates the variation in the intensity of light w.r.t. to voltage.  
### Example : 
Interface LDR with Arduino. Bring the torch or any light near to the sensor. Check the change in serial monitor. Now cover the LDR with hand and observe the change in readings.
```c
//LDR with Arduino

int LDR_pin = A0; 
int LDR_value;      //To store the current LDR value 
void setup()
{
  pinMode(LDR_pin,INPUT);   //Initialize the analog pin A0 as an Input
  Serial.begin(9600);       //Initialize Serial to check the LDR value
}

void loop() {
  LDR_value = analogRead(LDR_pin);  //Sample the LDR value at Analog pin A0 
  Serial.println(LDR_value);        //Write the LDR value to the Serial Monitor
  delay(1000);                      //Delay for 1 second before sampling again  
}
```
1. To check the LDR value we use serial monitor.
2. `Serial.begin()` function is used to initialize the serial monitor with a baud rate of 9600 bps. You can set other baud rates as well. To know more about baud rates check: [Serial Communication](https://learn.sparkfun.com/tutorials/serial-communication/all#serial-intro)
3. LDR value is given to Serial monitor through `Serial.println()` function.
4. Upload the code on the board, then open the serial monitor from the tools or click the symbol on the right side of IDE. 
5. Serial monitor will look like this.
6. Check the value of LDR, now cover the LDR or bring more light near to the LDR and observe the monitor value.