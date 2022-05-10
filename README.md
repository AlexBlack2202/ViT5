# ViT5
A pretrained Transformer-based encoder-decoder model for the Vietnamese language. With [T5](https://github.com/google-research/text-to-text-transfer-transformer)-style self-supervised pretraining, ViT5 is trained on a large corpus of high-quality and diverse Vietnamese texts. We benchmark ViT5 on two downstream text generation tasks, Abstractive Text Summarization and Named Entity Recognition. All the experiments are shown in our paper [ViT5: Pretrained Text-to-Text Transformer for Vietnamese Language Generation]()


### HF Model Checkpoint
- [ViT5-Base-1024 (1M)](https://huggingface.co/VietAI/vit5-base)
- [ViT5-Large-1024 (1M)](https://huggingface.co/VietAI/vit5-large)

#### Example
Below, we give an example of how to load ViT5 model from HuggingFace to summarize documents:
```python
from transformers import AutoTokenizer, AutoModelForSeq2SeqLM

tokenizer = AutoTokenizer.from_pretrained("VietAI/vit5-base")  
model = AutoModelForSeq2SeqLM.from_pretrained("VietAI/vit5-base")

sentence = "Xin chào"
text =  "summarize: " + sentence + " </s>"
encoding = tokenizer.encode_plus(text, pad_to_max_length=True, return_tensors="pt")
input_ids, attention_masks = encoding["input_ids"].to("cuda"), encoding["attention_mask"].to("cuda")
outputs = model.generate(
    input_ids=input_ids, attention_mask=attention_masks,
    max_length=512,
    early_stopping=True
)
for output in outputs:
    line = tokenizer.decode(output, skip_special_tokens=True, clean_up_tokenization_spaces=True)
    print(line)
```

## Evaluation
### Datasets
- [Wikilingua](https://github.com/esdurmus/Wikilingua)
- [Vietnews](https://github.com/ThanhChinhBK/vietnews)
- [Pho_NER](https://github.com/VinAIResearch/PhoNER_COVID19)


### Finetuning
#### Abstractive Text Summarization
...

#### Named Entity Recognition
...

## Citation
```
Coming soon
```

<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements
We would like to thank Google for the support of Cloud credits and TPU quota!
