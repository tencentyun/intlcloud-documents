## What Is a Host Header?
A host header refers to the website domain name accessed at the origin server by a CDN node during origin-pull. Please make sure that the configured host header domain name can be accessed; otherwise, origin-pull may fail. The host header can be customized according to your business.
>- Origin server and host header: The IP/domain name configured at the origin server allows a CDN node to find the corresponding origin server during origin-pull. There can be multiple websites on the server, and the host header indicates on which website a resource resides.
>- According to applicable regulations, if an origin server uses a Tencent Cloud CVM抯 accelerated domain name, the domain name configured to be the host header should have completed ICP filing through Tencent Cloud.

## Configuration Guide
### Viewing the Configuration
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the domain name you want to edit and click **Manage** in the operation column.
 ![Domain name list](https://main.qcloudimg.com/raw/38fd074fba05c89ad53497ba3fb3266c.jpg)
3. At the bottom of the basic configuration page, you can view the host header configuration information.
 ![](https://main.qcloudimg.com/raw/650b683d8908042600b24d0d410a9b10.jpg)
By default, the host header of a sub-domain name is the configured accelerated domain name, while that of a wildcard domain name is the access domain name:
 - If the accelerated domain name connected is `www.test.com`, when a node sends an origin-pull request to a resource under this domain name, the host field in the request HTTP header is `www.test.com`.
 - If the accelerated domain name connected is a wildcard domain such as `*.test.com` and the access domain name is `abc.test.com`, then the host header is `abc.test.com`.

### Modifying a Host Header
You can click **Edit** in the origin configuration section on the same page to adjust the host header configuration. **Host header can be customized only for your own origin servers but not COS origin servers.**
![](https://main.qcloudimg.com/raw/13e522ee379e14a998a5be0e0b2daf47.jpg)
## Sample Case
The user access domain name is `www.test.com`, the origin server is configured as domain name `origin.test.com`, and the A record corresponding to `origin.test.com` is `1.1.1.1`.
The user request is: `http://www.test.com/1.jpg`.
1. If the configuration is as follows:
 ![](https://main.qcloudimg.com/raw/13e522ee379e14a998a5be0e0b2daf47.jpg)
By default, the host header is the accelerated domain name, and the actual request is sent to `1.1.1.1` during origin-pull.
The resource obtained is: `http://www.test.com/1.jpg`.
2. If the configuration is as follows:
 ![](https://main.qcloudimg.com/raw/0ea2184b08ddfc4ad54ec3467ea93bc2.jpg)
The host header is `origin.test.com`, and the actual request is sent to `1.1.1.1` during origin-pull.
The resource obtained is: `http://origin.test.com/1.jpg`.
