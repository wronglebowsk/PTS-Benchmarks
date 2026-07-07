# Steam Deck (Van Gogh) - Ubuntu 22.04 LTS

## System Information

* **PROCESSOR:** AMD Custom APU 0405 @ 3.50GHz (4 Cores / 8 Threads, Zen 2)
* **GRAPHICS:** amdgpudrmfb (RDNA 2 APU, Frequency: 1600/687MHz)
* **MEMORY:** 16GB
* **DISK:** 512GB KINGSTON OM3PDP3512B-A01 + 513GB FF8S9
* **OPERATING SYSTEM:** Ubuntu 22.04.5 LTS (Running via Distrobox on SteamOS)
* **Kernel:** 6.16.12-drmexec7-valve24-1-neptune-616-drm-exec-gc61bd77b674c (x86_64)

## Benchmark Results

### pts/stream (Memory Bandwidth)
* **Copy:** 32,110.5 MB/s
* **Scale:** 21,374.0 MB/s
* **Add:** 24,198.5 MB/s
* **Triad:** 24,082.2 MB/s

### pts/sysbench (CPU & RAM)
* **CPU (Events/Sec):** 7,142.15
* **RAM Throughput:** 12,251.50 MiB/sec

### pts/vkmark (Vulkan Compute)
* **Status:** N/A (Headless Container Execution Unsupported)

### pts/fio (Storage I/O)
* **Random Read (4KB Block Size, 1 Job, IO_uring Engine, Direct):** 376 MB/s
* **Random Read IOPS (4KB Block Size, 1 Job, IO_uring Engine, Direct):** 96,273 IOPS

### pts/build-linux-kernel (Sustained Compilation)
* **Build (defconfig):** 380.48 Seconds

### pts/openvino (AI Inference)
* **Face Detection FP16:** 0.43 FPS (9156.03 ms)
* **Person Detection FP32:** 4.26 FPS (935.88 ms)
* **Vehicle Detection FP16:** 42.71 FPS (93.52 ms)
* **Handwritten English Recognition FP16:** 16.01 FPS (249.44 ms)

### pts/whisper-cpp (Audio AI)
* **Status:** Failed to execute (E: error: no input files specified)

### pts/phpbench (PHP Benchmark Suite)
* **Score:** 586,677

### pts/git (Time To Complete Common Git Commands)
* **Time:** 66.185 Seconds

### pts/sqlite (SQLite Database)
* **Threads / Copies 4:** 38.939 Seconds
* **Threads / Copies 8:** 39.868 Seconds

### pts/c-ray (Ray Tracing)
* **1080p - Rays Per Pixel: 16:** 244.157 Seconds
* **4K - Rays Per Pixel: 16:** 975.029 Seconds
* **5K - Rays Per Pixel: 16:** 1731.532 Seconds

### pts/build-llvm (Timed LLVM Compilation)
* **Build System: Unix Makefiles:** 3283.867 Seconds
