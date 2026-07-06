# Intel Core i7-11800H - OpenVINO AI Framework Results

These benchmarks were captured using `pts/openvino` on an Intel Core i7-11800H (8 Cores / 16 Threads) with 64GB of DDR4-3200 memory, using the CPU for AVX-512 VNNI accelerated inference.

## Highlighted Neural Network Topologies

| Model / Topology | Precision | Mode | Result |
| :--- | :--- | :--- | :--- |
| **Face Detection Retail** | FP16 | Throughput | **~546 FPS** |
| **Person Re-Identification Retail** | FP16 | Throughput | **~329 FPS** |
| **Machine Translation (EN to DE)** | FP16 | Latency | **~43.6 ms** |
| **Age/Gender Recognition Retail 0013** | FP16-INT8 | Throughput | **~13,683 FPS** |

*Note: The comprehensive test suite covered 45 different topology and latency/throughput permutations, but these standouts demonstrate the robust edge-AI capabilities of the Tiger Lake architecture when leveraging Intel's native OpenVINO frameworks over standard unoptimized execution.*
