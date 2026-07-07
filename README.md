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
> Run the following exact command to execute a headless hardware sprint targeting CPU, RAM, and GPU. Do *not* pipe `yes` into the command:
> ```bash
> TEST_RESULTS_IDENTIFIER=sprint TEST_RESULTS_NAME=sprint TEST_RESULTS_DESCRIPTION=sprint BATCH_MODE=1 phoronix-test-suite default-benchmark pts/sysbench pts/stream pts/vkmark
> ```
> 
> **Important:** Create a dedicated markdown file for each unique machine and operating system combination (e.g., `Intel_Core_i7-11800H_Ubuntu_26.04.md`). In this file, include the system's complete hardware information (CPU, GPU, RAM, OS version) and compile all of the benchmark results (both brief summaries and detailed test logs like EPP scaling or OpenVINO) for this specific machine. Ensure that the main `README.md` is also updated with brief metric summaries by category.

---

## 2. Benchmark Results by Category

### Memory Bandwidth (`pts/stream`)
*Critical metric dictating the absolute limit for Large Language Model token generation speeds. Measures memory copy bandwidth.*

| Device | APU/Graphics | Memory Bandwidth (Copy) |
| :--- | :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | RDNA3 iGPU | **58,150.2 MB/s** |
| **Intel Core i9-12900HK** | Alder Lake-P GT2 (Iris Xe) | **43,063.8 MB/s** |
| **Intel Core i7-11800H** | RTX 3070 Laptop (8GB) | **40,413.4 MB/s** |
| **Intel Core i3-1215U** | Alder Lake GT1 (UHD) | **37,550.9 MB/s** |
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
| **Intel Core i3-1215U** | **14,900.14** | **14,069.00 MiB/sec** |
| **Intel N100** | **8,436.38** | **9,320.09 MiB/sec** |
| **Steam Deck (Van Gogh)** | **7,142.15** | **12,251.50 MiB/sec** |
| **AMD Ryzen 7 2700U** | **5,787.14** | **722.55 MiB/sec** |
| **Apple Mac M3 (16GB)** | *N/A (macOS Unsupported)* | *N/A (macOS Unsupported)* |

### Vulkan Compute (`pts/vkmark`)
*Graphics and compute benchmark measuring the capabilities of the Vulkan rendering pipeline.*

| Device | VKMark (Mailbox) |
| :--- | :--- |
| **Intel Core i3-1215U** | **11,524** |
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
| **Apple Mac M3 (16GB)** | **2232 MB/s (571,333 IOPS)** | **2241 MB/s (573,667 IOPS)** |
| **Intel Core i7-11800H** (Samsung 990 PRO Gen4 x4) | **2201 MB/s (563,625 IOPS)** | **1137 MB/s (291,000 IOPS)** |
| **Intel Core i3-1215U** (Micron 3400 Gen4 x4) | **866 MB/s (221,733 IOPS)** | **519 MB/s (132,867 IOPS)** |
| **ASUS ROG Ally (Z1 Extreme)** | **738 MB/s (189,000 IOPS)** | **528 MB/s (135,000 IOPS)** |
| **AMD Ryzen 7 2700U** (Toshiba XG5 Gen3 x4) | **441 MB/s (112,750 IOPS)** | **288 MB/s (73,733 IOPS)** |
| **Intel Core i9-12900HK** | **417 MB/s (102,000 IOPS)** | **427 MB/s (104,000 IOPS)** |

### Sustained Multi-Core Compute (`pts/build-linux-kernel`)
*A brutal test of the system's thermal limits and sustained multi-thread performance compiling the Linux Kernel from source.*

> [!NOTE]
> **Kernel Configuration Notice**
> To avoid hours of unnecessary compile time, please ensure you only select and run the `defconfig` profile. Skip `allmodconfig`.

| Device | Build Time (defconfig) |
| :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | **218.37 Seconds** |
| **Steam Deck (Van Gogh)** | **380.48 Seconds** |
| **Intel Core i3-1215U** | **398.94 Seconds** |
| **AMD Ryzen 7 2700U** | **762.20 Seconds** |
| **Intel Core i7-11800H** | **191.88 Seconds** |

### Audio AI Processing & TTS (`pts/whisper-cpp` & `pts/espeak`)
*Real-world STT (Speech-to-Text) inference speed and Text-To-Speech synthesis executed on the CPU.*

> [!NOTE]
> **Audio Processing Configuration Notice**
> These benchmarks use a standard execution profile parsing fixed datasets (e.g., Gutenberg text). No interactive configuration is required.

| Device | Whisper Transcription Time | eSpeak Synthesis Time |
| :--- | :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | **206.08 Seconds** | **22.33 Seconds** |
| **Apple Mac M3 (16GB)** | *N/A (macOS Unsupported)* | **19.54 Seconds** |
| **Intel Core i9-12900HK** | **678.41 Seconds** | **45.22 Seconds** |
| **Intel Core i3-1215U** | **698.03 Seconds** | **53.20 Seconds** |
| **Steam Deck (Van Gogh)** | *N/A (Execution Failed)* | *N/A* |
| **Intel Core i7-11800H** | *N/A (Execution Failed)* | **25.13 Seconds** |
| **AMD Ryzen 7 2700U** | **1,215.74 Seconds** | **40.69 Seconds** |

### AI Inference (`pts/openvino`)
*Real-world AI model inferences across various topologies natively executed on the CPU using FP16 and INT8.*

> [!NOTE]
> **OpenVINO Configuration Notice**
> To avoid hours of unnecessary benchmarking, please ensure you only select and run the `Face Detection Retail` and `Vehicle Detection` topologies.

