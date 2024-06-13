# Bare-metal-ArduinoR4
The Arduino Uno microcontroller board has been based, until the R4 version, on the ATmega328P, an 8-bit AVR microcontroller. This architecture has been used a lot in the past and it is possible to find plenty of tutorials on the Internet on how to program *bare-metal* this kind of hadware. For *bare-metal* I simply mean to program the device without any use of the Arduino libraries, thus writing low-level C programs that directly manipulate the registers of the hardware.




## Usage
To get started with this model you can either follow the instructions on the ESM GitHub page ([github](https://github.com/facebookresearch/esm?tab=readme-ov-file#esmfold)) or use the [Huggin Face Transformers library](https://huggingface.co/docs/transformers/model_doc/esm), which provides an easy-to-use implementation and doesn't require the ESMFold dependencies. 

In order to use the tranformer library you need to install `transformers` and `accelerate` 
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
