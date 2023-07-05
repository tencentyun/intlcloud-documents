
## Background
In order to resolve to related services in the business when you use a TKE custom image, you may have modified the DNS resolution order in the custom image or completely replace Tencent's DNS service with your self-built DNS.

## Operation Impact
The above operation may cause a failure to resolve to Tencent Cloud's official resource library when registering a node into the cluster, resulting in a high probability of a node initialization failure or network/storage component exception.
- Node initialization: The error "Failed to resolve address, dns may be changed" may be reported during node initialization.
- Network components: Network components such as IPAMD depend on Tencent Cloud's private network DNS to work properly. The failure to resolve to the Tencent Cloud resource library may result in the unavailability of network components.
- Storage components: Mount/Unmount of storage components such as CBS-CSI fail.

>? The installation of relevant components in the cluster depends on the Tencent Cloud resource library at:
> `nameserver 183.60.83.19`
> `nameserver 183.60.82.98`

## Solution
### Configuring Tencent Cloud DNS nameserver as the upstream of self-built DNS
We recommend you add the nameserver in the `/etc/resolv.conf` to the upstream of your self-built DNS server. Because some services rely on Tencent Cloud DNS resolution, if the nameserver is not set as the upstream of your self-built DNS, some services may not work properly. This document takes [BIND 9](https://www.isc.org/bind/) as an example to modify the configuration file and write the upstream DNS address into forwarders as shown below:
```yaml
options {
        forwarders {
                183.60.83.19;
                183.60.82.98;
        };
        ...
```
Within 24 hours after the above operation is completed, the automatic retry policy of the node initialization process will keep trying to perform the node initialization until it is resolved to the Tencent Cloud resource library. After 24 hours, you need to delete the nodes and recreate them. If the above solution does not work, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.

>! If the self-built DNS server and the request source are not in the same region, some Tencent domain names that don't support cross-region access may become invalid. 
