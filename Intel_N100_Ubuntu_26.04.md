# Intel N100 (Ubuntu 26.04)

## Hardware Specifications
- **Processor:** Intel N100 @ 3.40GHz (4 Cores)
- **Memory:** 16GB (4 x 4GB LPDDR5-3200MT/s Micron)
- **Graphics:** Intel Alder Lake-N [UHD]
- **OS:** Ubuntu 26.04
- **Kernel:** 7.1.3-070103-generic (x86_64)

## Core Benchmarks (Sysbench & Stream)

| Metric | Score |
| --- | --- |
| **Stream (Memory Bandwidth - Copy)** | 20,018.9 MB/s |
| **Sysbench (RAM Throughput)** | 9,320.09 MiB/sec |
| **Sysbench (CPU Events/Sec)** | 8,436.38 |

## Energy Performance Preference (EPP) Scaling

| EPP Subcategory | Stream Memory (Copy) | Sysbench RAM | Sysbench CPU |
| :--- | :--- | :--- | :--- |
| **`performance`** | 19,594.2 MB/s | 9,244.25 MiB/sec | 8,632.25 Events/Sec |
| **`balance_performance`** | 19,706.8 MB/s | 9,167.55 MiB/sec | 8,645.61 Events/Sec |
| **`balance_power`** | 18,242.8 MB/s | 7,271.13 MiB/sec | 6,762.43 Events/Sec |
| **`power`** | 8,137.5 MB/s | 3,336.52 MiB/sec | 3,334.48 Events/Sec |

## Sustained Multi-Core Compute (Linux Kernel)

| Metric | Score |
| --- | --- |
| **Build Time (defconfig)** | 2,795.50 Seconds |

## Audio AI Processing (Whisper.cpp)

| Metric | Score |
| --- | --- |
| **Transcription Time (ggml-base.en)** | 4,914.43 Seconds |
