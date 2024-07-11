# SI-2024-CubeSat-AS
📡Repository for Summer Internship 2024 (CubeSat and Satelite Communication)
##### INTRODUCTION:-

![OIP](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/assets/173779301/4b125a76-c2fc-47c7-8569-c394e6201a28)

A CubeSat is a class of small satellite with a form factor of 10 cm (3.9 in) cubes.CubeSats have a mass of no more than 2 kg (4.4 lb) per unit,and often use commercial off-the-shelf (COTS) components for their electronics and structure.CubeSats are deployed into orbit from the International Space Station, or launched as secondary payloads on a launch vehicle.
The number of joined units classifies the size of CubeSats and according to the CubeSat Design Specification are scalable along only one axis to fit the forms of 0.5U, 1U, 1.5U, 2U, or 3U. 

# Lab Exercises

## Lab-1 Introduction to ESP32

-[Datasheet ESP32](https://github.com/silicon-sat/SI-2024-CubeSat/blob/main/docs/Datasheet-ESP32.pdf)

## Lab-2 Blinking LED
[Source](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/tree/main/Lab) 
```C
#define LED1 2
#define LED2 17
void setup() {
  pinMode(LED1,OUTPUT);
  pinMode(LED2,OUTPUT);
}

void loop() {
  digitalWrite(LED1,HIGH);
  delay(1000);
  digitalWrite(LED1,LOW);
  delay(1000);
  digitalWrite(LED2,HIGH);
  delay(1000);
  digitalWrite(LED2,LOW);
  delay(1000);
}
```

## Lab-3 Dimming LED
Parameters from the LED Datasheet

| Parameters | Value |
|--------|------|
|Max Forward Current| 30mA|
|Forward Voltage| 1.85V |
|Dominant Wavelength| 640 nm |
|Colour| Red |
|Typical Capacitance| 45 pF|
|Operating Range| -40 to 85 C|
