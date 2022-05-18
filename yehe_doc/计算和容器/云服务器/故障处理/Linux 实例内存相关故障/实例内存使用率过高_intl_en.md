## Error Description
The Linux CVM encounters memory issues, such as slow service response speed, CVM login failure, or Out of Memory (OOM).

## Possible Reasons
These issues may be caused by high memory utilization of the instance, i.e., memory utilization generally stays above 90%.


## Troubleshooting Approaches
1. Perform the [troubleshooting procedure](#ProcessingSteps) to check whether the memory utilization is too high.
2. See the [memory issue analysis](#OtherProcessingSteps) to find the causes of problems.

## Troubleshooting Procedure[](id:ProcessingSteps)
1. Follow the [directions](#RelatedOperations) to check whether the memory utilization is too high.
 - If yes, proceed to the next step.
 - If not, see the [memory issue analysis](#OtherProcessingSteps) to find the causes of problems.
2. Log in to the CVM, run the `top` command, and press **M** to check whether there are processes in the “RES” and “SHR” columns using much memory.
  - If not, proceed to the next step.
  - If yes, perform the operations as instructed in [process analysis](https://intl.cloud.tencent.com/document/product/213/32387) according to the process type.
3. Run the following command to check the shared memory utilization.
```
cat /proc/meminfo | grep -i shmem
```
The following information will appear:
![](https://main.qcloudimg.com/raw/269ca888f6f0232a63705b6f9fd578a8.png)
4. Run the following command to check the non-reclaimable slab memory utilization.
```
cat /proc/meminfo | grep -i SUnreclaim
```
The following information will appear:
![](https://main.qcloudimg.com/raw/9e6c84eb5bfb0be315fc39d1b768d168.png)
5. Run the following command to check if there are huge pages.
```
cat /proc/meminfo | grep -iE "HugePages_Total|Hugepagesize"
```
The following information will appear:
![](https://main.qcloudimg.com/raw/aae7ce06f7034c123c26ef92265b82ea.png)
 - If the `HugePages_Total` output is `0`, see the [memory issue analysis](#OtherProcessingSteps) to find the causes of problems.
 - If the `HugePages_Total` output is not `0`, there are huge pages. The huge page size equals to `HugePages_Total * Hugepagesize`. Check whether huge pages are configured by a malicious program, or if they are unnecessary, you can comment out the `vm.nr_hugepage` configuration item in the `/etc/sysctl.conf` file, and then run the `sysctl -p` command to abandon huge pages.

## Directions[](id:RelatedOperations)
### Viewing memory utilization
The `free` command output may vary with the Linux distributions, which is unreliable for calculating the memory utilization. Perform the following steps to view the memory utilization on the **Monitoring** page of the CVM console.
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index) and access the **Instances** page.
2. Click the **ID/Name** of the instance to enter its details page. Select the **Monitoring** tab.
3. View memory utilization in the **Memory Monitor** section.
![](https://main.qcloudimg.com/raw/4f9f423e6d9d460d1413ff0ead6c7e96.png)

### Calculating memory utilization
The memory utilization is the ratio of memory used to total memory, excluding the buffer and system cache. The calculation formula is as follows:
= `(Total - available)100% / Total`
= `(Total - (Free + Buffers + Cached + SReclaimable - Shmem)) * 100% / Total`
= `(Total - Free - Buffers - Cached - SReclaimable + Shmem) * 100% / Total`

The required parameters `Total`, `Free`, `Buffer`, `Cached`, `SReclaimable`, and `Shmem` can be obtained in `/proc/meminfo`. Below is an example of `/proc/meminfo`.
```plaintext
1. [root@VM_0_113_centos test]# cat /proc/meminfo 
2. MemTotal: 16265592 kB
3. MemFree: 1880084 kB
4. ......
5. Buffers: 194384 kB
6. Cached: 13647556 kB
7. ......
8. Shmem: 7727752 kB
9. Slab: 328864 kB
10. SReclaimable: 306500 kB
11. SUnreclaim: 22364 kB
12. ......
13. HugePages_Total: 0
14. Hugepagesize: 2048 kB
```
The parameters are described as follows:
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td><code>MemTotal</code></td>
<td>Total system memory</td>
</tr>
<tr>
<td><code>MemFree</code></td>
<td>Free memory</td>
</tr>
<tr>
<td><code>Buffers</code></td>
<td>Cached page used by block devices for reads/writes and file system metadata (such as SuperBlock)</td>
</tr>
<tr>
<td><code>Cached</code></td>
<td>Page cache, including <code>POSIX/SysV shared memory</code> and <code>shared anonymous mmap</code> of tmpfs
</td>
</tr>
<tr>
<td><code>Shmem</code></td>
<td>Including shared memory, tmpfs, etc.
</td>
</tr>
<tr>
<td><code>Slab</code></td>
<td>Memory allocated by the kernel slab memory allocator, which can be viewed using the <code>slabtop</code> command
</td>
</tr>
<tr>
<td><code>SReclaimable</code></td>
<td>Reclaimable slabs</td>
</tr>
<tr>
<td><code>SUnreclaim</code></td>
<td>Non-reclaimable slabs</td>
</tr>
<tr>
<td><code>HugePages_Total</code></td>
<td>Total number of huge pages</td>
</tr>
<tr>
<td><code>Hugepagesize</code></td>
<td>Size of a huge page</td>
</tr>
</table>

### Memory issue analysis[](id:OtherProcessingSteps)
If the problem persists, or an error shown below appears during your use of CVM, refer to the corresponding solutions:
- [Log Error “fork: Cannot allocate memory”](https://intl.cloud.tencent.com/document/product/213/40502)
- [VNC Login Error “Cannot allocate memory”](https://intl.cloud.tencent.com/document/product/213/40503)
- [Triggering Out of Memory When There is Available Memory](https://intl.cloud.tencent.com/document/product/213/40504) 
