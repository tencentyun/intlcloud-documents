### Node - CPU

| Metric Name | Unit | Description |
| ----------------- | ---- | ------------------------------ |
| CPU utilization_idle    | %    | Percentage of CPU idle time               |
| CPU utilization_irq     | %    | Percentage of interrupts                       |
| CPU utilization_nice    | %    | Percentage of CPU utilization under nice priority       |
| CPU utilization_steal   | %    | Percentage of wait time by virtual CPUs for physical CPUs |
| CPU utilization_softirq | %    | Percentage of CPU soft interrupts                 |
| CPU utilization_guest   | %    | Percentage of time spent running virtual processors |
| CPU utilization_system  | %    | Percentage of CPU in kernel state              |
| CPU utilization_user    | %    | Percentage of CPU in user state              |
| CPU utilization_iowait  | %    | Percentage of CPU idleness due to process I/O waits       |
| Load_1m           | 1/s  | 1-minute load                      |
| Load_5m           | 1/s  | 5-minute load                      |
| Load_15m          | 1/s  | 15-minute load                    |
| Core count_cpu_count    | -   | Number of CPU cores                       |

 

### Node - MEMORY

| Metric Name | Unit | Description |
| ------------------------------ | ---- | ------------------------------ |
| Memory usage_MemTotal          | GB   | Total memory size                       |
| Memory usage_MemFree           | GB   | Total free memory size                   |
| Memory usage_MemAvailable      | GB   | Total available memory size                   |
| Memory usage_Buffers           | GB   | Total memory size used by buffers        |
| Memory usage_Cached            | GB   | Total memory size used by file cache           |
| Memory usage_SwapCached        | GB   | Total swap memory size used by anonymous page writes       |
| Memory usage_SwapFree          | GB   | Total available swap size                 |
| Memory usage_AnonPages         | GB   | Total unmapped memory size                 |
| Memory usage_SwapTotal         | GB   | Total swap size                     |
| Memory usage_Dirty             | GB   | Total memory size to write to disk         |
| Memory usage_Writeback         | GB   | Total memory size being written back to disk       |
| Memory usage_HardwareCorrupted | GB   | Total unavailable memory size due to memory hardware failure |
| Memory usage_Shmem             | GB   | Total shared memory size         |
| Memory utilization_available_percent | %    | Percentage of available memory size in total memory         |
| Memory utilization_used_percent      | %    | Percentage of used memory size in total memory       |

### Node - NETWORK

