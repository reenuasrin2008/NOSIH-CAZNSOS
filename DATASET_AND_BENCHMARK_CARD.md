# Dataset & Benchmark Card

Structured documentation for the **NOSIH 240-Prompt Diurnal Benchmark**, **100-Case Zero-Trust Security Suite**, and **168-Hour Synthetic Carbon Trace** (following *Datasheets for Datasets* conventions).

---

## 1. Benchmark Suite Overview

| Artifact File | Records | Domain / Purpose | Format |
| :--- | :---: | :--- | :---: |
| [`results/benchmarks/benchmark_prompts_240.jsonl`](results/benchmarks/benchmark_prompts_240.jsonl) | `240` | 6-category diurnal neuro-symbolic routing workload | JSONL |
| [`results/benchmarks/raw_measurements.jsonl`](results/benchmarks/raw_measurements.jsonl) | `1,440+` | Per-prompt, per-seed raw latency, energy, CO₂, cost & success traces | JSONL |
| [`results/benchmarks/nosih_evaluation_results.json`](results/benchmarks/nosih_evaluation_results.json) | Summary | Aggregated statistics, Wilcoxon p-values, effect sizes, ablation & security metrics | JSON |
| [`results/benchmarks/hardware_environment.json`](results/benchmarks/hardware_environment.json) | `1` | Host OS, CPU, Python, RAPL/NVML availability & accounting mode | JSON |

---

## 2. 240-Prompt Workload Composition (6 Balanced Categories)

Each category contains exactly `40` prompts (`6 × 40 = 240`), evaluated across `3` deterministic seeds (`[42, 101, 202]`):

| Category | Count | Ground-Truth Tier | Execution / Evaluation Mode | NOSIH Mean Latency |
| :--- | :---: | :--- | :--- | :---: |
| `symbolic_math` | `40` | `T0b_SYMBOLIC` | `EXACT_DETERMINISTIC` (Host CPU AST) | `3.2 ms` |
| `policy_rag` | `40` | `T0b_SYMBOLIC` | `EXACT_DETERMINISTIC` (Host CPU L2 TF-IDF) | `2.8 ms` |
| `simple_factual` | `40` | `T1_SMALL` (3B) | `CALIBRATED_BERNOULLI_SIM` | `415.4 ms` |
| `medium_analytical` | `40` | `T2_MEDIUM` (8B) | `CALIBRATED_BERNOULLI_SIM` | `1258.5 ms` |
| `complex_multistep` | `40` | `T3_LARGE` (32B) | `CALIBRATED_BERNOULLI_SIM` | `2286.0 ms` |
| `ambiguous_cacheable` | `40` | `T0a_CACHE` / Neural | `PS-RCSC` Cache + Calibrated Neural Fallback | `279.9 ms` (`1.8 ms` P50) |

---

## 3. File Schemas

### `benchmark_prompts_240.jsonl`
```json
{
  "id": "SYM_MATH_00",
  "category": "symbolic_math",
  "prompt": "Calculate (100 + 25) * 2",
  "tier_true": "T0b_SYMBOLIC",
  "expected_answer": "250",
  "tokens": 180,
  "cache_key": "m_0"
}
```

### `raw_measurements.jsonl`
```json
{
  "mode": "static_baseline",
  "seed": 42,
  "id": "SYM_MATH_00",
  "category": "symbolic_math",
  "tier_true": "T0b_SYMBOLIC",
  "tier_routed": "T3_LARGE",
  "grid_carbon_gco2_kwh": 297.34,
  "latency_ms": 2594.458,
  "energy_kwh": 0.00011044,
  "co2_g": 0.03284,
  "cost_usd": 0.00016625,
  "success": true,
  "eval_judge": "CALIBRATED_BERNOULLI_SIM",
  "model_profile": "qwen2.5-32b"
}
```

---

## 4. Synthetic 168-Hour Diurnal Carbon Forecast Benchmark

- **Origin Tag:** `SYNTHETIC_DIURNAL_OU_BENCHMARK` (distinct from live commercial grid APIs).
- **Dynamics:** 7-day (`168 h`) diurnal solar-trough / evening-peak cycle (`180–520 gCO₂/kWh`) perturbed by an Ornstein-Uhlenbeck stochastic residual process.
- **Measured Accuracy:** Deterministic prior `11.37 gCO₂/kWh` MAE (`3.63%` MAPE); 5-minute live blending `4.10 gCO₂/kWh` MAE (`5.33` RMSE); 60-minute stale fallback `14.34` RMSE.

---

## 5. Licensing, Privacy & Intended Use

- **License:** MIT License (same as repository).
- **PII / Sensitive Data:** Contains **zero** personally identifiable information or proprietary customer data; all prompts and financial test cases are synthetically generated.
- **Intended Use:** Reproducible academic evaluation of carbon-aware neuro-symbolic routing, conformal risk control, and zero-trust MCP tool isolation.
