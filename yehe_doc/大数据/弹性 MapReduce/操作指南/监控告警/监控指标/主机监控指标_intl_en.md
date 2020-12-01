

### Node-CPU

| Metric Name | Unit | Description |
| --------- | ---- | ------------------------------ |
| idle      | %    | Percentage of CPU idle time |
| irq       | %    | Percentage of interrupts |
| nice      | %    | Percentage of CPU utilization under nice priority |
| steal     | %    | Percentage of wait time by virtual CPUs for physical CPUs |
| softirq   | %    | Percentage of CPU soft interrupts |
| guest     | %    | Percentage of time spent running virtual processors |
| system    | %    | CPU utilization in kernel state |
| user      | %    | CPU utilization in user state |
| iowait    | %    | Percentage of CPU idleness due to process I/O waits |
| 1m        | Load/s  | 1-minute load                      |
| 5m        | Load/s  | 5-minute load                      |
| 15m       | Load/s  | 15-minute load                     |
| cpu_count | - | Number of CPU cores |

### Node-MEMORY

| Metric Name | Unit | Description |
| ----------------- | ---- | ------------------------------ |
| MemTotal          | GB   | Total memory size |
| MemFree           | GB   | Total free memory size |
| MemAvailable      | GB   | Total available memory size |
| Buffers           | GB   | Total memory size used by buffers |
| Cached            | GB   | Total memory size used by file cache |
| SwapCached        | GB   | Total swap memory size by anonymous page writes |
| SwapFree          | GB   | Total available swap size |
| AnonPages         | GB   | Total unmapped memory size |
| SwapTotal         | GB   | Total swap size |
| Dirty             | GB   | Total memory size to write to disk       |
| Writeback         | GB   | Total memory size being written back to disk       |
| HardwareCorrupted | GB   | Total unavailable memory size due to memory hardware failure |
| Shmem             | GB   | Total shared memory size         |
| available_percent | %    | Percentage of available memory size out of total memory |
| used_percent      | %    | Percentage of used memory size out of total memory    |

### Node-NETWORK

