### Node - CPU
<table>
<thead>
<tr>
<th width=15%>Title</th>
<th width=15%>Metric</th>
<th width=15%>Unit</th>
<th width=55%>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan=9>CPU utilization</td>
<td>idle</td>
<td> %</td>
<td>Percentage of CPU idle time</td>
</tr><tr>
<td>irq</td>
<td> %</td>
<td>Percentage of interrupts</td>
</tr><tr>
<td>nice</td>
<td> %</td>
<td>Percentage of CPU utilization under nice priority</td>
</tr><tr>
<td>steal</td>
<td> %</td>
<td>Percentage of wait time by virtual CPUs for physical CPUs</td>
</tr><tr>
<td>softirq</td>
<td> %</td>
<td>Percentage of CPU soft interrupts</td>
</tr><tr>
<td>guest</td>
<td> %</td>
<td>Percentage of time spent running virtual processors</td>
</tr><tr>
<td>system</td>
<td> %</td>
<td>CPU utilization in kernel mode</td>
</tr><tr>
<td>user</td>
<td> %</td>
<td>CPU utilization in user mode</td>
</tr><tr>
<td>iowait</td>
<td> %</td>
<td>Percentage of CPU idleness due to process I/O waits</td>
</tr><tr>
<td rowspan=3>Load</td>
<td>1m</td>
<td> %</td>
<td>1-minute load</td>
</tr><tr>
<td>5m</td>
<td> %</td>
<td>5-minute load</td>
</tr><tr>
<td>15m</td>
<td> %</td>
<td>15-minute load</td>
</tr><tr>
<td >Cores</td>
<td>cpu_count</td>
<td>-</td>
<td>Number of CPU cores</td>
</tr>
</tbody></table>

### Node - memory
<table>
<thead>
<tr>
<th width=20%>Title</th>
<th width=15%>Metric</th>
<th width=15%>Unit</th>
<th width=50%>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan=14>Memory utilization</td>
<td>MemTotal</td>
<td>GB</td>
<td>Total memory size</td>
</tr><tr>
<td>MemFree</td>
<td>GB</td>
<td>Total free memory size</td>
</tr><tr>
<td>MemAvailable</td>
<td>GB</td>
<td>Total available memory size</td>
</tr><tr>
<td>Buffers</td>
<td>GB</td>
<td>Total memory size used by buffers</td>
</tr><tr>
<td>Cached</td>
<td>GB</td>
<td>Total memory size used by file cache</td>
</tr><tr>
<td>SwapCached</td>
<td> GB</td>
<td>Total swap memory size by anonymous page writes</td>
</tr><tr>
<td>SwapFree</td>
<td> GB</td>
<td>Total available swap size</td>
</tr><tr>
<td>AnonPages</td>
<td> GB</td>
<td>Total unmapped memory size</td>
</tr><tr>
<td>SwapTotal</td>
<td>GB</td>
<td>Total swap size</td>
</tr><tr>
<td>Dirty</td>
<td>GB</td>
<td>Total memory size to write to disk</td>
</tr><tr>
<td>Writeback</td>
<td>GB</td>
<td>Total memory size being written back to disk</td>
</tr><tr>
<td>HardwareCorrupted</td>
<td>GB</td>
<td>Total unavailable memory size due to memory hardware failure</td>
</tr><tr>
<td>Shmem</td>
<td>GB</td>
<td>Total shared memory size</td>
</tr><tr>
<td>MemUsed</td>
<td>GB</td>
<td>Total used memory size</td>
</tr><tr>
<td rowspan=2>Percentage of used memory</td>
<td>available_percent	</td>
<td> %</td>
<td>Percentage of available memory size out of total memory</td>
</tr><tr>
<td>used_percent</td>
<td> %</td>
<td>Percentage of used memory size out of total memory	</td>
</tr>
</tbody></table>

