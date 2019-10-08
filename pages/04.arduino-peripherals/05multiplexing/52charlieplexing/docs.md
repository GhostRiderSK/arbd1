---
title: 'Charlieplexing'
taxanomy:
    tags:
        - docs
visible: true
---
Charlieplexing is a LED multiplexing technique used to drive a large number of LEDs using only few pins. With this technique n(n − 1) LEDs can be controlled just by using n pins of a microcontroller. It uses 3-State Logic: HIGH(1), LOW(0) and High-Z or High Impedance (Z). To switch on any LED its corresponding pins are driven High and Low accordingly and all others pins are in High-Z state. All the LEDs cannot be switched on simultaneously.  
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
Interface Charlieplexed Leds with Arduino.
```arduino

```

#### Exercise :
+ Roulette with Charlieplexed leds, keypad matrix, LCD and push button.