# BSDM-HAD
This is the official repository for “BSDM: Background Suppression Diffusion Model for Hyperspectral Anomaly Detection”.

## Overview
BSDM-HAD trains a diffusion-based background suppression model for hyperspectral anomaly detection and evaluates it with an RX detector. The pipeline is script-driven and centered around `train.py`.

## Requirements
- Python 3
- torch
- numpy
- scipy
- matplotlib

Install dependencies with pip if needed:

```bash
pip install torch numpy scipy matplotlib
```

## Data Preparation
The MATLAB `.mat` files are expected to be located under `datasets/` by default. Each dataset file must include:

- `data`: hyperspectral cube in shape $(H, W, C)$
- `map`: ground-truth anomaly map in shape $(H, W)$ or $(H, W, 1)$

The provided datasets are referenced in [datasets/README.md](datasets/README.md).

## Quick Start

Train and evaluate on the same dataset:

```bash
python train.py --train_data abu-beach-1 --test_data abu-beach-1
```

Train on one dataset and test on another:

```bash
python train.py --train_data abu-beach-1 --test_data abu-airport-4
```

Save `.mat` outputs and figures:

```bash
python train.py --train_data abu-beach-1 --test_data abu-beach-1 --save_result
```

Run on CPU:

```bash
python train.py --device cpu
```

Use a specific GPU ID:

```bash
python train.py --device gpu --gpu_id 0
```

## Arguments

Key arguments from `train.py`:

- `--data_dir`: dataset folder (default: `./datasets/`)
- `--train_data`: training dataset name without extension (default: `abu-beach-1`)
- `--test_data`: test dataset name without extension (default: `abu-beach-1`)
- `--epochs`: training epochs (default: `500`)
- `--lr`: learning rate (default: `1e-4`)
- `--diffusion_mode`: `gamma` or `alpha` (default: `gamma`)
- `--T`: maximum diffusion time step (default: `1000`)
- `--t`: time step for noise generation (default: `500`)
- `--K`: number of inference iterations (default: `10`)
- `--RX`: enable RX detector evaluation (default: enabled)
- `--save_result`: save `.mat` outputs (default: disabled)
- `--result_save_dir`: output folder (default: `./results/`)
- `--pre_embed_dim`: pre-embedding channels (default: `128`)
- `--hidden_dim`: hidden channels list (default: `[200, 100, 50]`)
- `--seed`: random seed (default: random)
- `--device`: `cpu` or `gpu` (default: `gpu`)
- `--gpu_id`: GPU index when `--device gpu` (default: `0`)

## Outputs

When RX evaluation is enabled (`--RX`), the script prints AUC and FPR for:

- RX on the original test data
- RX on BSDM background-suppressed output

If `--save_result` is specified, the following files are saved under `results/`:

- `result-t{t}-K0{dataset}.mat`: RX result on original data
- `result-t{t}-K{K}{dataset}.mat`: RX result on BSDM output

The script also saves a visualization figure:

- `figure-{dataset}-t{t}-K{K}_AUC_{auc}.png`

## Reproducibility Notes

- Use `--seed` to fix randomness.
- Channel alignment is applied if test data has different band counts from training.

## Project Structure

- `train.py`: end-to-end training and evaluation pipeline
- `models/`: denoising network and diffusion model
- `noise_fn/`: pseudo background noise generation
- `anomaly_detector/`: RX anomaly detector
- `utils.py`: normalization, metrics, and channel alignment
- `datasets/`: `.mat` datasets
- `results/`: saved figures and `.mat` outputs


## Citation

If the work or the code is helpful, please cite the paper:

```
@ARTICLE{11112647,
  author={Ma, Jitao and Xie, Weiying and Shi, Ye and Xiang, Xueshuang and Li, Yunsong and Fang, Leyuan},
  journal={IEEE Transactions on Circuits and Systems for Video Technology}, 
  title={BSDM: Background Suppression Diffusion Model for Hyperspectral Anomaly Detection}, 
  year={2025},
  volume={},
  number={},
  pages={1-1},
  keywords={Noise;Diffusion models;Anomaly detection;Noise reduction;Hyperspectral imaging;Videos;Training;Circuits and systems;Transformers;Labeling;Anomaly detection;diffusion model;background suppression;hyperspectral images},
  doi={10.1109/TCSVT.2025.3595547}}
```

