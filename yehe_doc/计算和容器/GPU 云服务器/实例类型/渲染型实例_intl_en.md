**GPU Rendering instances** support GPU-based traditional graphics and image processing such as 3D rendering. They provide a fast, stable, and elastic computing service and can be **managed just like [CVM](https://intl.cloud.tencent.com/products/cvm) instances**.


## Use Cases
High-performance graphics processing and 3D rendering, such as:
 - Nonlinear editing
 - Cloud game
 - Cloud phone
 - Cloud desktop
 - CloudXR
 - Graphics and image processing



## Overview

**GPU Rendering instances are available in the following types:**


<table>
  <thead>
	<tr>
	  <th width="3%">Instance</th>
	  <th width="19%">GPU Type</th>
	  <th width="34%">Available Image</th>
	  <th width="38%">AZ</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td>
		<a href="#GNV4v">GNV4v</a>
	  </td>
	  <td>NVIDIA A10</td>
	  <td>Windows Server 2019 Datacenter 64-bit Chinese GRID 13
	  </td>
	  <td>Beijing, Shanghai, and Guangzhou</td>
	</tr>
	<tr>
	  <td>
		<a href="#GNV4">GNV4</a>
	  </td>
	  <td>NVIDIA A10</td>
	  <td>
		<ul class="params">
		  <li>CentOS 7.2 or later</li>
		  <li>Ubuntu 16.04 or later</li>
		  <li>Windows Server 2019 Datacenter 64-bit Chinese GRID 13</li>
		</ul>
	  </td>
	  <td>Beijing, Shanghai, Guangzhou, and Chongqing</td>
	</tr>
	<tr>
	  <td>
		<a href="#GN7vw">GN7vw</a>
	  </td>
	  <td>NVIDIA Tesla T4</td>
	  <td>
		<ul class="params">
		  <li>CentOS 8.0 64-bit GRID 11.1</li>
		  <li>Windows Server 2019 Datacenter 64-bit Chinese GRID 11.1</li>
		</ul>
	  </td>
	  <td>
	  Beijing, Shanghai, Guangzhou, Nanjing, Chengdu, Chongqing, Hong Kong (China), Singapore, Mumbai, Silicon Valley, Virginia, and Frankfurt</td>
	</tr>
	<tr>
	  <td><a href="#GI1">GI1</a></td> 
	  <td>Intel SG1</td>
	  <td><ul class="params"><li>CentOS 7.6 64-bit + SG1-pv1.3</li><li>CentOS 7.6 64-bit + SG1-pv1.4</li></td>
	  <td>Beijing, Shanghai, Guangzhou, Nanjing, and Chongqing</td>
	 </tr>
  </tbody>
</table>


<dx-alert infotype="explain" title="">
**AZ**: Accurate to the city level. For more information, see the instance configuration information below.
</dx-alert>





## Suggestions on Rendering Instance Model Selection

Tencent Cloud provides diverse GPU Computing instances to meet business needs in different scenarios. Refer to the following tables to select a Computing instance as needed.

The table below lists **recommended GPU Rendering instance models**. A tick (**✓**) indicates that the model supports the corresponding feature. A pentagram (**★**) indicates that the model is recommended.

<table>
        <thead>
        <tr>
            <th width="20%">Feature/Instance</th>
            <th width="11.5%">GNV4v</th>
            <th width="11.5%">GNV4</th>
            <th width="11.5%">GN7vw</th>
						<th width="11.5%">GI1</th>
        </tr>
        </thead>
        <tbody>
            <tr>
                <td>Graphics and image processing</td>
                <td>★</td>
                <td>★</td>
                <td>★</td>
								<td>★</td>
            </tr>
            <tr>
                <td>Video encoding and decoding</td> 
                <td>★</td>
                <td>★</td>
                <td>★</td>
								<td>★</td>
            </tr>
            <tr>
                <td>Deep learning training</td>
                <td>-</td>
                <td>✓</td>
                <td>-</td>
								<td>-</td>
            </tr>
            <tr>
                <td>Deep learning inference</td> 
                <td>-</td>
                <td>✓</td>
                <td>-</td>
								<td>-</td>
            </tr>
            <tr>
                <td>Scientific computing</td>
                <td>-</td>
                <td>-</td>
                <td>-</td>
								<td>-</td>
            </tr>
        </tbody>
</table>



<dx-alert infotype="notice" title="">
>- These recommendations are for reference only. Select an appropriate instance model based on your needs.
- To use NVIDIA GPU instances for 3D rendering tasks such as high-performance graphics processing and video encoding and decoding, you need to install a GRID driver and configure a license server. For GNV4v, GNV4, and GN7vw instances, you can select a specified image with a GRID driver preinstalled and a license server preconfigured.
- GNV4v, GNV4, and GN7vw instance clusters provide vGPU instance types that support vDWs and vWs. They also support graphics APIs such as DirectX and OpenGL.
</dx-alert>



## Service Options

- [Spot instances](https://intl.cloud.tencent.com/zh/document/product/213/2180#.E7.AB.9E.E4.BB.B7.E5.AE.9E.E4.BE.8B) and [pay-as-you-go instances](https://intl.cloud.tencent.com/document/product/213/2180) are supported.
- Instances can be launched in [VPC](https://intl.cloud.tencent.com/document/product/213/5227).
- Instances can be connected to other services such as [CLB](https://intl.cloud.tencent.com/document/product/214/524), without additional management and Ops costs. Private network traffic is free of charge.


## Instance Specification

### Rendering GNV4v[](id:GNV4v)

A **NVIDIA GNV4v instance** is a rendering instance configured with a vDWS license server and installed with a GRID driver. It is suitable for graphics and image processing scenarios such as 3D rendering and video encoding and decoding. It eliminates the need to manually configure the basic environment for GPU-based graphics and image processing.

<dx-alert infotype="notice" title="">
This instance model is currently made available through an allowlist. To purchase it, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
</dx-alert>


#### AZs
GNV4v instances are available in Guangzhou Zone 7, Shanghai Zone 5, and Beijing Zone 6.


#### Hardware specification

- **CPU:** AMD EPYCTM Milan CPU 2.55 GHz, with a Max Boost frequency of 3.5 GHz.
- **GPU:** NVIDIA<sup>®</sup> A10, providing 62.5 TFLOPS of single-precision floating point performance, 250 TOPS for INT8, and 500 TOPS for INT4.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GNV4v instances are available in the following configurations:**

<table>
  <thead>
	<tr>
	  <th width="10%">Model</th>
	  <th width="15%">GPU
	  <br />(NVIDIA A10)</th>
	  <th width="15%">GPU Video Memory
	  <br />(HBM2)</th>
	  <th width="8%">vCPU</th>
	  <th>Memory
	  <br />(DDR4)</th>
	  <th width="10%">Private Network Bandwidth</th>
	  <th>Packets In/Out<br />(PPS)</th>
	  <th>Number of Queues</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td>GNV4v.XLARGE24</td>
	  <td>1/4</td>
	  <td>6 GB vGPU</td>
	  <td>6 cores</td>
	  <td>24 GB</td>
	  <td>3 Gbps</td>
	  <td>0.5 million</td>
	  <td>6</td>
	</tr>
	<tr>
	  <td>GNV4v.3XLARGE58</td>
	  <td>1/2</td>
	  <td>12 GB vGPU</td>
	  <td>14 cores</td>
	  <td>58 GB</td>
	  <td>7 Gbps</td>
	  <td>1.1 million</td>
	  <td>14</td>
	</tr>
	<tr>
	  <td>GNV4v.7XLARGE116</td>
	  <td>1</td>
	  <td>1 * 24 GB</td>
	  <td>28 cores</td>
	  <td>116 GB</td>
	  <td>13 Gbps</td>
	  <td>2.3 million</td>
	  <td>28</td>
	</tr>
  </tbody>
</table>




### Rendering GNV4[](id:GNV4)

A **NVIDIA GNV4 instance** is a rendering instance configured with a vDWS license server and installed with a GRID driver. It is suitable for graphics and image processing scenarios such as 3D rendering and video encoding and decoding. It eliminates the need to manually configure the basic environment for GPU-based graphics and image processing.

<dx-alert infotype="notice" title="">
This instance model is currently made available through an allowlist. To purchase it, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
</dx-alert>

#### AZs
GNV4 instances are available in Beijing Zone 6, Shanghai Zone 5, Guangzhou Zone 6, and Chongqing Zone 1.

#### Hardware specification

- **CPU:** Intel<sup>®</sup> Xeon<sup>®</sup> Cooper Lake CPU, with a base clock of 3.4 GHz and a Max Turbo frequency of 3.8 GHz.
- **GPU:** NVIDIA<sup>®</sup> A10, providing 31.2 TFLOPS of single-precision floating point performance, 250 TOPS for INT8, and 500 TOPS for INT4.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GNV4 instances are available in the following configurations:**

<table>
  <thead>
	<tr>
	  <th width="10%">Model</th>
	  <th width="15%">GPU
	  <br />(NVIDIA A10)</th>
	  <th width="15%">GPU Video Memory
	  <br />(GDDR6)</th>
	  <th width="8%">vCPU</th>
	  <th>Memory
	  <br />(DDR4)</th>
	  <th width="10%">Private Network Bandwidth</th>
	  <th>Packets In/Out<br />(PPS)</th>
	  <th>Number of queues</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td>GNV4.3XLARGE44</td>
	  <td>1</td>
	  <td>24 GB</td>
	  <td>12 cores</td>
	  <td>44 GB</td>
	  <td>2 Gbps</td>
	  <td>0.53 million</td>
	  <td>4</td>
	</tr>
  </tbody>
</table>




### Rendering GN7vw[](id:GN7vw)

A **NVIDIA GN7vw instance** is a rendering instance configured with a vDWS license server and installed with a GRID driver on the basis of GN7. It is suitable for graphics and image processing scenarios such as 3D rendering and video encoding and decoding. It eliminates the need to manually configure the basic environment for GPU-based graphics and image processing.


<dx-alert infotype="notice" title="">
GPU Rendering GN7vw is offered with limited availability. 
</dx-alert>


#### AZs
GN7vw instances are available in Guangzhou Zones 3 and 4, Shanghai Zones 2, 4, and 5, Nanjing Zones 1 and 2, Beijing Zone 5, Chengdu Zone 1, Chongqing Zone 1, Hong Kong Zone 2, Singapore Zone 1, Mumbai Zone 2 , Silicon Valley Zone 2, Virginia Zone 2, and Frankfurt Zone 1.


#### Hardware specification

- **CPU:** Intel<sup>®</sup> Xeon<sup>®</sup> Platinum 8255C CPU, with a clock rate of 2.5 GHz.
- **GPU:** NVIDIA<sup>®</sup> Tesla<sup>®</sup> T4, providing 8.1 TFLOPS of single-precision floating point performance, 130 TOPS for INT8, and 260 TOPS for INT4.
- **Memory:** DDR4, providing memory bandwidth up to 2,666 MT/s.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.	 
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GN7vw instances are available in the following configurations:**

<table>
  <thead>
	<tr>
	  <th width="10%">Model</th>
	  <th width="15%">GPU
	  <br />(NVIDIA Tesla T4)</th>
	  <th width="15%">GPU Video Memory
	  <br />(GDDR6)</th>
	  <th width="8%">vCPU</th>
	  <th>Memory
	  <br />(DDR4)</th>
	  <th width="10%">Private Network Bandwidth</th>
	  <th>Packets In/Out<br />(PPS)</th>
	  <th>Number of queues</th>
	</tr>
  </thead>
  <tbody>
	<tr>
	  <td>GN7vw.LARGE16</td>
	  <td>1/4</td>
	  <td>4 GB vGPU</td>
	  <td>4 cores</td>
	  <td>16 GB</td>
	  <td>2 Gbps</td>
	  <td>0.5 million</td>
	  <td>8</td>
	</tr>
	<tr>
	  <td>GN7vw.2XLARGE32</td>
	  <td>1/2</td>
	  <td>8 GB vGPU</td>
	  <td>8 cores</td>
	  <td>32 GB</td>
	  <td>4 Gbps</td>
	  <td>0.8 million</td>
	  <td>8</td>
	</tr>
	<tr>
	  <td>GN7vw.4XLARGE64</td>
	  <td>1</td>
	  <td>1 * 16 GB</td>
	  <td>16 cores</td>
	  <td>64 GB</td>
	  <td>7 Gbps</td>
	  <td>1.5 million</td>
	  <td>8</td>
	</tr>
  </tbody>
</table>


### Rendering GI1[](id:GI1)

**GPU Rendering GI1 instances** are equipped with H3C XG310 graphics cards, with each containing four Intel SG1 chips. They are suitable for Android cloud games and apps and video transcoding.

<dx-alert infotype="notice" title="">
This instance model is currently made available through an allowlist. To purchase it, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
</dx-alert>

#### Use cases

- Android cloud phone
- Android cloud game
- Android cloud app
- Video transcoding

#### AZs
GI1 instances are available in Beijing Zone 6, Shanghai Zone 5, Guangzhou Zone 7, Nanjing Zone 3, and Chongqing Zone 1.


#### Hardware specification 
- **CPU:** Intel<sup>®</sup> Xeon<sup>®</sup> Platinum 8255c CPU, with a clock rate of 2.5 GHz.
- **GPU:** Intel<sup>®</sup> SG1, adopting H3C XG310 graphics cards with each containing four SG1 chips.
- **Storage:** Select the appropriate CBS [cloud disk type](https://intl.cloud.tencent.com/document/product/362/31636). To [expand the cloud disk capacity](https://intl.cloud.tencent.com/document/product/362/31600), create and mount an elastic cloud disk.
- **Network:** Network optimization is enabled by default. The network performance of an instance depends on its specification. You can purchase [public network bandwidth](https://intl.cloud.tencent.com/document/product/213/10578) as needed.

**GI1 instances are available in the following configurations:**

<table>
		<thead>
		<tr>
			<th width=8%>Model</th>
			<th width=25%>GPU<br>(Intel<br>SG1)</th>
      <th width=15%>GPU Video Memory</th>
			<th width=8%>vCPU</th>
			<th width=10%>Memory<br>(DDR4)</th>
      <th>Private Network Bandwidth</th>
      <th>Packets In/Out<br>(PPS)</th>
      <th>Number of Queues</th>
		</tr>
		</thead>
		<tbody>
      <tr>
			  <td>GI1.10XLARGE160</td>
			  <td>1 * H3C XG310 (four Intel SG1 chips)</td> 
        <td>32 GB (4 * 8 GB)</td>
			  <td>42 cores</td>
			  <td>160 GB</td>
        <td>13 Gbps</td>
			  <td>2.5 million</td>
        <td>32</td> 
		  </tr>
      <tr>
			  <td>GI1.21XLARGE320</td>
			  <td>2 * H3C XG310 (eight Intel SG1 chips)</td> 
        <td>64 GB (8 * 8 GB)</td>
			  <td>84 cores</td>
			  <td>320 GB</td>
        <td>25 Gbps</td>
			  <td>6 million</td>
        <td>32</td>
		  </tr>
  </tbody>





<style>
	.params{margin:0px !important}
</style>
