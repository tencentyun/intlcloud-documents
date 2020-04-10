## Overview
TKE-Optimized images are images of Kubernetes cluster nodes produced by Tencent Kubernetes Engine (TKE) based on [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel). Fully optimized for TKE, these images have higher security and stability. In particular, the images provide a custom kernel that is maintained by the Tencent Cloud team and can be updated by using hotpatches. We recommend that you select TKE-Optimized series images to deploy your TKE cluster nodes.


## Features

<table>
	<tr><th>Feature</th><th>Description</th></tr>
	<tr><td><b>Kernel Customization</b></td><td><ul style="margin: 0;"><li>Based on kernel 4.14.105, which has been long supported by the kernel community.</li><li>Adds new features applicable to Tencent Cloud scenarios to optimize the performance of the kernel and fix major defects.</li></ul></td></tr>
	<tr><td><b>Container Support</b></td><td><ul style="margin: 0;"><li>Enhances isolation and performance for TKE.</li><li>Supports isolating system files such as meminfo, vmstat, cpuinfo, stat, and loadavg.</li><li>Supports isolating sysctl interfaces, such as tcp_no_delay_ack and tcp_max_orphans.</li><li>Fixed many files system and network bugs.</li></ul></td></tr>
	<tr><td><b>Performance Optimization</b></td><td><ul style="margin: 0;"><li>Optimizes the xfs memory allocation to resolve the xfs kmem_alloc failure.</li><li>Optimizes memory allocation while receiving network packets, to prevent excessive memory usage when a large number of UDP packets are received.</li><li>Limits the memory usage of system page caches, to prevent the lack of memory from affecting service performance and causing the out-of-memory (OOM) error.</li></ul></td></tr>
	<tr><td><b>Support and Updates</b></td><td><ul style="margin: 0;"><li>Regularly updates the kernel to enhance security and functionality.</li><li>Updates the kernel by using hotpatches.</li></td></tr>
</table>