| Metric Name                             | Unit     | Description                                                     |
| ------------------------------------ | -------- | ------------------------------------------------------------ |
| TCPLISTEN exception_ListenDrops            | Connections/s     | Number of incoming connections (SYN packets) dropped for any reason per second                  |
| TCPLISTEN exception_ListenOverflows        | Occurrences/s     | Number of occurrences where the upper limit of the accept queue is exceeded per second after the last step of three-way handshake is completed          |
| TCPSyncookies_SyncookiesFailed       | Packets/s     | Number of packets received with invalid SYN cookie information per second                      |
| TCPSyncookies_SyncookiesRecv         | Packets/s     | Number of packets received with valid SYN cookie information per second                      |
| TCPSyncookies_SyncookiesSent         | Packets/s     | Number of SYN/ACK packets sent through SYN cookie per second                        |
| TCP connection exception Abort_TCPAbortOnTimeout   | Connections/s     | Number of connections closed per second because the attempts of retransmissions of various timers (RTO/PTO/keepalive) exceed the upper limit |
| TCP connection exception Abort_TCPAbortOnData      | Sockets/s     | Number of sockets closed per second due to unknown data received                          |
| TCP connection exception Abort_TCPAbortOnClose     | Sockets/s     | Number of sockets closed per second when the user-mode program has data in the buffer             |
| TCP connection exception Abort_TCPAbortOnMemory    | Connections/s     | Number of connections closed per second due to memory issues                                     |
| TCP connection exception Abort_TCPAbortOnLinger    | Connections/s     | Number of connections suspended in lingering state per second after being closed                           |
| TCP connection exception Abort_TCPAbortFailed      | Attempts/s     | Number of failed attempts to close connection per second                                     |
| TCP connection establishment_ActiveOpens              | Connections/s     | Number of actively established TCP connections per second                                       |
| TCP connection establishment_CurrEstab                | Connections/s     | Number of TCP connections currently established per second                                     |
| TCP connection establishment_PassiveOpens             | Connection/s     | Number of passively established TCP connections per second                                       |
| TCP connection establishment_AttemptFails             | Failures/s     | Number of connection establishment failures per second                                            |
| TCP connection establishment_EstabResets              | Connections/s     | Number of reset connections per second                                          |
| TCP packets_InSegs                     | Packets/s     | Number of received packets per second, including erroneous ones                         |
| TCP packets_OutSegs                    | Packets/s     | Number of sent data packets per second                                             |
| TCP packets_RetransSegs                | Packets/s     | Number of received TCP packets per second                                             |
| TCP packets_InErrs                     | Packets/s     | Number of retransmitted packets per second                                                 |
| TCP packets_OutRsts                    | Packets/s     | Number of sent RST packets per second                                              |
| TCP retransmission rate_RetransSegsRate            | %        | Retransmission rate at TCP layer                                                 |
| TCP retransmission rate_ResetRate                  | %        | RESET sending frequency                                               |
| TCP retransmission rate_InErrRate                  | %        | Percentage of erroneous packets                                                   |
| TCP TIME-WAIT_TW                     | Sockets/s     | Number of sockets ending the TIME_WAIT state after normal timeout per second             |
| TCP TIME-WAIT_TWKilled               | Sockets/s     | Number of sockets ending the TIME_WAIT state through the tcp_tw_recycle mechanism per second  |
| TCP TIME-WAIT_TWRecycled             | Sockets/s     | Number of sockets ending the TIME_WAIT state through tcp_tw_reuse mechanism per second      |
| TCP RTO_TCPTimeouts                  | Timeouts/s     | Number of first RTO timer timeouts per second                                     |
| TCP RTO_TCPSpuriousRTOs              | Timeouts/s     | Number of spurious timeouts detected through the F-RTO mechanism per second                           |
| TCP RTO_TCPLossProbes                | Packets/s     | Number of Tail Loss Probe (TLP) packets sent per second due to Probe Timeout (PTO)   |
| TCP RTO_TCPLossProbeRecovery         | Packets/s     | Number of lost packets repaired by TLP packets per second                           |
| TCP RTO_TCPRenoRecoveryFail          | Connections/s     | Number of connections that enter the Recovery phase and then undergo RTO per second (SACK option not supported by the peer) |
| TCP RTO_TCPSackRecoveryFail          | Connections/s     | Number of connections that enter the Recovery phase and then undergo RTO per second (SACK option supported by the peer)  |
| TCP RTO_TCPRenoFailures              | Connections/s     | Number of connections that enter the TCP_CA_Disorder phase and then undergo RTO per second (SACK option not supported by the peer) |
| TCP RTO_TCPSackFailures              | Connections/s     | Number of connections that enter the TCP_CA_Disorder phase and then undergo RTO per second (SACK option supported by the peer) |
| TCP RTO_TCPLossFailures              | Connections/s     | Number of connections that enter the TCP_CA_Loss phase and then undergo RTO per second                |
| TCP RTO constant_RtoAlgorithm             | -      | Number of delayed algorithms for forwarding unanswered objects                               |
| TCP RTO constant_RtoMax                   | -      | Maximum number of retransmissions due to TCP delay                                         |
| TCP RTO constant_RtoMin                   | -      | Minimum number of retransmissions due to TCP delay                                         |
| TCP retransmissions_TCPLostRetransmit            | Retransmissions/s     | Number of SKB retransmissions per second due to loss                                         |
| TCP retransmissions_TCPFastRetrans               | Retransmissions/s     | Number of fast SKB retransmissions per second                                              |
| TCP retransmissions_TCPForwardRetrans            | Retransmissions/s     | Number of regular SKB transmissions per second                                           |
| TCP retransmissions_TCPSlowStartRetrans          | Retransmissions/s     | Number of SKB retransmissions with successful slow start per second                                     |
| TCP retransmissions_TCPRetransFail               | Failures/s     | Number of retransmission failures per second                                            |
| UDP datagrams_OutDatagrams               | Datagrams/s     | Number of sent UDP datagrams per second                                      |
| UDP datagrams_InDatagrams                | Datagrams/s     | Number of received UDP datagrams per second                                        |
| ENI data receiving/sending rate_eth0-receive_bytes  | MB/s     | Volume of data received by ENI per second                                               |
| ENI data receiving/sending rate_eth0-transmit_bytes | MB/s     | Volume of data sent by ENI per second                                               |
| ENI packet rate_eth0-receive_drop       | Packets/s | Data packets received and then dropped by ENI per second                                          |
| ENI packet rate_eth0-receive_errs       | Packets/s | Data packets failed to be received by ENI per second                                            |
| ENI packet rate_eth0-transmit_drop      | Packets/s |  Data packets sent and then dropped by ENI per second                                          |
| ENI packet rate_eth0-transmit_errs      | Packets/s | Data packets failed to be sent by ENI per second                                          |
| ENI packet rate_eth0-transmit_packetsl  | Packets/s | Number of packets sent by ENI per second                                              |
| TCP sockets_TCP_inuse                  | -       | Number of TCP sockets in use (listening)                          |
| TCP sockets_TCP_orphan                 | -       | Number of TCP connections to be closed                                        |
| TCP sockets_TCP_tw                     | -       | Number of TCP sockets to be destroyed                                       |
| TCP sockets_TCP_alloc                  | -       | Number of TCP sockets allocated (established, sk_buff obtained)          |
| TCP connection state_ESTABLISHED              | -       | Number of TCP connections in the Established state                              |
| TCP connection state_SYN-SENT                 | -       | Number of TCP connections in the SYN-SENT state                                 |
| TCP connection state_SYN-RECV                 | -       | Number of TCP connections in the SYN-RECV state                                 |
| TCP connection state_CLOSE                    | -       | Number of TCP connections in the CLOSE state                                    |
| TCP connection state_CLOSE-WAIT               | -       | Number of TCP connections in the CLOSE-WAIT state                               |
| TCP connection state_LISTEN                   | -       | Number of TCP connections in the LISTEN state                                   |


