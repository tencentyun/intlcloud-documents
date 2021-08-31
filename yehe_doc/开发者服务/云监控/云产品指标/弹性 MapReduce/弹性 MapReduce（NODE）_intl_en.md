## Namespace

Namespace=QCE/TXMR_NODE

## Monitoring Metrics

### Server - CPU

| Parameter | Metric Name | Unit | Description | Dimension |
| -------------------- | ------------------ | ------- | ------------------------------ | ----------------------------- |
| NodeCpuIdle          | CPU utilization_idle    | %       | Percentage of CPU idle time              | id4nodecpu, <br/>host4nodecpu |
| NodeCpuIrq           | CPU utilization_irq     | %       | Percentage of interrupts                       | id4nodecpu, <br/>host4nodecpu |
| NodeCpuNice          | CPU utilization_nice    | %       | Percentage of CPU utilization under the nice priority       | id4nodecpu, <br/>host4nodecpu |
| NodeCpuSteal         | CPU utilization_steal   | %       | Percentage of wait time by virtual CPUs for physical CPUs | id4nodecpu, <br/>host4nodecpu |
| NodeCpuSoftirq       | CPU utilization_softirq | %       | Percentage of CPU soft interrupts                 | id4nodecpu, <br/>host4nodecpu |
| NodeCpuGuest         | CPU utilization_guest   | %       | Percentage of time spent running virtual processors | id4nodecpu, <br/>host4nodecpu |
| NodeCpuSystem        | CPU utilization_system  | %       | CPU utilization in the kernel state              | id4nodecpu, <br/>host4nodecpu |
| NodeCpuUser          | CPU utilization_user    | %       | CPU utilization in the user state              | id4nodecpu, <br/>host4nodecpu |
| NodeCpuIowait        | CPU utilization_iowait  | %       | Percentage of CPU idleness due to process I/O waits       | id4nodecpu, <br/>host4nodecpu |
| NodeCpuLoad1m        | Load_1m            | - | 1-minute load                      | id4nodecpu, <br/>host4nodecpu |
| NodeCpuLoad5m        | Load_5m            | -       | 5-minute load                      | id4nodecpu, <br/>host4nodecpu |
| NodeCpuLoad15m       | Load_15m           | -       | 15-minute load                     | id4nodecpu, <br/>host4nodecpu |
| NodeCpuCountCpuCount | Number of cores\_cpu_count    | Count      | Number of CPU cores                       | id4nodecpu, <br/>host4nodecpu |

### Server - Memory

| Parameter | Metric Name | Unit | Description | Dimension |
| ---------------------------------- | -------------------------------- | ---- | ------------------------------ | ----------------------------------- |
| NodeMemMemtotal                    | Memory usage_MemTotal            | GB   | Total memory size                       | host4nodememory, <br/>id4nodememory |
| NodeMemMemfree                     | Memory usage_MemFree             | GB   | Total free memory size                   | host4nodememory, <br/>id4nodememory |
| NodeMemBuffers                     | Memory usage_Buffers             | GB   | Total memory size used by buffers        | host4nodememory, <br/>id4nodememory |
| NodeMemCached                      | Memory usage_Cached              | GB   | Total memory size used by the file cache           | host4nodememory, <br/>id4nodememory |
| NodeMemSwapcached                  | Memory usage_SwapCached          | GB   | Total swap memory size used by anonymous page writes       | host4nodememory, <br/>id4nodememory |
| NodeMemSwapfree                    | Memory usage_SwapFree            | GB   | Total available swap size                 | host4nodememory, <br/>id4nodememory |
| NodeMemAnonpages                   | Memory usage_AnonPages           | GB   | Total unmapped memory size                 | host4nodememory, <br/>id4nodememory |
| NodeMemSwaptotal                   | Memory usage_SwapTotal           | GB   | Total swap size                     | host4nodememory, <br/>id4nodememory |
| NodeMemDirty                       | Memory usage_Dirty               | GB   | Total memory size to be written to the disk         | host4nodememory, <br/>id4nodememory |
| NodeMemWriteback                   | Memory usage_Writeback           | GB   | Total memory size being written back to the disk       | host4nodememory, <br/>id4nodememory |
| NodeMemHard<br>warecorrupted       | Memory usage_HardwareCorrupted   | GB   | Total unavailable memory size due to memory hardware failure | host4nodememory, <br/>id4nodememory |
| NodeMemShmem                       | Memory usage_Shmem               | GB   | Total shared memory size         | host4nodememory, <br/>id4nodememory |
| NodeMemPercent<br>AvailablePercent | Percentage of used memory\_available\_percent | %    | Percentage of available memory size out of the total memory         | host4nodememory, <br/>id4nodememory |
| NodeMemPercent<br>UsedPercent      | Percentage of used memory\_used\_percent      | %    | Percentage of used memory size out of the total memory       | host4nodememory, <br/>id4nodememory |

