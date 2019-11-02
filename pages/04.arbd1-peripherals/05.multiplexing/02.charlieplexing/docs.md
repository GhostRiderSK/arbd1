---
title: Charlieplexing
media_order: hatchnhack_charlieplexing_leds.png
taxonomy:
    category:
        - docs
visible: true
taxanomy:
    category: docs
---

Charlieplexing is a LED multiplexing technique used to drive a large number of LEDs using only few pins. With this technique n(n − 1) LEDs can be controlled just by using n pins of a microcontroller. It uses 3-State Logic: HIGH(1), LOW(0) and High-Z or High Impedance (Z). To switch on any LED its corresponding pins are driven High and Low accordingly and all others pins are in High-Z state. All the LEDs cannot be switched on simultaneously.

![hatchnhack_charlieplexing_leds](hatchnhack_charlieplexing_leds.png?classes=caption "ARBD1 Charlieplexed LEDs")

Following pin configurations are given to switch on any charlieplexed led  

| LED No | A2 | A3 | A4 | A5 |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 1 | Z | Z | 0 | 1 |
| 2 | Z | 0 | Z | 1 |
| 3 | 0 | Z | Z | 1 |
| 4 | Z | 0 | 1 | Z |
| 5 | 0 | Z | 1 | Z |
| 6 | Z | Z | 1 | 0 |
| 7 | 0 | 1 | Z | Z |
| 8 | Z | 1 | Z | 0 |
| 9 | Z | 1 | 0 | Z |
| 10 | 1 | Z | Z | 0 |
| 11 | 1 | Z | 0 | Z |
| 12 | 1 | 0 | Z | Z |
### Example :
Controlling the flashing rate of charliplexed leds using potentiometer on ARBD 1
```c
const int CP[4] = {A2,A3,A4,A5};	//Charlieplexed LEDs Pinmap
const int POT = A6;						   //Potentiometer Pin
char pattern[12][4] = {			// LEDs Pattern
  "ZZ01", //1
  "Z0Z1", //2
  "0ZZ1", //3
  "Z01Z", //4
  "0Z1Z", //5
  "ZZ10", //6
  "01ZZ", //7
  "Z1Z0", //8
  "Z10Z", //9
  "1ZZ0", //10
  "1Z0Z", //11
  "10ZZ"  //12
};                    

// Delays 
int MAX_DELAY = 1000;
int MIN_DELAY = 0;
int DELAY = MAX_DELAY;

void setup() {  
  pinMode(POT,INPUT);
}

void loop() {  
  for(int i=0 ; i<12 ; i++) {    
    DELAY = map(analogRead(POT), 0, 1023, 0, 1000);
    for(int j=0 ; j<4 ; j++){
      if(pattern[i][j] == 'Z'){
        pinMode(CP[j],INPUT);
      } else {
        pinMode(CP[j],OUTPUT);        
        digitalWrite(CP[j],int(pattern[i][j])-48);
      }          
    }
    delay(DELAY);   
  }    
}
```

#### Exercise :
+ Roulette with Charlieplexed leds, keypad matrix, LCD and push button.