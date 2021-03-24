## Configuration Overview
To control the source of access to your business resources, you can use the IP access limit feature in CDN. By limiting the number of access requests to a node per second from a client IP, you can defend against high-frequency CC attacks and prevent hotlinking by malicious users.

## Configuration Guide
### Viewing the configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Access Control** tab to find the **IP Access Limit Configuration** section. By default, it is disabled with no value set.
![](https://main.qcloudimg.com/raw/647b73c63e867b31dfc1116fec3225b0.png)

### Enabling the configuration
Toggle on the switch, set the frequency limit, and click **Confirm**.
![](https://main.qcloudimg.com/raw/31592b3562913dd366d8c3fc88c8a6d4.png)
**Configuration description**

+ After the configuration is enabled, a 514 error will be returned for requests that exceed the QPS limit. A low access frequency limit may impact the normal use of your business by high-frequency users. Configure a proper frequency limit according to your actual business conditions and use scenarios.
+ IP access limit is applied to accesses from a single IP. It cannot defense massive attacks.

### Disabling the configuration
You can toggle off this feature directly. In this case, existing configurations will not be applied to the production environment. 
![](https://main.qcloudimg.com/raw/66d7637604b7527fd0150d0cef15d051.png)

>!If your acceleration domain name is configured for global acceleration, the IP access limit will be applied to all global regions, and the configurations with regional differences do not work.

## Configuration Sample
The IP access limit for the acceleration domain name `www.test.com` is set to 1QPS, as shown below:
![](https://main.qcloudimg.com/raw/30d356e02a66a4d70f321715cf4ae659.png)
Then the actual access will be as follows:

1. A user (client IP `1.1.1.1`) sends 10 requests for the resource `http://www.test.com/1.jpg` in one second, and all access requests are directed to one server on CDN cache node A. 10 access logs will be generated on this server. In this case, 9 of the requests will get the 514 error due to the QPS limit.
2. A user (client IP `2.2.2.2`) sends two requests for the resource `http://www.test.com/1.jpg` in one second. These two quests may be distributed to two CDN cache nodes due to network conditions. Each node will return the content normally.