### Server - Network

| Parameter | Metric Name | Unit | Description | Dimension |
| --------------------------------------------- | ----------------------------------------- | -------- | ------------------------------------------------------------ | ------------------------------------- |
| NodeNetworkTcp<br>ListenExtListendrops        | TCPLISTEN<br>Exceptions_ListenDrops            | Connections/s     | Number of incoming connections (SYN packets) dropped for any reason                   | host4nodenetwork, <br>id4nodenetwork  |
| NodeNetworkTcpListen<br>ExtListenoverflows    | TCPLISTEN<br>Exceptions_ListenOverflows        | Occurrences/s     | Number of occurrences where the upper limit of the Accept queue is exceeded after the last step of the three-way handshake is completed          | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpSyncookies<br>Syncookiesfailed  | TCPSyncookies_Syn<br/>cookiesFailed       | Packets/s     | Number of packets received with invalid SYN Cookie information                       | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpSyncookies<br>Syncookiesrecv    | TCPSyncookies_Syn<br/>cookiesRecv         | Packets/s     | Number of packets received with valid SYN Cookie information                       | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpSyncookies<br>Syncookiessent    | TCPSyncookies_Syn<br/>cookiesSent         | Packets/s     | Number of SYN/ACK packets sent through SYN Cookie                        | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpAbort<br>Tcpabortontimeout      | TCP connection exception Abort_TCPAbort<br>OnTimeout  | Connections/s     | Number of connections closed because the attempts of the retransmissions of various timers (RTO/PTO/keepalive) exceeded the upper limit | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpAbort<br>Tcpabortondata         | TCP connection exception Abort_TCPAbort<br>OnData     | Sockets/s     | Number of sockets closed due to receiving unknown data                          | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpAbort<br>Tcpabortonclose        | TCP connection exception Abort_TCPAbort<br>OnClose    | Sockets/s     | Number of sockets closed when the user-mode program has data in the buffer             | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpAbort<br>Tcpabortonmemory       | TCP connection exception Abort_TCPAbort<br>OnMemory   | Connections/s     | Number of connections closed due to memory issues                                     | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpAbort<br>Tcpabortonlinger       | TCP connection exception Abort_TCPAbort<br>OnLinger   | Connections/s     | Number of connections suspended in the lingering state after being closed                           | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpAbort<br>Tcpabortfailed         | TCP connection exception Abort_TCPAbortFailed         | Times/s     | Number of failed attempts to close connections                                       | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpState<br>Activeopens            | Established TCP connections<br/>_ActiveOpens             | Connections/s     | Number of actively established TCP connections                                        | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>StateCurrestab              | Established TCP connections<br/>_CurrEstab               | Connections/s     | Number of TCP connections currently established                                      | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpState<br>Passiveopens           | Established TCP connections<br/>_PassiveOpens            | Connections/s     | Number of passively established TCP connections                                        | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>StateAttemptfails           | Established TCP connections<br/>_AttemptFails            | Connections/s     | Number of connection establishment failures                                             | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>StateEstabresets            | Established TCP connections<br/>_EstabResets             | Connections/s     | Number of reset connections                                           | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>PacketStatInsegs            | TCP data packets<br/>_InSegs                    | Packets/s     | Number of received packets, including erroneous ones                         | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br/>PacketStatOutsegs          | TCP data packets<br/>_OutSegs                   | Packets/s     | Number of sent data packets                                             | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>PacketStatRetranssegs       | TCP data packets<br/>_RetransSegs               | Packets/s     | Number of received TCP packets                                             | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>PacketStatInerrs            | TCP data packets<br/>_InErrs                    | Packets/s     | Number of retransmitted packets                                                 | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>PacketStatOutrsts           | TCP data packets<br/>_OutRsts                   | Packets/s     | Number of sent RST packets                                              | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpPacketRate<br>Retranssegsrate   | TCP retransmission rate<br/>_RetransSegsRate           | %        | Retransmission rate at the TCP layer                                                 | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>PacketRateResetrate         | TCP retransmission rate<br/>_ResetRate                 | %        | RESET sending frequency                                               | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpPacket<br>RateInerrrate         | TCP retransmission rate<br/>_InErrRate                 | %        | Percentage of erroneous packets                                                   | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpTimeWaitTw                      | TCPTIME-WAIT_TW                           | Sockets/s     | Number of sockets ending the TIME_WAIT state after normal timeout              | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>TimeWaitTwkilled            | TCPTIME-WAIT_TWKilled                     | Sockets/s     | Number of sockets ending the TIME_WAIT state through the tcp_tw_recycle mechanism    | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpTime<br>WaitTwrecycled          | TCPTIME-WAIT_TWRecycled                   | Sockets/s     | Number of sockets ending the TIME_WAIT state through the tcp_tw_reuse mechanism      | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRtoStat<br>Tcptimeouts          | TCPRTO_TCPTimeouts                        | Timeouts/s     | Number of first RTO timer timeouts                                     | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRtoStat<br>Tcpspuriousrtos      | TCPRTO_TCPSpur<br/>iousRTOs               | Timeouts/s     | Number of spurious timeouts detected through the F-RTO mechanism                            | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRtoStat<br>Tcplossprobes        | TCPRTO_TCPLoss<br/>Probes                 | Packets/s     | Number of Tail Loss Probe (TLP) packets sent due to Probe Timeout (PTO)    | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRtoStat<br>Tcplossproberecovery | TCPRTO_TCPLoss<br/>ProbeRecovery          | Packets/s     | Number of lost packets just repaired by TLP probes                            | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRtoStat<br>Tcprenorecoveryfail  | TCPRTO_TCPReno<br>RecoveryFail            | Connections/s     | Number of connections that enter the Recovery phase and then undergo RTO (SACK option not supported by the opposite) | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRtoStat<br>Tcprenorecoveryfail  | TCPRTO_TCPReno<br>RecoveryFail            | Connections/s     | Number of connections that enter the Recovery phase and then undergo RTO (SACK option supported by the opposite)  | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRtoStat<br>Tcprenofailures      | TCPRTO_TCPReno<br>Failures                | Failures/s     | Number of connections that enter the TCP_CA_Disorder phase and then undergo RTO (SACK option not supported by the opposite) | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRtoStat<br>Tcpsackfailures      | TCPRTO_TCPSack<br>Failures                | Connections/s     | Number of connections that enter the TCP_CA_Disorder phase and then undergo RTO (SACK option supported by the opposite) | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>RtoStatTcplossfailures      | TCPRTO_TCPLoss<br>Failures                | Connections/s     | Number of connections that enter the TCP_CA_Loss phase and then undergo RTO timeout                 | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRto<br>ConstRtoalgorithm        | TCPRTO <br/>Constant_RtoAlgorithm             | Algorithms/s      | Number of delayed algorithms for forwarding unanswered objects                               | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>RtoConstRtomax              | TCPRTO <br/>Constant_RtoMax                   | Retransmissions/s      | Maximum number of retransmissions due to TCP delay                                         | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>RtoConstRtomin              | TCPRTO <br/>Constant_RtoMin                   | Retransmissions/s      | Minimum number of retransmissions due to TCP delay                                         | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRetrans<br>Tcplostretransmit    | TCP retransmissions<br/>_TCPLostRetransmit           | Retransmissions/s     | Number of SKB retransmissions due to loss                                          | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRetrans<br>Tcpfastretrans       | TCP retransmissions<br/>_TCPFastRetrans              | Retransmissions/s     | Number of fast SKB retransmissions                                              | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRetrans<br>Tcpforwardretrans    | TCP retransmissions<br/>_TCPForwardRetrans           | Retransmissions/s     | Number of regular SKB retransmissions                                            | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRetrans<br>Tcpslowstartretrans  | TCP retransmissions<br/>_TCPSlowStart<br>Retrans     | Retransmissions/s     | Number of SKB retransmissions with successful slow starts                                      | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcpRetrans<br>Tcpretransfail       | TCP retransmissions<br/>_TCPRetransFail              | Failures/s     | Number of failed retransmission attempts                                             | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkUdp<br>DgIndatagrams               | UDP datagrams<br/>_InDatagrams               | Datagrams/s     | Number of sent UDP datagrams                                        | host4nodenetwork, <br/>id4nodenetwork |
| INodeNetworkUdpDg<br>Outdatagrams             | UDP datagrams<br/>_OutDatagrams              | Datagrams/s     | Number of received UDP datagrams                                        | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkRwBytes<br>Eth0TransmitBytes       | ENI data receiving and sending rate<br>\_eth0-transmit_bytes | MB/s     | Volume of data sent by ENI                                               | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkPackets<br>Eth0ReceiveDrop         | ENI data packet rate<br>\_eth0-receive_drop       | Packets/s | Volume of data received and then dropped by ENI                                           | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkPackets<br>Eth0ReceiveErrs         | ENI data packet rate<br>\_eth0-receive_errs       | Packets/s | Volume of data failed to be received by ENI                                             | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkPackets<br>Eth0TransmitDrop        | ENI data packet rate<br>\_eth0-transmit_drop      | Packets/s | Volume of data sent and then dropped by ENI                                           | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkPackets<br>Eth0TransmitErrs        | ENI data packet rate<br>\_eth0-transmit_errs      | Packets/s | Volume of data failed to be sent by ENI                                           | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkPackets<br>Eth0TransmitPackets     | ENI data packet rate<br>\_eth0_transmit_packets   | Packets/s | Number of packets sent by ENI                                               | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>SocketTcpInuse              | TCP sockets<br/>\_TCP_inuse                | Count       | Number of TCP sockets in use (listening)                          | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>SocketTcpOrphan             | TCP sockets<br/>\_TCP_orphan                | Count       | Number of TCP connections waiting to be closed                                        | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetwork<br>TcpSocketTcpTw                 | TCP sockets<br/>\_TCP_tw                   | Count       | Number of TCP sockets to be destroyed                                       | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>SocketSocketsUsed           | TCP sockets<br/>\_sockets_used             | Count       | Number of users using TCP sockets                                       | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>SocketTcpAlloc              | TCP sockets<br/>\_TCP_alloc                | Count       | Number of TCP sockets allocated (established, obtained sk_buff)          | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>ConnectionStateEstablished  | TCP connection status<br/>_ESTABLISHED             | Count       | Number of TCP connections in the Established state                              | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>ConnectionStateSynSent      | TCP connection status<br/>_SYN-SENT                | Count       | Number of TCP connections in the SYN-SENT state                                 | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>ConnectionStateSynRecv      | TCP connection status<br/>\_SYN-RECV               | Count       | Number of TCP connections in the SYN-RECV state                                 | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>ConnectionStateClose        | TCP connection status<br/>\_CLOSE                  | Count       | Number of TCP connections in the CLOSE state                                    | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>ConnectionStateCloseWait    | TCP connection status<br/>\_CLOSE-WAIT             | Count       | Number of TCP connections in the CLOSE-WAIT state                               | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>ConnectionStateListen       | TCP connection status<br/>\_LISTEN                 | Count       | Number of TCP connections in the LISTEN state                                   | host4nodenetwork, <br/>id4nodenetwork |
| NodeNetworkTcp<br>ConnectionStateClosing      | TCP connection status<br/>\_CLOSING                | Count       | Number of TCP connections in the CLOSING state                                 | host4nodenetwork, <br/>id4nodenetwork |

