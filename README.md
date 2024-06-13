# Bare-metal ArduinoR4
The Arduino Uno microcontroller board has been based, until the R4 version, on the ATmega328P, an 8-bit AVR microcontroller. This architecture has been used a lot in the past and it is possible to find plenty of tutorials on the Internet on how to program *bare-metal* this kind of hadware. For *bare-metal* I simply mean to program the device without any use of the Arduino libraries, thus writing low-level C programs that directly manipulate the registers of the hardware. This implies reading and understanding the datasheet of our microcontroller in order to know where the desired ports are located. My aim here is to do the exact same thing but with a different architecture, the Arduino Uno R4 wifi, which, on the other hand, is based on the RA4M1 microprocessor from Renesas. We can start by looking at a simple example as blinking a led. 


## Previous Arduino Unos
If we want to blink the built-in LED on an AVR-based Arduino what we first need to know is to what port our digital pin is associated. In other words, where are located in memory the registers that we want to modify. This information can be found on the datasheet of our microcontroller board. For instance, for the Arduino Uno Rev3 we find

![](https://github.com/davideaguglia/Bare-metal-ArduinoR4/blob/6ac86773811ca865364ca5cb69d9fa065511b6db/images/Arduino-R3.png | width=100)

<img src="[https://your-image-url.type](https://github.com/davideaguglia/Bare-metal-ArduinoR4/blob/6ac86773811ca865364ca5cb69d9fa065511b6db/images/Arduino-R3.png)" width="250">


```
pip install transformers accelerate
```
Predicting the protein structure for a given sequence is then straightforward. First you need to instantiate the model, eventually transferring it to GPU

```c
from transformers import AutoTokenizer, EsmForProteinFolding

tokenizer = AutoTokenizer.from_pretrained("facebook/esmfold_v1")
model = EsmForProteinFolding.from_pretrained("facebook/esmfold_v1")

model = model.cuda()
```
Then given a `sequence` it is possible to create the model inputs through the `tokenizer`
