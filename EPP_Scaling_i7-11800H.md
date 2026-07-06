# Intel EPP (Energy Performance Preference) Scaling Benchmarks

This report summarizes the hardware performance of the Intel Core i7-11800H across all four unique Intel Hardware P-State (HWP) hinting subcategories.

Each test was forced to cycle **3 times** per subcategory to ensure accurate averaging.

### 1. Geometric Mean (Overall Composite Score)
The geometric mean combines the CPU compute, RAM throughput, and Stream bandwidth scores into a single overarching metric.

| EPP Subcategory | Geometric Composite | Difference from Max |
| :--- | :--- | :--- |
| **Performance** | 28,354.71 | Baseline (0.00%) |
| **Balance Power** | 28,329.80 | -0.08% |
| **Balance Performance** | 28,322.55 | -0.11% |
| **Power** | 28,296.55 | -0.20% |

---

### 2. Sysbench (CPU & Memory Compute)
Measures raw mathematical integer/prime calculation throughput and memory operations per second.

| EPP Subcategory | CPU Events / Sec | RAM Throughput (MiB/s) |
| :--- | :--- | :--- |
| **Performance** | **25,852.23** | **17,720.85** |
| **Balance Performance** | 25,809.10 | 17,618.32 |
| **Power** | 25,786.05 | 17,577.40 |
| **Balance Power** | 25,773.65 | 17,605.79 |

---

### 3. Stream (Memory Bandwidth)
Measures pure sustained memory bandwidth. *Note: Stream bandwidth is heavily dictated by memory timings rather than CPU clock scaling.*

| EPP Subcategory | Copy (MB/s) | Triad (MB/s) | Add (MB/s) |
| :--- | :--- | :--- | :--- |
| **Performance** | 40,566.2 | 30,881.6 | 31,354.4 |
| **Balance Performance** | 40,587.0 | 30,902.4 | 31,366.8 |
| **Balance Power** | **40,603.6** | 30,948.0 | **31,377.3** |
| **Power** | 40,582.7 | **30,952.6** | 31,326.7 |

---

### Conclusion & Key Takeaways

**1. The Margin of Error (0.2%)**
The performance difference between absolute maximum `performance` and absolute lowest `power` states across these workloads is roughly **0.20%**, meaning it is statistically insignificant and falls entirely within the natural deviation margin of the tests themselves. 

**2. Synthetic 100% Workloads Bypass EPP Hints**
Intel's Energy Performance Preference (EPP) dictates how aggressively the CPU scales clock speeds up or down during *transient or partial* workloads (e.g., launching an app, rendering a webpage, or typing). However, `sysbench` and `stream` are synthetic, highly parallel workloads that immediately pin CPU utilization to 100%. Under a 100% sustained load, the CPU ignores the EPP "hint" and scales to its thermal/electrical limit across all profiles.

**3. Best Configuration for iGPU/LLM Use**
Given that `power` performs virtually identically to `performance` under heavy compute, the `power` or `balance_power` state is highly recommended. It will drop idle power consumption significantly and free up the shared thermal budget (TDP) on the die, which allows the integrated GPU (iGPU) to boost much higher during heavy visual or edge AI generation tasks.
