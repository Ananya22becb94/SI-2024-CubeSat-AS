# SI-2024-CubeSat-AS
📡Repository for Summer Internship 2024 (CubeSat and Satelite Communication)
# INTRODUCTION:-

![OIP](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/assets/173779301/4b125a76-c2fc-47c7-8569-c394e6201a28)

A CubeSat is a class of small satellite with a form factor of 10 cm (3.9 in) cubes.CubeSats have a mass of no more than 2 kg (4.4 lb) per unit,and often use commercial off-the-shelf (COTS) components for their electronics and structure.CubeSats are deployed into orbit from the International Space Station, or launched as secondary payloads on a launch vehicle.

The number of joined units classifies the size of CubeSats and according to the CubeSat Design Specification are scalable along only one axis to fit the forms of 0.5U, 1U, 1.5U, 2U, or 3U. 


![Screenshot 2024-07-13 001940](https://github.com/user-attachments/assets/15f2b07e-e147-450f-85f0-6a9699d2d722)
# CubeSat Dispenser System
The dispenser provides attachment to a launch vehicle (or rocket), protects the CubeSat during launch, and releases it into space at the appropriate time.
![Screenshot 2024-07-13 121742](https://github.com/user-attachments/assets/629c7a8d-e172-419e-8052-a19e3ffee26f)


# Development Process Overview
Typical Development Cycle:-
- Concept Development (1–6 months)
- Securing Funding (1–12 months)
- Merit and Feasibility Reviews (1–2 months)
- CubeSat Design (1–6 months)
- Development and Submittal of Proposal in Response to CSLI Call (3–4 months)
- Selection and Manifesting (1–36 months)
- Mission Coordination (9–18 months)
- Licensing (4–6 months)
- Flight-Specific Documentation Development and Submittal (10–12 months)
- Ground Station Design, Development, and Testing (2–12 months)
- CubeSat Hardware Fabrication and Testing (2–12 months)
- Mission Readiness Reviews (half-day)
- CubeSat to Dispenser Integration and Testing (1 day)
- Dispenser to Launch Vehicle Integration (1 day)
- Launch (1 day)
- Mission Operations (variable, up to 20 years)
  
# Modulation Schemes  
![Screenshot 2024-07-13 122015](https://github.com/user-attachments/assets/8a29754d-26df-4962-aa94-e8e1a7a75203)



![spread spectrum](https://github.com/user-attachments/assets/48df8716-d061-427a-b6e3-df05f8100018)




![spread spectrum principles](https://github.com/user-attachments/assets/c8b3c61b-491d-4ee8-a5ef-b963736513cd)




![ss demodulation](https://github.com/user-attachments/assets/0f83fd65-5db0-41b0-a51e-8994b6ede1f6)

## RSSI and SNR LoRa Mode in LF Mode (433MHz)
### For SNR > 0:
- RSSI or Packet Strength (dBm) = -164 + RSSI 
### For SNR < 0:
- RSSI or Packet Strength (dBm) = -164 + PacketRSSI + 0.25*PacketSNR


# Lab Exercises

## Lab-1 Introduction to ESP32
#### Arduino                         <img align="right" width="200" height="100" src="https://github.com/user-attachments/assets/d1ea6397-1819-4357-a4ed-60843544cfcc">

- Arduino is an Italian open-source hardware and software company, project, and user community that designs and manufactures single-board microcontrollers and        
microcontroller kits for building digital devices.
- Arduino board designs use a variety of microprocessors and controllers. The boards are equipped with sets of digital and analog input/output (I/O) pins that may be interfaced to various expansion boards ('shields') or breadboards (for prototyping) and other circuits.
- ESP32 is a series of low-cost, low-power system on a chip microcontrollers with integrated Wi-Fi and dual-mode Bluetooth.
- Here is the datasheet of ESP 32 devolopment kit [Datasheet ESP32](https://github.com/silicon-sat/SI-2024-CubeSat/blob/main/docs/Datasheet-ESP32.pdf)
  
- Here is a simple code to blink a led-[LED Blinking](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/blinking%20led)

## Lab-2 Introduction to GPIO programming                            <img align="right" width="200" height="200" src="https://github.com/user-attachments/assets/d406281f-0678-4159-9289-151b28b29aa4">
- GPIO, General Purpose Input Output is a set of pins in the microcontroller, which functions by passing data into and out of the board. They serve as a bidirectional pin, either as an input or output pin, or it also serves as an alternate functionality pin.
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
<img align="right" width="500" height="250" src="https://github.com/Rajesh100903/SI-2024-22BECB73/assets/173932157/5d93dee8-790e-4790-976c-a0a2285f1d4b">
 From the ESP 32 Datasheet
| Parameters | Values |
|------------|--------|
| max output voltage | 4.34 V|
| max output current that GPIO can source from supply to load | .06mA |  
equivalent resistance calculation- for the circuit as shown GPIO->R->LED diode->0

=>4.34-30x10pow(-3)(R)-0.7=0 =>R=3.64/30x10pow(-3)= 121.33 ohms
so the equivalent resistance which we had choosen for our convienience was= 100 ohms

- Code for controlling the led intensity-
``` C
int led = 5;
int brightness = 0;
int fadeamount = 5;
void setup() {
  pinMode(led,OUTPUT);
}
void loop() {
  analogWrite(led,brightness);
  brightness=brightness+fadeamount;
  if(brightness<=0 || brightness>=255) {
    fadeamount=-fadeamount;
  }
  delay(30);
}
``` 
- Code to assign an input port for 2-step dimmer control.
Full intensity, 0: 25-percent intensity.
``` C
#define ledcSetup
#define ledcAttachPin
const int ledpin = 18;
const int freq = 5000;
const int resolution = 8;
void setup() {
 ledcAttachPin(ledpin,freq,resolution);
} 
void loop() {
 for(int dutyCycle = 255; dutyCycle <= 0; dutyCycle++ ){
   ledcWrite(ledpin, dutyCycle);
   delay(1000);
 }
 for(int dutyCycle = 255; dutyCycle >=0; dutyCycle--){
   ledcWrite(ledpin, dutyCycle);
   delay(1000);
 }
}
```
## Lab-4 Dimming multiple LEDs
``` C
int led13 = 11;                // LED connected to digital pin 11
      int led12 = 10;
      int led11 = 9;
      int led10 = 6;
      int led09 = 5;
      int led08 = 3;
      
      void setup()                    // run once, when the sketch starts
      {
            
            pinMode(led13, OUTPUT);      // sets the digital pin as output
            pinMode(led12, OUTPUT);
            pinMode(led11, OUTPUT);
            pinMode(led10, OUTPUT);
            pinMode(led09, OUTPUT);
            pinMode(led08, OUTPUT);
      }
      void loop()                     // run over and over again
      {
            int analogValue = analogRead(0);
            int analogValue1 = analogRead(2);
            Serial.println(analogValue);
            Serial.println(analogValue1);
            delay(10);
            if (analogValue > 500) {
                  for(int fadeValue = 0; fadeValue <= 255; fadeValue += 5){
                  analogWrite(led13, fadeValue);   
                  delay(30);                               
                  }
                  for(int fadeValue = 0; fadeValue <= 255; fadeValue += 5){      
                  analogWrite(led12, fadeValue);    
                  delay(30); 
                         }
```
## Lab-5 Printing data in the serial monitor
- Data can be printed the OLED display by a serial monitor and the following code can be used to print the message in the display.
[OLED](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/OLED%20Display)
![oled](https://github.com/user-attachments/assets/f5305fb5-a027-4e0c-9fb6-c8ba7d1f6545)

- Hardware Setup
   - Connect the OLED Display: OLED displays typically use I2C or SPI communication protocols.
- For I2C:
   - Connect VCC to 3.3V or 5V (depending on your OLED).
   - Connect GND to GND.
   - Connect SCL to A5 (for Arduino Uno) or the corresponding SCL pin on your board.
   - Connect SDA to A4 (for Arduino Uno) or the corresponding SDA pin on your board.
- For SPI:
    - Connections vary, but generally involve VCC, GND, SCK, MOSI, and a few other pins like CS and DC.
- Install Necessary Libraries
    - Adafruit SSD1306 Library: This library is commonly used for controlling OLED displays.
    - Adafruit GFX Library: This library provides graphics functions for drawing on the display.
- To install these libraries:
    - Open the Arduino IDE.
    - Go to Sketch > Include Library > Manage Libraries.
    - Search for "Adafruit SSD1306" and "Adafruit GFX", then install them

## Lab-6 Controlling an LED through serial monitor
- We can control a led through the code [Control](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/Control)
  ### To control an LED through a serial monitor using an Arduino, you can follow these steps:

- Set up your hardware:
    - Connect the anode (long leg) of the LED to a digital pin on the Arduino (e.g., pin 13).
    - Connect the cathode (short leg) of the LED to a resistor (220 ohms recommended).
    - Connect the other end of the resistor to the ground (GND) on the Arduino.
- Write the Arduino code:
     - Open the Arduino IDE.
     - Write the code to control the LED based on serial input.
- Upload the code to the Arduino:
    - Connect your Arduino to your computer using a USB cable.
    - Select the appropriate board and port from the Arduino IDE.
    - Click on the "Upload" button to upload the code to the Arduino.
- Open the Serial Monitor:
  - Click on the magnifying glass icon in the top-right corner of the Arduino IDE to open the Serial Monitor.
  - Set the baud rate to 9600 to match the Serial.begin(9600); in your code.
- Control the LED:
  - Type 1 and press enter to turn the LED on.
  - Type 0 and press enter to turn the LED off.

## Lab-7 I2C-based OLED Display control


## Lab-8 SIGNAL PROCESSING USING PYTHON:-
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

##  Lab-9 I2C temperature sensor interface
We have simulated DHT22 to sense temperature and humidity and display every packet of data recieved by a serial monitor. Code for temperature sensing -[temperature sensor interface](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/temperature%20sensor)
## Lab-10 Introduction to LoRa module
##### LoRa 
LoRa is a long-distance wireless transmission technology based on spread spectrum technology. It adopts the direct sequence spread spectrum method, which has strong anti-interference and high receiving sensitivity, while meeting the needs of low power consumption.
<img width="360" alt="LoRa mdoule" src="https://github.com/user-attachments/assets/929733aa-b627-4cbe-91fb-bf3ce72462c7">
𝐶ℎ𝑎𝑛𝑛𝑒𝑙 𝐶𝑎𝑝𝑎𝑐𝑖𝑡𝑦 𝐶 = 𝐵 ⋅ log2 (1 +𝑆/𝑁) 𝑏𝑖𝑡𝑠/𝑠𝑒𝑐
𝑤ℎ𝑒𝑟𝑒:
𝐵 𝑖𝑠 𝑡ℎ𝑒 𝑐ℎ𝑎𝑛𝑛𝑒𝑙 𝑏𝑎𝑛𝑑𝑤𝑖𝑑𝑡ℎ 𝐵 ,
𝑆 𝑖𝑠 𝑡ℎ𝑒 𝑎𝑣𝑒𝑟𝑎𝑔𝑒 𝑠𝑖𝑔𝑛𝑎𝑙 𝑝𝑜𝑤𝑒𝑟 𝑊𝑎𝑡𝑡𝑠 ,
𝑁: 𝑎𝑣𝑒𝑟𝑎𝑔𝑒 𝑛𝑜𝑖𝑠𝑒 𝑝𝑜𝑤𝑒𝑟 (𝑤𝑎𝑡𝑡𝑠)
With some algebra and assuming S/N << 1 :
𝐶ℎ𝑎𝑛𝑛𝑒𝑙 𝐶𝑎𝑝𝑎𝑐𝑖𝑡𝑦 𝐶 ≈ 𝐵 ⋅𝑆/𝑁 𝑏𝑖𝑡𝑠/𝑠𝑒c
## Lab 11- LoRa communication
#### Introduction to Lora communication using Ra-02 Lora transceiver module with ESP32:-
LoRa (Long Range) communication is a wireless communication technology designed for long-range communication with low power consumption. In this case, we'll explore using the Ra-02 LoRa transceiver module with the ESP32 microcontroller.


![Screenshot 2024-07-13 065555](https://github.com/user-attachments/assets/6534032b-f539-4f9f-903a-17abb5349a31)

 Conditions for efficient communication between LoRa and Antenna
- Frequency: Ensure both Ra-02 modules are set to the same frequency (e.g., 915 MHz in the example).
- Antennas: Attach suitable antennas to Ra-02 modules for better range.
- Power: Ra-02 modules operate at 3.3V, ensure stable power supply.
- Range: LoRa can achieve several kilometers in range under ideal conditions. 
We can refer to the following code to communicate through the LoRa as a transmitter and reciever-[LoRa](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/LoRa)


## Lab 12-Communication between two LoRa nodes
The packets were sent and recieved with RSSI(Received Signal Strength Indicator) and SNR through serial monitor.The code for LoRa transmitter is [LoRa transmitter](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/LoRa%20transmitter) and for reciever is [LoRa reciever](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/LoRa%20Reciever).
We had also sensed temperature and humidity packets through DHT 22 and sent it through LoRa module with ESP 32 board to a serial monitor in form of packets.[temp and humidity](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/temp%20and%20humidity)

## Lab 13- LoRa one-to-many communication setup
In a one-to-many communication setup, a single LoRa transmitter (e.g., a gateway or base station) communicates with multiple LoRa receivers (e.g., sensors or nodes). This is a common configuration in IoT networks, where a central gateway collects data from numerous distributed sensors.


The following is the code for transmitting message from one transmitter and recieving with different serial monitors[LoRa one to many](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/LoRa%20one%20to%20many)

## Lab 14-Introduction to antenna modeling and simulation software 4NEC2
4nec2 is a popular free NEC-2 based antenna modeler and optimizer for Windows. It allows users to design, analyze, and optimize antenna structures and calculate their properties such as radiation patterns, impedance, and more. Here's a brief overview and some guidance on how to use 4nec2.We can manufacture dipole antennas, horn shapped antennas , V shapped antennas.

Using 4NEC2, we did modelling of Antenna and observed the frequency sweep , radiation pattern,SWR etc.
This is the code for antenna modelling of loaded v dipole type
Code-[loaded v dipole](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/Antenna%20modelling%20in%204NEC2)





![Screenshot 2024-07-12 154512](https://github.com/user-attachments/assets/e5ddc66e-4bdc-4b05-8a5e-4035d30e49d6)




![Screenshot 2024-07-12 154642](https://github.com/user-attachments/assets/bda36b98-77a5-4ef7-a34f-3f6633e60e41)





![Screenshot 2024-07-12 154752](https://github.com/user-attachments/assets/312d587c-75d6-4a36-8e3e-080a346d0ede)

The matching network is:-





![Screenshot 2024-07-13 092955](https://github.com/user-attachments/assets/968daec7-b88c-4012-b2ed-b4789c1f1ac0)

## Lab 15: Physical design of Dipole and V-dipole antennas
The following steps were taken to design an antenna and tune it to 433 Mhz:-

- First the length approxing to 18cm were cut and the SWR and minimum frequency were observed using a nano VNA.
- Then it was tuned using VNA and cut respectively by .5 cm or 1 cm to cut down the impedance close to 50 ohm and to lower the frequency to 433 MHz.
- Then the ESP32 and LoRa module were inbtegrated in a pcb boarde and soldered.
- Then it was connected to the antenna by an axial cable and the packets were recieved by the board.





![WhatsApp Image 2024-07-13 at 14 02 47](https://github.com/user-attachments/assets/18eac2ff-1dff-4f13-9386-34dcb8f8871b)




![WhatsApp Image 2024-07-12 at 12 51 57](https://github.com/user-attachments/assets/e0e10087-c9e7-423a-ba14-80a24143f02d)





![WhatsApp Image 2024-07-13 at 10 22 44](https://github.com/user-attachments/assets/cd8a1d79-196e-43b9-9953-2eea6e712c8d)

## Lab 16: Introduction to TinyGS
TinyGS is a community-driven project focused on providing a global network of low-cost ground stations for tracking and receiving data from low Earth orbit (LEO) satellites.TinyGS is an open-source project, allowing anyone to set up a ground station and contribute to the network.

## Lab 17: Setting up a TinyGS ground station
The link to the ground station created by us[SIT BBS](https://tinygs.com/station/SITBBS2_0GS@5483354857)








![Screenshot 2024-07-13 103737](https://github.com/user-attachments/assets/33f7b9c7-76b9-4c5d-ad41-0ff2d7f889a0)

This is the excel sheet containing all the data about the 49 packets that our ground station and antenna recieved from various satelites orbiting around earth.





[SITBBS_02.xlsx](https://github.com/user-attachments/files/16201026/SITBBS_02.xlsx)








![WhatsApp Image 2024-07-13 at 10 34 35](https://github.com/user-attachments/assets/fabcc967-5cea-41a3-82f4-487777d42632)

## Lab 18: Processing TLE data with Python
Two Line Element (TLE) sets are data formats used to describe the orbits of Earth-orbiting objects such as satellites. Each TLE consists of two lines of data that provide information about the satellite's orbital parameters. These elements are essential for tracking and predicting the satellite's position and motion.


Here is an example of a TLE data
- 1 25544U 98067A   20335.91902778  .00000825  00000-0  23903-4 0  9993
- 2 25544  51.6465 105.5483 0002365  23.9857 336.1391 15.49450779249916
Explanation:-
# Line 1 Breakdown:
- Line number (1)
- 25544: Satellite number (25544)
- U: Classification (Unclassified)
- 98067A: International Designator
- 98: Launch Year (1998)
- 067: Launch Number of the Year (67th launch in 1998)
- A: Piece of the launch (first piece)
- 20335.91902778: Epoch
- 20: Year (2020)
- 335.91902778: Day of the year and fractional portion of the day (335th day of 2020, 22.06 hours into the day)
- .00000825: First Derivative of Mean Motion (rev/day²)
- 00000-0: Second Derivative of Mean Motion (rev/day³) (often set to zero)
- 23903-4: BSTAR drag term (a measure of atmospheric drag)
- 0: Ephemeris type (0 is used for SGP4)
- 999: Element number (element set number, 999)
- 3: Checksum for line 1
# Line 2 Breakdown:
- 2: Line number (2)
- 25544: Satellite number (25544)
- 51.6465: Inclination (degrees, 51.6465°)
- 105.5483: Right Ascension of the Ascending Node (degrees, 105.5483°)
- 0002365: Eccentricity (0.0002365)
- 23.9857: Argument of Perigee (degrees, 23.9857°)
- 336.1391: Mean Anomaly (degrees, 336.1391°)
- 15.49450779: Mean Motion (revolutions per day, 15.49450779 rev/day)
- 24991: Revolution number at epoch (24991st orbit since launch)
- 6: Checksum for line 2


  The code for finding out the position of a satelite from it's given TLE data is [TLE](https://github.com/Ananya22becb94/SI-2024-CubeSat-AS/blob/main/Lab/TLE)
  Latitude was generated to be as 33.07590399036185 longitude was -39.341103283558745 and altitude was 830.8149737295089 kms

  ## Lab 19: Simulating Digital Spread Spectrum Modulation
- Resimulate FSK from Lab 8
- Introduce code to convert the digital data into spread spectrum before modulating it to a higher frequency.
- Simulating Digital Spread Spectrum Modulation involves using software tools to model and analyze the behavior of spread spectrum communication techniques, which are widely used in wireless communication 
  systems for their robustness against interference and security advantages.
- Spread spectrum modulation techniques spread the signal over a wider bandwidth compared to the minimum necessary for the transmission of information.

