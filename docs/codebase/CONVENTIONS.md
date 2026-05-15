# Coding Conventions

## Core Sections (Required)

### 1) Naming Rules

| Item | Rule | Example | Evidence |
|------|------|---------|----------|
| Files | snake_case | denoising_network.py | models/denoising_network.py |
| Functions/methods | snake_case | generate_pseudo_background_noise | noise_fn/gauss.py |
| Types/interfaces | PascalCase classes | GaussianDiffusion, Network | models/diffusion_model.py |
| Constants/env vars | [TODO] | [TODO] | [TODO] |

### 2) Formatting and Linting

- Formatter: [TODO]
- Linter: [TODO]
- Most relevant enforced rules: [TODO]
- Run commands: [TODO]

### 3) Import and Module Conventions

- Import grouping/order: standard libs, third-party libs, then local modules (observed in train.py)
- Alias vs relative import policy: relative package imports via __init__.py
- Public exports/barrel policy: __init__.py re-exports key objects

### 4) Error and Logging Conventions

- Error strategy by layer: minimal explicit error handling; assertions used in utils.false_alarm_rate
- Logging style and required context fields: simple print statements in train.py and noise_fn/gauss.py
- Sensitive-data redaction rules: [TODO]

### 5) Testing Conventions

- Test file naming/location rule: [TODO]
- Mocking strategy norm: [TODO]
- Coverage expectation: [TODO]

### 6) Evidence

- train.py
- models/__init__.py
- utils.py
- noise_fn/gauss.py

## Extended Sections (Optional)

Add only for large or inconsistent codebases:

- Layer-specific error handling matrix
- Language-specific strictness options
- Repo-specific commit/branching conventions
- Known convention violations to clean up
