You can quickly try out Enterprise Content Delivery Network (ECDN) in the following steps.  
![](https://main.qcloudimg.com/raw/ba38c3ab45bd2d376b37784afda44de8.svg)

## Activating ECDN
ECDN has been made fully available. You can apply for activating ECDN in the [ECDN Console](https://console.cloud.tencent.com/dsa). If ECDN has been activated for your account, please directly go to step 2. [Adding Domain Name Configuration](#yuming).
Activate ECDN as follows:

1. According to applicable rules and regulations, a new user needs to complete identity verification before using ECDN. In the [Account Center](https://console.cloud.tencent.com/developer), you can click **Submit Verification** under "Verification Info" to verify your identity.
 ![](https://main.qcloudimg.com/raw/6416b89ce540152ee336246ae406a23b.png)
 >
>- For detailed directions, please see [Identity Verification Guide](https://cloud.tencent.com/doc/product/378/3629).
>- Individual identity verification will be completed immediately after the application is submitted. Organizational identity verification takes about one business day to complete, and you will be notified through SMS after the verification is completed. You can submit a [ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=1&level2_id=41&level1_name=%E5%85%AC%E5%85%B1%E5%9F%BA%E7%A1%80%E7%B1%BB%E9%97%AE%E9%A2%98&level2_name=%E8%B4%A6%E5%8F%B7%E7%B1%BB) to query the identity verification progress.
2. If you have already completed identity verification, you can directly enter the [ECDN Console](https://console.cloud.tencent.com/dsa). Click **Product Billing Description** to view the product billing description and click **Activate Now** to activate the service.
 ![](https://main.qcloudimg.com/raw/7d35603a3a47f2d45ed7495ce7c15adb.png)
3. After successfully activating ECDN, click **OK** to enter the ECDN Console and use the ECDN service.
![](https://main.qcloudimg.com/raw/364038ff4e2afd4aba6c05d2dd650535.png)

<span id="yuming"></span>
## Adding Domain Name Configuration
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the management page.
2. Click **Add Domain Name**.
![](https://main.qcloudimg.com/raw/6a4e4954729548a1d5983bc4fba21857.png)
3. Enter the domain name that needs to be accelerated as **Acceleration Domain Name**.
4. Select **Origin Server Type** and enter the origin server information. **The origin server type can only be **origin IP** or **origin domain**.**
 - **Origin IP:**
    - Default origin-pull configuration: the optimal route selection origin-pull policy is used by default. In this mode, you can enter the origin IPs as "IP Address" (one per line; up to 32 IPs can be entered). You can set the port in `IP:Port` format, and the port number should be between 0 and 65536.
    - Advanced origin-pull configuration: if the origin server type is origin IP, weighted origin-pull and master/slave origin-pull policies are supported. For more information on the configuration, please see [Advanced Origin-Pull Policy Configuration Description](https://cloud.tencent.com/document/product/570/19915).
 -  **Origin domain:**
 You can enter only one origin domain, which must be different from the acceleration domain name. You can set the port in `Host:Port` format, and the port number should be between 0 and 65536.
5. Select the origin-pull protocol, which is the transfer protocol used for communication between the edge server and origin server.
6. Configure caching rules. You can use the default configurations or modify them.
7. After the domain name is configured, click **Submit** to add it. After the domain name is added, the system will deploy relevant configurations on the backend, which will take effect in about 5 minutes.
![](https://main.qcloudimg.com/raw/e21ce732356c7d45b70f6c351edb57ab.png) 

## Adding CNAME Record
1. After the domain name is connected, the system will assign it a corresponding **CNAME** record suffixed with `.dsa.dnsv1.com`. You can view it on the domain management page.
![](https://main.qcloudimg.com/raw/7d35d4feeb306c88316da6380db21aa7.png)
2. You need to complete the CNAME configuration at your DNS service provider of the connected domain name. For more information on how to configure a CNAME record, please see [CNAME Record Configuration](https://cloud.tencent.com/doc/product/570/11134).
3. Check whether the CNAME record of the domain name takes effect: the time it takes for a CNAME record to take effect varies by DNS service provider. You can also run the `ping` command to check whether the CNAME record is in effect. If a domain name suffixed with `.dsa.sp.spcdntip.com` or `.dsa.p23.tc.cdntip.com` is returned, the CNAME record has taken effect.