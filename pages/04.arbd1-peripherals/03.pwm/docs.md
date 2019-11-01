---
title: PWM
taxonomy:
    category:
        - docs
visible: true
taxanomy:
    category: docs
---

PWM is a technique for getting analog results with digital means. PWM works as a switch which can vary the on or off time of a rectangular wave. When the PWM signal is passed through a low pass filter the signal is averaged out in such a way that the average signal value is equal to the duty cycle i.e on time of PWM signal. Thus working as an analog signal which can vary from ‘0’ to ‘VCC’.  
PWM has many applications such as controlling servos and speed controllers, limiting the effective power of motors and LEDs.  
Arduino has eight bit default PWM which means that Arduino PWM duty cycle can vary from *0* to *2<sup>8</sup>* i.e *255* value and thus resultant analog voltage can vary from *0* to *VCC* in 256 steps.
### Exercise :
Led fading with PWM
```c
int led_pin = 11; 
int led_value = 0;  //To store the current intensity of led. 
void setup() 
{
  pinMode(led_pin,OUTPUT);  //Initialize the Digital Pin 11 as output
}

void loop() 
{
    for(led_value = 0; led_value <= 255 ; led_value = led_value+10)     //Increasing the pwm value by 10 after every 100 ms 
    {
      analogWrite(led_pin,led_value);   //Output the PWM value on LED
      delay(100);
    }
    delay(1000);                             		
    // Wait for 1s at its Highest intensity
    for(led_value = 250 ; led_value >= 0 ; led_value = led_value-10)
    //Decreasing the PWM value by 10 after every 100 ms 
    {
        analogWrite(led_pin,led_value); 
        delay(100); 
    }
    delay(1000);                              		
    // Wait for 1s at its lowest intensity 
}
```
### Example :
Control the intensity of led using potentiometer.
```c
int led_pin = 9; 
int pot_pin = A6; 
int pot_value;                         //To store the potentiometer value at Analog pin A6 
int led_value;                         //To store the led intensity value 
void setup()
{
  pinMode(led_pin,OUTPUT);              //Initialize the Digital pin 9 as Output
  pinMode(pot_pin,INPUT);               //Initialize the Analog pin A6 as Input
}

void loop() 
{
  pot_value = analogRead(pot_pin);                		
  //Read the value on Analog pin A6, i.e Potentiometer value 
  led_value = map(pot_value, 0, 1023, 0, 255);   
  //Used to map 10 bit ADC value to 8 bit PWM value 
  analogWrite(led_pin,led_value);  
  delay(100); 
}
```