### Server - Filehandle 

| Parameter | Metric Name | Unit | Description | Dimension |
| --------------------- | ------------------ | ---- | ------------------ | ------------------------------------------- |
| NodeFdFilefdAllocated | File handles_allocated | Count   | Number of allocated file handles | host4nodefilehandle, <br>id4nodefilehandle  |
| NodeFdFilefdMaximum   | File handles_maximum   | Count   | Maximum number of file handles   | host4nodefilehandle, <br/>id4nodefilehandle |

### Server - Process

| Parameter | Metric Name | Unit | Description | Dimension |
| ------------------------------------ | -------------------------------------- | ------- | ------------------ | ------------------------------------- |
| NodeIntrIntrTotal                    | System interrupts\_intr_total                   | Interrupts/s    | Number of system interrupts       | host4nodeprocess, <br>id4nodeprocess  |
| NodeSwitchesContext<br>SwitchesTotal | System context switches\_context_switches_total | Switches/s    | Number of system context switches | host4nodeprocess, <br/>id4nodeprocess |
| NodeProcsForksTotal                  | System processes\_forks_total                  | Processes/s    | Number of new system processes   | host4nodeprocess, <br/>id4nodeprocess |
| NodeProcsProcsRunning                | System processes\_procs_running                | Processes/s    | Number of running system processes   | host4nodeprocess, <br/>id4nodeprocess |
| NodeProcsProcsBlocked                | System processes\_procs_blocked                | Processes/s    | Number of blocked system processes   | host4nodeprocess, <br/>id4nodeprocess |
| NodeProcsProcsTotal                  | System processes\_procs_total                  | Processes/s    | Total number of system processes     | host4nodeprocess, <br/>id4nodeprocess |
| NodeAgentVersion<br>Agentversion     | Agent version\_AgentVersion               | version | Agent version       | host4nodeprocess, <br/>id4nodeprocess |

