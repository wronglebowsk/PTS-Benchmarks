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

---

## 2. Benchmark Results by Category

### Memory Bandwidth (`pts/stream`)
*Critical metric dictating the absolute limit for Large Language Model token generation speeds. Measures memory copy bandwidth.*

| Device | APU/Graphics | Memory Bandwidth (Copy) |
| :--- | :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | RDNA3 iGPU | **58,150.2 MB/s** |
| **Intel Core i9-12900HK** | Alder Lake-P GT2 (Iris Xe) | **43,063.8 MB/s** |
| **Intel Core i7-11800H** | RTX 3070 Laptop (8GB) | **40,413.4 MB/s** |
| **Steam Deck (Van Gogh)** | RDNA 2 APU | **32,110.5 MB/s** |
| **AMD Ryzen 7 2700U** | Vega 10 Mobile | **27,469.0 MB/s** |
| **Intel N100** | Intel UHD Graphics | **20,018.9 MB/s** |
| **Apple Mac M3 (16GB)** | M3 10-Core GPU | *N/A (Clang OpenMP Unsupported)* |

### CPU & RAM Throughput (`pts/sysbench`)
*Synthetic measurement of raw multi-threaded CPU event processing and RAM system routing.*

| Device | Sysbench CPU (Events/Sec) | Sysbench RAM Throughput |
| :--- | :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | **36,404.00** | **22,807.26 MiB/sec** |
| **Intel Core i9-12900HK** | **34,428.88** | **14,679.19 MiB/sec** |
| **Intel Core i7-11800H** | **25,796.01** | **17,575.14 MiB/sec** |
| **Intel N100** | **8,436.38** | **9,320.09 MiB/sec** |
| **Steam Deck (Van Gogh)** | **7,142.15** | **12,251.50 MiB/sec** |
| **AMD Ryzen 7 2700U** | **5,787.14** | **722.55 MiB/sec** |
| **Apple Mac M3 (16GB)** | *N/A (macOS Unsupported)* | *N/A (macOS Unsupported)* |

### Vulkan Compute (`pts/vkmark`)
*Graphics and compute benchmark measuring the capabilities of the Vulkan rendering pipeline.*

| Device | VKMark (Mailbox) |
| :--- | :--- |
| **AMD Ryzen 7 2700U** | **3,804** |
| **ASUS ROG Ally (Z1 Extreme)** | *N/A (Headless)* |
| **Intel Core i9-12900HK** | *N/A (Headless)* |
| **Intel Core i7-11800H** | *N/A (Headless)* |
| **Steam Deck (Van Gogh)** | *N/A (Headless)* |
| **Intel N100** | *N/A (Headless)* |
| **Apple Mac M3 (16GB)** | *N/A (macOS Unsupported)* |

### Storage I/O Speeds (`pts/fio`)
*Measurements of the internal NVMe storage limits.*

> [!WARNING]
> **FIO Configuration Notice**
> If you run `pts/fio` interactively, be extremely careful not to select heavy sequential write benchmarks with massive job counts, as they can take days to complete on slower drives.
> Our standardized sprint uses the following configuration:
> * **Type:** Random Read
> * **Engine:** IO_uring
> * **Direct:** Yes / No (Both recorded)
> * **Block Size:** 4KB
> * **Job Count:** 1

| Device | FIO Random Read (Direct) | FIO Random Read (Buffered) |
| :--- | :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | **738 MB/s (189,000 IOPS)** | **528 MB/s (135,000 IOPS)** |
| **AMD Ryzen 7 2700U** | **441 MB/s (112,750 IOPS)** | **288 MB/s (73,733 IOPS)** |
| **Apple Mac M3 (16GB)** | **2232 MB/s (571,333 IOPS)** | **2241 MB/s (573,667 IOPS)** |

### Sustained Multi-Core Compute (`pts/build-linux-kernel`)
*A brutal test of the system's thermal limits and sustained multi-thread performance compiling the Linux Kernel from source.*

| Device | Build Time (defconfig) |
| :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | **218.37 Seconds** |
| **AMD Ryzen 7 2700U** | **762.20 Seconds** |

### Audio AI Processing (`pts/whisper-cpp`)
*Real-world STT (Speech-to-Text) inference speed executed entirely on the CPU using the `ggml-base.en` architecture.*

| Device | Input File | Transcription Time |
| :--- | :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | 2016 State of the Union (~60m) | **206.08 Seconds** |
| **AMD Ryzen 7 2700U** | 2016 State of the Union (~60m) | **1,215.74 Seconds** |

### Pure Compute & Cryptography (`pts/hashcat` & `pts/compress-7zip`)
*Tests of raw mathematical throughput, integer math capabilities, and OpenCL compute speeds.*

| Device | Hashcat (MD5) | 7-Zip Compression | 7-Zip Decompression |
| :--- | :--- | :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | **5,887,600,000 H/s** | **65,413 MIPS** | **55,327 MIPS** |
| **Apple Mac M3 (16GB)** | *N/A (macOS Unsupported)* | **64,897 MIPS** | **43,755 MIPS** |

### Database Insertion Speed (`pts/sqlite`)
*Synthetic measurement of database insertion and transaction speeds.*

| Device | 4 Threads | 8 Threads |
| :--- | :--- | :--- |
| **Apple Mac M3 (16GB)** | **2.53 Seconds** | **4.29 Seconds** |

### Sustained Compilation (`pts/build-llvm`)
*A brutal test of the system's thermal limits and sustained multi-thread performance compiling the LLVM codebase from source.*

| Device | Build Time (Unix Makefiles) |
| :--- | :--- |
| **Apple Mac M3 (16GB)** | **1071.325 Seconds** |
