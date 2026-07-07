# ASUS ROG Ally (Z1 Extreme) - Bazzite 43

## System Hardware Information
* **Processor:** AMD Ryzen Z1 Extreme @ 5.13GHz (8 Cores / 16 Threads)
* **Graphics:** ASUS AMD Phoenix1 (RDNA3 iGPU)
* **Memory:** 16GB (4 x 4GB LPDDR5-6400MT/s Micron)
* **Storage:** 512GB Micron_2400_MTFDKBK512QFM NVMe
* **Motherboard:** ASUS ROG Ally RC71L_RC71L RC71L v1.0
* **Operating System:** Bazzite 43
* **Kernel:** 6.17.7-ba29.fc43.x86_64 (x86_64)

---

## Benchmark Results

### 1. General System Compute (Sysbench & Stream)
These benchmarks reflect the baseline synthetic compute capabilities.

| Metric | Result |
| :--- | :--- |
| **Sysbench CPU Compute** | 36,404.00 Events/sec |
| **Sysbench RAM Throughput** | 22,807.26 MiB/sec |
| **Stream Memory Bandwidth (Copy)** | 58,150.2 MB/s |
| **Vulkan Compute (VKMark)** | N/A (Headless Environment) |

---

### 2. Storage I/O Speeds (`pts/fio`)
Measurements of the internal NVMe storage limits (Random Read, IO_uring, 4KB, 1 Job).

| Direct | Buffered |
| :--- | :--- |
| **738 MB/s (189,000 IOPS)** | **528 MB/s (135,000 IOPS)** |

---

### 3. Sustained Multi-Core Compute (`pts/build-linux-kernel`)
A test of the system's thermal limits and sustained multi-thread performance compiling the Linux Kernel from source.

| Metric | Result |
| :--- | :--- |
| **Build Time (defconfig)** | 218.37 Seconds |

---

### 4. Audio AI Processing & TTS (`pts/whisper-cpp` & `pts/espeak`)
Speech-to-Text inference executed entirely on the CPU using the `ggml-base.en` architecture, alongside explicit Text-To-Speech synthesis.

| Metric | Result |
| :--- | :--- |
| **Whisper (2016 State of the Union)** | 206.08 Seconds |
| **eSpeak (Text-To-Speech Synthesis)** | 22.329 Seconds |

---

### 5. Pure Compute & Cryptography (`pts/hashcat` & `pts/compress-7zip`)
Tests of raw mathematical throughput and integer math capabilities.

| Metric | Result |
| :--- | :--- |
| **Hashcat (MD5)** | 5,887,600,000 H/s |
| **7-Zip Compression** | 65,413 MIPS |
| **7-Zip Decompression** | 55,327 MIPS |

---

### 6. Database Insertion Speed (`pts/sqlite`)
Synthetic measurement of database insertion and transaction speeds.

| Metric | Result |
| :--- | :--- |
| **4 Threads** | 23.33 Seconds |
| **8 Threads** | 30.59 Seconds |

---

### 7. Sustained Compilation (`pts/build-llvm`)
A brutal test of the system's thermal limits and sustained multi-thread performance compiling the LLVM codebase from source.

| Metric | Result |
| :--- | :--- |
| **Build Time (Unix Makefiles)** | 1421.00 Seconds |

---

### 8. CPU Ray Tracing (`pts/c-ray`)
A simple, multi-threaded raytracer testing floating-point CPU performance.

| Metric | Result |
| :--- | :--- |
| **1080p** | 112.37 Seconds |
| **4K** | 456.53 Seconds |
| **5K** | 812.30 Seconds |

---

### 9. Single-Thread PHP Scripting (`pts/phpbench`)
A benchmark suite testing the raw execution speed of the PHP engine.

| Metric | Result |
| :--- | :--- |
| **PHPBench Score** | 1,134,855 Score |

---

### 10. Developer Git Commands (`pts/git`)
Real-world benchmark simulating developer operations by timing massive git repository commands.

| Metric | Result |
| :--- | :--- |
| **Time To Complete** | 30.54 Seconds |
