## Fine-tuning Pre-trained Model

### Evaluation

Evaluate model - Single GPU 
(`${dir}` is a directory containing `{train, val}` sets of weed data):

```
python main_finetune.py --eval --resume ${checkpoint_path} --model vit_base_patch14 --batch_size 16 --data_path ${dir}
```

### Fine-tuning

Fine-tune model 

```
torchrun main_finetune.py \
    --batch_size ${batch_size} \
    --model vit_base_patch14 \
    --finetune ${checkpoint_path} \
    --epochs ${epoch} \
    --blr ${blr} \
    --layer_decay ${layer_decay} \
    --weight_decay ${weight_decay} \
    --drop_path ${drop_path} \
    --reprob ${reprob} \
    --mixup ${mixup}$ \
    --cutmix ${cutmix} \
    --dist_eval \
    --data_path ${dir}
```


- Hyperparemeter details can be found in [WeedNet: A Foundation Model-Based Global-to-Local AI Approach for Real-Time Weed Species Identification and Classification](https://arxiv.org/pdf/2505.18930).
