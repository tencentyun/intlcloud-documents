## Configuration Scenario

To control the source of access to your business resources, you can use the IP access limit feature in ECDN. By limiting the number of access requests to a node per second from a client IP, you can defend against high-frequency CC attacks and prevent hotlinking by malicious users.


>? If your application has been migrated to the CDN console, you can go to the console for operation by referring to [Content Delivery Network](https://intl.cloud.tencent.com/document/product/228).
## Configuration Guide

### Viewing configuration

Log in to the ECDN Console, select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. You will find the IP access frequency limit configuration in **Access Configuration**. It is disabled by default:
![](https://main.qcloudimg.com/raw/647b73c63e867b31dfc1116fec3225b0.png)

### Modifying configuration

#### 1. Modify the configuration

Enter the frequency threshold and click **OK** to enable IP access limit.
![](https://main.qcloudimg.com/raw/31592b3562913dd366d8c3fc88c8a6d4.png)
**Configuration description**

- After the configuration is enabled, a 514 error will be returned for requests that exceed the QPS limit. A low access frequency limit may impact the normal use of your business by high-frequency users. Configure the proper threshold according to your actual business conditions and use cases.
- IP access limit is effective for attacks from a single IP to a single node. If a malicious user uses a high number of IPs to attack nodes on your entire network, this feature is no longer applicable.

#### 2. Disable the configuration

You can switch to disable this feature. When the switch is off, this feature does not take effect in the production environment even if there is an existing configuration. When the switch is on, this configuration will take effect across the entire network:
![](https://main.qcloudimg.com/raw/66d7637604b7527fd0150d0cef15d051.png)

## Configuration Sample

Suppose the IP access limit for the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/30d356e02a66a4d70f321715cf4ae659.png)
The actual access status will be as follows:

1. If a user with client IP `1.1.1.1` requests the resource `http://www.test.com/1.jpg` for 10 times in one second, and all access requests are made to one server on ECDN cache node A, then 10 access logs will be generated on this server, 9 of which exceed the QPS limit, and the status code "514" will be returned.
2. If a user with client IP `2.2.2.2` requests the resource `http://www.test.com/1.jpg` twice in one second, and the access requests may be distributed to two ECDN cache nodes for processing due to network conditions, then each node will return the content normally.

