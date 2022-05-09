**GPU Computing instances** provide powerful computing capabilities to help you process a large number of concurrent computing tasks in real time. They are suitable for general computing scenarios such as deep learning and scientific computing. They provide a fast, stable, and elastic computing service and can be **managed just like [CVM](https://intl.cloud.tencent.com/products/cvm) instances**.


## Use Cases
High-performance graphics processing and 3D rendering, such as:
- AI computing
 - Deep learning inference
 - Deep learning training
- Scientific computing/HPC
 - Fluid dynamics
 - Molecular modeling
 - Meteorological engineering
 - Seismic analysis
 - Genomics


## Overview

**GPU Computing instances are available in the following types:**

<table>
  <thead>
	<tr>
	  <th width="8%">Availability</th>
	  <th width="3%">Instance</th>
	  <th width="20%">GPU Type</th>
	  <th width="34%">Available Image</th>
	  <th width="35%">AZ</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td rowspan="5">Featured</td>
	  <td>
		<a href="#PNV4">PNV4</a>
	  </td>
	  <td>NVIDIA A10</td>
	  <td rowspan="2">
		<ul class="params">
		  <li>CentOS 7.2 or later</li>
		  <li>Ubuntu 16.04 or later</li>
		  <li>Windows Server 2016 or later</li>
		</ul>
	  </td>
	  <td rowspan="2">Guangzhou, Shanghai, and Beijing</td>
	</tr>
	<tr>
	  <td>
		<a href="#GT4">GT4</a>
	  </td>
	  <td>NVIDIA A100 NVLink 40 GB</td>
	</tr>
	<tr>
	  <td>
		<a href="#GN10Xp">GN10Xp</a>
	  </td>
	  <td>NVIDIA Tesla V100 NVLink 32 GB</td>
	  <td rowspan="2">
		<ul class="params">
		  <li>CentOS 7.2 or later</li>
		  <li>Ubuntu 14.04 or later</li>
		  <li>Windows Server 2012 or later</li>
		</ul>
	  </td>
	  <td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (China), and Frankfurt</td>
	</tr>
	<tr>
	  <td rowspan="2">
		<a href="#GN7">GN7</a>
	  </td>
	  <td>NVIDIA Tesla T4</td>
	  <td>
	  Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (China), Singapore, Silicon Valley, Mumbai, Virginia, and Frankfurt</td>
	</tr>
	<tr>
	  <td>vGPU - NVIDIA Tesla T4</td>
	  <td>
		<ul class="params">
		  <li>CentOS 8.0 64-bit GRID 11.1</li>
		  <li>Ubuntu 20.04 LTS 64-bit GRID 11.1</li>
		</ul>
	  </td>
	  <td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (China), and Silicon Valley</td>
	</tr>
	<tr>
	  <td rowspan="5">Available</td>
	  <td>
		<a href="#GI3X">GI3X</a>
	  </td>
	  <td>NVIDIA Tesla T4</td>
	  <td rowspan="5">
		<ul class="params">
		  <li>CentOS 7.2 or later</li>
		  <li>Ubuntu 14.04 or later</li>
		  <li>Windows Server 2012 or later</li>
		</ul>
	  </td>
	  <td>Guangzhou, Shanghai, Beijing, and Nanjing</td>
	</tr>
	<tr>
	  <td>
		<a href="#GN10X">GN10X</a>
	  </td>
	  <td>NVIDIA Tesla V100 NVLink 32 GB</td>
	  <td>Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Singapore, Silicon Valley, Frankfurt, and Mumbai</td>
	</tr>
	<tr>
	  <td>
		<a href="#GN8">GN8</a>
	  </td>
	  <td>NVIDIA Tesla P40</td>
	  <td>Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Hong Kong (China), and Silicon Valley</td>
	</tr>
	<tr>
	  <td>
		<a href="#GN6GN6S">GN6
		<br />GN6S</a>
	  </td>
	  <td>NVIDIA Tesla P4</td>
	  <td>
		<ul class="params">
		  <li>GN6: Chengdu</li>
		  <li>GN6S: Guangzhou, Shanghai, and Beijing</li>
		</ul>
	  </td>
	</tr>
  </tbody>
</table>

<dx-alert infotype="explain" title="">
**AZ**: Accurate to the city level. For more information, see the instance configuration information below.
</dx-alert>





## Suggestions on Computing Instance Model Selection

Tencent Cloud provides diverse GPU Computing instances to meet business needs in different scenarios. Refer to the following tables to select a Computing instance as needed.

The table below lists **recommended GPU Computing instance models**. A tick (**✓**) indicates that the model supports the corresponding feature. A pentagram (**★**) indicates that the model is recommended.

<table>
        <thead>
        <tr>
            <th width="20%">Feature/Instance</th>
            <th width="11.5%">PNV4</th>
            <th width="11.5%">GT4</th>
            <th width="11.5%">GN10Xp</th>
            <th width="11.5%">GN7</th>
            <th width="11.5%">GI3X</th>
            <th width="11.5%">GN10X</th>
            <th width="11.5%">GN8</th>
            <th width="11.5%">GN6<br>GN6S</th>    
        </tr>
        </thead>
        <tbody>
            <tr>
                <td>Graphics and image processing</td>
                <td>✓</td>
                <td>-</td>
                <td>✓</td>
                <td>✓</td>
                <td>✓</td>
                <td>✓</td>
                <td>✓</td>
                <td>✓</td>
            </tr>
            <tr>
                <td>Video encoding and decoding</td> 
                <td>✓</td>
                <td>-</td>
                <td>✓</td>
                <td>★</td>
                <td>★</td>
                <td>✓</td>
                <td>✓</td>
                <td>✓</td>
            </tr>
            <tr>
                <td>Deep learning training</td>
                <td>✓</td>
                <td>★</td>
                <td>★</td>
                <td>✓</td>
                <td>✓</td>
                <td>★</td>
                <td>★</td>
                <td>✓</td>
            </tr>
            <tr>
                <td>Deep learning inference</td> 
                <td>★</td>
                <td>✓</td>
                <td>★</td>
                <td>★</td>
                <td>★</td>
                <td>★</td>
                <td>✓</td>
                <td>✓</td>
            </tr>
            <tr>
                <td>Scientific computing</td>
                <td>-</td>
                <td>★</td>
                <td>★</td>
                <td>-</td>
                <td>-</td>
                <td>★</td>
                <td>-</td>
                <td>-</td>
            </tr>
        </tbody>
</table>

<dx-alert infotype="notice" title="">
>- These recommendations are for reference only. Select an appropriate instance model based on your needs.
- To use NVIDIA GPU instances for general computing tasks, you need to install the Tesla driver and CUDA toolkit. For more information, see [Installing NVIDIA Driver](https://intl.cloud.tencent.com/document/product/560/8048) and [Installing CUDA Toolkit](https://intl.cloud.tencent.com/document/product/560/8064).
- To use NVIDIA GPU instances for 3D rendering tasks such as high-performance graphics processing and video encoding and decoding, you must install a GRID driver and configure a license server.
</dx-alert>



## Service Options

- [Spot instances](https://intl.cloud.tencent.com/zh/document/product/213/2180#.E7.AB.9E.E4.BB.B7.E5.AE.9E.E4.BE.8B) and [pay-as-you-go instances](https://intl.cloud.tencent.com/document/product/213/2180) are supported.
- Instances can be launched in [VPC](https://intl.cloud.tencent.com/document/product/213/5227).
- Instances can be connected to other services such as [CLB](https://intl.cloud.tencent.com/document/product/214/524), without additional management and Ops costs. Private network traffic is free of charge.


## Instance Specification

### Computing PNV4[](id:PNV4) 

**Computing PNV4** supports not only general GPU computing tasks such as deep learning, but also graphics and image processing tasks such as 3D rendering and video encoding and decoding.



<dx-alert infotype="notice" title="">
This instance model is currently made available through an allowlist. To purchase it, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
</dx-alert>

#### Use cases

PNV4 is cost-effective and suitable for the following scenarios:

- Deep learning inference and small-scale training scenarios, such as:
  - AI inference for mass deployment
  - Small-scale deep learning training
- Graphics and image processing scenarios, such as:
  - Graphics and image processing
  - Video encoding and decoding
  - Graph database

#### AZs
PNV4 instances are available in Guangzhou Zone 7, Shanghai Zone 5, and Beijing Zone 6.

#### Hardware specification

- **CPU:** AMD EPYCTM Milan CPU 2.55 GHz, with a Max Boost frequency of 3.5 GHz.
- **GPU:** NVIDIA<sup>®</sup> A10, providing 62.5 TFLOPS of single-precision floating point performance, 250 TOPS for INT8, and 500 TOPS for INT4.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**PNV4 instances are available in the following configurations:**

<table>
  <thead>
<tr>
      <th width="10%">Model</th>
      <th width="25%">GPU
      <br>(NVIDIA A10)</th>
      <th width="20%">GPU Video Memory
      <br>(HBM2)</th>
      <th width="12%">vCPU</th>
      <th>Memory
      <br>(DDR4)</th>
      <th width="8%">Private Network Bandwidth</th>
      <th width="8%">Packets In/Out<br>(PPS)</th>
      <th width="6%">Number of Queues</th>
    </tr>
  </thead>
  <tbody>
	<tr>
	  <td>PNV4.7XLARGE116</td>
	  <td>1</td>
	  <td>1 * 24 GB</td>
	  <td>28 cores</td>
	  <td>116 GB</td>
	  <td>13 Gbps</td>
	  <td>2.3 million</td>
	  <td>28</td>
	</tr>
	<tr>
	  <td>PNV4.14XLARGE232</td>
	  <td>2</td>
	  <td>2 * 24 GB</td>
	  <td>56 cores</td>
	  <td>232 GB</td>
	  <td>25 Gbps</td>
	  <td>4.7 million</td>
	  <td>48</td>
	</tr>
	<tr>
	  <td>PNV4.28XLARGE466</td>
	  <td>4</td>
	  <td>4 * 24 GB</td>
	  <td>112 cores</td>
	  <td>466 GB</td>
	  <td>50 Gbps</td>
	  <td>9.5 million</td>
	  <td>48</td>
	</tr>
	<tr>
	  <td>PNV4.56XLARGE932</td>
	  <td>8</td>
	  <td>8 * 24 GB</td>
	  <td>224 cores</td>
	  <td>932 GB</td>
	  <td>100 Gbps</td>
	  <td>19 million</td>
	  <td>48</td>
	</tr>
  </tbody>
</table>




### Computing GT4[](id:GT4) 

**Computing GT4 instances** are suitable for general GPU computing tasks such as deep learning and scientific computing.

#### Use cases

GT4 features powerful double-precision floating point computing capabilities. It is suitable for large-scale deep learning training and inference as well as scientific computing scenarios, such as:
- Deep learning
- High-performance database
- Computational fluid dynamics
- Computational finance
- Seismic analysis
- Molecular modeling
- Genomics and others


#### AZs
GT4 instances are available in Guangzhou Zone 4, Shanghai Zone 4, and Beijing Zone 5.

#### Hardware specification

- **CPU:** AMD EPYC™ ROME CPU, with a clock rate of 2.6 GHz.
- **GPU:** NVIDIA<sup>®</sup> A100 NVLink 40 GB, providing 19.5 TFLOPS of single-precision floating point performance, 9.7 TFLOPS of double-precision floating point performance, and 600 GB/s NVLink.
- **Memory:** DDR4 with stable computing performance.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Private network bandwidth of up to 50 Gbps is supported, with strong packet sending/receiving capabilities. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GT4 instances are available in the following configurations:**

<table>
  <thead>
  <tr>
      <th width="10%">Model</th>
      <th width="20%">GPU
      <br>(NVIDIA
 Tesla A100 NVLink 40 GB)</th>
      <th width="12%">GPU Video Memory
      <br>(HBM2)</th>
      <th width="10%">vCPU</th>
      <th>Memory
      <br>(DDR4)</th>
      <th width="10%">Private Network Bandwidth</th>
      <th width="10%">Packets In/Out<br>(PPS)</th>
      <th width="7%">Number of Queues</th>
    </tr>
  </thead>
  <tbody>
	<tr>
	  <td>GT4.4XLARGE96</td>
	  <td>1</td>
	  <td>1 * 40 GB</td>
	  <td>16 cores</td>
	  <td>96 GB</td>
	  <td>5 Gbps</td>
	  <td>1.2 million</td>
	  <td>4</td>
	</tr>
	<tr>
	  <td>GT4.8XLARGE192</td>
	  <td>2</td>
	  <td>40 GB x2</td>
	  <td>32 cores</td>
	  <td>192 GB</td>
	  <td>10 Gbps</td>
	  <td>2.35 million</td>
	  <td>8</td>
	</tr>
	<tr>
	  <td>GT4.20XLARGE474</td>
	  <td>4</td>
	  <td>4 * 40 GB</td>
	  <td>82 cores</td>
	  <td>474 GB</td>
	  <td>25 Gbps</td>
	  <td>6 million</td>
	  <td>16</td>
	</tr>
	<tr>
	  <td>GT4.41XLARGE948</td>
	  <td>8</td>
	  <td>8 * 40 GB</td>
	  <td>164 cores</td>
	  <td>948 GB</td>
	  <td>50 Gbps</td>
	  <td>12 million</td>
	  <td>32</td>
	</tr>
  </tbody>
</table>


<dx-alert infotype="explain" title="">
**GPU driver**: Drivers of NVIDIA Tesla 450 or later are required for NVIDIA A100 GPUs, and version 460.32.03 (Linux)/461.33 (Windows) are recommended. For more information on driver versions, see [NVIDIA Driver Documentation](https://docs.nvidia.com/datacenter/tesla/index.html#nvidia-driver-documentation).
</dx-alert>




### Computing GN10Xp[](id:GN10Xp) 

**Computing GN10Xp instances** support not only general GPU computing tasks such as deep learning and scientific computing, but also graphics and image processing tasks such as 3D rendering and video encoding and decoding.

#### Use cases

GN10Xp features powerful double-precision floating point computing capabilities. It is suitable for the following scenarios:

- Large-scale deep learning training and inference as well as scientific computing scenarios, such as:
  - Deep learning
  - High-performance database
  - Computational fluid dynamics
  - Computational finance
  - Seismic analysis
  - Molecular modeling
  - Genomics and others
- Graphics and image processing scenarios, such as:
  - Graphics and image processing
  - Video encoding and decoding
  - Graph database


#### AZs
GN10Xp instances are available in Guangzhou Zones 3 and 4, Shanghai Zone 2, Nanjing Zone 1, Beijing Zone 5, Chengdu Zone 1, Chongqing Zone 1, Hong Kong Zone 2, and Frankfurt Zone 1.


#### Hardware specification

- **CPU:** Intel<sup>®</sup> Xeon<sup>®</sup> Platinum 8255C CPU, with a clock rate of 2.5 GHz.
- **GPU: **NVIDIA<sup>®</sup> Tesla<sup>®</sup> V100 NVLink 32GB, providing 15.7 TFLOPS of single-precision floating point performance, 7.8 TFLOPS of double-precision floating point performance, 125 TFLOPS of deep learning accelerator performance with Tensor cores, and 300 GB/s NVLink.
- **Memory:** DDR4, providing memory bandwidth up to 2,666 MT/s.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GN10Xp instances are available in the following configurations:**

<table>
  <thead>
		<th width="10%">Model</th>
	  <th width="25%">GPU
	  <br />(NVIDIA Tesla V100 NVLink 32 GB)</th>
	  <th width="12%">GPU Video Memory
	  <br />(HBM2)</th>
	  <th width="8%">vCPU</th>
	  <th>Memory
	  <br />(DDR4)</th>
	  <th width="10%">Private Network Bandwidth</th>
	  <th width="10%">Packets In/Out<br />(PPS)</th>
	  <th width="7%">Number of Queues</th>
  </thead>
  <tbody>
	<tr>
	  <td>GN10Xp.2XLARGE40</td>
	  <td>1</td>
	  <td>1 * 32 GB</td>
	  <td>10 cores</td>
	  <td>40 GB</td>
	  <td>3 Gbps</td>
	  <td>0.8 million</td>
	  <td>2</td>
	</tr>
	<tr>
	  <td>GN10Xp.5XLARGE80</td>
	  <td>2</td>
	  <td>2 * 32 GB</td>
	  <td>20 cores</td>
	  <td>80 GB</td>
	  <td>6 Gbps</td>
	  <td>1.5 million</td>
	  <td>5</td>
	</tr>
	<tr>
	  <td>GN10Xp.10XLARGE160</td>
	  <td>4</td>
	  <td>4 * 32 GB</td>
	  <td>40 cores</td>
	  <td>160 GB</td>
	  <td>12 Gbps</td>
	  <td>2.5 million</td>
	  <td>10</td>
	</tr>
	<tr>
	  <td>GN10Xp.20XLARGE320</td>
	  <td>8</td>
	  <td>8 * 32 GB</td>
	  <td>80 cores</td>
	  <td>320 GB</td>
	  <td>24 Gbps</td>
	  <td>4.9 million</td>
	  <td>16</td>
	</tr>
  </tbody>
</table>



### Computing GN7[](id:GN7) 

**NVIDIA GN7** supports not only general GPU computing tasks such as deep learning, but also graphics and image processing tasks such as 3D rendering and video encoding and decoding.

#### Use cases

GN7 is cost-effective and suitable for the following scenarios:

- Deep learning inference and small-scale training scenarios, such as:
  - AI inference for mass deployment
  - Small-scale deep learning training
- Graphics and image processing scenarios, such as:
  - Graphics and image processing
  - Video encoding and decoding
  - Graph database

#### AZs
GN7 instances are available in the following AZs:
- **GN7.LARGE20 and GN7.2XLARGE40**: Guangzhou Zones 3 and 4, Shanghai Zones 2 and 4, Nanjing Zone 1 and 2, Beijing Zones 3 and 5, Chengdu Zone 1, Chongqing Zone 1, and Silicon Valley Zone 2.
- **Other GN7 instances**: Guangzhou Zones 3 and 4, Shanghai Zones 2 and 4, Nanjing Zones 1 and 2, Beijing Zones 3 and 5, Chengdu Zone 1, Chongqing Zone 1, Singapore Zone 1, Silicon Valley Zone 2, Hong Kong Zone 2, Mumbai Zone 2, Virginia Zone 2, and Frankfurt Zone 1.


#### Hardware specification

- **CPU:** Intel<sup>®</sup> Xeon<sup>®</sup> Platinum 8255C CPU, with a clock rate of 2.5 GHz.
- **GPU:** NVIDIA<sup>®</sup> Tesla<sup>®</sup> T4, providing 8.1 TFLOPS of single-precision floating point performance, 130 TOPS for INT8, and 260 TOPS for INT4.
- **Memory:** DDR4, providing memory bandwidth up to 2,666 MT/s.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GN7 instances are available in the following configurations:**

<table>
  <thead>
	<tr>
		<th width="10%">Model</th>
	  <th width="15%">GPU
	  <br />(NVIDIA
	  <br />Tesla T4)</th>
	  <th width="15%">GPU Video Memory
	  <br />(HBM2)</th>
	  <th width="8%">vCPU</th>
	  <th width="8%">Memory
	  <br />(DDR4)</th>
	  <th width="10%">Private Network Bandwidth</th>
	  <th width="10%">Packets In/Out<br />(PPS)</th>
	  <th width="7%">Number of Queues</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td>GN7.LARGE20</td>
	  <td>1/4</td>
	  <td>4 GB vGPU</td>
	  <td>4 cores</td>
	  <td>20 GB</td>
	  <td>1.5 Gbps</td>
	  <td>0.5 million</td>
	  <td>8</td>
	</tr>
	<tr>
	  <td>GN7.2XLARGE40</td>
	  <td>1/2</td>
	  <td>8 GB vGPU</td>
	  <td>10 cores</td>
	  <td>40 GB</td>
	  <td>3 Gbps</td>
	  <td>0.7 million</td>
	  <td>8</td>
	</tr>
	<tr>
	  <td>GN7.2XLARGE32</td>
	  <td>1</td>
	  <td>1 * 16 GB</td>
	  <td>8 cores</td>
	  <td>32 GB</td>
	  <td>3 Gbps</td>
	  <td>0.6 million</td>
	  <td>8</td>
	</tr>
	<tr>
	  <td>GN7.5XLARGE80</td>
	  <td>1</td>
	  <td>1 * 16 GB</td>
	  <td>20 cores</td>
	  <td>80 GB</td>
	  <td>7 Gbps</td>
	  <td>1.4 million</td>
	  <td>10</td>
	</tr>
	<tr>
	  <td>GN7.8XLARGE128</td>
	  <td>1</td>
	  <td>1 * 16 GB</td>
	  <td>32 cores</td>
	  <td>128 GB</td>
	  <td>10 Gbps</td>
	  <td>2.4 million</td>
	  <td>16</td>
	</tr>
	<tr>
	  <td>GN7.10XLARGE160</td>
	  <td>2</td>
	  <td>2 * 16 GB</td>
	  <td>40 cores</td>
	  <td>160 GB</td>
	  <td>13 Gbps</td>
	  <td>2.8 million</td>
	  <td>20</td>
	</tr>
	<tr>
	  <td>GN7.20XLARGE320</td>
	  <td>4</td>
	  <td>4 * 16 GB</td>
	  <td>80 cores</td>
	  <td>320 GB</td>
	  <td>25 Gbps</td>
	  <td>5.6 million</td>
	  <td>32</td>
	</tr>
  </tbody>
</table>


<dx-alert infotype="explain" title="">
**vGPU**:
- GN7 instance cluster provides vGPU-based instances. The vGPU type is vComputeServer, which only supports CUDA APIs.
- vCS instances require a GRID driver and don't support Windows.
</dx-alert>


### Interference GI3X[](id:GI3X) 

**NVIDIA GI3X** supports not only general GPU computing tasks such as deep learning, but also graphics and image processing tasks such as 3D rendering and video encoding and decoding.

#### Use cases

GI3X is cost-effective and suitable for the following scenarios:

- Deep learning inference and small-scale training scenarios, such as:
  - AI inference for mass deployment
  - Small-scale deep learning training
- Graphics and image processing scenarios, such as:
  - Graphics and image processing
  - Video encoding and decoding
  - Graph database

#### AZs
GI3X instances are available in Guangzhou Zone 3, Shanghai Zone 4, Nanjing Zones 1 and 2, and Beijing Zone 5.

#### Hardware specification
- **CPU:** AMD EPYC™ ROME CPU 2.6 GHz, with a Max Boost frequency of 3.3 GHz.
- **GPU:** NVIDIA<sup>®</sup> Tesla<sup>®</sup> T4, providing 8.1 TFLOPS of single-precision floating point performance, 130 TOPS for INT8, and 260 TOPS for INT4.
- **Memory**: Latest eight-channel DDR4 with stable computing performance.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GI3X instances are available in the following configurations:**

<table>
  <thead>
		<tr>
		<th width="10%">Model</th>
	  <th width="15%">GPU
	  <br />(NVIDIA
	  <br />Tesla T4)</th>
	  <th width="15%">GPU Video Memory
	  <br />(GDDR6)</th>
	  <th width="8%">vCPU</th>
	  <th width="8%">Memory
	  <br />(DDR4)</th>
	  <th width="10%">Private Network Bandwidth</th>
	  <th width="10%">Packets In/Out<br />(PPS)</th>
	  <th width="7%">Number of Queues</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td>GI3X.8XLARGE64</td>
	  <td>1</td>
	  <td>1 * 16 GB</td>
	  <td>32 cores</td>
	  <td>64 GB</td>
	  <td>5 Gbps</td>
	  <td>1.4 million</td>
	  <td>8</td>
	</tr>
	<tr>
	  <td>GI3X.22XLARGE226</td>
	  <td>2</td>
	  <td>2 * 16 GB</td>
	  <td>90 cores</td>
	  <td>226 GB</td>
	  <td>13 Gbps</td>
	  <td>3.75 million</td>
	  <td>16</td>
	</tr>
	<tr>
	  <td>GI3X.45XLARGE452</td>
	  <td>4</td>
	  <td>4 * 16 GB</td>
	  <td>180 cores</td>
	  <td>452 GB</td>
	  <td>25 Gbps</td>
	  <td>7.5 million</td>
	  <td>32</td>
	</tr>
  </tbody>
</table>








### Computing GN10X[](id:GN10X) 

**Computing GN10X** supports not only general GPU computing tasks such as deep learning and scientific computing, but also graphics and image processing tasks such as 3D rendering and video encoding and decoding.

#### Use cases

GN10X features powerful double-precision floating point computing capabilities. It is suitable for the following scenarios:

- Large-scale deep learning training and inference as well as scientific computing scenarios, such as:
  - Deep learning
  - High-performance database
  - Computational fluid dynamics
  - Computational finance
  - Seismic analysis
  - Molecular modeling
  - Genomics and others
- Graphics and image processing scenarios, such as:
  - Graphics and image processing
  - Video encoding and decoding
  - Graph database


#### AZs
GN10X instances are available in Guangzhou Zones 3 and 4, Shanghai Zones 2 and 3, Nanjing Zone 1, Beijing Zones 4 and 5, Chengdu Zone 1, Chongqing Zone 1, Singapore Zone 1, Silicon Valley Zone 2, Frankfurt Zone 1, and Mumbai Zone 2.



#### Hardware specification

- **CPU:** GN10X is configured with an Intel<sup>®</sup> Xeon<sup>®</sup> Gold 6133 CPU, with a clock rate of 2.5 GHz.
- **GPU: **NVIDIA<sup>®</sup> Tesla<sup>®</sup> V100 NVLink 32GB, providing 15.7 TFLOPS of single-precision floating point performance, 7.8 TFLOPS of double-precision floating point performance, 125 TFLOPS of deep learning accelerator performance with Tensor cores, and 300 GB/s NVLink.
- **Memory:** DDR4, providing memory bandwidth up to 2,666 MT/s.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GN10X instances are available in the following configurations:**

<table>
  <thead>
	<tr>
		<th width="10%">Model</th>
	  <th width="25%">GPU
	  <br />(NVIDIA Tesla V100 NVLink 32 GB)</th>
	  <th width="12%">GPU Video Memory
	  <br />(HBM2)</th>
	  <th width="8%">vCPU</th>
	  <th>Memory
	  <br />(DDR4)</th>
	  <th width="10%">Private Network Bandwidth</th>
	  <th width="10%">Packets In/Out<br />(PPS)</th>
	  <th width="7%">Number of Queues</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td>GN10X.2XLARGE40</td>
	  <td>1</td>
	  <td>1 * 32 GB</td>
	  <td>8 cores</td>
	  <td>40 GB</td>
	  <td>3 Gbps</td>
	  <td>0.8 million</td>
	  <td>2</td>
	</tr>
	<tr>
	  <td>GN10X.9XLARGE160</td>
	  <td>4</td>
	  <td>4 * 32 GB</td>
	  <td>36 cores</td>
	  <td>160 GB</td>
	  <td>13 Gbps</td>
	  <td>2.5 million</td>
	  <td>9</td>
	</tr>
	<tr>
	  <td>GN10X.18XLARGE320</td>
	  <td>8</td>
	  <td>8 * 32 GB</td>
	  <td>72 cores</td>
	  <td>320 GB</td>
	  <td>25 Gbps</td>
	  <td>4.9 million</td>
	  <td>16</td>
	</tr>
  </tbody>
</table>




### Computing GN8[](id:GN8) 

**NVIDIA GN8** supports not only general GPU computing tasks such as deep learning, but also graphics and image processing tasks such as 3D rendering and video encoding and decoding.

#### Use cases

GN8 is suitable for the following scenarios:

- Deep learning training and inference scenarios, such as:
  - AI inference with high throughput
  - Deep learning
- Graphics and image processing scenarios, such as:
  - Graphics and image processing
  - Video encoding and decoding
  - Graph database


#### AZs
GN8 instances are available in Hong Kong Zone 2, Guangzhou Zone 3, Shanghai Zone 3, Beijing Zones 2 and 4, Chengdu Zone 1, Chongqing Zone 1, and Silicon Valley Zone 1.


#### Hardware specification

- **CPU:** Intel<sup>®</sup> Xeon<sup>®</sup> E5-2680 v4 CPU, with a clock rate of 2.4 GHz.
- **GPU:** NVIDIA<sup>®</sup> Tesla<sup>®</sup> P40, providing 12 TFLOPS of single-precision floating point performance and 47 TOPS for INT8.
- **Memory:** DDR4, providing memory bandwidth up to 2,666 MT/s.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GN8 instances are available in the following configurations:**

<table>
  <thead>
	<tr>
		<th width="10%">Model</th>
	  <th width="25%">GPU
	  <br />(NVIDIA Tesla P40)</th>
	  <th width="12%">GPU Video Memory
	  <br />(HBM2)</th>
	  <th width="8%">vCPU</th>
	  <th>Memory
	  <br />(DDR4)</th>
	  <th width="10%">Private Network Bandwidth</th>
	  <th width="10%">Packets In/Out<br />(PPS)</th>
	  <th width="7%">Number of Queues</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td>GN8.LARGE56</td>
	  <td>1</td>
	  <td>24 GB</td>
	  <td>6 cores</td>
	  <td>56 GB</td>
	  <td>1.5 Gbps</td>
	  <td>0.45 million</td>
	  <td>8</td>
	</tr>
	<tr>
	  <td>GN8.3XLARGE112</td>
	  <td>2</td>
	  <td>48 GB</td>
	  <td>14 cores</td>
	  <td>112 GB</td>
	  <td>2.5 Gbps</td>
	  <td>0.5 million</td>
	  <td>8</td>
	</tr>
	<tr>
	  <td>GN8.7XLARGE224</td>
	  <td>4</td>
	  <td>96 GB</td>
	  <td>28 cores</td>
	  <td>224 GB</td>
	  <td>5 Gbps</td>
	  <td>0.7 million</td>
	  <td>14</td>
	</tr>
	<tr>
	  <td>GN8.14XLARGE448</td>
	  <td>8</td>
	  <td>192 GB</td>
	  <td>56 cores</td>
	  <td>448 GB</td>
	  <td>10 Gbps</td>
	  <td>0.7 million</td>
	  <td>28</td>
	</tr>
  </tbody>
</table>

### Computing GN6 and GN6S[](id:GN6GN6S) 

**NVIDIA GN6 and GN6S** support not only general GPU computing tasks such as deep learning, but also graphics and image processing tasks such as 3D rendering and video encoding and decoding.

#### Use cases

GN6 and GN6S are cost-effective and suitable for the following scenarios:

- Deep learning inference and small-scale training scenarios, such as:
  - AI inference for mass deployment
  - Small-scale deep learning training
- Graphics and image processing scenarios, such as:
  - Graphics and image processing
  - Video encoding and decoding
  - Graph database


#### AZs
GN6 and GN6S instances are available in the following AZs:
- **GN6**: Chengdu Zone 1.
- **GN6S**: Guangzhou Zone 3, Shanghai Zones 2, 3, and 4, and Beijing Zones 4 and 5.


#### Hardware specification

- **CPU:** GN6 is configured with an Intel<sup>®</sup> Xeon<sup>®</sup> E5-2680 v4 CPU, with a clock rate of 2.4 GHz. GN6S is configured with an Intel<sup>®</sup> Xeon<sup>®</sup> Silver 4110 CPU, with a clock rate of 2.1 GHz.
- **GPU:** NVIDIA<sup>®</sup> Tesla<sup>®</sup> P4, providing 5.5 TFLOPS of single-precision floating point performance and 22 TOPS for INT8.
- **Memory:** DDR4, providing memory bandwidth up to 2,666 MT/s.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GN6 and GN6S instances are available in the following configurations:**

<table>
  <thead>
	<tr>
		<th width="10%">Model</th>
	  <th width="25%">GPU
	  <br />(NVIDIA Tesla P4)</th>
	  <th width="12%">GPU Video Memory
	  <br />(HBM2)</th>
	  <th width="8%">vCPU</th>
	  <th>Memory
	  <br />(DDR4)</th>
	  <th width="10%">Private Network Bandwidth</th>
	  <th width="10%">Packets In/Out<br />(PPS)</th>
	  <th width="7%">Number of Queues</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td>GN6.7XLARGE48</td>
	  <td>1</td>
	  <td>8 GB</td>
	  <td>28 cores</td>
	  <td>48 GB</td>
	  <td>5 Gbps</td>
	  <td>1.2 million</td>
	  <td>14</td>
	</tr>
	<tr>
	  <td>GN6.14XLARGE96</td>
	  <td>2</td>
	  <td>16 GB</td>
	  <td>56 cores</td>
	  <td>96 GB</td>
	  <td>10 Gbps</td>
	  <td>1.2 million</td>
	  <td>28</td>
	</tr>
	<tr>
	  <td>GN6S.LARGE20</td>
	  <td>1</td>
	  <td>8 GB</td>
	  <td>4 cores</td>
	  <td>20 GB</td>
	  <td>5 Gbps</td>
	  <td>0.5 million</td>
	  <td>8</td>
	</tr>
	<tr>
	  <td>GN6S.2XLARGE40</td>
	  <td>2</td>
	  <td>16 GB</td>
	  <td>8 cores</td>
	  <td>40 GB</td>
	  <td>9 Gbps</td>
	  <td>0.8 million</td>
	  <td>8</td>
	</tr>
  </tbody>
</table>



<style>
	.params{margin:0px !important}
</style>
