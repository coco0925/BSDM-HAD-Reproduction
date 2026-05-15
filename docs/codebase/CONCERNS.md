# Codebase Concerns

## Core Sections (Required)

### 1) Top Risks (Prioritized)

| Severity | Concern | Evidence | Impact | Suggested action |
|----------|---------|----------|--------|------------------|
| high | No automated tests or test config detected | docs/codebase/.codebase-scan.txt | Changes may break training/evaluation silently | Add a minimal test harness for utils and RX |
| med | No dependency manifest or pinned versions | README.md | Reproducibility and environment drift | Add requirements.txt or pyproject.toml |
| med | RX detector uses Python loop over all pixels | anomaly_detector/rx_AD.py | Slow on large images | Vectorize or use optimized linear algebra |
| med | AUC calculation uses 30,000 thresholds loop | utils.py | Slow evaluation for large datasets | Reduce sampling or vectorize |

### 2) Technical Debt

| Debt item | Why it exists | Where | Risk if ignored | Suggested fix |
|-----------|---------------|-------|-----------------|---------------|
| Single script orchestration | Research prototype style | train.py | Harder to extend or reuse modules | Split data IO, training, and eval into modules |
| Implicit dataset expectations | No explicit dataset schema docs | train.py, datasets/README.md | Misuse or misaligned data formats | Document expected MAT keys and shapes |

### 3) Security Concerns

| Risk | OWASP category (if applicable) | Evidence | Current mitigation | Gap |
|------|--------------------------------|----------|--------------------|-----|
| None observed | N/A | docs/codebase/.codebase-scan.txt | N/A | [TODO] |

### 4) Performance and Scaling Concerns

| Concern | Evidence | Current symptom | Scaling risk | Suggested improvement |
|---------|----------|-----------------|-------------|-----------------------|
| RX per-pixel loop | anomaly_detector/rx_AD.py | O(M*N) loop in Python | Slow on large HSI | Vectorize computation |
| AUC loop over thresholds | utils.py | 30,000-step loop | Slow evaluation | Use vectorized thresholding or fewer steps |

### 5) Fragile/High-Churn Areas

| Area | Why fragile | Churn signal | Safe change strategy |
|------|-------------|-------------|----------------------|
| [TODO] | [TODO] | No git history found | [TODO] |

### 6) [ASK USER] Questions

1. [ASK USER] What Python version and hardware (CPU/GPU) are expected for reproducible runs?
2. [ASK USER] Do you want a formal dependency file (requirements.txt/pyproject.toml) and pinned versions?
3. [ASK USER] Are there expected dataset schemas (keys/shapes) that should be documented?

### 7) Evidence

- docs/codebase/.codebase-scan.txt
- README.md
- train.py
- utils.py
- anomaly_detector/rx_AD.py

## Extended Sections (Optional)

Add only when needed:

- Full bug inventory
- Component-level remediation roadmap
- Cost/effort estimates by concern
- Dependency-risk and ownership mapping
