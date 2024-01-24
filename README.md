# Regent_lab3
# lab3 : "Display the gyroscope data on the 7-segments display" 

## Introduction

The aim is to deepening our knowledge and putting it into practice through the creation of a NIOS architecture to retrieve values from an accelerometer. The specifications were clear:
- Calibrate your board's accelerometer
- Request acceleration data every second
- Read acceleration in X, Y and Z directions
- Display their value on the 7seg displays
- Toggle between values using a push-button



## Architecture
Based on the specifications, we determined the architecture to be implemented on the designer platform.
Creating a basic NIOS II Platform Designer system

![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/63963a32-19a8-4ec8-9220-e61ddd2a44d5)

The components of our system are:
onchip_memory: A RAM with a storage capacity of 40 MB.
pio_0 : Represents the Qsys input connected to our pushbutton.
pio_1,pio_2,pio_3,pio_4: Represents the Qsys outputs displaying the value of our accelerometer on 7-segment displays.
pio_5: Represents the Qsys outputs displaying the sign of our accelerometer value on a 7-segment display.
Timer_0: Set the timer period to 1 second.
Opencores_i2c_0: Represents the I2C that will interface with our accelerometer.




![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/8ca04559-f379-46bf-9cc4-e5b0cb1d978f)
![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/070c4928-81d1-4fff-b2ea-99cae997fc78)


![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/ba6cf7f1-a51b-4519-b882-8caa46407784)

![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/fb3b180e-254d-4eff-99e4-5bdbbae72d8b)
![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/14071e73-8f29-4e5b-8dc9-3a405bc72a71)
![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/219889f6-17e5-4a85-9aef-64dfff9254aa)

