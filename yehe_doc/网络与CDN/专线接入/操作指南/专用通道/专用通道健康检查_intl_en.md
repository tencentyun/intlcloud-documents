You can modify configurations and bandwidths of and execute health checks for connected dedicated tunnels in the Direct Connect console. This document describes how to condut the health check of a 2.0 tunnel in the console.
>?For a shared connection, only the connection owner can modify the bandwidth of a dedicated tunnel.
>

## Prerequisites
- You have applied for a dedicated tunnel as instructed in [Creating a Dedicated Tunnel](https://www.tencentcloud.com/document/product/216/19250).
- You have backed up the dedicated tunnel.

## Background
You can use BFD and NQA to conduct the health check for a dedicated tunnel of Tencent Cloud Direct Connect:
- BFD: BFD establishes a session between network devices to detect the bidirectional forwarding path between these devices. It reports messages periodically after the session is established. The path is considered to be faulty when no messages reported during the detection. The application using the path will receives the detection result. Currently, BFD can be used in a linkage with BGP route and static route.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/PzgE344_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230331174218.png)
- NQA: NQA pings the dedicated tunnel to detect whether it is connected or not. It helps you know the robustness of the tunnel in real time and locate the fault quickly.

## Configuring Health Check After a Tunnel Is Created
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/conn) and click **Exclusive virtual interface** in the left sidebar.
2. On the **Exclusive virtual interface** page, click the name of the tunnel for which you want to configure health check.
3. On the **Advanced configuration** tab of the tunnel details page, click **Edit** on the right of **Routing mode**.
4. Enable **Health check**.
5. Configure the health check parameters.
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
>- You shall apply different methods to conduct health checks for dedicated tunnels using different routing modes. Currently, for the health check of dedicated tunnels using the BGP routing mode, only BFD is applicable. For the health check of dedicated tunnels using the static routing mode, both BFD and NQA are applicable.
>- You can switch BFD and NQA to conduct the health check of a dedicated tunnel using static routing mode. The health check will be executed with the method after switching.
>
6. Click **Save**.


## Configuring Health Check When You Create a Tunnel
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/conn-exclusive) and click **Exclusive virtual interface** in the left sidebar.
2. Click **Create** on the **Dedicated tunnels** page. Then, specify the parameters on the **Basic configuration** tab, and specify other parameters and enable health check on the **Advanced configuration** tab as prompted.
This section describes how to configure the health check feature. For more information about other parameters, see [Exclusive Virtual Interface](https://intl.cloud.tencent.com/document/product/216/48574) or [Shared Dedicated Tunnel](https://intl.cloud.tencent.com/document/product/216/48575).
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
>- You shall apply different methods to conduct health checks for dedicated tunnels using different routing modes. Currently, for the health check of dedicated tunnels using the BGP routing mode, only BFD is applicable. For the health check of dedicated tunnels using the static routing mode, both BFD and NQA are applicable.
>- You can switch BFD and NQA to conduct the health check of a dedicated tunnel using static routing mode. The health check will be executed with the method after switching.
>
3. Click **Next**. Specify other parameters to create the tunnel.
