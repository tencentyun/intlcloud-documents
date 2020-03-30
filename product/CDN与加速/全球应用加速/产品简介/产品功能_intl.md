Key features of GAAP include acceleration proxy configuration, origin server management, acceleration statistics collection, connection monitoring, and acquisition of real user IPs.
## Acceleration Proxy
- GAAP supports configuring an acceleration connection by target user region and origin server region. It will automatically select the most appropriate connection based on the target user region and origin server region to achieve the shortest and optimal path from user to origin server, delivering a smoother access experience. For more information on configuration, see [Access Management](https://intl.cloud.tencent.com/document/product/608/13765).
- TCP and UDP forwarding are supported.
- Forwarding of URL rules is supported for HTTP and HTTPS.
- One listener can be bound with multiple origin servers, and one connection can have multiple listeners created.
- Configuration and modification of forwarding rules are supported, which take effect in real time and do not affect online business.
- Flexible configuration of acceleration forwarding rules within an connection satisfies scenarios that need step-by-step beta test verification. For more information on configuration, see [Listener Management](https://intl.cloud.tencent.com/document/product/608/13764).

## Origin Server Management
- GAAP can manage massive amount of origin servers whose types are IP and domain name, and add them in batches.

## Statistics Collection
- GAAP can collect statistics of an acceleration connection such as its bandwidth, concurrence, packet loss, delay, and packet forwarding volume. Based on the statistics, you can flexibly adjust the capacity cap of an acceleration connection as needed. For more information, see [Statistics](https://intl.cloud.tencent.com/document/product/608/14425).

## Connection Monitoring
- GAAP supports monitoring connection and origin server status. It alerts you promptly to connection or origin server problems for easier and quicker troubleshooting. For more information, see [Access Cloud Monitoring](https://intl.cloud.tencent.com/document/product/608/17541).
