## Kernel Customization
Based on the long-term stable Linux Kernel version, TencentOS Server introduces new features applicable to cloud scenarios and improves the kernel performance and resolves major defects.

## Performance Optimizations for Container Scenarios
TencentOS Server is optimized for container scenarios, with enhanced isolation and optimized performance:
- meminfo, vmstat, cpuinfo, stat, and loadavg isolation.
- Sysctl isolation, such as tcp_no_delay_ack, tcp_max_orphans.
- Fixes bugs in file systems and networks.
- Fixes exceptions caused by reuse of connections in high-concurrence scenarios in IPVS mode.
- Fixes network glitches caused by excessive IPVS rules under high-spec nodes (with many CPU cores) in IPVS mode.
- Fixes network glitches caused when cAdvisor got stuck in the kernel state for too long while reading memcg in high-density container scenarios (many containers on a single node)
- Fixes network glitches caused by CPU load balancing in scenarios of high-spec nodes (with many CPU cores) and large pods (occupying many cores with high usage per core).
- Fixes the problem of periodic network jitter caused by TCP connection monitoring (for example, cAdvisor configuration is deployed separately to monitor TCP connection) in high-concurrency scenarios.
- Optimizes soft interrupt for receiving network packets to enhance network performance.

## Customized Container Features
### Isolated display of container resources
- Adds a host-level switch: TencentOS Server realizes a LXCFS-like feature in its kernel. Instead of deploying nodes in the LXCFS file system or modifying POD spec, you only need to run the `sysctl -w kernel.stats_isolated=1` command to enable a global switch on nodes, and then files such as `/proc/cpuinfo` and `/proc/meminfo` obtained will be isolated by container.
<dx-alert infotype="notice" title="">
The `kernel.stats_isolated` parameter is supported only by TencentOS Server 2.4 but not TencentOS Server 2.4 (TK4), 3.1, or above.
</dx-alert>
- Adds a container-level switch: TencentOS Server adds a container-level switch `kernel.container_stats_isolated` for special containers such as node monitoring component. When the host-level switch is enabled, you only need to run the `sysctl -w kernel.container_stats_isolated=0` command in the container startup script to disable the container-level switch, and then the host information will be obtained by reading files such as `/proc/cpuinfo` and `/proc/meminfo` in containers.

### Kernel parameter isolation
TencentOS Server isolates the following kernel parameters by namespace:
- `net.ipv4.tcp_max_orphans`
- `net.ipv4.tcp_workaround_signed_windows`
- `net.ipv4.tcp_rmem`
- `net.ipv4.tcp_wmem`
- `vm.max_map_count`

### Optimization of default container kernel parameters
TencentOS Server increases the default value of `net.core.somaxconn` in the container network namespace to 4096, thus preventing packet loss caused by a full SYN queue in high-concurrence situations.

## Performance Optimization
- TencentOS Server optimizes computing, storage, and network subsystems:
- Optimizes XFS memory allocation to resolve the XFS kmem_alloc failure alarm.
- Optimizes memory allocation for received network packets to resolve excessive memory usage when a large number of UDP packets are received.
- Limits the memory usage of the system page caches to maintain optimal service performance and prevent out-of-memory (OOM) errors.

## Software Packages
- The user-mode software package for TencentOS Server 2 is compatible with the latest CentOS 7, which can be used directly on TencentOS Server 2.4.
- The user-mode software package for TencentOS Server 3 is compatible with the latest RHEL 8, which can be used directly on TencentOS Server 3.1.
- The software packages can be updated and installed via Yellowdog Updater, Modified (YUM).
- Software packages in the Extra Packages for Enterprise Linux (EPEL) repository can be used after the epel-release package is installed via YUM.

## Defect Fixes
- The Kdump feature is provided in the event of an operating system crash.
- Kernel live patching is supported.

## Security Updates
TencentOS Server offers regular updates to enhance its security and features.
