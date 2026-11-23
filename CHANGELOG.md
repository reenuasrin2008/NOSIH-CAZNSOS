# Changelog

All notable changes to **NOSIH** are documented in this file.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and [Semantic Versioning](https://semver.org/).

---

## [1.0.0] — 2026-11-22

### Added
- **Tri-Plane Closed-Loop Kernel (`src/nosih/`)**:
  - **Plane I**: RFC 8785 JCS canonicalization, signed tool manifests, offline-attenuated Macaroon capabilities with atomic SQLite WAL `jti` replay protection, `POSTW+` Integrity × Confidentiality provenance semiring, exact-`Decimal` linear budgets, quarantine receipts, RFC 6962/9162 Merkle Transparency Log (`MTLog`), and Scope-2 Carbon Execution Certificates (`CCEC`).
  - **Plane II**: Provenance-scoped semantic cache (`PS-RCSC`), diurnal carbon-aware primal-dual contextual bandit (`CA-DPD-LinUCB`), Provenance-Coupled Shadow Pricing (`PCSP`), and Online Conformal PID risk controller.
  - **Plane III**: Deterministic CPU symbolic/RAG offload, capability-gated async DAG executor, durable replay journal, hardware telemetry probe, and Pre-Authorized 3-State GPU Power Manager (`PA-PCS-PMC`).
- **Verification & Reproducibility Suite**:
  - `46/46` automated tests across 7 layers (`tests/`).
  - 240-prompt diurnal benchmark, 100-case 10-family security suite, concurrency WAL benchmark, and 58-claim automated parity verifier (`experiments/`).
  - 8-page IEEE manuscript (`paper/nosih_paper.pdf`), formal proofs (`docs/FORMAL_PROOFS.md`), and Architecture & Logic Guide (`docs/NOSIH_Architecture_and_Logic_Guide.docx`).
- **Root-Level Documentation & Visual Suite**:
  - Added publication-grade root documentation (`ARCHITECTURE.md`, `QUICKSTART.md`, `BENCHMARKS.md`, `REPRODUCIBILITY.md`, `THREAT_MODEL.md`, `DATASET_AND_BENCHMARK_CARD.md`, `ETHICS_AND_IMPACT.md`, `ROADMAP.md`, `FAQ.md`, `CHANGELOG.md`, `CODE_OF_CONDUCT.md`) and `.github/` issue/PR templates.
  - Upgraded all 7 dark-mode animated telemetry GIFs and added 3 new animated simulations (`nosih_zero_trust_pipeline.gif`, `nosih_tier_routing_flow.gif`, `nosih_concurrency_wal.gif`).

### Changed
- Standardized repository author metadata and contact details to **GOKULRAMAN B** (`gokulrmn2178@mail.com`) and recorded contributor `reenuasrin2008@gmail.com`.
