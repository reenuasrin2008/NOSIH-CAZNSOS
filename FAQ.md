# Frequently Asked Questions (Reviewers & Developers)

### 1. Why is NOSIH's latency standard deviation (`899.6 ms`) larger than its mean (`707.6 ms`)?
Heterogeneous neuro-symbolic routing is intentionally **multimodal**: `50.0%` of queries (`120/240`) resolve on host CPU in `1.8–3.5 ms` (`T0a_CACHE` / `T0b_SYMBOLIC`), while complex reasoning tasks run on `T3_LARGE` (`~2393.5 ms` mean, plus occasional `1.4 s` `DEEP_SLEEP` wakeups). That is why we report full quantiles alongside the mean: **Median / P50 = `169.8 ms`**, **P95 = `2549.2 ms`**, **P99 = `2878.7 ms`**.

### 2. Are the energy and latency numbers physically measured or simulated?
Both—and every metric is transparently tagged. Plane I cryptographic enforcement (`2.69 ms` mean), Merkle proof verification (`488.15 µs`), deterministic CPU symbolic/RAG tiers (`80` prompts), and async SQLite WAL concurrency (`C = 1..100`, `706.1 req/s` peak) are **physically executed and measured on host CPU**. Neural tier latency, accuracy, and GPU power (`160` prompts) use **calibrated model traces** in GPU-less CI containers, with [`experiments/run_hardware_validation.py`](experiments/run_hardware_validation.py) provided for live NVML/RAPL/Ollama runs.

### 3. Why is the Online Conformal PID post-shift error `5.30%` instead of strictly `≤ 5.00%`?
At finite horizon $T_{\text{post}} = 800$, integral lag contributes $+0.30\text{ pp}$ (bounded by $O(1/(\eta T))$ in Theorem 4). Extending to $T_{\text{post}} = 3000$ converges to **`5.07% ± 0.02%`**, and setting a conservative design target $\alpha_{\text{design}} = 0.045$ holds finite-window risk strictly below 5% at **`4.72% ± 0.09%`** (while static calibration diverges to `28.88%`).

### 4. Does `CCEC` protect against a root-compromised host falsifying GPU power readings?
No—and we state this explicitly in [`THREAT_MODEL.md`](THREAT_MODEL.md) and [`ETHICS_AND_IMPACT.md`](ETHICS_AND_IMPACT.md). `CCEC` + `MTLog` guarantees tamper-evident, Merkle-auditable Scope-2 records under the host TCB (`20/20` post-commit tampers caught, `20/20` unattested hardware spoofs rejected). Root-compromised host resistance requires hardware TEE attestation (Intel TDX / NVIDIA Confidential Computing).

### 5. Why use SQLite WAL for `jti` replay protection instead of Redis?
SQLite WAL provides zero-dependency, ACID-compliant, crash-safe single-node replay protection with zero external daemons—achieving `706.1 req/s` at `C = 50` and `0` lock errors across `161` concurrent requests while blocking `15/16` parallel replay-race threads. Distributed multi-node clusters can swap `AtomicJTIReplayStore` for a Raft/PostgreSQL backend.

### 6. How do I cite NOSIH in my paper?
Use GitHub's **"Cite this repository"** button (powered by [`CITATION.cff`](CITATION.cff)) or copy the BibTeX block in [`README.md`](README.md#9-citation-author--license).
