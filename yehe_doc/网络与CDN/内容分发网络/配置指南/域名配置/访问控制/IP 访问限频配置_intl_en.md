## Configuration Overview
To control the source of access to your business resources, you can use the IP access limit feature in CDN. By limiting the number of access requests to a node per second from a client IP, you can defend against high-frequency CC attacks and prevent hotlinking by malicious users.


## Configuration Guide
### Viewing the configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Access Control** tab to see the **IP Access Limit Configuration** section. It is disabled with no value set by default:
![](https://main.qcloudimg.com/raw/647b73c63e867b31dfc1116fec3225b0.png)

### Enabling the configuration

Toggle on the switch, set the threshold, and click **OK**.
![](https://main.qcloudimg.com/raw/15303948df14017a03ed7b5890c3673a.png)
**Configuration description**

+ After the configuration is enabled, a 514 error will be returned for requests that exceed the QPS limit. A low access frequency limit may impact the normal use of your business by high-frequency users. Configure a proper frequency limit according to your actual business conditions and use scenarios.
+ IP access limit is effective for attacks from a single IP to a single node. If a malicious user uses a high number of IPs to attack nodes on your entire network, this feature is no longer applicable.

### Disabling the configuration
You can toggle off the switch to disable this feature. When the switch is off, this feature does not take effect in the production environment even if there is an existing configuration. When the switch is on, this configuration will take effect across the entire network:
![](https://main.qcloudimg.com/raw/1f3c1893aed28e3845a1adaea9abf1d9.png)

> !If your acceleration domain name is configured for global acceleration, the IP access limit configuration will take effect globally. This configuration does not distinguish between requests from regions in and outside the Chinese mainland.

## Configuration Sample
The IP access limit for the acceleration domain name `www.test.com` is as the following:
![](https://main.qcloudimg.com/raw/0d78c86a122b3b58c35ca2ba8b3316b6.png)
Then the actual access will be as follows:
1. A user with the client IP `1.1.1.1` requests the resource `http://www.test.com/1.jpg` for 10 times in one second, and all access requests are made to one server on CDN cache node A. 10 access logs will be generated on this server, 9 of which exceed the QPS limit. The status code "514" will be returned.
2. A user with the client IP `2.2.2.2` requests the resource `http://www.test.com/1.jpg` twice in one second, and the access requests may be distributed to two CDN cache nodes for processing due to network conditions. Each node will return the content normally.

