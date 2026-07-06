# Universal Hardware Benchmarks (PTS-Benchmarks)

This repository documents the testing methodology and accumulated results for comparing raw hardware metrics across various mobile architectures (Apple Silicon, Intel x86_64, AMD APUs) exclusively using the Phoronix Test Suite (PTS).

## 1. Automated Hardware Benchmark Methodology
To accurately compare raw CPU and memory capabilities across different operating systems without encountering interactive prompt deadlocks, we use a universal headless execution directive for the Phoronix Test Suite.

### Agent Directive
If you are instructing an AI agent to run this benchmark on a new device, provide it with the following block:

> **CRITICAL INSTRUCTION:** Identify your OS and use your native package manager (`apt`, `dnf`, `brew`) to install PHP (`php-cli`, `php-xml`, `php-sqlite3`), C++ build essentials (`git`, `build-essential`, `pkg-config`), and Vulkan development headers. 
> 
> Clone `https://github.com/phoronix-test-suite/phoronix-test-suite.git` and install it.
> 
> Finally, run the following exact command to execute a headless hardware sprint targeting CPU, RAM, and GPU. Do *not* pipe `yes` into the command:
> ```bash
> TEST_RESULTS_IDENTIFIER=sprint TEST_RESULTS_NAME=sprint TEST_RESULTS_DESCRIPTION=sprint BATCH_MODE=1 phoronix-test-suite default-benchmark pts/sysbench pts/stream pts/vkmark
> ```

## 2. Accumulated Hardware Metrics (PTS Sprint)
*These results reflect raw CPU and Memory bounds measured via `sysbench` and `stream`.*

| Device | APU/Graphics | Memory Bandwidth (Copy) | Sysbench RAM Throughput | Sysbench CPU | VKMark (Mailbox) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Intel Core i9-12900HK** | Alder Lake-P GT2 (Iris Xe) | **43,063.8 MB/s** | **14,679.19 MiB/sec** | **34,428.88 Events Per Sec** | **N/A (Headless)** |
| **AMD Ryzen 7 2700U** | Vega 10 Mobile | **27,469 MB/s** | **722.55 MiB/sec** | **5,787.14 Events Per Sec** | **3,804** |
