# Intel Core i9-12900HK (Ubuntu 26.04) Benchmark Results

## System Information
- **CPU:** Intel Core i9-12900HK (14 Cores, 20 Threads, Alder Lake)
- **iGPU:** Intel Alder Lake-P GT2 [Iris Xe]
- **RAM:** 64GB DDR4-3200MT/s (2x 32GB G.Skill F4-3200C22-32GRS)
- **Storage:** 1000GB Samsung SSD 990 PRO 1TB + 2000GB Samsung SSD 870
- **OS:** Ubuntu 26.04 (Kernel 7.1.3-070103-generic x86_64)

## Core Hardware Metrics (PTS Sprint)
*Measured using the `balance_performance` EPP hint under the `powersave` governor.*
- **Sysbench CPU:** 34,428.88 Events/sec
- **Sysbench RAM Throughput:** 14,679.19 MiB/sec
- **Stream Copy:** 43,063.8 MB/s
- **Stream Scale:** 34,486.9 MB/s
- **Stream Triad:** 35,915.2 MB/s
- **Stream Add:** 35,696.6 MB/s
- **VKMark:** N/A (Failed Headless)

## Audio AI Processing (Whisper.cpp)
*Input: 2016 State of the Union (~60m audio)*
- **ggml-base.en:** 678.41 Seconds (~11.3 minutes)
- **ggml-small.en:** 2,153.13 Seconds (~35.9 minutes)
- **ggml-medium.en:** 6,688.02 Seconds (~1 hour, 51.5 minutes)

## LLM Inference (llama.cpp)
*Llama 3.2 1B (Q4_0)*
- **CPU (Native):** Token Generation: ~46.60 t/s
- **Vulkan (iGPU):** Prompt Processing: ~300.00 t/s, Token Generation: ~35.10 t/s
- **OpenVINO (iGPU):** Prompt Processing: ~336.00 t/s, Token Generation: ~28.20 t/s

## EPP Thermal & Hardware Scaling Matrix (powersave governor)
| EPP Profile | Sysbench CPU (Events/sec) | Sysbench RAM (MiB/s) | Stream Copy (MB/s) | Stream Triad (MB/s) |
| :--- | :--- | :--- | :--- | :--- |
| **`balance_performance`** | **34,428.88** | **14,679.19** | **43,063.8** | **35,915.2** |
| **`performance`** | 34,373.12 | 14,571.06 | 42,401.7 | 35,410.7 |
| **`balance_power`** | 24,181.79 | ~14,600.00 | 42,143.1 | 35,935.9 |
| **`power`** | 14,699.56 | 4,886.59 | 21,937.9 | 18,578.3 |

## OpenVINO AI (Select Throughput Results)
*Completed 42 overall permutations.*
- **Age Gender Recognition Retail 0013 FP16:** 2,669.13 FPS
- **Age Gender Recognition Retail 0013 FP16-INT8:** 5,924.29 FPS
- **Person Re-Identification Retail FP16:** 132.93 FPS
- **Noise Suppression Poconet-Like FP16:** 151.00 FPS
- **Handwritten English Recognition FP16-INT8:** 51.14 FPS

## Sustained Multi-Core Compute (Kernel Compilation)
- **Build Time:** Failed to run (missing dependencies `bison` / `flex`).
