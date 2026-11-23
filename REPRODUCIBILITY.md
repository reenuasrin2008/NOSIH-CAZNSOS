# Artifact Evaluation & Reproducibility Guide

This document follows **IEEE / ACM Artifact Review and Badging** standards (*Artifacts Available*, *Artifacts Evaluated — Functional*, and *Artifacts Evaluated — Reusable*) so reviewers and researchers can independently reproduce every quantitative claim, table, and figure in **NOSIH**.

---

## 1. Artifact Summary & Claims Scope

| Artifact Dimension | Verification Status | Evidence File |
| :--- | :---: | :--- |
| **7-Layer Automated Test Suite** | `46 / 46` Passed (`0` failures) | [`results/tests/test_suite_summary.json`](results/tests/test_suite_summary.json) |
| **Automated Claim-to-Evidence Parity** | `58 / 58` Claims Verified (`0` violations) | [`results/verification/claim_evidence_matrix.json`](results/verification/claim_evidence_matrix.json) |
| **240-Prompt Diurnal Benchmark** | Deterministic 3-seed reproduction (`[42, 101, 202]`) | [`results/benchmarks/nosih_evaluation_results.json`](results/benchmarks/nosih_evaluation_results.json) |
| **100-Case 10-Family Security Suite** | Physically executed on host CPU (`70/70` blocked, `30/30` benign) | [`results/benchmarks/nosih_evaluation_results.json`](results/benchmarks/nosih_evaluation_results.json) |
| **Online Conformal PID Shift Study** | Deterministic 5-seed reproduction (`[11, 22, 33, 44, 55]`) | [`results/benchmarks/nosih_evaluation_results.json`](results/benchmarks/nosih_evaluation_results.json) |
| **Host-CPU Async Concurrency & WAL** | Physically executed (`C = 1, 10, 50, 100`; `161/161` OK) | [`results/benchmarks/nosih_evaluation_results.json`](results/benchmarks/nosih_evaluation_results.json) |

> **Measurement Honesty Distinction:** Every metric is explicitly tagged as either `PHYSICALLY_MEASURED_HOST_CPU` / `EXACT_DETERMINISTIC` (Plane I crypto/proxy, Merkle proofs, SQLite WAL concurrency, symbolic/RAG CPU execution) or `CALIBRATED_TRACE_SIM` / `HYBRID_CPU_TDP` (neural tier latency/energy profiles when no physical GPU is attached). See [`VERIFICATION_CHECKLIST_STATUS.md`](VERIFICATION_CHECKLIST_STATUS.md) for the complete item-by-item audit.

---

## 2. Reference Hardware & Software Environment

Reference artifact evaluation environment recorded in [`results/benchmarks/hardware_environment.json`](results/benchmarks/hardware_environment.json):

- **OS / Architecture:** Linux `x86_64` (works identically on macOS and Windows/WSL2)
- **Python:** `3.11+` (tested on `Python 3.11.2`)
- **CPU:** Standard 2+ logical cores (no GPU required for the software & hybrid benchmark suite)
- **Dependencies:** `numpy>=1.26.0`, `scipy>=1.11.0`, `jsonschema>=4.20.0`, `matplotlib>=3.8.0`, `Pillow>=10.0.0`, `python-docx>=1.1.0`

---

## 3. One-Command Full Reproduction

```bash
git clone https://github.com/gokulraman-b/nosih.git
cd nosih
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
pip install -e ".[dev]"
make all
```

### Step-by-Step Commands & Expected Runtime

| Stage | Command | Typical Runtime | Outputs Regenerated |
| :--- | :--- | :---: | :--- |
| **Step 1: Unit & Security Tests** | `python3 tests/run_all_tests.py` | `~1–5 s` | `results/tests/test_suite_summary.json` |
| **Step 2: Full Benchmark Suite** | `python3 experiments/run_nosih_evaluation.py` | `~20–45 s` | `results/benchmarks/nosih_evaluation_results.json`, `raw_measurements.jsonl` |
| **Step 3: Claim Parity Audit** | `python3 experiments/verify_nosih_claims.py` | `< 1 s` | `results/verification/claim_evidence_matrix.json` |

---

## 4. Paper Claim-to-Code Traceability Matrix

| Paper Section / Result | Source Module(s) | Evaluation Function / Test |
| :--- | :--- | :--- |
| **Theorem 1 (Macaroon Non-Escalation & JTI Replay)** | `src/nosih/plane1_security/spcce_v3.py` | `tests/crypto/test_layer2_crypto_and_merkle.py`, `tests/security/test_checklist_security_hardening.py` |
| **Theorem 2 (`POSTW+` Provenance Semiring IFC)** | `src/nosih/plane1_security/postw_v3.py`, `proxy_v3.py` | `tests/security/test_layer3_postw_and_ifc.py` |
| **Theorem 3 (Carbon-Aware Primal-Dual Bandit)** | `src/nosih/plane2_control/primal_dual_bandit.py` | `tests/control/test_layer4_bandit_aci_and_cache.py` |
| **Theorem 4 (Online Conformal PID Risk Bound)** | `src/nosih/plane2_control/online_conformal.py` | `experiments/run_nosih_evaluation.py` (5-seed shift study) |
| **Theorem 5 (`PCSP` C-DoW & `PA-PCS-PMC` Sleep-DoS)** | `src/nosih/plane2_control/pcsp.py`, `plane3_execution/power_carbon.py` | `tests/power/test_cross_plane_novelties.py` |
| **CCEC Scope-2 Merkle Audit** | `src/nosih/plane1_security/carbon_cert.py`, `merkle_log.py` | `tests/power/test_cross_plane_novelties.py` |

---

## 5. Physical GPU & Hardware Validation (Optional)

On machines equipped with an NVIDIA GPU (NVML), Intel/AMD RAPL energy counters, and a local Ollama server, run:

```bash
python3 experiments/run_hardware_validation.py
```

This script probes live NVML GPU power, RAPL CPU package energy, and real Ollama inference latency to replace calibrated neural traces with direct physical hardware readings.

---

## 6. Contact for Artifact Support

For reproduction questions or artifact evaluation assistance, contact **GOKULRAMAN B** (`gokulrmn2178@mail.com`).
