---
title: '4x4 Keypad Matrix'
media_order: hatchnhack_keypad_matrix.png
taxonomy:
    category:
        - docs
visible: true
taxanomy:
    category: docs
---

Keypad matrix is a superb example of multiplexing. In keypad we interface 16 keys with 8 pins.  
In Keypad, total number of rows required is &radic;(16) = 4.  
Total number of columns required is (16)/(rows) = 4.  
Thus the total number of pins required are (R+C) = 8.  
Thus with this method of multiplexing we can interface N<sup>2</sup> leds or push button by 2N pins.
![hatchnhack_keypad_matrix](hatchnhack_keypad_matrix.png?classes=caption "ARBD1 Keypad Matrix")
### Example :
Interface Keypad interface with Arduino.
1. We have four rows and four columns
2. We define rows as ‘OUTPUT’ and columns as ‘INPUT’. 3. Give the ‘HIGH’ voltage on output pins. 
4. Now, we detect if any button is pressed. 
5. If any button is pressed, make all the row output ‘LOW’. 
6. Now, we give the HIGH voltage to each row one by one and check the input voltage at each column pin. 
7. Thus we detect the push button which is pressed according to the row which is driven High and the column at which the input voltage is High.  

```c
int R[4] = {10,11,12,13};       			// Rows of the Keypad Matrix
int C[4] = {6,7,8,9};           			// Columns of the keypad Matrix 
int row  = 0;                  			//To store which rows button is pressed
int column = 0;                			//To store which column button is pressed
int i; 
bool is_switch_pressed;                //To detect whether the switch is pressed or not 
char key_press[16] = {'1','2','3','A','4','5','6','B','7','8','9','C','*','0','#','D'}; 
void setup()
{
  Serial.begin(9600);
  for(i=0; i<4;i++) 
  
    pinMode(R[i],OUTPUT);              // Initialize all rows pin as Output
    pinMode(C[i],INPUT);               //Initialize all column pin as Input
}
void loop() {
  for(i =0 ; i< 4; i++) 
  {
    digitalWrite(R[i],HIGH);           //Put all row pin as HIGH to detect 
//which button is pressed 
    is_switch_pressed = digitalRead(C[0]) || digitalRead(C[1]) || digitalRead(C[2]) || digitalRead(C[3]); 
    //If any button is pressed 
    if(is_switch_pressed) 
    { 
        for(i = 0 ; i<4 ; i++) 
        {
            for(int j = 0 ; j<4; j++) 
            {
                digitalWrite(R[j],LOW); 
                digitalWrite(R[i],HIGH);          
                for(int j = 0 ; j<4; j++ ) 
                if(digitalRead(C[j])) 
                {
                    row = j;                    
                    column  = i; 
                    exit; 
                }
            }
        }
        Serial.print("The key pressed is : "); 
        Serial.println(key_press[row+(column*4)]);
    }
    for(int i =0 ; i<4 ; i++) 
    {
        digitalWrite(R[i],HIGH);
        while(is_switch_pressed) 
        {
            is_switch_pressed = digitalRead(C[0]) || digitalRead(C[1]) || digitalRead(C[2]) || digitalRead(C[3]); 
        }
    }
}
```  

#### Exercise :
+ Interface keypad matrix and lcd with Arduino such that whenever you press any key, the number or symbol display on the lCD.
+ Make a calculator with the help of keypad matrix, lcd and Navi switches. 
