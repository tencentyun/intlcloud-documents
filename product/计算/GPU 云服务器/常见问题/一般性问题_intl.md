**Q: What is NVIDIA Tesla?**
A: NVIDIA Tesla is a new product line introduced by NVIDIA following the launch of professional acceleration card QUADRO and entertainment graphics card GeForce series, which is mainly used for scientific research that requires high performance computing. With NVIDIA® Tesla® GPU accelerator, it can accelerate your most demanding HPC and hyperscale data center workloads.

**Q: What is computing acceleration?**
A: Computing acceleration uses hardware accelerators or co-processors to perform floating point number calculations and graphics processing, which is more efficient than using software running on CPUs. Tencent Cloud offers three computing acceleration models: GPU computing GN2 and GN8 for generic computing, and GPU rendering GA2 for graphics-intensive applications.

**Q: What are the advantages of GPU over CPU?**
A: GPU has more arithmetic logic units (ALU) than CPU and supports large-scale multi-threaded parallel computing.

**Q: When should I use GPU instances?**
A: GPU instances are most suitable for highly parallel applications, such as workloads that use thousands of threads. When massive computations are required for graphics processing where each task is relatively small, a group of operations to be performed form a pipeline. The throughput of this pipeline is more important than the latency of a single operation. To build an application that makes full use of this parallelism, you need to master the expertise of GPU devices, and learn how to program for various graphical APIs (DirectX, OpenGL) or GPU computing programming models (CUDA, OpenCL).

**Q: How is GCC billed?**
A: Fees are calculated per second and settled per hour, and the resources are released whenever you purchase the service. This method is applicable to scenarios where the demand for devices fluctuates dramatically, such as snap-up campaign on an e-commerce site. For more information, see [Price Overview](https://cloud.tencent.com/doc/product/560/8025).

**Q: Can I upgrade/degrade GPU instance specification?**
A: No. Specifications of GPU instances cannot be changed.

**Q: What is local SSD?**
A: Local SSD is a local storage on the physical device where the CVM resides. It provides instances with block-level data access capability with a low latency, high random IOPS, and high I/O throughput. 

**Q: Can GPU instances access CVMs?**
A: Yes. GPU instances have private IPs and public IPs, so they can communicate with other Tencent Cloud products such as CVMs.

