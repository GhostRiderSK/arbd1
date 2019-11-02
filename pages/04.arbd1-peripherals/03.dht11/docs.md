---
title: DHT11
media_order: 'Hatchnhack_Arduino_Ide_Libraries_Adafruit.PNG,Hatchnhack_Arduino_Ide_Libraries_DHT11.PNG,Hatchnhack_Arduino_Ide_Libraries.PNG'
taxonomy:
    category:
        - docs
visible: true
taxanomy:
    category: docs
---

To use DHT11 we will use Adafruit's DHT and Unified sensor libraries.  
To add these libraries goto Sketch > Include Libraries > Manage Libraries
![Hatchnhack_Arduino_Ide_Libraries](Hatchnhack_Arduino_Ide_Libraries.PNG?classes=caption "Arduino IDE Manage Libraries")
Search and install DHT sensor library and Adafruit Unified Sensor library.
![Hatchnhack_Arduino_Ide_Libraries_DHT11](Hatchnhack_Arduino_Ide_Libraries_DHT11.PNG?classes=caption "Arduino IDE Install DHT11 Library")
![Hatchnhack_Arduino_Ide_Libraries_Adafruit](Hatchnhack_Arduino_Ide_Libraries_Adafruit.PNG?classes=caption "Arduino IDE Install Adafruit Unified Sensor Library")
Further if you want to manually install the libraries, they can be downloaded using the following links  

DHT Sensor Library: [Adafruit DHT Sensor](https://github.com/adafruit/DHT-sensor-library)
Adafruit Unified Sensor Lib: [Adafruit Unified Sensor](https://github.com/adafruit/Adafruit_Sensor)  

#### Example :
Measuring temperature and humidity using DHT11 on ARBD 1
```c
#include "DHT.h"		//Include the DHT sensor library

#define DHT_TYPE DHT11	//Define DHT sensor type
#define DHT_PIN A0		//Define Pin connected to DHT sensor
DHT dht(DHT_PIN, DHT_TYPE);

void setup() {
	Serial.begin(115200);
    Serial.print(DHT_TYPE);
    Serial.println(" Sensor Test");
    dht.begin();
}
void loop(){
	float h = dht.readHumidity();
    float t = dht.readTemperature();
    if(isnan(h) || isnan(t)){
    	Serial.println("Error!! Reading from DHT sensor");
        return;
    }
    Serial.println("===========================");
    Serial.print(" Humidity : ");
    Serial.print(h);
    Serial.println("%");
    Serial.print(" Temperature : ");
    Serial.print(t);
    Serial.print("\xC2\xB0");
    Serial.println("C");  
    Serial.println("===========================");
    delay(1000);
}
```