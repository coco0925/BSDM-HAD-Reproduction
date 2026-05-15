# External Integrations

## Core Sections (Required)

### 1) Integration Inventory

| System | Type (API/DB/Queue/etc) | Purpose | Auth model | Criticality | Evidence |
|--------|---------------------------|---------|------------|-------------|----------|
| [TODO] | [TODO] | [TODO] | [TODO] | [TODO] | [TODO] |

### 2) Data Stores

| Store | Role | Access layer | Key risk | Evidence |
|-------|------|--------------|----------|----------|
| Local MAT files | Training/testing data input | train.py via scipy.io.loadmat | Missing versioning or checksums | train.py |

### 3) Secrets and Credentials Handling

- Credential sources: [TODO]
- Hardcoding checks: none found in scanned files
- Rotation or lifecycle notes: [TODO]

### 4) Reliability and Failure Behavior

- Retry/backoff behavior: none observed
- Timeout policy: [TODO]
- Circuit-breaker or fallback behavior: none observed

### 5) Observability for Integrations

- Logging around external calls: no explicit integration logging
- Metrics/tracing coverage: none observed
- Missing visibility gaps: dataset IO and RX runtime metrics not logged

### 6) Evidence

- train.py
- datasets/README.md

## Extended Sections (Optional)

Add only when needed:

- Endpoint-by-endpoint catalog
- Auth flow sequence diagrams
- SLA/SLO per integration
- Region/failover topology notes