## Overview of the Parameters in Each Dimension

| Parameter Name | Dimension Name | Dimension Description | Format |
| ------------------------------ | ------------------- | ----------------------------- | -------------------------------------------- |
| Instances.N.Dimensions.0.Name  | id4nodecpu          | Dimension name of the EMR instance ID        | String-type dimension name, such as id4nodecpu         |
| Instances.N.Dimensions.0.Value | id4nodecpu          | Specific EMR instance ID               | Specific instance ID, such as emr-abcdef88          |
| Instances.N.Dimensions.1.Name  | host4nodecpu        | Dimension name of the node IP in the EMR instance  | String-type dimension name, such as host4nodecpu        |
| Instances.N.Dimensions.1.Name  | host4nodecpu        | Specific node IP in the EMR instance         | Specific node IP, such as 1.1.1.1              |
| Instances.N.Dimensions.0.Name  | id4nodememory       | Dimension name of the EMR instance ID       | String-type dimension name, such as id4nodememory      |
| Instances.N.Dimensions.0.Value | id4nodememory       | Specific EMR instance ID              | Specific instance ID, such as emr-abcdef88         |
| Instances.N.Dimensions.1.Name  | host4nodememory     | Dimension name of the node IP in the EMR instance | String-type dimension name, such as host4nodememory     |
| Instances.N.Dimensions.1.Name  | host4nodememory     | Specific node IP in the EMR instance        | Specific node IP, such as 1.1.1.1             |
| Instances.N.Dimensions.0.Name  | id4nodenetwork      | Dimension name of the EMR instance ID       | String-type dimension name, such as id4nodenetwork    |
| Instances.N.Dimensions.0.Value | id4nodenetwork      | Specific EMR instance ID              | Specific instance ID, such as emr-abcdef88          |
| Instances.N.Dimensions.1.Name  | host4nodenetwork    | Dimension name of the node IP in the EMR instance  | String-type dimension name, such as host4nodenetwork    |
| Instances.N.Dimensions.1.Name  | host4nodenetwork    | Specific node IP in the EMR instance         | Specific node IP, such as 1.1.1.1             |
| Instances.N.Dimensions.0.Name  | id4nodefilehandle   | Dimension name of the EMR instance ID        | String-type dimension name, such as id4nodefilehandle  |
| Instances.N.Dimensions.0.Value | id4nodefilehandle   | Specific EMR instance ID               | Specific instance ID, such as emr-abcdef88         |
| Instances.N.Dimensions.1.Name  | host4nodefilehandle | Dimension name of the node IP in the EMR instance  | String-type dimension name, such as host4nodefilehandle |
| Instances.N.Dimensions.1.Name  | host4nodefilehandle | Specific node IP in the EMR instance         | Specific node IP, such as 1.1.1.1             |
| Instances.N.Dimensions.0.Name  | id4nodeprocess      | Dimension name of the EMR instance ID        | String-type dimension name, such as id4nodeprocess    |
| Instances.N.Dimensions.0.Value | id4nodeprocess      | Specific EMR instance ID               | Specific instance ID, such as emr-abcdef88         |
| Instances.N.Dimensions.1.Name  | host4nodeprocess    | Dimension name of the node IP in the EMR instance  | String-type dimension name, such as host4nodeprocess    |
| Instances.N.Dimensions.1.Name  | host4nodeprocess    | Specific node IP in the EMR instance         | Specific node IP, such as 1.1.1.1             |

