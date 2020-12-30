Tencent Cloud provides the Linux public images with default configurations, but we recommend you separately configure `sysctl` to adapt to your specific business. This document describes the default and optimal configurations of Tencent Cloud Linux public images and helps you manually tune them as needed.
>?
>- The parameters expressed as “-” under **Initial Configuration** use the official image’s default configurations.
>- The `sysctl -w` command only makes the configurations take effect temporarily, while parameters wrote to `/etc/sysctl.conf` take effect permanently.


### Network-related
<table>
<tr>
<th>Parameter</th><th>Description</th><th>Initial Configuration</th>
</tr>
<tr>
<td><code>net.ipv4.tcp_tw_recycle</code></td>
<td>This parameter is used to quickly recycle the TIME_WAIT connection. If enabled, kernel will check the packet timestamp.<br>We do not recommend enabling this parameter, because packet loss may occur when the timestamp is not monotonically increasing. This parameter is disused in later kernel versions.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.core.somaxconn</code></td>
<td>This parameter is used to define the ESTABLISH state at the end of the three-way handshake when there is no ACCEPT queue. A longer ACCEPT queue indicates low processing rate of the client, or a burst of new connections in a short time. Setting <code>net.core.somaxconn</code> too low may cause packet loss because the new SYN connection will be discarded when the server receives SYN packet and the somaxconn table is full. Setting it too high is only necessary for high concurrence service, but the latency may increase.
</td>
<td>128</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_max_syn_backlog</code></td>
<td>This parameter specifies the maximal number of connections in SYN_RECV queue, which was once used to defend the common synflood attacks. However, if <code>tcp_syncookies=1</code>, connections in SYN_RECV queue will exceed the upper limit.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_syncookies</code></td>
<td>This parameter is used to enable SYN Cookies, which prevents some SYN attacks. If enabled, the connections can still be established when the SYN queue is overflowed. However, SHA1 will be used to verify Cookies, which theoretically increases the CPU utilization.</td>
<td>1</td>
</tr>
<tr>
<td><code>net.core.rmem_default</code><br>
<code>net.core.rmem_max</code><br>
<code>net.ipv4.tcp_mem</code><br>
<code>net.ipv4.tcp_rmem</code>
</td>
<td>These parameters are used to configure the cache size of received data. Setting this too high may waste memory resources, while setting it too low may cause packet loss. You can tune them according to the concurrence and throughput of your business.<ul><li>rmem_default: the theoretically optimal configuration is equal to the value of bandwidth divided by RTT, which will overwrite the configurations of tcp_rmem and tcp_rmem </li><li>rmem_max: approximately five times of rmem_default</li><li>tcp_mem: total TCP memory consumed, which is automatically set to to 3/32, 1/8 or 3/16 of the CVM’s available memory. The parameters tcp_mem and rmem_default also determine the maximum number of concurrent connections.</li></ul></td>
<td><code>rmem_default<br>=655360</code><br>
<code>rmem_max<br>=3276800</code></td>
</tr>
<tr>
<td><code>net.core.wmem_default</code><br>
<code>net.core.wmem_max</code><br>
<code>net.ipv4.tcp_wmem</code>
</td>
<td>These parameters are used to configure the data transmission cache. Data sending on Tencent Cloud usually does not have bottlenecks, so these configurations are optional.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.tcp_keepalive_intvl</code><br>
<code>net.ipv4.tcp_keepalive_probes</code><br>
<code>net.ipv4.tcp_keepalive_time</code>
</td>
<td>These parameters are relevant to TCP Keepalive, which default to 75/9/7200. The default settings mean that the kernel will initiate detection when a TCP connection is idle for 7,200 seconds, and will send RST after 9 failed detections (each for 75 seconds). These values are too high for a server. You can adjust them to 30/3/1800 as needed.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.ip_local_port_range</code></td>
<td>This parameter is used to configure the available port range, which can be adjusted as needed.</td>
<td>-</td>
</tr>
<tr>
<td><code>tcp_tw_reuse</code></td>
<td>This parameter is used to reuse a socket in TIME-WAIT state for new TCP connections. This help you quickly restart links that use fixed ports, but may involve risks in the NAT-based network. Later kernel versions support values 0, 1, and 2 and configure it to 2.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.ip_forward</code><br>
<code>net.ipv6.conf.all.forwarding</code>
</td>
<td>This parameter is used to specify the IP forwarding. You can configure it to 1 in the Docker’s route forwarding scenario.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.ipv4.conf.default.rp_filter</code></td>
<td>This parameter is used to specify the reverse path validation rule of ENI on received data packets. Valid values include 0, 1 (recommended by RFC3704), and 2. The recommended configuration is a strict mode that can prevent DDoS attacks and IP spoofing acts.</td>
<td>-</td>
</tr>
<tr>
<td><code>net.ipv4.conf.default.accept_source_route</code></td>
<td>This parameter is used to specify whether to accept IP packets containing source routes, which is not allowed by default, as recommended on the CentOS website.</td>
<td>0</td>
</tr>
<tr>
<td><code>net.ipv4.conf.all.promote_secondaries</code><br>
<code>net.ipv4.conf.default.promote_secondaries</code></td>
<td>This parameter is used to specify whether a secondary IP address will become a primary IP after the original primary IP address is deleted.</td>
<td>1</td>
</tr>
<tr>
<td><code>net.ipv6.neigh.default.gc_thresh3</code><br>
<code>net.ipv4.neigh.default.gc_thresh3</code>
</td>
<td>This parameter is used to define the maximum records stored in the ARP cache. The garbage collector immediately starts once the stored records exceed the set value.</td>
<td>4096</td>
</tr>
</table>



