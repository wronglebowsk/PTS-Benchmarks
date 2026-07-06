# Intel Core i7-11800H - Ubuntu 26.04

## System Hardware Information
* **Processor:** Intel Core i7-11800H (8 Cores / 16 Threads, 4.60GHz Max Boost, 24MB Cache)
* **Graphics:** NVIDIA GeForce RTX 3070 Laptop GPU (8GB VRAM) & Intel UHD Graphics (Tiger Lake-H)
* **Memory:** 64GB DDR4-3200MT/s Dual-Channel
* **Storage:** 2TB Samsung SSD 990 PRO (PCIe 4.0 NVMe)
* **Motherboard:** HP OMEN by Laptop 16-b0xxx
* **Operating System:** Ubuntu 26.04 (Resolute Raccoon)
* **Kernel:** 7.1.2-070102-generic (x86_64)

---

## Benchmark Results

### 1. General System Compute (Sysbench & Stream)
These benchmarks reflect the baseline synthetic compute capabilities.

| Metric | Result |
| :--- | :--- |
| **Sysbench CPU Compute** | 25,796.01 Events/sec |
| **Sysbench RAM Throughput** | 17,575.14 MiB/sec |
| **Stream Memory Bandwidth (Copy)** | 40,413.4 MB/s |
| **Vulkan Compute (VKMark)** | N/A (Headless Environment) |

---

### 2. Intel Energy Performance Preference (EPP) Scaling
Testing how the hardware scaling hint (EPP) affects heavy, sustained multi-core workloads. Tests were cycled 3 times each across `pts/sysbench` and `pts/stream` for each state.

**Finding:** The EPP subcategory essentially does not matter for heavy, sustained 100% compute workloads like LLM inference or synthetic benchmarking. The difference between absolute maximum `performance` and absolute lowest `power` states was a negligible ~0.20%, falling within standard testing deviation. Under 100% load, the CPU bypasses efficiency hints and scales to absolute thermal limits.

| EPP Subcategory | Geometric Composite | Sysbench CPU (Events/s) | Stream Copy (MB/s) |
| :--- | :--- | :--- | :--- |
| **Performance** | 28,354.71 (Base) | 25,852.23 | 40,566.2 |
| **Balance Power** | 28,329.80 (-0.08%) | 25,773.65 | 40,603.6 |
| **Balance Performance**| 28,322.55 (-0.11%) | 25,809.10 | 40,587.0 |
| **Power** | 28,296.55 (-0.20%) | 25,786.05 | 40,582.7 |

---

### 3. OpenVINO AI Framework Inference
Extensive AI capability testing using Intel's native OpenVINO frameworks (`pts/openvino`). The i7-11800H leverages AVX-512 VNNI instructions to dramatically accelerate inference without offloading to a dedicated GPU.

| Model / Topology | Precision | Benchmark Mode | Result |
| :--- | :--- | :--- | :--- |
| **Face Detection Retail** | FP16 | Throughput | ~546 FPS |
| **Person Re-Identification Retail** | FP16 | Throughput | ~329 FPS |
| **Machine Translation (EN to DE)** | FP16 | Latency | ~43.6 ms |
| **Age/Gender Recognition Retail 0013** | FP16-INT8 | Throughput | ~13,683 FPS |
