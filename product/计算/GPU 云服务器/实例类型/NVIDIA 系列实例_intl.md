## Instance Overview
**NVIDIA Series GPU Instance GN?** is not only suitable for GPU general computing scenarios such as deep learning, scientific computing, but also for graphic/image processing (3D rendering, video encoding/decoding) scenarios. Tencent Cloud provides fast, stable and elastic computing services **managed in the same way as with standard CVM**.

>**Note:**
> Using the GN? Series instance for 3D graphics rendering (not supported by GN2) requires installing the GRID driver and configuring the license server.

## Use Cases
It is suitable for working scenarios where data throughput is large and calculation speed is demanding.
 - Deep learning;
 - Graphic/image processing;
 - Video encoding/decoding;
 - Graphic database;
 - High-performance database;
 - Computational fluid dynamics;
 - Computational finance;
 - Earthquake analysis;
 - Molecular modeling;
 - Genomics and others;

## Hardware Specification
The basic hardware specifications are as follows
![](https://main.qcloudimg.com/raw/375f1b8e54a52936f7ca72530d82c84b.png)
#### Specifications:
- GPU performance: The main indicator is GPU's floating-point computing performance. TF stands for T Flops, SP for single-precision floating-point computing, DP for double-precision floating-point computing, INT8 for INT8 integer computing, and DL for Deep Learning Tensor Core computing (V100 only).

- Storage/network: The storage list shows the storage types supported by the current instance; the network bandwidth refers to the network bandwidth of the physical server where an instance of this type is located. See the purchase page for the network bandwidth assigned by an instance of a certain type.

- Availability zone: Beijing 2 represents Beijing Zone 2, Shanghai 1 represents Shanghai Zone 1, and Guangzhou 3 represents Guangzhou Zone 3, and so on.

>**Note:**
>GN2 and GN8 provide SSD-based local storage. When instances are stored locally, their system and data disks only exist within the life cycle of the instance. When these instances expire or are terminated by you, the applications and data in the instance storage will be wiped out. We suggest that you back up or copy the data in the instance storage regularly.

## Service Options
- It can be launched in basic network and [VPC](/doc/product/213/5227).
- It can be interfaced with [Cloud Load Balance](/doc/product/214/524) and other Tencent Cloud products, without additional management and OPS costs. Private network traffic is free of charge.