| Device | Face Detection FP16 (FPS) | Vehicle Detection FP16 (FPS) |
| :--- | :--- | :--- |
| **Steam Deck (Van Gogh)** | **0.43 FPS** | **42.71 FPS** |
| **Intel Core i7-11800H** | **546.00 FPS** | **127.84 FPS** |

### Pure Compute & Cryptography (`pts/hashcat` & `pts/compress-7zip`)
*Tests of raw mathematical throughput, integer math capabilities, and OpenCL compute speeds.*

| Device | Hashcat (MD5) | 7-Zip Compression | 7-Zip Decompression |
| :--- | :--- | :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | **5,887,600,000 H/s** | **65,413 MIPS** | **55,327 MIPS** |
| **Intel Core i9-12900HK** | *N/A (Missing OpenCL)* | **39,125 MIPS** | **21,025 MIPS** |
| **Apple Mac M3 (16GB)** | *N/A (macOS Unsupported)* | **64,897 MIPS** | **43,755 MIPS** |
| **AMD Ryzen 7 2700U** | *N/A (OpenCL Unsupported)* | **19,026 MIPS** | **15,615 MIPS** |
| **Intel Core i7-11800H** | *N/A (Execution Failed)* | **64,554 MIPS** | **62,711 MIPS** |

### Database Insertion Speed (`pts/sqlite`)
*Synthetic measurement of database insertion and transaction speeds.*

> [!NOTE]
> **SQLite Configuration Notice**
> Our standardized sprint tests database insertion speeds using two thread configurations:
> * **Threads:** 4 and 8

| Device | 4 Threads | 8 Threads |
| :--- | :--- | :--- |
| **Apple Mac M3 (16GB)** | **2.53 Seconds** | **4.29 Seconds** |
| **Intel Core i3-1215U** | **6.97 Seconds** | **8.62 Seconds** |
| **ASUS ROG Ally (Z1 Extreme)** | **23.33 Seconds** | **30.59 Seconds** |
| **Intel Core i7-11800H** | **85.83 Seconds** | **84.49 Seconds** |
| **Intel Core i9-12900HK** | **91.27 Seconds** | **90.55 Seconds** |

### Sustained Compilation (`pts/build-llvm`)
*A brutal test of the system's thermal limits and sustained multi-thread performance compiling the LLVM codebase from source.*

> [!NOTE]
> **LLVM Configuration Notice**
> This benchmark tests sustained compilation using the standard `Unix Makefiles` build system configuration.

| Device | Build Time (Unix Makefiles) |
| :--- | :--- |
| **Apple Mac M3 (16GB)** | **1071.325 Seconds** |
| **Intel Core i7-11800H** | **1202.723 Seconds** |
| **ASUS ROG Ally (Z1 Extreme)** | **1421.00 Seconds** |

### CPU Ray Tracing (`pts/c-ray`)
*A simple, multi-threaded raytracer testing floating-point CPU performance.*

> [!NOTE]
> **C-Ray Configuration Notice**
> Our standardized sprint tests floating-point throughput at three specific rendering scales:
> * **Resolutions:** 1080p, 4K, 5K
> * **Rays Per Pixel:** 16

| Device | 1080p | 4K | 5K |
| :--- | :--- | :--- | :--- |
| **Apple Mac M3 (16GB)** | **81.55 Seconds** | **323.51 Seconds** | **586.34 Seconds** |
| **Intel Core i7-11800H** | **100.82 Seconds** | **407.97 Seconds** | **726.93 Seconds** |
| **ASUS ROG Ally (Z1 Extreme)** | **112.37 Seconds** | **456.53 Seconds** | **812.30 Seconds** |
| **Intel Core i9-12900HK** | **152.96 Seconds** | **613.34 Seconds** | **1090.25 Seconds** |
| **Intel Core i3-1215U** | **320.18 Seconds** | **1285.04 Seconds** | **2285.50 Seconds** |
| **AMD Ryzen 7 2700U** | **350.92 Seconds** | *N/A* | *N/A* |

### Single-Thread PHP Scripting (`pts/phpbench`)
*A benchmark suite testing the raw execution speed of the PHP engine.*

> [!NOTE]
> **PHPBench Configuration Notice**
> This benchmark has a single default execution profile. No interactive configuration is required; it defaults to a standard script suite.

| Device | PHPBench Score |
| :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | **1,134,855 Score** |
| **Apple Mac M3 (16GB)** | **1,086,652 Score** |
| **Intel Core i7-11800H** | **1,058,417 Score** |
| **Intel Core i9-12900HK** | **573,371 Score** |
| **Intel Core i3-1215U** | **547,163 Score** |
| **AMD Ryzen 7 2700U** | **374,353 Score** |

### Developer Git Commands (`pts/git`)
*Real-world benchmark simulating developer operations by timing massive git repository commands.*

> [!NOTE]
> **Git Configuration Notice**
> This benchmark executes a fixed script of common Git commands (like `git gc` and `git diff`). No interactive configuration is required.

| Device | Time To Complete |
| :--- | :--- |
| **ASUS ROG Ally (Z1 Extreme)** | **30.54 Seconds** |
| **Apple Mac M3 (16GB)** | **35.35 Seconds** |
| **Intel Core i7-11800H** | **40.50 Seconds** |
| **AMD Ryzen 7 2700U** | **59.49 Seconds** |
| **Intel Core i3-1215U** | **82.69 Seconds** |
| **Intel Core i9-12900HK** | **83.23 Seconds** |
