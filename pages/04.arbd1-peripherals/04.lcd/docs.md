---
title: LCD
taxonomy:
    category:
        - docs
visible: true
taxanomy:
    category: docs
---

ArBrd1 has an on-board Liquid Crystal Display (LCD) that can be used to display alphanumeric characters. The LCD can operate in 4-bit and 8-bit mode. In 4-bit mode, the data is transferred as a nibble with most-significant nibble first then the least-significant. In this mode, only 4 of the data pins are used. In 8-bit mode, the data is transferred as a whole byte. In 8-bit, the data transfer time is reduced to half of that in 4-bit mode but as a trade-off, 4 extra pins are used.  
In ArBrd1 LCD pins are connected with the following Arduino pins. You can only operate LCD in 4-bit mode in ArBrd1. Pin Mapping of LCD with Arduino:  

| LCD Pin | Arduino Pin |
| ------- | ----------- |
| D4 | D0 |
| D5 | D1 |
| D6 | D2 |
| D7 | D3 |
| RS | D4 |
| EN | D5 |
### Example :
Interface LCD with Arduino  

```c
/*
  LiquidCrystal Library - Hello World
  This sketch prints "HatchnHack!" to the LCD
  and shows the time.
*/

// include the library code:
#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to

const int rs = 4, en = 5, d4 = 0, d5 = 1, d6 = 2, d7 = 3;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

void setup()
{
    lcd.begin(16, 2);  	            
    // set up the LCD's number of columns and rows:
    lcd.print("HATCHnHACK");  	    
    // Print a message to the LCD
}

void loop() 
{
    // set the cursor to column 0, line 1
    // (note: line 1 is the second row, since counting begins with 0):
    lcd.setCursor(0, 1);
    // print the number of seconds since reset:
    lcd.print(millis() / 1000);
}
```
#### Exercise
+ Display temperature and light intensity reading on LCD.