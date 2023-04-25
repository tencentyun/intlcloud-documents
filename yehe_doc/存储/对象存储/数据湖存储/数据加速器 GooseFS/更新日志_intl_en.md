The update history for GooseFS is described as follows. If you have any queries or suggestions, please [contact us](https://www.tencentcloud.com/contact-sales).

<table ><thead ><tr>
<th >Version</th><th >Update Date</th><th >Description</th><th >Download URL</th></tr>

</thead><tbody>

<tr>
<td>1.4.1</td>
<td>March 1, 2023</td>
<td><ul>
<li>Optimizations:<ol ><li>Supported clearing and viewing the list of incomplete files.</li>
<li>Optimized the locking granularity for the recursive metadata loading operation (loadmetadata -R).</li>
</ol></li>
<li>Bug fixes:<ol ><li>Fixed the issue where the status of the authentication flow and data flow was inconsistent during Flume data write.</li>
<li>Fixed the issue where deadlock occurred after writing large files exhausted client resources.</li>

</ol>
</ul>

</td>
<td><li>GooseFS: <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.1/release/goosefs-1.4.1-bin.tar.gz" >Click to download</a></li>
<li>GooseFS (Kona JDK Edition): <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.1/release/goosefs-1.4.1-bin-konajdk11.tar.gz" >Click to download</a></li>
<li>GooseFS client: <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.1/release/goosefs-client-1.4.1-bin.tar.gz" >Click to download</a></li>
<li>GooseFS client (Kona JDK Edition): <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.1/release/goosefs-client-1.4.1-bin-konajdk11.tar.gz" >Click to download</a></li>
<li>GooseFS-FUSE client: <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.1/release/goosefs-fuse-1.4.1-bin.tar.gz" >Click to download</a></li>
<li>GooseFS-FUSE client (Kona JDK Edition): <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.1/release/goosefs-fuse-1.4.1-bin-konajdk11.tar.gz" >Click to download</a></li>
</td>
</tr>


<tr>
<td>1.4.0</td>
<td>November 11, 2022</td>
<td><ul>
<li>New features:<ol ><li>Provided the file decompression feature, which is in beta test and available in Shanghai Auto-Driving Cloud Zone only.</li>
<li>Supported the temporary key management feature.</li>
<li>Supported hierarchical traversal for `distributedLoad`.</li>
<li>Supported downgraded read in GooseFS-FUSE.</li>
</ol></li>
<li>Optimizations:<ol ><li>Supported hierarchical traversal capabilities for distributedLoad in GooseFS to recursively pull the metadata in the specified directory.</li>
<li>Improved the sequential read performance of GooseFS-FUSE for large files.</li>
<li>Added the percentile duration monitoring for master query and RocksDB update to improve the monitoring sensitivity of the metadata service.</li>
<li>Reduced the cluster recovery time of GooseFS in HA mode to improve the cluster availability.</li>
<li>Updated the COSN dependency version. You can access buckets with metadata acceleration enabled over the native HDFS protocol, which improves the file operation performance in big data scenarios.</li>
<li>Simplified and optimized GooseFS configuration by removing unnecessary configuration items.</li>
<li>Simplified and optimized `listInfo` to improve the file listing performance.</li>
</ol></li>
<li>Bug fixes:<ol ><li>Fixed the issue where workers received a high number of invalid async block requests.</li>
<li>Optimized the processing logic of orphan blocks during worker reporting.</li>
</ol></li>
</ul>

</td>
<td><li>GooseFS: <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.0/release/goosefs-1.4.0-bin.tar.gz" >Click to download</a></li>
<li>GooseFS (Kona JDK Edition): <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.0/release/goosefs-1.4.0-bin-konajdk11.tar.gz" >Click to download</a></li>
<li>GooseFS client: <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.0/release/goosefs-client-1.4.0-bin.tar.gz" >Click to download</a></li>
<li>GooseFS client (Kona JDK Edition): <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.0/release/goosefs-client-1.4.0-bin-konajdk11.tar.gz" >Click to download</a></li>
<li>GooseFS-FUSE client: <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.0/release/goosefs-fuse-1.4.0-bin.tar.gz" >Click to download</a></li>
<li>GooseFS-FUSE client (Kona JDK Edition): <a href="https://downloads.tencentgoosefs.cn/goosefs/1.4.0/release/goosefs-fuse-1.4.0-bin-konajdk11.tar.gz" >Click to download</a></li>
</td>
</tr>

<tr>
<td>1.3.0</td>
<td>July 25, 2022</td>
<td><ul>
<li>New features:<ol ><li>Supported Kerberos authentication.</li>
<li>Supported access to buckets with <a href="https://www.tencentcloud.com/document/product/436/43305" >metadata acceleration</a> enabled by using native POSIX semantics.</li>
<li>Supported the LRU algorithm for the master node cache elimination policy to avoid frequent cache replacement.</li>
<li>Supported expired metadata cleanup for the master node.</li>
</ol></li>
<li>Optimizations:<ol ><li>Optimized the lock bottleneck problem for the GooseFS master node to greatly improve the master QPS and increase the performance by around 35%.</li>
<li>Supported concurrent formatting to improve the performance of GooseFS worker nodes.</li>
<li>Supported overwrite operations for the GooseFS-FUSE client.</li>
<li>Optimized the memory usage of the <code >ls</code> command in the GooseFS-FUSE client.</li>
<li>Optimized the performance of ListNamespace in the GooseFS HDFS client.</li>
</ol></li>
<li>Bug fixes:<ol ><li>Fixed RocksDB leaks and Core issues to avoid memory leaks.</li>
<li>Fixed the issue where ZooKeeper Curator mistakenly printed logs.</li>
<li>Fixed the issue of inaccurate UFS bandwidth reading.</li>
<li>Fixed the LostWorker issue caused by excessive log printing during DistributedLoad.</li>
</ol></li>
</ul>

</td>
<td><ul>
<li>GooseFS: <a href="https://downloads.tencentgoosefs.cn/goosefs/1.3.0/release/goosefs-1.3.0-bin.tar.gz" >Click to download</a></li>
<li>GooseFS (Kona JDK Edition): <a href="https://downloads.tencentgoosefs.cn/goosefs/1.3.0/release/goosefs-1.3.0-bin-konajdk11.tar.gz" >Click to download</a></li>
<li>GooseFS client: <a href="https://downloads.tencentgoosefs.cn/goosefs/1.3.0/release/goosefs-client-1.3.0-bin.tar.gz" >Click to download</a></li>
<li>GooseFS client (Kona JDK Edition): <a href="https://downloads.tencentgoosefs.cn/goosefs/1.3.0/release/goosefs-client-1.3.0-bin-konajdk11.tar.gz" >Click to download</a></li>
<li>GooseFS-FUSE client: <a href="https://downloads.tencentgoosefs.cn/goosefs/1.3.0/release/goosefs-fuse-1.3.0-bin.tar.gz" >Click to download</a></li>
<li>GooseFS-FUSE client (Kona JDK Edition): <a href="https://downloads.tencentgoosefs.cn/goosefs/1.3.0/release/goosefs-fuse-1.3.0-bin-konajdk11.tar.gz" >Click to download</a></li>
</ul>

</td>
</tr>

<tr>
<td>1.2.0</td>
<td>January 25, 2022</td>
<td><ul>
<li>New features:<ol ><li>Supported using GooseFS to upload logs to CLS.</li>
<li>Supported separated configuration of RocksDB by using Inode and Block metadata.</li>
<li>Added the hot switch capability in the GooseFS client to improve disaster recovery measures.</li>
<li>Added the infrastructure for certain full-linkage logs.</li>
</ol></li>
<li>Optimizations:<ol ><li>Optimized the high Raft failover latency.</li>
<li>Optimized the memory usage of the GooseFS HCFS client.</li>
</ol></li>
<li>Bug fixes:<ol ><li>Fixed the issue of journal disorder.</li>
<li>Fixed the gRPC issue caused by Ratis deadlock.</li>
<li>Fixed the incorrect HDFSUnderFileSystemFactory loading position.</li>
<li>Fixed the Log4j2 vulnerabilities.</li>
<li>Fixed ufsPath prefix check errors.</li>
</ol></li>
</ul>

</td>
<td><ul>
<li>GooseFS: <a href="https://cos-data-lake-release-1253960454.cos.ap-guangzhou.myqcloud.com/goosefs/1.2.0/release/goosefs-1.2.0-bin.tar.gz" >Click to download</a></li>
<li>GooseFS (Kona JDK Edition): <a href="https://cos-data-lake-release-1253960454.cos.ap-guangzhou.myqcloud.com/goosefs/1.2.0/release/goosefs-1.2.0-bin-with-konajdk11.tar.gz" >Click to download</a></li>
<li>GooseFS-FUSE client: <a href="https://cos-data-lake-release-1253960454.cos.ap-guangzhou.myqcloud.com/goosefs/1.2.0/release/goosefs-fuse-1.2.0-bin.tar.gz" >Click to download</a></li>
</ul>

</td>
</tr>

<tr>
<td>1.1.0</td>
<td>September 1, 2021</td>
<td><ul>
<li>New features:<ol ><li>Supported Ranger authentication (click <a href="https://cos-data-lake-release-1253960454.cos.ap-guangzhou.myqcloud.com/goosefs/extensions/ranger-plugin/1.0.0/release/ranger-goosefs-plugin-1.0.0.jar" >here</a> to download the Ranger plugin).</li>
<li>Supported concurrent listing.</li>
<li>Supported DistributedLoad directory atomicity.</li>
<li>Supported the namespace cache allowlist.</li>
<li>Supported imperceptible OFS scheme acceleration.</li>
</ol></li>
<li>Optimizations:<ol ><li>Added help commands for each subcommand in CLI.</li>
<li>Optimized the logic to check for namespace existence during table mounting.</li>
<li>Improved the monitoring of job workers and worker metrics.</li>
</ol></li>
<li>Bug fixes:<br>
Fixed the issue of DistributedLoad read bloat.</li>
</ul>

</td>
<td>This version is no longer maintained. Download the latest version.</td>
</tr>

<tr>
<td>1.0.0</td>
<td>June 1, 2021</td>
<td><ol ><li>Namespace-based read/write policy and TTL management.</li>
<li>Prefetch at Hive table and table partition levels.</li>
<li>Compatibility with paths of existing COSN users to achieve imperceptible acceleration.</li>
<li>Fluid integration with GooseFS.</li>
<li>CHDFS support integration.</li>
</ol></td>
<td>This version is no longer maintained. Download the latest version.</td>
</tr>

</tbody>
</table>

