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
| **ASUS ROG Ally (Z1 Extreme)** | RDNA3 iGPU | **58,150.2 MB/s** | **22,807.26 MiB/sec** | **36,404 Events Per Sec** | **N/A (Headless)** |
| **Intel Core i9-12900HK** | Alder Lake-P GT2 (Iris Xe) | **43,063.8 MB/s** | **14,679.19 MiB/sec** | **34,428.88 Events Per Sec** | **N/A (Headless)** |
| **Intel Core i7-11800H** | RTX 3070 Laptop (8GB) | **40,413.4 MB/s** | **17,575.14 MiB/sec** | **25,796.01 Events Per Sec** | **N/A (Headless)** |
| **Steam Deck (Van Gogh)** | RDNA 2 APU | **32,110.5 MB/s** | **12,251.50 MiB/sec** | **7,142.15 Events Per Sec** | **N/A (Headless)** |
| **AMD Ryzen 7 2700U** | Vega 10 Mobile | **27,469 MB/s** | **722.55 MiB/sec** | **5,787.14 Events Per Sec** | **3,804** |

## 3. LLM Inference Cross-Device Results
*Tested using `llama.cpp` across varying contexts and backends. The following table showcases the peak Token Generation (TG) speed achieved on each architecture.*

### Llama 3.2 1B (Q4_0)
| Device | Best Backend | Prompt Processing | Token Generation |
| :--- | :--- | :--- | :--- |
| **Apple M3 (16GB)** | Metal (GPU) | 1,132.14 t/s | **102.37 t/s** |
| **ROG Ally (Z1 Extreme)** | Vulkan (GPU) | ~560.00 t/s | **~85.00 t/s** |
| **Steam Deck (Van Gogh)** | Vulkan (GPU) | ~350.00 t/s | **~65.00 t/s** |
| **AMD Ryzen 7 2700U** | Vulkan (GPU) | 263.75 t/s | **32.47 t/s** |
| **Intel Core i3-1215U** | OpenVINO | 711.52 t/s | **28.14 t/s** |

### Gemma 4 E2B (Q8_0)
| Device | Best Backend | Prompt Processing | Token Generation |
| :--- | :--- | :--- | :--- |
| **Apple M3 (16GB)** | Metal (GPU) | 194.29 t/s | **54.23 t/s** |
| **ROG Ally (Z1 Extreme)** | Vulkan (GPU) | *(Not Recorded)* | **~45.70 t/s** |
| **Steam Deck (Van Gogh)** | Vulkan (GPU) | 98.20 t/s | **27.38 t/s** |
| **AMD Ryzen 7 2700U** | Vulkan (GPU) | 133.00 t/s | **14.60 t/s** |
| **Intel Core i3-1215U** | Vulkan (GPU) | 64.75 t/s | **14.32 t/s** |

### Key Observations
* **Memory Bandwidth defines the APU:** The gaming handhelds (ROG Ally, Steam Deck) drastically outperform traditional laptops (Ryzen 2700U, Intel 1215U) in token generation due to their hyper-optimized LPDDR5 memory configurations. 
* **Speculative Decoding is unreliable on edge devices:** Multi-Token Prediction (MTP) draft evaluation typically introduces a compute bottleneck on laptops, severely reducing generation speed compared to standard vanilla execution.
