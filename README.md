# NativeMEM (Code Release WIP)

<div id="top" align="left">
  <a href="https://opendrivelab.com/NativeMEM"><img src="https://img.shields.io/badge/Proj_Page-blue" alt="Project Page"></a>
  <a href="https://arxiv.org/abs/2607.06678"><img src="https://img.shields.io/badge/arXiv-2607.06678-b31b1b" alt="arXiv"></a>
</div>

⚠️ This repository is a work-in-progress public code release for NativeMEM.

> The code in this repository is being actively cleaned, renamed, and validated for public use. APIs, config names, preprocessing scripts, and training commands may still change. 

## Current Scope

NativeMEM is a two-stage memory-augmented vision-language-action training pipeline for long-horizon robot manipulation.

The repository keeps the upstream `openpi` package namespace for compatibility.

## Temporary Usage Notes

Prepare RoboTwin/RMBench-style raw HDF5 episodes for memory-tokenizer training:

```bash
python scripts/prepare_mem_tokenizer_h5.py \
    --dataset_dir /path/to/task_a/demo/data /path/to/task_b/demo/data \
    --output_path /path/to/sim_all.h5 \
    --dataset_type sim
```

Merge multiple prepared shards (e.g., sim and real):

```bash
python scripts/merge_mem_tokenizer_h5.py \
    --input_path /path/to/sim_all.h5 --dataset_type sim \
    --input_path /path/to/arx_all.h5 --dataset_type arx \
    --output_path /path/to/train.h5
```

Train the memory tokenizer:

```bash
python scripts/train_mem_tokenizer.py mem_tokenizer_pretrain \
    --exp_name=my_mem_tokenizer \
    --data.repo_id=/path/to/train.h5 \
    --overwrite
```
