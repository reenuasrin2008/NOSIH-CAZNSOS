# Broader Impact, Sustainability & Ethics Statement

---

## 1. Positive Societal & Environmental Impact

- **Reducing Agentic AI Carbon Footprint:** By offloading `50.0%` of deterministic queries to CPU tiers (`≤ 3.5 ms`), modulating neural routing against diurnal grid carbon intensity, and gating GPU idle power via `PA-PCS-PMC`, NOSIH demonstrates `-75.2%` active energy, `-68.7%` operational CO₂, and `-79.35%` idle GPU power reductions in hybrid evaluation.
- **Preventing Automated Financial & Data Harm:** Enforcing non-bypassable RFC 8785 JCS canonicalization, Macaroon capabilities, exact-`Decimal` linear budgets, and `POSTW+` provenance semirings protects organizations deploying autonomous MCP agents from indirect prompt injection, silent exfiltration, and budget-drain attacks.
- **Open, Auditable Science:** Every benchmark trace, test suite, formal proof, and claim-parity check is openly published under the MIT License to support transparent peer review.

---

## 2. Transparency & Honest Reporting of Limitations

- **Hybrid vs. Physical Hardware Scope:** Because standard CI/container environments lack physical GPUs and NVML/RAPL counters, neural tier metrics are explicitly labeled `CALIBRATED_TRACE_SIM` / `HYBRID_CPU_TDP` rather than presented as physical datacenter telemetry. A dedicated physical validation script (`experiments/run_hardware_validation.py`) is included for GPU-equipped deployments.
- **Scope-2 Accounting vs. Hardware TEE Attestation:** `CCEC` provides cryptographically tamper-evident Scope-2 logs under the host TCB, preventing silent post-hoc alteration of sustainability reports. It does not claim resistance against a root-compromised host without hardware TEEs (Intel TDX / NVIDIA Confidential Computing).
- **No Overclaiming on Pure-Text Safety:** NOSIH's `0.0%` FNR (`70/70` blocked) applies strictly to architectural MCP tool-boundary enforcement and does not replace model-level alignment for pure natural-language generation.

---

## 3. Dual-Use & Responsible Disclosure

- The 10-family adversarial test harness (`tests/security/`) is intentionally confined to self-contained, synthetic local tool stubs (mock finance/ERP/email sinks) and cannot be weaponized against external production infrastructure.
- Security researchers discovering weaknesses in NOSIH's cryptographic or IFC boundaries are invited to follow coordinated disclosure in [`SECURITY.md`](SECURITY.md).