### Node - disk 
<table>
<thead>
<tr>
<th width=20%>Title</th>
<th width=15%>Metric</th>
<th width=15%>Unit</th>
<th width=50%>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan=2>Device read/write rate</td>
<td>Read</td>
<td> MB/s</td>
<td>Data read per second</td>
</tr><tr>
<td>Write</td>
<td> MB/s</td>
<td>Data written per second	</td>
</tr>
<tr>
<td rowspan=1>Device IOPS</td>
<td>all</td>
<td>count/s</td>
<td>Number of I/O operations in progress on current device</td>
</tr>
<tr>
<td rowspan=3>I/O operation time</td>
<td>Read</td>
<td> ms</td>
<td>Average wait time per device I/O read operation</td>
</tr><tr>
<td>Write</td>
<td>ms</td>
<td>Average wait time per device I/O write operation	</td>
</tr><tr>
<td>	IO</td>
<td>ms</td>
<td>Average processing time per I/O request</td>
</tr>
<tr>
<td rowspan=4>Device read/write QPS</td>
<td>Read</td>
<td>count/s</td>
<td>Read QPS</td>
</tr><tr>
<td>Write</td>
<td>count/s</td>
<td>Write QPS</td>
</tr><tr>
<td>Merge-Read</td>
<td>count/s</td>
<td>Merged read QPS</td>
</tr><tr>
<td>Merge-Write</td>
<td>count/s</td>
<td>Merged write QPS</td>
</tr><tr>
<td rowspan=1>I/O device utilization</td>
<td>all</td>
<td>%</td>
<td>Disk busyness</td>
</tr><tr>
<td rowspan=3>Disk space</td>
<td>Free		</td>
<td> GB</td>
<td>Free disk storage space</td>
</tr><tr>
<td>Available</td>
<td>GB	</td>
<td>Available disk storage space (for unprivileged users)</td>
</tr><tr>
<td>Total</td>
<td>GB	</td>
<td>Total disk storage space</td>
</tr><tr>
<td rowspan=1>Disk space utilization</td>
<td>Used</td>
<td>%</td>
<td>Disk space utilization</td>
</tr><tr>
<td rowspan=2>INODES</td>
<td>	Free</td>
<td>-</td>
<td>Number of remaining disk inodes</td>
</tr><tr>
<td>Total</td>
<td>-</td>
<td>Total number of disk inodes</td>
</tr><tr>
<td rowspan=1>Inode utilization</td>
<td>Used</td>
<td>%</td>
<td>Disk inode utilization</td>
</tr>
</tbody></table>

### Node - file handle
<table>
<thead>
<tr>
<th width=20%>Title</th>
<th width=15%>Metric</th>
<th width=15%>Unit</th>
<th width=50%>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan=2>File handle</td>
<td>allocated</td>
<td>-	</td>
<td>Number of allocated file handles</td>
</tr><tr>
<td>maximum</td>
<td>-	</td>
<td>Maximum number of file handles</td>
</tr><tr>
<td >System interrupt	</td>
<td>intr_total</td>
<td>count/s</td>
<td>Number of system interrupts</td>
</tr><tr>
<td >System context switch	</td>
<td>context_switches_total</td>
<td>count/s</td>
<td>Number of system context switches</td>
</tr><tr>
<td rowspan=5>System process</td>
<td>forks_total</td>
<td>-	</td>
<td>Number of new system processes</td>
</tr><tr>
<td>	procs_running</td>
<td>-</td>
<td>Number of running system processes</td>
</tr><tr>
<td>procs_blocked		</td>
<td>-</td>
<td>Number of blocked system processes</td>
</tr><tr>
<td>procs_total</td>
<td>-</td>
<td>Total number of system processes</td>
</tr><tr>
<td>thrds_total</td>
<td>-</td>
<td>Total number of system threads</td>
</tr><tr>
<td>Agent version</td>
<td>AgentVersionl</td>
<td>version</td>
<td>Agent version</td>
</tr>
</tbody></table>	
		
