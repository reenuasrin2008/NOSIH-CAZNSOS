# NOSIH Research & Engineering Roadmap

This roadmap tracks verified milestones and planned extensions for physical datacenter validation, live grid telemetry, and hardware-attested sustainability accounting.

---

## Milestone 1 — Verified Tri-Plane Kernel (`v1.0` — Completed)
- [x] **Plane I:** RFC 8785 JCS, signed manifests, Macaroon capabilities + atomic SQLite WAL `jti` replay store, `POSTW+` provenance semiring, exact-`Decimal` linear budgets, `MTLog`, and `CCEC`.
- [x] **Plane II:** `PS-RCSC` provenance-scoped semantic cache, `CA-DPD-LinUCB` diurnal carbon-aware bandit, `PCSP` C-DoW defense, and Online Conformal PID risk controller.
- [x] **Plane III:** Deterministic CPU symbolic/RAG tiers, capability-gated async DAG executor, durable replay journal, and `PA-PCS-PMC` pre-authorized 3-state GPU sleep manager.
- [x] **Verification:** `46/46` tests passing, `58/58` paper claims verified, 8-page IEEE manuscript, and full dark-mode visual telemetry suite.

---

## Milestone 2 — Physical GPU & Hardware Telemetry Validation (`v1.1` — Next)
- [ ] Run end-to-end 240-prompt sweeps on physical NVIDIA A100 / L40S / RTX 4090 hardware via `experiments/run_hardware_validation.py` with live NVML GPU power and Intel/AMD RAPL CPU package counters.
- [ ] Benchmark live local inference backends (Ollama / vLLM sleep-mode APIs) to validate physical `WARM_STANDBY` and `DEEP_SLEEP` wakeup latencies against calibrated profiles.
- [ ] Publish physical hardware telemetry JSONL traces alongside the hybrid reference suite.

---

## Milestone 3 — Live Grid Carbon APIs & Multi-Region Scheduling (`v1.2`)
- [ ] Plug-in live marginal carbon intensity adapters for **ElectricityMaps** and **WattTime** with automatic fallback to the diurnal prior when APIs are stale (`> 60 min`).
- [ ] Add geo-distributed region selection for latency-tolerant batch DAG workloads.

---

## Milestone 4 — Hardware TEE Attestation & Distributed Scale (`v1.3`)
- [ ] Integrate **Intel TDX / AMD SEV-SNP** and **NVIDIA Confidential Computing** attestation quotes into `CCEC` Scope-2 receipts to remove the host-TCB trust assumption.
- [ ] Replace single-node SQLite WAL `jti` replay store with a Raft/PostgreSQL-backed distributed capability lease service for multi-GPU clusters.
