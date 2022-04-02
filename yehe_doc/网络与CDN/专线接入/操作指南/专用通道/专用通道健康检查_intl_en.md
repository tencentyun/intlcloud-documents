You can modify configurations and bandwidths of and execute health checks for connected dedicated tunnels in the Direct Connect console. This document describes how to condut the health check of a 2.0 tunnel in the console.
>?For a shared connection, only the connection owner can modify the bandwidth of a dedicated tunnel.
>

## Prerequisites
- You have applied for a dedicated tunnel as instructed in [Creating a Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/216/19250).
- You have backed up the dedicated tunnel.

## Background
You can use BFD and NQA to conduct the health check for a dedicated tunnel of Tencent Cloud Direct Connect:
- BFD: BFD establishes a session between network devices to detect the bidirectional forwarding path between these devices. It reports messages periodically after the session is established. The path is considered to be faulty when no messages reported during the detection. The application using the path will receives the detection result. Currently, BFD can be used in a linkage with BGP route and static route.
![]()
- NQA: NQA pings the dedicated tunnel to detect whether it is connected or not. It helps you know the robustness of the tunnel in real time and locate the fault quickly.

## Tunnel health check
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/conn) and click **Dedicated Tunnels** on the left sidebar to access the **Dedicated Tunnels** page.
2. Click the name of the tunnel to check on the "Dedicated Tunnels" page.
![]()
3. Click **Edit** on the right of **Routing Modes** on the "Advanced Tunnels" tab of the tunnel details page.
5. Enable **Health Check**.
4. Configure the health check parameters.
![]()
<table>
<tr>
<th width="20%">Health Check Configuration Parameters</th>
<th width="30%">Description</th>
<th width="50%">Valid Range</th>
</tr>
<tr>
<td>Health Check Interval</td>
<td>The interval between two health checks.</td>
<td><ul><li>BFD: 1000 ms - 3000 ms, default value-1000 ms. </li><li>NQA: 1000 ms - 5000 ms, default value-2000 ms.</li></ul></td>
</tr>
<tr>
<td>Number of Failed Health Checks</td>
<td>Switch the route after the configured consecutive failed health checks.</td>
<td><ul><li>BFD：3 - 8, default value-3. </li><li>NQA：3 - 8, default value-5.</li></ul></td>
</tr>
</table>
>? 
> - You shall apply different methods to conduct health checks for dedicated tunnels using different routing modes. Currently, for the health check of dedicated tunnels using BGP routing mode, only BFD is applicable. For the health check of dedicated tunnels using static routing mode, BFD and NQA are both applicable.
>- You can switch BFD and NQA to conduct the health check of a dedicated tunnel using static routing mode. The health check will be executed with the method after switching.
>
6. Click **Save**.