### Memory-related

<table>
<tr>
<th>Parameter</th><th>Description</th><th>Initial Configuration</th>
</tr>
<tr>
<td><code>vm.vfs_cache_pressure</code></td>
<td>This controls the tendency of the kernel to reclaim the memory. At the default value of 100, the kernel will attempt to reclaim dentries back to memory. The curl-based services usually accumulate dentries, which may use up all the free memory and cause OOM or kernel bug. We configure it to 250 to balance the reclaiming frequency and performance, which is tunable.</td>
<td>250</td>
</tr>
<tr>
<td><code>vm.min_free_kbytes</code></td>
<td>This parameter is used to force the Linux MEM to keep a minimum number of kilobytes free memory for use by kernel threads. The value is automatically calculated according to the free physical memory (MEM) at startup by: 4*sqrt (MEM). When the server receives microbursts of packets, your server may become subtly broken and cause OOM. On a high-configuration server, we recommend configuring <code>vm.min_free_kbytes</code> at about 1% of the total memory by default.
</td>
<td>-</td>
</tr>
<tr>
<td><code>kernel.printk</code></td>
<td>This specifies the level for kernel’s printk printing function. The default configuration is five or above. </td>
<td>5 4 1 7</td>
</tr>
<tr>
<td><code>kernel.numa_balancing</code></td>
<td>This indicates that kernel can automatically move processes to the corresponding NUMA node, but it is actually ineffective and affects performance. You can try to enable it in the Redis use cases.</td>
<td>0</td>
</tr>
<tr>
<td><code>kernel.shmall</code><br>
<code>kernel.shmmax</code>
</td>
<td><ul><li>shmmax: defines the maximum size of a single shared memory segment (in bytes) a Linux process can allocate.</li><li>shmall: defines system-wide total amount of shared memory pages.</li></ul></td>
<td><code>kernel.shmmax<br>=68719476736</code><br>
<code>kernel.shmall<br>=4294967296</code>
</td>
</tr>
</table>

### Process-related
<table>
<tr>
<th>Parameter</th><th>Description</th><th>Initial Configuration</th>
</tr>
<tr>
<td><code>fs.file-max</code><br>
<code>fs.nr_open</code>
</td>
<td>They denote the maximum number of file-handles that the Linux kernel or a process can allocate, respectively.<ul><li>file-max: automatically configures to approximate 100,000/GB when OS starts.</li><li>nr_open: sets to the fixed value of 1048576, which limits the maximum open file handles in a user-mode environment. Generally, keep this value unchanged. To modify the maximum open file handles, configure the <code>ulimit -n</code> parameter in the /etc/security/limits.conf configuration file.</li></ul></td>
<td>
<code>ulimit -n=100001</code><br>
<code>fs.nr_open=1048576</code>
</td>
</tr>
<tr>
<td><code>kernel.pid_max</code></td>
<td>This specifies maximum processes in a system. The official image uses the default value of 32768, which can be adjusted as needed.</td>
<td>-</td>
</tr>
<tr>
<td><code>kernel.core_uses_pid</code></td>
<td>This determines whether the generated coredump filename will contain .PID.</td>
<td>1</td>
</tr>
<tr>
<td><code>kernel.sysrq</code></td>
<td>This enables you to operate on /proc/sysrq-trigger later.</td>
<td>1</td>
</tr>
<tr>
<td><code>kernel.msgmnb</code><br>
<code>kernel.msgmax</code>
</td>
<td>They defines the maximum size in bytes of a single message queue and the maximum allowable size in bytes of any single message in a message queue, respectively</td>
<td>65536</td>
</tr>
<tr>
<td><code>kernel.softlockup_panic</code></td>
<td>This controls whether the kernel will panic when a soft lockup is detected. If enabled, a vmcore will be generated based on the kdump configuration, which can be used to analyze the cause of soft lockup.</td>
<td>-</td>
</tr>
</table>


### IO-related
<table>
<tr>
<th>Parameter</th><th>Description</th><th>Initial Configuration</th>
</tr>
<tr>
<td><code>vm.dirty_background_bytes</code><br>
<code>vm.dirty_background_ratio</code><br>
<code>vm.dirty_bytes</code><br>
<code>vm.dirty_expire_centisecs</code><br>
<code>vm.dirty_ratio</code><br>
<code>vm.dirty_writeback_centisecs</code>
</td>
<td>These parameters are mainly used to configure the policy for IO being written back to the disk.<ul><li>dirty_background_bytes/dirty_bytes and dirty_background_ratio/dirty_ratio refer to the amount and percentage of system memory that can be filled with “dirty” pages, respectively. In general, the ratio will be specified.</li><li>dirty_background_ratio: refers to a percentage of dirty pages in the system memory (10% by default) at which the background kernel flush processes will start writing back to the disk. </li><li>dirty_ratio: refers to the absolute maximum amount of system memory that can be filled with dirty pages before everything must get committed to disk. When the system gets to this point, all new I/O blocks until dirty pages have been written to disk, causing long I/O pauses. The system will first get to the `vm.dirty_background_ratio` condition at which the flush processes will start asynchronous writeback, and applications continue writing. When the system gets to the specified value of ` vm.dirty_ratio`, OS will handle dirty pages synchronously, blocking applications.<br>
</li><li>vm.dirty_expire_centisecs: specifies how long dirty page can be in cache before it needs to be written. It is expressed in 100'ths of a second. Data which has been dirty in-memory for longer than this interval will be written out next time a flush process wakes up.</li><li>vm.dirty_writeback_centisecs: specifies how often kernel flush processes wake up. It is expressed in 100'ths of a second.</li></ul>
</td>
<td>-</td>
</table>
