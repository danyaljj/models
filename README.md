# Models
Because I forget.

## MNLI 
 - [Training](https://github.com/danyaljj/fairseq/blob/master/examples/roberta/README.glue.md) 
 - Training script: 
 ```
 CUDA_VISIBLE_DEVICES=6,7 python train.py /home/danielk/fairseq/examples/roberta/MNLI-bin/     --restore-file $ROBERTA_PATH     --max-positions 512     --max-sentences $MAX_SENTENCES     --max-tokens 4400     --task sentence_prediction     --reset-optimizer --reset-dataloader --reset-meters     --required-batch-size-multiple 1     --init-token 0 --separator-token 2     --arch roberta_large     --criterion sentence_prediction     --num-classes $NUM_CLASSES     --dropout 0.1 --attention-dropout 0.1     --weight-decay 0.1 --optimizer adam --adam-betas "(0.9, 0.98)" --adam-eps 1e-06     --clip-norm 0.0     --lr-scheduler polynomial_decay --lr $LR --total-num-update $TOTAL_NUM_UPDATES --warmup-updates $WARMUP_UPDATES     --fp16 --fp16-init-scale 4 --threshold-loss-scale 1 --fp16-scale-window 128     --max-epoch 10     --find-unused-parameters     --best-checkpoint-metric accuracy --maximize-best-checkpoint-metric;
 ```
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
 - Training script: 
 ```
 CUDA_VISIBLE_DEVICES=6 python train.py /home/danielk/fairseq/examples/roberta/SNLI-simplified-bin/     --restore-file $ROBERTA_PATH     --max-positions 512     --max-sentences $MAX_SENTENCES     --max-tokens 4400     --task sentence_prediction     --reset-optimizer --reset-dataloader --reset-meters     --required-batch-size-multiple 1     --init-token 0 --separator-token 2     --arch roberta_large     --criterion sentence_prediction     --num-classes $NUM_CLASSES     --dropout 0.1 --attention-dropout 0.1     --weight-decay 0.1 --optimizer adam --adam-betas "(0.9, 0.98)" --adam-eps 1e-06     --clip-norm 0.0     --lr-scheduler polynomial_decay --lr $LR --total-num-update $TOTAL_NUM_UPDATES --warmup-updates $WARMUP_UPDATES     --fp16 --fp16-init-scale 4 --threshold-loss-scale 1 --fp16-scale-window 128     --max-epoch 40     --find-unused-parameters     --skip-invalid-size-inputs-valid-test     --best-checkpoint-metric accuracy --maximize-best-checkpoint-metric;
 ```
 
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
 - [Model](https://drive.google.com/drive/folders/1s7F__A3x5i29nJUyqxFKyyUsapugHpR_?usp=sharing) 
 - Training script: 
 ```bash 
 TOTAL_NUM_UPDATES=3000  # 10 epochs through RTE for bsz 16
WARMUP_UPDATES=180      # 6 percent of the number of updates
LR=1e-05                # Peak LR for polynomial LR scheduler.
NUM_CLASSES=2
MAX_SENTENCES=16        # Batch size.
ROBERTA_PATH=/home/danielk/fairseq/examples/roberta/roberta.large/model.pt


CUDA_VISIBLE_DEVICES=0 python train.py /home/danielk/fairseq/examples/roberta/BoolQ-bin/ \
    --restore-file $ROBERTA_PATH \
    --max-positions 512 \
    --max-sentences $MAX_SENTENCES \
    --max-tokens 4400 \
    --task sentence_prediction \
    --reset-optimizer --reset-dataloader --reset-meters \
    --required-batch-size-multiple 1 \
    --init-token 0 --separator-token 2 \
    --arch roberta_large \
    --criterion sentence_prediction \
    --num-classes $NUM_CLASSES \
    --dropout 0.1 --attention-dropout 0.1 \
    --weight-decay 0.1 --optimizer adam --adam-betas "(0.9, 0.98)" --adam-eps 1e-06 \
    --clip-norm 0.0 \
    --lr-scheduler polynomial_decay --lr $LR --total-num-update $TOTAL_NUM_UPDATES --warmup-updates $WARMUP_UPDATES \
    --fp16 --fp16-init-scale 4 --threshold-loss-scale 1 --fp16-scale-window 128 \
    --max-epoch 50 \
    --find-unused-parameters \
    --skip-invalid-size-inputs-valid-test \
    --best-checkpoint-metric accuracy --maximize-best-checkpoint-metric;
 ```
 - [Evaluation and prediction files](https://github.com/danyaljj/fairseq/tree/master/examples/roberta/glue_data/BoolQ/predictions) 
 - Output log: 
```
(env3.6) danielk@aristo-server2 ~/fairseq/examples/roberta/glue_data/BoolQ $ python3 boolq_inference.py
loading archive file ../../boolq-checkpoint/
| [input] dictionary: 50265 types
| [label] dictionary: 9 types
| Accuracy:  0.8234394124847001
```

## SQuAD 1.1 

## SQuAD 2.0 

## SciTail 

## 
