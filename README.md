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

equivalent resistance calculation- for the circuit as shown GPIO->R->LED diode->0

=>4.34-30x10pow(-3)(R)-0.7=0 =>R=3.64/30x10pow(-3)= 121.33 ohms

so the equivalent resistance which we had choosen for our convienience was= 100 ohms

## Lab-4 SIGNAL PROCESSING USING PYTHON:-
#### FFT
Fourier analysis transforms signals from the time domain to the frequency domain. A mathematical method for transforming a finite time function of equally spaced time samples into a function of frequency of equally spaced complex frequency samples.
We have used python to implement FFT using WSL to change signals from time to frequency domain and observe the waveform.
Code -[FFT](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/FFT)
![WhatsApp Image 2024-07-11 at 21 09 13](https://github.com/user-attachments/assets/3c2dad6a-7f93-4b60-ab6e-8ecc8d3669d9)

#### FSK
Frequency-shift keying (FSK) is a digital modulation technique that transmits information wirelessly by shifting the frequency of a carrier signal to represent binary 1s and 0s.
Code-[FSK](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/FSK)
![WhatsApp Image 2024-07-11 at 21 09 14](https://github.com/user-attachments/assets/dabcf1fd-2ac1-4b33-8b07-b0a43f650c3e)

#### Generation of Cos Wave
We used python to generate a cos wave of desired frequency
Code-[Generation of cos wave](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/Generation%20of%20cos%20wave)

## Introduction to antenna modeling and simulation software 4NEC2:-

Using 4NEC2, we did modelling of Antenna and observed the frequency sweep , radiation pattern,SWR etc.
Code-[loaded v dipole](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/Antenna%20modelling%20in%204NEC2)





![Screenshot 2024-07-12 154512](https://github.com/user-attachments/assets/e5ddc66e-4bdc-4b05-8a5e-4035d30e49d6)




![Screenshot 2024-07-12 154642](https://github.com/user-attachments/assets/bda36b98-77a5-4ef7-a34f-3f6633e60e41)





![Screenshot 2024-07-12 154752](https://github.com/user-attachments/assets/312d587c-75d6-4a36-8e3e-080a346d0ede)
