# Bare-metal ArduinoR4
The Arduino Uno microcontroller board has been based, until the R4 version, on the ATmega328P, an 8-bit AVR microcontroller. This architecture has been used a lot in the past and it is possible to find plenty of tutorials on the Internet on how to program *bare-metal* this kind of hadware. For *bare-metal* I simply mean to program the device without any use of the Arduino libraries, thus writing low-level C programs that directly manipulate the registers of the hardware. This implies reading and understanding the datasheet of our microcontroller in order to know where the desired ports are located. My aim here is to do the exact same thing but with a different architecture, the Arduino Uno R4 wifi, which, on the other hand, is based on the RA4M1 microprocessor from Renesas. We can start by looking at a simple example as blinking a led. 


## Previous Arduino Unos
If we want to blink the built-in LED on an AVR-based Arduino what we first need to know is to what port our digital pin is associated. In other words, where are located in memory the registers that we want to modify. This information can be found on the datasheet of our microcontroller board. For instance, for the Arduino Uno Rev3 we find:

<img width="642" alt="Arduino-R3" src="https://github.com/davideaguglia/Bare-metal-ArduinoR4/assets/151211663/57e924b5-8312-4769-96d3-fd93c3dd7523">

The D13 pin is related to the PB5. From at the ATmega328P datasheet we get these informations

<img width="616" alt="PORTB" src="https://github.com/davideaguglia/Bare-metal-ArduinoR4/assets/151211663/852e9d3f-ec71-40e9-b9a9-04030c9cdcd0">

The Data Direction Register (DDRB) is located in 0x24 and the bit that we want to flip, in order to set that pin as an output, is bit 5. Once that pin is set as an output we can manipulate the Port B Data Register, located in 0x25, in order to turn the led on, setting bit 5 to 1, or to turn it off, setting bit 5 to 0.  


## Arduino R4
<img width="593" alt="Arduino-R4" src="https://github.com/davideaguglia/Bare-metal-ArduinoR4/assets/151211663/7e8022f3-d04d-46b0-b445-423c28ab857a">

From the datasheet of the Arduino uno R4 we can see that the D13 pin is associated with the pin P102. The necessary informations to manipulate this port can be found in the Renesas RA4M1 datsheet. 

<img width="887" alt="PORT1" src="https://github.com/davideaguglia/Bare-metal-ArduinoR4/assets/151211663/a80b6e5e-f9e1-4a35-8976-ea711ccf7923">


From table 19.1 we find that our pin P102 is asssociated with PORT1. In the same document we find the following informations

<img width="871" alt="PORT1_registers" src="https://github.com/davideaguglia/Bare-metal-ArduinoR4/assets/151211663/02dc4aee-c7ed-483e-9944-be690e4eccd9">

First, the base address of our register block is 0x40040000. Then we can see that the Port Control Register 1 (PCNTR1) "specifies the port direction and the output data, and is accessed in 32-bit units. The PODRn (bits [31:16] in PCNTR1) and PDRn (bits [15:0] in PCNTR1) respectively, are accessed in 16-bit units". This means that in our code we can first define the desired base address, write 1 to the bit number 2 in order to set the led as an output and finally write 1 or 0 to the bit 18 to turn on or off the led, respectively.   

