---
layout: home
title: Home
permalink: /
---

# CC-Bench: High-Performance Communication & Compression Benchmark

**CC-Bench** is a modular benchmark framework for **HPC** (High-Performance Computing) scenarios, supporting **MPI / NCCL / RCCL** communication backends. It leverages `LD_PRELOAD`-based instrumentation to decouple communication compression, performance profiling, and background monitoring.

## Key Features

- **Multi-backend support** — MPI, NCCL, RCCL communication backends
- **Compression plugins** — CCL and general compression algorithm plugins
- **LD_PRELOAD instrumentation** — Transparent wrapper-based profiling
- **Daemon monitoring** — Background resource monitoring during benchmarks
- **Configurable pipeline** — JSONC-based configuration with auto-generation

## Quick Start

```bash
# 1. Load environment modules
source scripts/configure_modules.sh

# 2. Configure and build
# Edit configs in userconfig/config_in_jsonc/ then:
bash scripts/build_script.sh

# 3. Run benchmarks
# Execute generated scripts (local / srun / sbatch)
```

## Pipeline

```
Config (userconfig/*.jsonc) → Build (build_script.sh) → Run → Results
```

---

**Check the [Leaderboard](/leaderboard/) for the latest benchmark results, or read the [Paper](/paper/) for technical details.**
