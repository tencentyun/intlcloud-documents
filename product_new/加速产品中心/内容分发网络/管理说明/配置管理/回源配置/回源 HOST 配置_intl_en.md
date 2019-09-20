## What Is a Host Header?
A host header refers to the website domain name accessed at the origin server by a CDN node during origin-pull. Please make sure that the configured host header domain name can be accessed properly; otherwise, origin-pull may fail. You can customize the host header based on your business conditions.
>- Origin server and host header: The IP/domain name configured at the origin server allows a CDN node to find the corresponding origin server during origin-pull. There can be multiple websites on the server, and the host header indicates on which website a resource resides.
>- According to applicable regulations, if an origin server is at an accelerated domain name of Tencent Cloud CVM, the domain name configured for the host header should have the ICP filing completed through Tencent Cloud.

## Configuration Guide
### Viewing the Configuration
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the row of the domain name to be edited and click **Manage** in the operation column.
 ![Domain name list](https://main.qcloudimg.com/raw/18a3dd6931e3fe4ea109f971e5afe410.png)
3. At the bottom of the basic configuration page, you can view the host header configuration information.
 ![](https://main.qcloudimg.com/raw/d4a2560be715caeccfab0894d6a8e175.png)
By default, the host header of a sub-domain name is the configured accelerated domain name, while that of a wildcard domain name is the access domain name:
 - If the accelerated domain name connected is `www.test.com`, when a node sends an origin-pull request to a resource under this domain name, the host field in the request HTTP header is `www.test.com`.
 - If the accelerated domain name connected is a wildcard domain such as `*.test.com` and the access domain name is `abc.test.com`, then the host header is `abc.test.com`.

### Modifying a Host Header
In the origin-pull configuration section, click **Edit** to adjust the host header configuration. **Host header can be customized only for your own origin servers but not COS origin servers.**
![](https://main.qcloudimg.com/raw/43f9b9cc952c77169d8eecda4f8fa6df.png)
## Configuration Case
The user access domain name is `www.test.com`, the origin server is configured as domain name `origin.test.com`, and the A record corresponding to `origin.test.com` is `1.1.1.1`.
The user requests is: `http://www.test.com/1.jpg`.
1. If the configuration is as follows:
 ![](https://main.qcloudimg.com/raw/43f9b9cc952c77169d8eecda4f8fa6df.png)
By default, the host header is the accelerated domain name, and the actual request is sent to `1.1.1.1` during origin-pull.
The resource obtained is: `http://www.test.com/1.jpg`.
2. If the configuration is as follows:
 ![](https://main.qcloudimg.com/raw/7b3821894aafae537a818ab862129cda.png)
The host header is `origin.test.com`, and the actual request is sent to `1.1.1.1` during origin-pull.
The resource obtained is: `http://origin.test.com/1.jpg`.