### Node - network
<table>
<thead>
<tr>
<th width=22%>Title</th>
<th width=15%>Metric</th>
<th width=15%>Unit</th>
<th width=48%>Description</th>
</tr>
</thead>
<tr>
<td rowspan=2>TCP LISTEN exception</td>
<td>ListenDrops	</td>
<td>count/s</td>
<td>Number of incoming connections (SYN packets) dropped for any reason</td>
</tr><tr>
<td>ListenOverflows</td>
<td>	count/s	</td>
<td>Number of occurrences where the upper limit of the Accept queue is exceeded after the last step of three-way handshake is completed</td>
</tr><tr>
<td rowspan=3>TCPSyncookies</td>
<td>SyncookiesFailed</td>
<td>count/s</td>
<td>Number of packets received with invalid SYN Cookie information</td>
</tr><tr>
<td>SyncookiesRecv</td>
<td>	count/s	</td>
<td>Number of packets received with valid SYN Cookie information</td>
</tr><tr>
<td>SyncookiesSent</td>
<td>	count/s	</td>
<td>Number of SYN/ACK packets sent through SYN Cookie</td>
</tr><tr>
<td rowspan=6>TCP connection abort exception</td>
<td>TCPAbortOnTimeout</td>
<td>count/s</td>
<td>Number of connections closed because the attempts of retransmissions of various timers (RTO/PTO/keepalive) exceed the upper limit</td>
</tr><tr>
<td>	TCPAbortOnData</td>
<td>	count/s	</td>
<td>Number of sockets closed due to unknown data received</td>
</tr><tr>
<td>TCPAbortOnClose	</td>
<td>	count/s	</td>
<td>Number of sockets closed when the user-mode program has data in the buffer</td>
</tr><tr>
<td>TCPAbortOnMemory</td>
<td>count/s</td>
<td>Number of connections closed due to memory issues</td>
</tr><tr>
<td>TCPAbortOnLinger</td>
<td>	count/s	</td>
<td>Number of connections suspended in lingering status after being closed</td>
</tr><tr>
<td>TCPAbortFailed</td>
<td>	count/s	</td>
<td>Number of failed attempts to close connection</td>
</tr><tr>
<td rowspan=5>TCP connection establishment</td>
<td>ActiveOpens		</td>
<td>count/s</td>
<td>Number of actively established TCP connections</td>
</tr><tr>
<td>	CurrEstab</td>
<td>	count/s	</td>
<td>Number of TCP connections currently established</td>
</tr><tr>
<td>	PassiveOpens			</td>
<td>	count/s	</td>
<td>Number of passively established TCP connections</td>
</tr><tr>
<td>AttemptFails</td>
<td>count/s</td>
<td>Number of connection establishment failures</td>
</tr><tr>
<td>EstabResets		</td>
<td>	count/s	</td>
<td>Number of reset connections</td>
</tr>
<tr>
<td rowspan=5>TCP packet</td>
<td>InSegs</td>
<td>count/s</td>
<td>Number of received packets, including erroneous ones</td>
</tr><tr>
<td>OutSegs</td>
<td>	count/s	</td>
<td>Number of sent packets</td>
</tr><tr>
<td>RetransSegs</td>
<td>	count/s	</td>
<td>Number of received TCP packets</td>
</tr><tr>
<td>InErrs</td>
<td>count/s</td>
<td>Number of retransmitted packets</td>
</tr><tr>
<td>OutRsts		</td>
<td>	count/s	</td>
<td>Number of sent RST packets</td>
</tr>
<tr><td rowspan=3>TCP retransmission rate</td>
<td>RetransSegsRate</td>
<td>%</td>
<td>	Retransmission rate at TCP layer</td>
</tr><tr>
<td>ResetRate</td>
<td>	%	</td>
<td>RESET sending frequency</td>
</tr><tr>
<td>InErrRate</td>
<td>	%	</td>
<td>Percentage of erroneous packets</td>
</tr>
<tr><td rowspan=4>TCP TIME-WAIT</td>
<td>TW</td>
<td>count/s</td>
<td>Number of sockets ending TIME_WAIT status after normal timeout</td>
</tr><tr>
<td>TWKilled</td>
<td>count/s		</td>
<td>Number of sockets ending TIME_WAIT status through tcp_tw_recycle mechanism</td>
</tr><tr>
<td>TCPTimeWaitOverflow		</td>
<td>	count/s	</td>
<td>Number of TIME_WAIT sockets unable to be allocated due to limit exceeding</td>
</tr><tr>
<td>TWRecycled		</td>
<td>	count/s	</td>
<td>Number of sockets ending TIME_WAIT status through tcp_tw_reuse mechanism</td>
</tr>
<tr>
<td rowspan=9>	TCP RTO</td>
<td>TCPTimeouts	</td>
<td>count/s</td>
<td>Number of first RTO timer timeouts</td>
</tr><tr>
<td>TCPSpuriousRTOs	</td>
<td>count/s	</td>
<td>Number of spurious timeouts detected through F-RTO mechanism</td>
</tr><tr>
<td>TCPLossProbes	</td>
<td>count/s	</td>
<td>Number of Tail Loss Probe (TLP) packets sent due to Probe Timeout (PTO)</td>
</tr><tr>
<td>	TCPLossProbeRecovery		</td>
<td>count/s</td>
<td>Number of lost packets just repaired by TLP probes</td>
</tr><tr>
<td>TCPRenoRecoveryFail	</td>
<td>count/s</td>
<td>Number of connections that enter the Recovery phase and then undergo RTO (SACK option not supported by the opposite)</td>
</tr><tr>
<td>TCPSackRecoveryFail	</td>
<td>count/s</td>
<td>Number of connections that enter the Recovery phase and then undergo RTO (SACK option supported by the opposite)</td>
</tr><tr>
<td>TCPRenoFailures	</td>
<td>count/s</td>
<td>Number of failures that enter the TCP_CA_Disorder phase and then undergo RTO (SACK option not supported by the opposite)</td>
</tr><tr>
<td>TCPSackFailures	</td>
<td>count/s</td>
<td>Number of failures that enter the TCP_CA_Disorder phase and then undergo RTO (SACK option supported by the opposite)</td>
</tr><tr>
<td>TCPLossFailures</td>
<td>count/s</td>
<td>Number of connections that enter the TCP_CA_Loss phase and then undergo RTO timeout</td>
</tr><tr>
<td rowspan=3>TCP RTO constant</td>
<td>RtoAlgorithm</td>
<td>1/s	</td>
<td>Number of delayed algorithms for forwarding unanswered objects</td>
</tr><tr>
<td>RtoMax</td>
<td>1</td>
<td>Maximum number of retransmissions due to TCP latency</td>
</tr><tr>
<td>RtoMin</td>
<td>1</td>
<td>Minimum number of retransmissions due to TCP latency</td>
</tr><tr>
<td rowspan=5>TCP retransmission</td>
<td>TCPLostRetransmit</td>
<td>count/s</td>
<td>Number of SKB retransmissions due to loss</td>
</tr><tr>
<td>TCPFastRetrans</td>
<td>count/s</td>
<td>Number of fast SKB retransmissions</td>
</tr><tr>
<td>TCPForwardRetrans</td>
<td>count/s</td>
<td>Number of regular SKB retransmissions</td>
</tr><tr>
<td>TCPSlowStartRetrans</td>
<td>count/s</td>
<td>Number of SKB retransmissions with successful slow start</td>
</tr><tr>
<td>TCPRetransFail</td>
<td>count/s</td>
<td>Number of failed retransmission attempts</td>
</tr><tr>
<td rowspan=2>UDP datagram</td>
<td>OutDatagrams</td>
<td>count/s</td>
<td>Number of sent UDP datagrams</td>
</tr><tr>
<td>InDatagrams</td>
<td>count/s</td>
<td>Number of received UDP datagrams</td>
</tr><tr>
<td rowspan=2>ENI data receiving/sending rate</td>
<td>eth0-receive_bytes</td>
<td>MB/s</td>
<td>Volume of data received by ENI</td>
</tr><tr>
<td>eth0-transmit_bytes</td>
<td>MB/s</td>
<td>Volume of data sent by ENI</td>
</tr><tr>
<td rowspan=5>ENI packet receiving/sending rate</td>
<td>eth0-receive_drop	</td>
<td>count/s</td>
<td>Volume of data received and then dropped by ENI</td>
</tr><tr>
<td>eth0-receive_errs 		</td>
<td>count/s</td>
<td>Volume of data failed to be received by ENI</td>
</tr><tr>
<td>eth0-transmit_drop</td>
<td>count/s</td>
<td>Volume of data sent and then dropped by ENI</td>
</tr><tr>
<td>eth0-transmit_errs</td>
<td>count/s</td>
<td>Volume of data failed to be sent by ENI</td>
</tr><tr>
<td>eth0-transmit_packetsl</td>
<td>count/s</td>
<td>Number of packets sent by ENI</td>
</tr><tr>
<td rowspan=5>TCP socket</td>
<td>TCP_inuse		</td>
<td>-</td>
<td>Number of TCP sockets in use (listening)</td>
</tr><tr>
<td>TCP_orphan</td>
<td>-</td>
<td>Number of TCP connections waiting to be closed</td>
</tr><tr>
<td>TCP_tw</td>
<td>-</td>
<td>Number of TCP sockets to be terminated</td>
</tr><tr>
<td>TCP_alloc</td>
<td>-</td>
<td>Number of TCP sockets allocated (established, sk_buff obtained)</td>
</tr><tr>
<td>sockets_used</td>
<td>-</td>
<td>Total number of used sockets</td>
</tr><tr>
<td rowspan=11>TCP connection status</td>
<td>ESTABLISHED	</td>
<td>-</td>
<td>Number of TCP connections in Established status</td>
</tr><tr>
<td>SYN-SENT</td>
<td>-</td>
<td>Number of TCP connections in SYN-SENT status</td>
</tr><tr>
<td>SYN-RECV</td>
<td>-</td>
<td>Number of TCP connections in SYN-RECV status</td>
</tr><tr>
<td>FIN-WAIT1</td>
<td>-</td>
<td>	Number of TCP connections in FIN-WAIT1 status</td>
</tr><tr>
<td>FIN-WAIT2	</td>
<td>-</td>
<td>Number of TCP connections in FIN-WAIT2 status</td>
</tr><tr>
<td>TIME-WAIT</td>
<td>-</td>
<td>Number of TCP connections in TIME-WAIT status</td>
</tr><tr>
<td>	CLOSE</td>
<td>-</td>
<td>Number of TCP connections in CLOSE status</td>
</tr><tr>
<td>CLOSE-WAIT</td>
<td>-</td>
<td>Number of TCP connections in CLOSE-WAIT status</td>
</tr><tr>
<td>LAST-ACK</td>
<td>-</td>
<td>Number of TCP connections in LAST-ACK status</td>
</tr><tr>
<td>LISTEN</td>
<td>-</td>
<td>Number of TCP connections in LISTEN status</td>
</tr><tr>
<td>CLOSEING</td>
<td>-</td>
<td>Number of TCP connections in CLOSEING status</td>
</tr>
</table>

