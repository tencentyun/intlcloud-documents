An intermediate server is an origin-pull server located at the intermediate layer between a business server (i.e., origin server) and a CDN edge server (or GCD edge server in GCD scenarios). When a user initiates a request, the request will reach the CDN edge server first. If the edge server does not have the required resource, it will initiate a resource request to the intermediate server. If the intermediate server does not have the resource, it will initiate a resource request to the origin server.

> To improve the acceleration result, starting on October 15, 2018, the intermediate server had been enabled for all newly connected domain names by default and cannot be manually disabled. After the intermediate source configuration was enabled by default, corresponding configuration item became hidden in the console.

## Configuration Guide
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page. Find the domain name you want to edit and click **Manage** in the "Operation" column.
![img](https://main.qcloudimg.com/raw/c2c5fa124f81a8056635cf83bec15182.png)
Click **Origin-Pull Configuration** and if you don't see the "Intermediate Server Configuration" module, **an intermediate server has been enabled for your domain name by default**. User requests will be converged to the intermediate server, which will perform origin-pulls in a unified manner, improving the CDN acceleration result and alleviating the access pressure on your origin server.
>For legacy connected domain names, if you see that the intermediate server configuration is disabled in **Origin-pull Configuration**, we recommend you manually enable this feature to improve the acceleration result. Once enabled, this configuration item will be hidden and cannot be disabled.

## Sample Case
- The user request will reach an edge server first. If the requested resource is missed on the edge server, the request will be forwarded to a parent node. If there is still a miss, the request will be forwarded to the origin server. The CDN architecture is as shown below:
![](https://main.qcloudimg.com/raw/bfe35d9aa2c3a959ecc10501835bc15c.png)
- The user request will reach an edge server first. If the requested resource is missed on the edge server, it will be pulled from the origin server directly. The CDN architecture is shown in the figure:
![](https://main.qcloudimg.com/raw/9698dfb085f6abeabc2aa7d3a05f41cb.png)

