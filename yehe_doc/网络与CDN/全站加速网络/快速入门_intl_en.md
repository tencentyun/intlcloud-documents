You can quickly use Enterprise Content Delivery Network (ECDN) service in the following steps.  
![](https://main.qcloudimg.com/raw/efc38b1772f7b12fa21e6388de73e88e.png)

## Activating ECDN
ECDN service is fully available and you can apply for the service in the [ECDN Console](https://console.cloud.tencent.com/dsa). If ECDN has been activated for your account, please directly go to step 2 [Creating a Distribution](#yuming).
You can activate ECDN as follows:

1. According to China's rules and regulations, a new user needs to complete identity verification before using ECDN. You can have your identity verified in the [Account Center](https://console.cloud.tencent.com/developer). In the "Root Account Information" section, please click **Submit for Verification** to verify your identity.
 ![](https://main.qcloudimg.com/raw/f4f9c571ccbc82912aab084315d36dff.png)
 >
>- For detailed directions, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).
>- Individual identity verification will be completed immediately after the application is submitted. Organizational identity verification takes about one business day to complete, and you will be notified through SMS after the verification is completed. You can submit a [ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=1&level2_id=41&level1_name=%E5%85%AC%E5%85%B1%E5%9F%BA%E7%A1%80%E7%B1%BB%E9%97%AE%E9%A2%98&level2_name=%E8%B4%A6%E5%8F%B7%E7%B1%BB) to query the identity verification progress.
2. If you have already completed identity verification, you can directly enter the [ECDN Console](https://console.cloud.tencent.com/dsa). Click **Billing Description** to view the product billing description and click **Activate Now** to activate the service.
 ![](https://main.qcloudimg.com/raw/df8fead92c1b97f550b83fe94c35b4e5.png)


<span id="yuming"></span>
## Creating a Distribution
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Name Management** on the left sidebar to enter the management page.
2. Click **Create Distribution**.
![](https://main.qcloudimg.com/raw/36265ae189909f1b34e1b393c1af607c.png)
3. Enter the domain name that needs to be accelerated as an **Acceleration Domain Name**.
4. Select an **Origin Server Type** and enter the origin server information. **The origin server type can only be "origin server IP" or "origin server domain".**
 - **Origin server IP:**
    - Default origin-pull configuration: the optimal origin-pull policy is used by default. In this mode, you can enter the origin server IP in the "Origin-pull Address" box (one IP per line; up to 32 IPs can be entered). You can set the port in `IP:Port` format, and the port number should be between 0 and 65536.
    - Advanced origin-pull configuration: if the origin server is an origin server IP, weighted origin-pull and primary/secondary origin-pull policies are supported. For more information on the configuration, please see [Advanced Origin-Pull Policies](https://intl.cloud.tencent.com/document/product/570/35821).
 -  **Origin server domain:**
 You can enter only one origin domain, which must be different from the acceleration domain name. You can set the port in `Host:Port` format, and the port number should be between 0 and 65536.
5. Select the origin-pull protocol, which is the transfer protocol used for communication between the edge server and origin server.
6. Configure caching rules. You can use the default configurations or modify them.
7. After the domain name is configured, click **Submit** to add it. After the domain name is added, the system will deploy relevant configurations on the backend, which will take effect in about 5 minutes.
![](https://main.qcloudimg.com/raw/c2414b82d62ca3644822ca4b7daa4e99.png) 

## Adding a CNAME Record
1. After the domain name is connected, the system will assign it a corresponding **CNAME** suffixed with `.dsa.dnsv1.com`. You can view it on the domain name management page.
![](https://main.qcloudimg.com/raw/2c23e8238a172a6961ab55f1b9725ab0.png)
2. You need to complete the CNAME configuration at your DNS service provider of the connected domain name. For more information on CNAME configuration, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/570/11134).
3. Check whether the CNAME of the domain name is effective: a CNAME record usually takes effect in 30 minutes, but the time varies by DNS service providers. You can also run the `ping` command to check whether the CNAME is effective. If a domain name suffixed with `.dsa.sp.spcdntip.com` or `.dsa.p23.tc.cdntip.com` is returned, the CNAME record has taken effect.