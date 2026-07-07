# Intel Core i3-1215U (Ubuntu 26.04)

## System Information
- **CPU**: Intel Core i3-1215U @ 4.40GHz (6 Cores / 8 Threads)
- **GPU**: ASUS Intel Alder Lake-UP3 GT1 [UHD]
- **RAM**: 16GB (2 x 8GB DDR4-3200MT/s)
- **OS**: Ubuntu 26.04
- **Kernel**: 7.1.3-070103-generic (x86_64)

## Benchmark Summaries

### Memory Bandwidth (`pts/stream`)
- **Copy**: 37,550.9 MB/s
- **Scale**: 25,419.8 MB/s
- **Triad**: 27,607.6 MB/s
- **Add**: 27,672.8 MB/s

### CPU & RAM Throughput (`pts/sysbench`)
- **Sysbench CPU**: 14,900.14 Events/Sec
- **Sysbench RAM**: 14,069.00 MiB/sec

### Vulkan Compute (`pts/vkmark`)
- **800x600 (Mailbox)**: 11,524

### Sustained Multi-Core Compute (`pts/build-linux-kernel`)
- **defconfig**: 398.940 Seconds

### Audio AI Processing (`pts/whisper-cpp`)
- **ggml-base.en**: 698.03 Seconds

## Detailed EPP Scaling Analysis

We conducted a deep dive into the `intel_pstate` EPP (Energy Performance Preference) subcategories on this machine to identify the CPU-to-iGPU power budgeting bottleneck.

| EPP State | Sysbench CPU (EPS) | Sysbench RAM (MiB/s) | Stream Copy (MB/s) | VKMark 1024x768 |
| :--- | :--- | :--- | :--- | :--- |
| **`performance`** | 14,902.99 | 13,976.41 | 37,830.7 | 10,058 |
| **`balance_performance`** | 14,900.83 | 14,014.93 | 37,712.8 | 10,026 |
| **`balance_power`** | 9,379.21 | 7,009.62 | 32,144.4 | 9,497 |
| **`power`** | 6,729.13 | 3,905.73 | 15,475.0 | 7,805 |

**Takeaway**: Dropping the EPP to `balance_power` or `power` does *not* increase Vulkan graphics scores. It actually slashes RAM throughput and starves the CPU, crippling both graphics and AI memory bandwidth. The ideal default is `balance_performance`.
