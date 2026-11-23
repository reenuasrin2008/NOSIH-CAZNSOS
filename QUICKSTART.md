# NOSIH Quickstart Guide

Get the complete **NOSIH** kernel running, tested, benchmarked, and claim-verified in under 3 minutes.

---

## 1. Prerequisites

- **Python 3.11+**
- Standard Linux / macOS / WSL2 environment (no GPU required for software verification & hybrid benchmark reproduction; optional NVIDIA GPU + Ollama for physical hardware validation).

---

## 2. Clone & Install

```bash
git clone https://github.com/gokulraman-b/nosih.git
cd nosih
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
pip install -e ".[dev]"
```

---

## 3. One-Command Verification (`make all`)

Run the full 7-layer test suite, 240-prompt benchmark evaluation, and automated 58-claim parity check:

```bash
make all
```

Or run each step individually:

| Step | Command | Expected Output |
| :--- | :--- | :--- |
| **1. Test Suite** | `python3 tests/run_all_tests.py` | `46/46` tests passing across 7 layers (`~1.0 s`) |
| **2. Benchmarks** | `python3 experiments/run_nosih_evaluation.py` | Regenerates `results/benchmarks/nosih_evaluation_results.json` |
| **3. Claim Parity** | `python3 experiments/verify_nosih_claims.py` | `58/58` claims verified, `0` violations |
| **4. Hardware Probe** | `python3 experiments/run_hardware_validation.py` | Measures live host CPU / optional NVML + RAPL + Ollama |

---

## 4. Minimal Python Usage Example

```python
import asyncio
from nosih.kernel import ZeroTrustKernel

async def main():
    kernel = ZeroTrustKernel()
    result = await kernel.execute(
        query="Compute exact invoice total: (1450.25 * 1.18) - 120.00",
        tenant_id="acme_finance",
        origin="ERP",
    )
    print("Tier:", result["tier"], "| Stages:", result["stage_trace"])
    print("Answer:", result["output"], "| CO2 (g):", result["co2_g"])

asyncio.run(main())
```

---

## 5. Next Steps

- Explore the system design in [`ARCHITECTURE.md`](ARCHITECTURE.md)
- Inspect all empirical charts and tables in [`BENCHMARKS.md`](BENCHMARKS.md)
- Review the security model in [`SECURITY.md`](SECURITY.md)
- Read the 8-page manuscript in [`paper/nosih_paper.pdf`](paper/nosih_paper.pdf)
