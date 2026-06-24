---
layout: page
title: About
permalink: /about/
---

## CC-Bench

CC-Bench is a benchmark framework developed by the **HPDPS Group** for evaluating high-performance communication and compression in HPC environments.

### Research Background

Modern HPC and distributed training workloads increasingly rely on efficient communication. As model sizes grow and cluster scales expand, the cost of communication (AllReduce, AllGather, etc.) becomes a dominant factor. CC-Bench provides a systematic way to:

1. Measure raw communication performance across different backends
2. Evaluate the impact of compression techniques on communication
3. Profile system-level resource usage during benchmark runs
4. Provide reproducible and standardized benchmark results

### Architecture

CC-Bench uses an LD_PRELOAD-based wrapping approach to intercept communication calls, allowing transparent profiling without modifying application code. The framework includes:

- **Wrappers** — Intercept MPI/NCCL/RCCL calls for profiling
- **Daemons** — Background monitoring of CPU, memory, and network
- **Plugins** — Extensible compression algorithms (CCL, etc.)
- **Job/Device Mapper** — Map benchmark jobs to hardware topology

### Publication

*[Link to paper — add your publication details here]*