### Node - event
<table>
<thead>
<tr>
<th width=25%>Title</th>
<th width=20%>Metric</th>
<th width=10%>Unit</th>
<th width=45%>Description</th>
</tr>
</thead>
<tr>
<td >CPU utilization</td>
<td>used</td>
<td> %</td>
<td>1 - (percentage of CPU idle time)</td>
</tr><tr>
<td >15-minute CPU load</td>
<td>15m</td>
<td>-</td>
<td>15-minute load</td>
</tr><tr>
<td>1-minute CPU load</td>
<td>1m</td>
<td>-</td>
<td>1-minute load</td>
</tr><tr>
<td >5-minute CPU load		</td>
<td>	5m</td>
<td> -</td>
<td>5-minute load</td>
</tr><tr>
<td >Disk IOPS</td>
<td>all</td>
<td>-</td>
<td>Number of I/O operations in progress on current device</td>
</tr><tr>
<td>Disk I/O operation time</td>
<td>IO</td>
<td>-</td>
<td>Average processing time per I/O request</td>
</tr><tr>
<td >Disk space utilization		</td>
<td>	Used</td>
<td> -</td>
<td>Disk space utilization</td>
</tr><tr>
<td >Disk I/O device utilization</td>
<td>all</td>
<td>-</td>
<td>Disk busyness</td>
</tr><tr>
<td>Memory utilization</td>
<td>used_percent</td>
<td>-</td>
<td>Percentage of used memory size out of total memory</td>
</tr><tr>
<td >Outbound network traffic rate</td>
<td>*-transmit_bytes</td>
<td>-</td>
<td>Volume of data sent by ENI</td>
</tr><tr>
<td>Inbound network traffic rate</td>
<td>*-receive_bytes	</td>
<td>-</td>
<td>Volume of data received by ENI</td>
</tr><tr>
<td>TCP connections</td>
<td>CurrEstab	</td>
<td>-</td>
<td>Number of TCP connections currently established</td>
</tr>
</table>
