---
title: LEDs
media_order: hatchnhack_led_schematic.png
taxonomy:
    category:
        - docs
visible: true
---

ARBD 1 consists of one Red, one Green and one Blue LED. They are covered with a diffuser to appear as one RGB LED source. All LEDs are connected with PWM pins(will discuss about PWM pins later),  so that their intensity can be controlled. Red LED is connected with D11, Blue colour LED is connected with D10 and Green LED is connected with D9. See Figure for connections.

![hatchnhack_rgb_led_schematic](hatchnhack_led_schematic.png?classes=caption "ARBD1 RGB LEDs")

#### Example 1 : Blinky
Turn on Red LED for 1 second and then turn it off for 1 second, repeatedly.  
```c
int Led_pin = 11 ;  

// the setup function runs once when you press reset or power the board
void setup() 
{
    pinMode(Led_pin, OUTPUT);   //initialize digital pin 11 as an output
}

// the loop function runs over and over again forever
void loop()
{
    digitalWrite(Led_pin, HIGH);// turn the LED on (HIGH is the voltage level)
    delay(1000);                // wait for a second
    digitalWrite(Led_pin,LOW);  // turn the LED off by making the voltage LOW
    delay(1000);                // wait for a second
}
```
1. To use the digital pin as an output we use the built-in function ```pinMode()```. As this is one-time work, we call ```pinMode()``` function in ```setup()``` function. Generally, we call ```pinMode()``` function in ```setup()``` until we want to change the mode of a pin in between the program.
2. To write the value on output pin(digital pin:11) we use ```digitalWrite()``` function.
3. ```delay()``` is used to wait for a mentioned value in milliseconds.
4. Both ```digitalWrite()``` and ```delay()``` are written in ```loop()``` function as we want to repeat the process again and again.

#### Exercise 1 :
+ Blink Blue and Green LEDs.
+ Make different color patterns using all three LEDs. 