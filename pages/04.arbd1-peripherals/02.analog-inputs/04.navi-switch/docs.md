---
title: 'Navigation Switches'
taxanomy:
    category:
        - docs
visible: true
---
There are five 10xx Omron switches on Board 1. These five push buttons are connected with an analog input pin in such a way that whenever you press a different button, you get a different voltage and thus detect which button is pressed. This configuration is used when you want to interface multiple push button with a single pin. Navi switches are connected to A1(Analog pin 1) of Arduino.  
1. Voltage at A1 when no button is pressed = VCC i.e. 5V
2. Voltage at A1 when “DOWN” button is pressed = 0.8Vcc
3. Voltage at A1 when “RIGHT” button is pressed = 0.75Vcc
3. Voltage at A1 when “CENTRE” button is pressed = 0.66Vcc
3. Voltage at A1 when “LEFT” button is pressed = 0.5Vcc
3. Voltage at A1 when “UP” button is pressed = 0Vcc

Navi Switch value at Arduino input pin  

| Push Button | Voltage(Vcc) | ADC Value |
| ----------- | ------------ | --------- |
| No Button is Pressed | 1 | 1023 |
| DOWN | 0.8 | 819 |
| RIGHT | 0.75 | 768 |
| CENTRE | 0.66 | 676 |
| LEFT | 0.5 | 512 |
| UP | 0 | 0 |
### Example :
Interface Navi switches with Arduino and detect which button is pressed.  

```c
int Switch_pin = A1;       
int switch_value;           		    //To store the current push button value 
int prev_switch_value;      		    //To store the prev value of push buttons
int button;                 		    //To store which button is pressed
void setup() 
{
    Serial.begin(9600);       	    //Initialize Serial to show which button is pressed
    pinMode(Switch_pin,INPUT);     //Initialize the analog pin A1 as an Input 
    prev_switch_value = analogRead(Switch_pin);      
    //Store the initial value of Analog pin A1
}

void loop() 
{
    switch_value = analogRead(Switch_pin); 
    //Read the value at Analog pin A1
    if((switch_value > (prev_switch_value+20)) ||
    (switch_value <(prev_switch_value-20)))     
    //If any button is pressed or value change due to noise 
    delay(20) ;             			
    //Wait for 20 ms to avoid any bouncing in the button 
    switch_value = analogRead(Switch_pin) ; 
    //Read again the value at pin A1
    if((switch_value > (prev_switch_value+20)) || (switch_value <(prev_switch_value-20)))
    {
    //If the button is actually pressed
        if(switch_value < 100) 	
        //The ADC value for UP button should be approx. 0
            Serial.println("----UP BUTTON IS PRESSED----") ; 
        else if((switch_value > 400) && (switch_value < 600))
        //The ADC value for LEFT button should be approx.512
            Serial.println("----LEFT BUTTON IS PRESSED----")
        else if((switch_value > 600) && (switch_value < 725))
        //The ADC value for CENTRE button should be approx. 676
            Serial.println("----CENTRE BUTTON IS PRESSED") ; 
        else if((switch_value > 725) && (switch_value < 790))
        //The ADC value for RIGHT button should be approx. 768
            Serial.println("----RIGHT BUTTON IS PRESSED") ; 
        else if((switch_value > 790) && (switch_value < 850))
        //The ADC value for DOWN button should be approx. 819
            Serial.println("----DOWN BUTTON IS PRESSED----"); 
        else if(switch_value > 900) 
            Serial.println("----BUTTON IS RELEASED----");    
        prev_switch_value = switch_value ;    
  }   
}
/*
1. Read the analog value at analog pin A1 where push button is connected. 
2. If the value is changed from the old value then either the push button is pressed or value changes due to some noise.
3. Wait for 20ms to avoid any noise or switch bouncing.
4. Read again the value at pin A1.
5. If the value is actually changed that it must be because of pressing one of five push buttons.
6. Detect which button is pressed and display it on the serial monitor. 
*/
```