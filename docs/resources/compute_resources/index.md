# Compute Resources

## General Description

The **Argon High Performance Computing (HPC) system** at the University of Iowa was deployed in **February 2017**. It features a diverse set of compute node configurations, offering flexibility for a wide range of computational workloads.

## Compute Node Configurations

- **40-core**: 96GB, 192GB  
- **64-core**: 192GB, 384GB, 768GB  
- **80-core**: 96GB, 192GB, 384GB, 768GB, 1.5TB  
- **112-core**: 256GB, 512GB, 1TB, 1.5TB  
- **128-core**: 256GB, 512GB, 1TB, 1.5TB  

## GPU Accelerators

Argon includes a wide variety of GPU-equipped machines to support accelerated computing:

- 21 × Nvidia P100  
- 2 × Nvidia K80  
- 2 × Nvidia P40  
- 17 × Nvidia 1080Ti  
- 19 × Nvidia Titan V  
- 14 × Nvidia V100  
- 38 × Nvidia 2080Ti  
- 1 × Nvidia RTX8000  
- 7 × Nvidia A100  
- 5 × machines with 4 × A40 each  
- 2 × machines with 4 × L40S each  
- 1 × machine with 4 × L4  

## Data Center Locations

The Argon cluster is distributed across two data centers:

- **ITF** – *Information Technology Facility*  
- **LC** – *Lindquist Center*

Most nodes in the **LC data center** are connected via **OmniPath** high-speed interconnect fabric. Nodes in the **ITF data center** utilize **Mellanox InfiniBand EDR** fabric, which is split into two separate, non-interconnected fabrics—referred to as **islands**.

---

## Heterogeneity

Unlike previous HPC systems at the University of Iowa, which were largely homogeneous, <mark> **Argon is a heterogeneous cluster** with a wide mix of compute node types. This includes variability in both **GPU accelerators** and **CPU architectures**.</mark>

## CPU Architecture and AVX Capabilities

Argon nodes feature processors with varying **Advanced Vector Extensions (AVX)** capabilities, which significantly impact performance and compatibility.

| Architecture           | AVX Level | Floating Point Ops/Cycle | Notes                                      |
|------------------------|-----------|---------------------------|--------------------------------------------|
| Haswell / Broadwell    | AVX2      | 16                        |                                            |
| Skylake Silver         | AVX512    | 16                        | 1 AVX unit per core                        |
| Skylake Gold           | AVX512    | 32                        | 2 AVX units per core                       |
| Cascadelake Gold       | AVX512    | 32                        |                                            |
| Sapphire Rapids Gold   | AVX512    | —                         |                                            |

!!! info "Code must be compiled with appropriate optimization flags to utilize AVX instructions."
    - **AVX512-optimized code** will not run on Haswell/Broadwell systems (AVX2 only).  
    - **Backward compatibility** is maintained: AVX2-optimized code will run on Skylake and newer architectures.



