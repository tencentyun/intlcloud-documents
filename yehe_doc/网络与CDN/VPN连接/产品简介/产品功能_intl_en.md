
## VPN gateway bandwidth limit
> Currently, VPN gateway for CCN does not support configuring bandwidth limit.
>
- VPN gateway bandwidth limit provides **monitoring** and **control** capabilities at **IP-gateway** granularity. The visualization helps network OPS personnel get a clear picture of the gateway traffic. The speed limiting capability at IP-gateway granularity helps block unhealthy traffic.
The gateway bandwidth limit has the following advantages:
 - It can accurately troubleshoot gateway exceptions to minimize network downtime. Using real-time traffic query and Top-N ranking features, it can analyze the source IP and its key metrics to quickly locate unhealthy traffic.
 - With **monitoring** and **control** capabilities at IP-gateway granularity as well as minute-level network traffic queries, it can efficiently identify unhealthy traffic that consumes the bandwidth. The bandwidth limit at IP-gateway granularity ensures the stable operation of key businesses.
 - With gateway traffic analysis capability for all traffic at all times, it helps minimize network costs. By means of QoS, it can limit the bandwidth of non-key businesses to reduce costs.
- For example, the gateway traffic of an enterprise surges on one morning. With intelligent gateway bandwidth limit, the OPS personnel can trace the IP that caused this surge based on a point in time. The gateway bandwidth limit features IP-gateway granularity to control the bandwidth from an IP to the gateway, blocking unhealthy traffic to protect key businesses.

## Traffic Alarms
You can customize traffic alarms for VPN connections. When a metric value exceeds its threshold, alarm notifications are sent to you automatically via emails and SMS message. Monitoring and alarm services are free of charge, helping you quickly locate problems.
- For more information about VPN gateway metrics, see [VPN Gateway Monitor Metrics](https://intl.cloud.tencent.com/document/product/248/12226)
- For more information about VPN tunnel metrics, see [VPN Tunnel Monitor Metrics](https://intl.cloud.tencent.com/document/product/248/12225)
- For more information about how to configure alarm policies, see [Setting Alarms](https://intl.cloud.tencent.com/document/product/1037/32699).