### Node - Disk

| Metric Name | Unit | Description |
| -------------------------------- | ---- | --------------------------------- |
| Device read/write rate_read_all            | MB/s | Data read per second                      |
| Device read/write rate_write_all           | MB/s | Data written per second                      |
| Device IOPS_all                     | -   | Number of I/O operations in progress on the current device      |
| IO operation time_read_all              | ms   | Average wait time per device I/O read operation |
| IO operation time_write_all             | ms   | Average wait time per device I/O write operation |
| IO operation time_io_all                | ms   | Average processing time per I/O request        |
| Device read/write QPS_read_all         | Queries/s | Read QPS                        |
| Device read/write QPS_write_all        | Queries/s | Write QPS                        |
| Device read/write QPS_merged_read_all  | Queries/s | Merged read QPS                    |
| Device read/write QPS_merged_write_all | Queries/s | Merged write QPS                    |
| IO device utilization_all                 | %    | Disk busyness                      |
| Disk space_free_all                | GB   | Free disk space                    |
| Disk space_used_all          | GB   | Used disk space                  |
| Disk space_total_all               | GB   | Total disk space                        |
| Disk utilization_used_all          | %    | Disk utilization                      |
| Inodes_free_all                | -   | Number of remaining disk inodes              |
| Inodes_total_all               | -   | Total number of disk inodes                |
| Inode utilization_used_all            | %    | Disk inode utilization                |

 

### Node - File Handle

| Metric Name           | Unit | Description           |
| ------------------ | ---- | ------------------ |
| File handles_allocated | -   | Number of allocated file handles |
| File handles_maximum   | -   | Maximum number of file handles   |

### Node - Process

| Metric Name                              | Unit    | Description           |
| ------------------------------------- | ------- | ------------------ |
| System interrupts _intr_total                   | Interrupts/s    | Number of system interrupts per second      |
| System context switches_context_switches_total | Switches/s    | Number of system context switches per second |
| System processes_forks_total                  | Processes/s    | Number of new system processes per second  |
| System processes_procs_running                | Processes/s    | Number of running system processes per second  |
| System processes_procs_blocked                | Processes/s    | Number of blocked system processes per second  |
| System processes_procs_total                  | Processes/s    | Total number of system processes per second    |
| Agent version_AgentVersionl               | version | Agent version       |

 

 
