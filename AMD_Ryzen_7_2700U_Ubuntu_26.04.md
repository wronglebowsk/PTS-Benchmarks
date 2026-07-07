# AMD Ryzen 7 2700U

## System Specifications
* **CPU:** AMD Ryzen 7 PRO 2700U (4 Cores / 8 Threads)
* **GPU:** Radeon Vega 10 Mobile Gfx
* **RAM:** 32GB
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
* **Random Read (Direct):** 441 MB/s (112,750 IOPS)
* **Random Read (Buffered):** 288 MB/s (73,733 IOPS)

### 5. Sustained Multi-Core Compute (`pts/build-linux-kernel`)
* **Build Time (defconfig):** 762.20 Seconds

### 6. Audio AI Processing (`pts/whisper-cpp`)
* **Transcription Time (2016 State of the Union):** 1,215.74 Seconds

### 7. AI Inference (`pts/openvino`)
* **Face Detection FP16 (Latency):** 0.32 FPS (3,098.42 ms)
* **Face Detection FP16 (Throughput):** 0.30 FPS (13,330.01 ms)

### 8. Pure Compute & Cryptography (`pts/compress-7zip` & `pts/hashcat`)
* **7-Zip Compression:** 19,026 MIPS
* **7-Zip Decompression:** 15,615 MIPS
* **Hashcat (MD5):** N/A (OpenCL Driver Unsupported)

### 9. Database Insertion Speed (`pts/sqlite`)
* **1 Thread:** 13.920 Seconds
