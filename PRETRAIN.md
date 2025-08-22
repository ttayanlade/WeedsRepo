## Pre-training Model

```
torchrun main_pretrain.py \
    --batch_size ${batch_size} \
    --model mae_vit_huge_patch14 \
    --norm_pix_loss \
    --mask_ratio ${mask_ratio} \
    --epochs ${epoch} \
    --warmup_epochs ${warmup_epochs} \
    --blr ${blr} \
    --weight_decay ${weight_decay} \
    --data_path ${dir}
```
- Here the effective batch size is e.g For 64 (`batch_size` per gpu) * 8 (`nodes`) * 8 (gpus per node) = 4096. If memory or # gpus is limited, use `--accum_iter` to maintain the effective batch size, which is `batch_size` (per gpu) * `nodes` * 8 (gpus per node) * `accum_iter`.
- `blr` is the base learning rate. The actual `lr` is computed by the [linear scaling rule](https://arxiv.org/abs/1706.02677): `lr` = `blr` * effective batch size / 256.
- Here we use `--norm_pix_loss` as the target for better representation learning. To train a baseline model (e.g., for visualization), use pixel-based construction and turn off `--norm_pix_loss`.

- Hyperparemeter details can be found in [WeedNet: A Foundation Model-Based Global-to-Local AI Approach for Real-Time Weed Species Identification and Classification](https://arxiv.org/pdf/2505.18930).

