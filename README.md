# Bare-metal-ArduinoR4

ESMFold is a protein language model based on the ESM-2 3B parameter architecture developed by the Meta Fundamental AI Research Protein Team (FAIR) ([paper](https://www.biorxiv.org/content/10.1101/2022.07.20.500902v2)).
It is one of the best model available when it comes to predicting the structure of a protein from the amino acids sequence. However, the GPU resources that are necessary to run this model can be prohibitive, even for sequences of a few hundreds of residues. This article aim at finding some possible solutions to overcome this issue, using quantization techniques.

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
