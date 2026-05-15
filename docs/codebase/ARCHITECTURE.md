# Architecture

## Core Sections (Required)

### 1) Architectural Style

- Primary style: Script-driven pipeline with modular helper packages
- Why this classification: train.py orchestrates data loading, training, inference, and evaluation by calling functions/classes in models/, noise_fn/, anomaly_detector/, and utils.py
- Primary constraints: Offline batch processing of hyperspectral MAT data; diffusion model requires noise schedule and time step configuration

### 2) System Flow

```text
train.py -> load MAT data -> normalize -> build model + diffusion -> train -> denoise/test -> RX detection -> save outputs
```

Flow detail (evidence in train.py):
1) Load train/test data via scipy.io.loadmat.
2) Normalize data and convert to torch tensor.
3) Build Network and GaussianDiffusion; generate pseudo background noise.
4) Train via GaussianDiffusion.p_loss in a loop.
5) Run test inference (K steps) and align channels if needed.
6) Run RX detector on original and BSDM outputs; compute AUC and save figures.

### 3) Layer/Module Responsibilities

| Layer or module | Owns | Must not own | Evidence |
|-----------------|------|--------------|----------|
| train.py | Orchestration, IO, training loop, evaluation, saving results | Model internals | train.py |
| models/denoising_network.py | Denoising network architecture | Data loading or metrics | models/denoising_network.py |
| models/diffusion_model.py | Diffusion schedule, forward/backward math | Dataset IO | models/diffusion_model.py |
| noise_fn/gauss.py | Noise generation based on mean/std | Training loop | noise_fn/gauss.py |
| anomaly_detector/rx_AD.py | RX anomaly detection | Model training | anomaly_detector/rx_AD.py |
| utils.py | Normalization, metrics, channel alignment | Model definitions | utils.py |

### 4) Reused Patterns

| Pattern | Where found | Why it exists |
|---------|-------------|---------------|
| PyTorch nn.Module subclasses | models/denoising_network.py, models/diffusion_model.py | Standard structure for trainable models and components |
| Utility function modules | utils.py, noise_fn/gauss.py | Shared preprocessing and generation helpers |

### 5) Known Architectural Risks

- Single-script orchestration makes extension (e.g., multi-dataset or multi-run workflows) harder without refactor
- No manifest for dependencies or runtime version, which can impede reproducibility

### 6) Evidence

- train.py
- models/denoising_network.py
- models/diffusion_model.py
- noise_fn/gauss.py
- anomaly_detector/rx_AD.py

## Extended Sections (Optional)

Add only when needed:

- Startup or initialization order details
- Async/event topology diagrams
- Anti-pattern catalog with refactoring paths
- Failure-mode analysis and resilience posture
