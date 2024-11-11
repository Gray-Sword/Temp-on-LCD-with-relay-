# Temperature Monitoring System with Fan Control

## Description
This project monitors the temperature using an analog temperature sensor (like the LM35) connected to an Arduino. The temperature is displayed on an LCD screen, and the system includes basic fan control based on the temperature. If the temperature exceeds a set threshold, the fan will be turned on.

## Features
- **Temperature Reading**: Reads the temperature from an analog sensor.
- **LCD Display**: Displays the current temperature in Celsius on a 16x2 LCD.
- **Fan Control**: Turns the fan on if the temperature is high.

## Components
- **Arduino Board (e.g., Uno, Nano)**
- **Analog Temperature Sensor (e.g., LM35)**
- **16x2 LCD**
- **Relay or Fan (connected to pin 7)**

## Wiring
- **Temperature Sensor (LM35)**: Connected to analog pin A1.
- **LCD Display**: 
  - RS -> Pin 12
  - EN -> Pin 11
  - D4 -> Pin 5
  - D5 -> Pin 4
  - D6 -> Pin 3
  - D7 -> Pin 2
- **Fan**: Controlled by digital pin 7 (requires relay if controlling high voltage fan).

## Arduino Code

```cpp
#include<LiquidCrystal.h>

const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2; 
LiquidCrystal lcd(rs, en, d4, d5, d6, d7); 

float celsius;
int temp = A1;
int fan = 7;

void setup(){
  pinMode(temp, INPUT);
  pinMode(fan, OUTPUT);
}

void loop(){
  digitalWrite(7, HIGH);
  
  celsius = analogRead(temp) * 0.004882814;
  celsius = (celsius - 0.5) * 100.0;
  
  lcd.setCursor(0, 1);
  lcd.print("Temp: ");
  lcd.print(celsius);
  lcd.print(" C");
  delay(1000);
  lcd.clear();
}
