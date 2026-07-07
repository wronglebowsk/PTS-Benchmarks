# AMD Ryzen 7 2700U

## System Specifications
* **CPU:** AMD Ryzen 7 PRO 2700U (4 Cores / 8 Threads)
* **GPU:** Radeon Vega 10 Mobile Gfx
* **RAM:** 32GB
* **Storage:** Toshiba XG5 512GB NVMe (KXG50ZNV512G) connected via PCIe 3.0 x4 (8GT/s)
* **OS:** Ubuntu 26.04 LTS

## Benchmark Results

### 1. Memory Bandwidth (`pts/stream`)
* **Copy Bandwidth:** 27,469.0 MB/s

### 2. CPU & RAM Throughput (`pts/sysbench`)
* **CPU:** 5,787.14 Events/Sec
* **RAM:** 722.55 MiB/sec

### 3. Vulkan Compute (`pts/vkmark`)
* **Score (Mailbox):** 3,804

### 4. Storage I/O (`pts/fio`)
*Note: The Toshiba XG5 NVMe is connected via a full PCIe 3.0 x4 link, yet performance is severely capped, pointing to heavy drive wear, OEM firmware degradation, or CPU overhead.*
* **Random Read (Direct):** 441 MB/s (112,750 IOPS)
* **Random Read (Buffered):** 288 MB/s (73,733 IOPS)

### 5. Sustained Multi-Core Compute (`pts/build-linux-kernel`)
* **Build Time (defconfig):** 762.20 Seconds

### 6. Audio Processing & TTS (`pts/whisper-cpp` & `pts/espeak`)
* **Transcription Time (Whisper):** 1,215.74 Seconds
* **Synthesis Time (eSpeak):** 40.69 Seconds

### 7. AI Inference (`pts/openvino`)
* **Face Detection FP16 (Latency):** 0.32 FPS (3,098.42 ms)
* **Face Detection FP16 (Throughput):** 0.30 FPS (13,330.01 ms)

### 8. Pure Compute & Cryptography (`pts/compress-7zip` & `pts/hashcat`)
* **7-Zip Compression:** 19,026 MIPS
* **7-Zip Decompression:** 15,615 MIPS
* **Hashcat (MD5):** N/A (OpenCL Driver Unsupported)

### 9. Database Insertion Speed (`pts/sqlite`)
* **1 Thread:** 13.920 Seconds

### 10. CPU Ray Tracing (`pts/c-ray`)
* **1080p (16 Rays):** 350.92 Seconds

### 11. Single-Thread PHP Scripting (`pts/phpbench`)
* **PHPBench Score:** 374,353

### 12. Developer Git Commands (`pts/git`)
* **Time To Complete:** 59.49 Seconds
