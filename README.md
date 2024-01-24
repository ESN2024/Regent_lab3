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
pio_1 : Represents the Qsys input connected to our pushbutton.
pio_0: Represents the Qsys outputs displaying the value of our accelerometer on 7-segment displays.
Timer_0: Set the timer period to 1 second.
Opencores_i2c_0: Represents the I2C that will interface with our accelerometer.


## Processes and results
- Processes
After configuring our qsys file, we need to create the VHDl codes for our Quartus system.
The various project files are
lab3_sys.qsys: the qsys file previously generated in platform designer
bin_to_7seg.vhd: This VHDL file takes a 4-bit signal as input and generates a 7-bit correspondence for segment activation as output.

![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/ba6cf7f1-a51b-4519-b882-8caa46407784)

regent_lab3.vhd: This file defines the inputs and outputs with all their connections.

![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/8ca04559-f379-46bf-9cc4-e5b0cb1d978f)
![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/070c4928-81d1-4fff-b2ea-99cae997fc78)

NIOS II software flow
Let's open a NIOS II terminal and generate the BSP according to the DE-10 board specifications, preferably in the same directory as our vhd and qsys files:
To generate the BSP file, use the command nio2-bsp hal <system.sopcinfo>.
Generate the project Makefile with the command nios2-app-generate-makefile --app-dir --bsp-dir --elf-name <system.elf> --src-files <file.c>.
All set, we're now going to write our C code that runs on our own processor.

![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/fb3b180e-254d-4eff-99e4-5bdbbae72d8b)
![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/14071e73-8f29-4e5b-8dc9-3a405bc72a71)
![image](https://github.com/ESN2024/Regent_lab3/assets/131348400/219889f6-17e5-4a85-9aef-64dfff9254aa)

Our C program is structured as follows:
Functions for reading or writing 1 data to any register.
We can see that the sign of the value is displayed on the sixth digit and that the fifth value display only a 0 because we'll not be able to overpass the 10 g with the card, as we are showing the different axis values in mg, the value are between 09999 and -09999.
A main function initializing my timer, activating my interruptions, resetting and configuring my offsets for each axis.
To calculate the offset, we used the table of scale factors for the offsets.
We can see that, in our case, the scale factor is 3.9 mg/LSB. Next, let's place the card in a well-defined initial position. Record the acceleration values in this position. These values represent the initial offset. To these values, we subtract the desired theoretical value on each axis and divide by the scale factor.
To retrieve and display accelerometer data, we use the irqhandler_timer function, which is activated every second when the timer is interrupted. 
And finally, to switch between the values of the different axes, we use the irq_button push-button interrupt function, which increments a counter that switch the value that we are displaying (X,Y or Z). 

## Result
After making download-elf, which allows our board to receive the c code created, we obtain the wanted values for each axes with a well done calibration.

## Conclusion
This lab has been a synthesis of everything we learned in the previous 2, solidifying our knowledge and skills while bringing new ones to the task of recovering and calibrating our board's accelerometer data.

