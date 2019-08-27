# Models
Because I forget.

## MNLI 
 - [Training](https://github.com/danyaljj/fairseq/blob/master/examples/roberta/README.glue.md) 
 - [Model files](https://drive.google.com/drive/folders/1ysmtlOJo7qGypLRqyJeHe_CoG6mgsAhl?usp=sharing)
 - [Inference and evaluation](https://github.com/danyaljj/fairseq/blob/master/examples/roberta/glue_inference.py).  
 - [Predictions](https://github.com/danyaljj/fairseq/tree/master/examples/roberta/glue_data/MNLI/predictions)
 - Evaluation output:  
 ```bash
# Matched: 
(env3.6) danielk@aristo-server2 ~/fairseq/examples/roberta $ python3 glue_inference.py
loading archive file mnli-checkpoints/
loading archive file MNLI-bin
| [input] dictionary: 50265 types
| [label] dictionary: 9 types
1042301B [00:00, 3931487.18B/s]
456318B [00:00, 8495321.26B/s]
| Accuracy:  0.9018848700967906


# Mismatched: 
(env3.6) danielk@aristo-server2 ~/fairseq/examples/roberta $ python3 glue_inference.py
loading archive file mnli-checkpoints/
loading archive file MNLI-bin
| [input] dictionary: 50265 types
| [label] dictionary: 9 types
| Accuracy:  0.899613506916192

 ```
 

## SNLI 
 - Training: same as MNLI (above)
 - [Model file](https://drive.google.com/drive/folders/1uv8IpJ_QEp-hUAThWUZ7gDBC1nGN5-p7?usp=sharing) 
 - [Inference and predictions]
 - Evaluation output: 

```bash
# dev 
(env3.6) danielk@aristo-server2 ~/fairseq/examples/roberta/glue_data/SNLI-simplified $ python3 snli_inference.py
loading archive file ../../snli-checkpoint/
| [input] dictionary: 50265 types
| [label] dictionary: 9 types
| Accuracy:  0.9233895549685024

# test 
(env3.6) danielk@aristo-server2 ~/fairseq/examples/roberta/glue_data/SNLI-simplified $ python3 snli_inference.py 
loading archive file ../../snli-checkpoint/
| [input] dictionary: 50265 types
| [label] dictionary: 9 types
| Accuracy:  0.9178542345276873
```

## BoolQ 

## SQuAD 1.1 

## SQuAD 2.0 

## SciTail 

## 
