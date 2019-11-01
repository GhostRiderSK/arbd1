---
title: 'Push Buttons'
media_order: hatchnhack_push_button.png
taxonomy:
    category:
        - docs
visible: true
taxanomy:
    category: docs
---

There are five 10xx Omron switches on ArBrd1. Switches can have two states **_open_** or **_closed_**. The **_UP_** button works as a digital input switch which gives **_LOW_** i.e 0 volts when pressed and **_HIGH_** i.e. *5* volts when not pressed. This **_UP_** button is connected to _A1_  pin of Arduino.
![hatchnhack_push_button](hatchnhack_push_button.png?classes=caption "ARBD1 PUSH BUTTON")
Whenever you press a button, it does not settle down to other configuration. It is actually a spring which moves up and down before settling and thus results in lots of high, low combinations before reaching the final value. This is called bouncing.  
Removing this bouncing or taking care of this bouncing while sampling the input is called de-bouncing.  
### Example 2 :
Make a program such that Red led goes on whenever the user presses the “UP” button and it goes off whenever a user releases the button.
```c
int buttonPin = A1; //Push Button 
int ledPin = 11;    //LED 

int buttonstate;                //Present state of push button 
int prev_buttonstate = HIGH;    //Previous state of push button

void setup() 
{
  pinMode(buttonPin,INPUT);                 //Initialize the digital pin 2 as an Input
  pinMode(ledPin,OUTPUT);                   //Initialize the digital pin 13 as an Output 
  digitalWrite(ledPin,prev_buttonstate);    //Initially put the Led in ON state
}
void loop() 
{
  buttonstate = digitalRead(buttonPin); //Samples the input at digital pin 2
  if(buttonstate != prev_buttonstate)   //Value Changed due to noise or pressing of push button
  { 
    delay(20);                              //Wait for 20 ms to avoid any noise or bouncing 
    buttonstate = digitalRead(buttonPin);   //Store the current state of push button  
    prev_buttonstate = buttonstate;         //Store the current state in prev_buttonstate for the next comparison
  }
  digitalWrite(ledPin,buttonstate) ;        //Drive the Led with the current state of push button 
```
>Generally a push button bounces from 5ms to 10ms. So in order to take care of bouncing glitches we wait for 20ms and samples the value again. That gives us accurate value of a push button.
#### Exercise :
+ Make a program such that Blue led toggles whenever user presses the button and remains in the same state whenever a user releases the button. 