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

### 2. Storage I/O Speeds (`pts/fio`)
Measurements of the internal NVMe storage limits using Random Read, IO_uring, 4KB Block Size.

| Direct I/O | Result |
| :--- | :--- |
| **Yes** | 2201 MB/s (563,625 IOPS) |
| **No (Buffered)** | 1137 MB/s (291,000 IOPS) |

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
| **Vehicle Detection** | FP16 | Throughput | ~127.84 FPS |

---

### 4. Database Insertion Speed (`pts/sqlite`)
Synthetic measurement of database insertion and transaction speeds across varying thread counts.

| Threads | Time (Seconds) |
| :--- | :--- |
| **1 Thread** | 46.09s |
| **2 Threads** | 84.96s |
| **4 Threads** | 85.84s |
| **8 Threads** | 84.49s |
| **16 Threads** | 85.20s |

---

### 5. Sustained Compilation (`pts/build-linux-kernel` & `pts/build-llvm`)
A test of the system's sustained multi-thread performance compiling the Linux Kernel (defconfig) and LLVM codebase from source.

| Build System | Time (Seconds) |
| :--- | :--- |
| **Linux Kernel (defconfig)** | 191.87s |
| **LLVM (Ninja)** | 1,172.86s |
| **LLVM (Unix Makefiles)** | 1,202.72s |

---

### 6. Pure Compute & Cryptography (`pts/hashcat` & `pts/compress-7zip`)
Tests of raw mathematical throughput and integer math capabilities. *(Note: Hashcat execution failed due to a missing OpenCL runtime).*

| Metric | Result |
| :--- | :--- |
| **7-Zip Compression** | 64,554 MIPS |
| **7-Zip Decompression** | 62,711 MIPS |
| **Hashcat (MD5)** | N/A (Execution Failed) |

---

### 7. CPU Ray Tracing (`pts/c-ray`)
A simple, multi-threaded raytracer testing floating-point CPU performance at 16 Rays Per Pixel.

| Resolution | Time (Seconds) |
| :--- | :--- |
| **1080p** | 100.82s |
| **4K** | 407.97s |
| **5K** | 726.93s |

---

### 8. Single-Thread PHP Scripting (`pts/phpbench`)
A benchmark suite testing the raw execution speed of the PHP engine.

| Metric | Result |
| :--- | :--- |
| **PHPBench Score** | 1,058,417 Score |

---

### 9. Developer Git Commands (`pts/git`)
Real-world benchmark simulating developer operations by timing massive git repository commands.

| Metric | Time (Seconds) |
| :--- | :--- |
| **Time To Complete** | 40.50s |

---

### 10. Audio AI Processing & TTS (`pts/whisper-cpp` & `pts/espeak`)
Real-world STT (Speech-to-Text) inference speed and Text-To-Speech synthesis executed on the CPU.

| Metric | Time (Seconds) |
| :--- | :--- |
| **Whisper Transcription** | N/A (Execution Failed) |
| **eSpeak Synthesis** | 25.13s |
