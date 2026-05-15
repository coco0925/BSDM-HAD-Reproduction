# Codebase Structure

## Core Sections (Required)

### 1) Top-Level Map

| Path | Purpose | Evidence |
|------|---------|----------|
| anomaly_detector/ | RX anomaly detector implementation | anomaly_detector/rx_AD.py |
| datasets/ | Local MAT datasets for training/testing | datasets/README.md |
| docs/ | Documentation output (codebase scan and docs) | docs/codebase/.codebase-scan.txt |
| models/ | Diffusion model and denoising network | models/diffusion_model.py |
| noise_fn/ | Noise generation utilities | noise_fn/gauss.py |
| results/ | Saved result images and outputs | results/README.md |
| supplementary material/ | Paper supplementary material PDFs | supplementary material/Readme.md |
| train.py | Main training/testing script | train.py |
| utils.py | Normalization, metrics, and channel alignment | utils.py |
| README.md | Project overview and run instructions | README.md |
| BSDM_Background_Suppression_Diffusion_Model_for_Hyperspectral_Anomaly_Detection.pdf | Paper PDF | docs/codebase/.codebase-scan.txt |

### 2) Entry Points

- Main runtime entry: train.py
- Secondary entry points (worker/cli/jobs): NONE
- How entry is selected (script/config): manual run via `python train.py` in README.md

### 3) Module Boundaries

| Boundary | What belongs here | What must not be here |
|----------|-------------------|------------------------|
| train.py | End-to-end training/testing orchestration | Core model definitions
| models/ | Network and diffusion model implementations | Data loading and evaluation IO
| noise_fn/ | Noise generation helpers | Training loops
| anomaly_detector/ | RX detector implementation | Model training code
| utils.py | Metrics and preprocessing helpers | Model architecture
| datasets/ | Dataset artifacts only | Code logic
| results/ | Output artifacts only | Code logic

### 4) Naming and Organization Rules

- File naming pattern: snake_case for modules (denoising_network.py, diffusion_model.py)
- Directory organization pattern: top-level modules by role (models, noise_fn, anomaly_detector)
- Import aliasing or path conventions: relative package imports via module __init__.py files

### 5) Evidence

- docs/codebase/.codebase-scan.txt
- train.py
- models/__init__.py

## Extended Sections (Optional)

Add only when repository complexity requires it:

- Subdirectory deep maps by feature/layer
- Middleware/boot order details
- Generated-vs-source layout boundaries
- Monorepo workspace-level structure maps
