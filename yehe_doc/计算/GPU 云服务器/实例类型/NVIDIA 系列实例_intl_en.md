## Overview

GPU Cloud Computing (GCC) **NVIDIA GPU Instance GN**\* is designed for general GPU computing tasks such as deep learning and scientific computing. It also excels at graphic processing tasks such as 3D rendering and video encoding and decoding. GCC is a fast, stable, and elastic computing service and you manage NVIDIA GPU instances the same way you manage **[CVM instnaces](https://intl.cloud.tencent.com/product/cvm)**.

> To use GN\* Series instances for 3D rendering (GN2 does not support 3D rendering), you need to install the GRID Driver and configure a License Server.

## Use Cases
Suitable for tasks that have high data throughput and demands high performance, such as:
- Deep learning
- Graphic and image processing
- Video encoding and decoding
- Graph database
- High-performance database
- Computational fluid dynamics
- Computational finance
- Seismic analysis
- Molecular modeling
- Genomics and others

#### Specification

- **GPU performance**: the main metric is GPU’s floating-point computing performance. TF stands for T Flops; SP for single-precision floating-point computing; DP for double-precision floating-point computing; INT8 for INT8 integer computing; and DL for accelerated deep learning using Tensor Core (V100 only).
- **Storage/network**: the storage list shows the storage classes supported by the current instance (Enhanced SSD Cloud Storage is now in beta); network bandwidth refers to the network bandwidth of the physical server where an NVIDIA GPU instance resides. See the purchase page for the network bandwidth assigned by an instance of a certain type.
- **vGPU**: GN10X and GN7 instance clusters supports vGPU. The type of vGPU is vComputeServer, which only supports CUDA computing API and does not support graphical APIs such as DirectX and OpenGL.
- **Availability zone**: Beijing 4 represents Beijing Zone 4, Singapore 1 represents Singapore Zone 1, and so on.
> GN2 and GN8 instances provide storage based on SSD local disks. The storage of GN2 instances only allows for fixed-capacity SSD local disks by default. For more information, see the purchase page. When using local storage, the system disk and data disk of these instances only exist during the instance lifecycle. When the instance expires or you terminate the instance, the apps and data in its instance storage are erased. We recommend that you back up the data stored in the instance storage on a regular basis.

## Pick an Instance Types
Tencent Cloud provides a wide variety of GPU computing instances for different use cases. For information on how to select the right computing instances for your needs, refer to [Selection of Instance Types](https://cloud.tencent.com/document/product/560/30130).

## Service Options
- [Pay-as-you-go](https://intl.cloud.tencent.com/document/product/213/2180)
- NVIDIA GPU instances can be launched in [VPC](https://intl.cloud.tencent.com/document/product/213/5227).
- NVIDIA GPU instances support services such as [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524), without additional management and OPS costs. Private network traffic is free of charge.