| Metric Name | Unit | Description |
| ---------------------- | -------- | ------------------------------------------------------------ |
| ListenDrops            | Connections/s     | Number of incoming connections (SYN packets) dropped for any reason |
| ListenOverflows        | Occurrences/s | Number of occurrences where the upper limit of the Accept queue is exceeded after the last step of three-way handshake is completed |
| SyncookiesFailed       | Packets/s | Number of packets received with invalid SYN Cookie information |
| SyncookiesRecv         | Packets/s | Number of packets received with valid SYN Cookie information |
| SyncookiesSent         | Packets/s     | Number of SYN/ACK packets sent through SYN Cookie                        |
| TCPAbortOnTimeout | Connections/s | Number of connection closed because the attempts of retransmissions of various timers (RTO/PTO/keepalive) exceed the upper limit |
| TCPAbortOnData         | Sockets/s     | Number of sockets closed due to unknown data received                          |
| TCPAbortOnClose        | Sockets/s     | Number of sockets closed when the user-mode program has data in the buffer             |
| TCPAbortOnMemory       | Connections/s     | Number of connections closed due to memory issues                                     |
| TCPAbortOnLinger | Connections/s | Number of connections suspended in lingering state after being closed |
| TCPAbortFailed         | Attempts/s     | Number of failed attempts to close connection                                       |
| ActiveOpens            | Connections/s     | Number of actively established TCP connections                                        |
| CurrEstab              | Connections/s     | Number of TCP connections currently established                                      |
| ActiveOpens            | Connections/s     | Number of passively established TCP connections                                        |
| AttemptFails           | Failures/s     | Number of connection establishment failures                                             |
| EstabResets            | Connections/s     | Number of reset connections                                           |
| InSegs  | Packets/s | Number of received packets, including erroneous ones |
| OutSegs                | Packet/s     | Number of sent data packets                                                 |
| RetransSegs            | Packets/s     | Number of received TCP packets                                             |
| InErrs                 | Packet/s     | Number of retransmitted packets                                                 |
| OutRsts                 | Packet/s     | Number of sent RST packets                                                 |
| RetransSegsRate        | %        | Retransmission rate at TCP layer                                                 |
| ResetRate              | %        | RESET sending frequency                                               |
| InErrRate              | %        | Percentage of erroneous packets                                                   |
| TW | Sockets/s     | Number of sockets ending TIME_WAIT state after normal timeout      |
| TWKilled               | Sockets/s     | Number of sockets ending TIME_WAIT state through tcp_tw_recycle mechanism      |
| TCPTimeWaitOverflow    | Sockets/s     | Number of TIME_WAIT sockets unable to be allocated due to limit exceeding               |
| TWRecycled             | Sockets/s     | Number of sockets ending TIME_WAIT state through tcp_tw_reuse mechanism      |
| TCPTimeouts            | Timeouts/s     | Number of first RTO timer timeouts                                     |
| TCPSpuriousRTOs        | Timeouts/s     | Number of spurious timeouts detected through F-RTO mechanism                            |
| TCPLossProbes          | Packets/s     | Number of Tail Loss Probe (TLP) packets sent due to Probe Timeout (PTO)      |
| TCPLossProbeRecovery   | Packets/s | Number of lost packets just repaired by TLP probes |
| TCPRenoRecoveryFail    | Connections/s | Number of connections that enter the Recovery phase and then undergo RTO (SACK option not supported by the opposite) |
| TCPSackRecoveryFail | Connections/s | Number of connections that enter the Recovery phase and then undergo RTO (SACK option supported by the opposite) |
| TCPRenoFailures        | Failures/s | Number of failures that enter the TCP_CA_Disorder phase and then undergo RTO (SACK option not supported by the opposite) |
| TCPSackFailures        | Failures/s | Number of failures that enter the TCP_CA_Disorder phase and then undergo RTO (SACK option supported by the opposite) |
| TCPLossFailures        | Connections/s | Number of connections that enter the TCP_CA_Loss phase and then undergo RTO timeout |
| RtoAlgorithm           | Algorithms/s | Number of delayed algorithms for forwarding unanswered objects |
| RtoMax                 | Retransmissions/s      | Maximum number of retransmissions due to TCP delay                                         |
| RtoMin                 | Retransmissions/s      | Minimum number of retransmissions due to TCP delay                                         |
| TCPLostRetransmit      | Retransmissions/s     | Number of SKB retransmissions due to loss                                          |
| TCPFastRetrans         | Retransmissions/s     | Number of fast SKB retransmissions                                              |
| TCPForwardRetrans      | Retransmissions/s     | Number of regular SKB transmissions                                              |
| TCPSlowStartRetrans    | Retransmissions/s     | Number of SKB retransmissions with successful slow start                                      |
| TCPRetransFail         | Failures/s     | Number of failed retransmission attempts                                             |
| OutDatagrams           | Datagrams/s     | Number of sent UDP datagrams                                        |
| InDatagrams            | Datagrams/s     | Number of received UDP datagrams                                        |
| eth0-receive_bytes     | MB/s     | Volume of data received by ENI                                               |
| eth0-transmit_bytes    | MB/s     | Volume of data sent by ENI                                               |
| eth0-receive_drop      | Packets/s | Volume of data received and then dropped by ENI                                               |
| eth0-receive_errs      | Packets/s | Volume of data failed to be received by ENI                                             |
| eth0-transmit_drop     | Packets/s | Volume of data sent and then dropped by ENI                                           |
| eth0-transmit_errs     | Packets/s | Volume of data failed to be sent by ENI                                          |
| eth0-transmit_packetsl | Packet/s | Number of packets sent by ENI                                               |
| TCP_inuse | - | Number of TCP sockets in use (listening) |
| TCP_orphan             | -       | Number of TCP connections waiting to be closed                                        |
| TCP_tw | - | Number of TCP sockets to be destroyed |
| TCP_alloc | - | Number of TCP sockets allocated (established, sk_buff obtained) |
| ESTABLISHED                           | -       | Number of TCP connections in Established state                                 |
| SYN-SENT               | -       | Number of TCP connections in SYN-SENT state                                 |
| SYN-RECV              | -       | Number of TCP connections in SYN-RECV state                                |
| FIN-WAIT1              | -       | Number of TCP connections in FIN-WAIT1 state                                |
| FIN-WAIT2              | -       | Number of TCP connections in FIN-WAIT2 state                                |
| TIME-WAIT              | -       | Number of TCP connections in TIME-WAIT state                                |
| CLOSE              | -       | Number of TCP connections in CLOSE state                                |
| CLOSE-WAIT               | -       | Number of TCP connections in CLOSE-WAIT state                                 |
| LAST-ACK                           | -       | Number of TCP connections in LAST-ACK state                                 |
| LISTEN                           | -       | Number of TCP connections in LISTEN state                                 |
| CLOSEING               | -       | Number of TCP connections in CLOSEING state                                 |

### Node-DISK

| Metric Name | Unit | Description |
| ----------- | ---- | ------------------------------- |
| Read        | MB/s | Data read per second                    |
| Write       | MB/s | Data written per second                    |
| vd-         | -   | Number of I/O operations in progress on current device      |
| Read        | ms   | Average wait time per device I/O read operation |
| Write       | ms   | Average wait time per device I/O write operation |
| IO          | ms   | Average processing time per I/O request |
| Read        | Queries/s | Read QPS                      |
| Write       | Queries/s | Write QPS                      |
| Merge-Read  | Queries/s | Merged read QPS                  |
| Merge-Write | Queries/s | Merged write QPS                  |
| vd-         | %    | Disk busyness                 |
| Free        | GB   | Free disk space                    |
| Used        | GB   | Used disk space                  |
| Total       | GB   | Total disk space                      |
| Used        | %    | Disk utilization                      |
| Free        | -   | Number of remaining disk inodes            |
| Total       | -   | Total number of disk inodes              |
| Used        | %    | Disk inode utilization              |

### Node-FILE HANDLE

| Metric Name | Unit | Description |
| --------- | ---- | ------------------ |
| allocated | - | Number of allocated file handles |
| maximum   | - | Maximum number of file handles |

### Node-PROCESS

| Metric Name | Unit | Description |
| ---------------------- | ------- | ------------------ |
| intr_total             | Interrupts/s    | Number of system interrupts       |
| context_switches_total | Switches/s    | Number of system context switches |
| forks_total | Processes/s | Number of new system processes |
| procs_running          | Processes/s    | Number of running system processes   |
| procs_blocked          | Processes/s    | Number of blocked system processes   |
| procs_total            | Processes/s    | Total number of system processes     |
| AgentVersionl          | version | Agent version       |
