# SI-2024-CubeSat-AS
📡Repository for Summer Internship 2024 (CubeSat and Satelite Communication)

# Lab Exercises

## Lab-1 Introduction to ESP32

-[Datasheet ESP32](https://github.com/silicon-sat/SI-2024-CubeSat/blob/main/docs/Datasheet-ESP32.pdf)

## Lab-2 Blinking LED
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