## Input Parameters

EMR (Node) supports querying monitoring data based on the following five combinations of dimensions. The values for the input parameters are as follows: 

**1. To query the metric monitoring data of Server - CPU, use the following input parameters:**
&Namespace=QCE/TXMR_NODE
&Instances.N.Dimensions.0.Name=id4nodecpu
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4nodecpu
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance

**2. To query the metric monitoring data of Server - Memory, use the following input parameters:**
&Namespace=QCE/TXMR_NODE
&Instances.N.Dimensions.0.Name=id4nodememory
&Instances.N.Dimensions.0.Value=EMR instance ID
&Instances.N.Dimensions.1.Name=host4nodememory
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance 

**3. To query the metric monitoring data of Server - Network, use the following input parameters:**
&Namespace=QCE/TXMR_NODE
&Instances.N.Dimensions.0.Name=id4nodenetwork
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4nodenetwork
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance

**4. To query the metric monitoring data of Server - Filehandle, use the following input parameters:**
&Namespace=QCE/TXMR_NODE
&Instances.N.Dimensions.0.Name=id4nodefilehandle
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4nodefilehandle
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance

**5. To query the metric monitoring data of Server - Process, use the following input parameters:**
&Namespace=QCE/TXMR_NODE
&Instances.N.Dimensions.0.Name= id4nodeprocess
&Instances.N.Dimensions.0.Value=EMR instance ID 
&Instances.N.Dimensions.1.Name=host4nodeprocess
&Instances.N.Dimensions.1.Value=Specific node IP in the EMR instance
