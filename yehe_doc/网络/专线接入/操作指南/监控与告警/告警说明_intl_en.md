This document describes the metric alarms and event alarms for connections and dedicated tunnels to help you configure alarm policies.

## Metric Alarms

You can use the `BandwidthOut`, `BandwidthIn`, and `dc_band_rate` metrics as the trigger conditions of metric alarms for a connection. The `BandwithOut` and `BandwidthIn` metrics also applies to metric alarms for a dedicated tunnel.

| Metric       | Description                              |
| ---------- | --------------------------------- |
| BandwidthOut     | Average outbound traffic of a connection/dedicated tunnel per second|
| BandwidthIn     | Average inbound traffic of a connection/dedicated tunnel per second |
| dc_band_rate | Current bandwidth/connection bandwidth * 100%    |

## Event Alarms

You can use the `DirectConnectDown` event as the trigger condition of event alarms for a dedication. You can use the `DirectConnectTunnelDown`, `DirectConnectTunnelBGPSessionDown`, `DirectConnectTunnelRouteTableOverload`, and `DirectConnectTunnelBFDDown` events as the trigger conditions of event alarms for a dedicated tunnel.

| Event Name | Event Parameter | Event Type | Dimension | Recoverable | Description | Troubleshooting Method |
| ------------------------ | ----------------------------------------- | -------- | ------------ | ---------------- | ------------------------------------ | ------------------------------------------------------------ |
| Connection downtime            | DirectConnectDown                     | Exception | Connection | Yes               | The physical link of the connection is interrupted or has an exception           | 1. Check whether the physical link has an exception or is interrupted (for example, the fiber cable is cut off, the line is unplugged, etc.).<br>2. Check whether the receiving port and optical/electrical modules are normal.<br>3.Check whether the network device port is closed. |
| Dedicated tunnel downtime            | DirectConnectTunnelDown                     | Exception | Dedicated tunnel | Yes               | The physical link of the connection is interrupted or has an exception           | 1. Check whether the physical link has an exception or is interrupted (for example, the fiber cable is cut off, the line is unplugged, etc.).<br>2. Check whether the receiving port and optical/electrical modules are normal.<br>3.Check whether the network device port is closed. |
| Dedicated tunnel BGP session downtime   | DirectConnectTunnelBGPSessionDown     | Exception | Dedicated tunnel | Yes               | The dedicated tunnel BGP session is interrupted            | 1. Check whether the BGP process of the network device is normal.<br>2. Check whether the dedicated tunnel is normal. <br>3. Check whether the physical line is normal. |
| Alarm for exceeded number of BGP tunnel routes | DirectConnectTunnelRouteTableOverload | Exception | Dedicated tunnel | No               | The number of BGP session routes in a dedicated tunnel exceeds 80% of the threshold | Check whether routes published by the BGP session of the dedicated tunnel have reached 80% of the maximum, which is 100 by default. For more information, see [Resource Limits](https://intl.cloud.tencent.com/document/product/216/546). |
| Dedicated tunnel BFD detection downtime   | DirectConnectTunnelBFDDown            | Exception | Dedicated tunnel | Yes               | The dedicated tunnel BFD detection is interrupted                | 1. Check whether the dedicated tunnel is normal.<br>2. Check whether the physical line is normal.       |

