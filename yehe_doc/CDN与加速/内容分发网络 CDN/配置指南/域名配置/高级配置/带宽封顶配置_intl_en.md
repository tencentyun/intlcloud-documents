
## Configuration Overview

Tencent Cloud CDN is a pay-as-you-go service. If you are concerned about excessive bandwidth usage and fee surges due to hotlinking by malicious users, you can set a bandwidth cap to control usage. This feature is only applicable to bill-by-bandwidth users.

Bandwidth cap configuration can detect the bandwidth generated in a statistical period (at a 5-minute granularity) and perform forced origin-pull according to the configuration or disable the CDN service (a 404 error will be returned for all requests) if the cap is exceeded. This will avoid incurring additional CDN acceleration fees.

>! The bandwidth cap configuration takes about 10 minutes to take effect, during which the consumption generated is charged.

## Configuration Guide
### Viewing the configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Advanced Configuration** tab to see the **Bandwidth Cap Configuration** section. It is disabled by default:
![](https://main.qcloudimg.com/raw/2dc4d64a3c1f4054471a31681c19765e.png)
### Modifying the configuration
#### 1. Modify the configuration
You can toggle on the switch to configure the bandwidth cap:
- For domain names with COS origins, returning a 404 error is the only option when the cap is reached.
- If the detected domain name bandwidth exceeds the cap, origin-pull or return of the 404 error for access needs to be implemented across the entire network node by node; therefore, there may be a certain delay for the configuration to take effect.

![](https://main.qcloudimg.com/raw/7520963775f790d2adaf588b9418bd7c.png)

#### 2. Disable the configuration
You can toggle off this feature directly. When it’s disabled, the configuration does not take effect in the production environment. If you toggle the switch on, the configuration will take effect across the entire network after the action is confirmed.
![](https://main.qcloudimg.com/raw/1a18d747e269347c90aa17f116601509.png)

#### 3. Add the region-specific configuration
If your acceleration domain name is configured for global acceleration and you want to configure acceleration in and outside the Chinese mainland with different bandwidth cap settings, you can click **Add Special Configuration**.
![](https://main.qcloudimg.com/raw/ee63c14e4bcbd38899e8d9c063499db9.png)

>!
>
>- Currently, region-specific configuration items cannot be deleted once added but can be disabled.


## Configuration Sample
If the bandwidth cap configuration of the acceleration domain name `cloud.tencent.com` is as follows:
![](https://main.qcloudimg.com/raw/772256e11f3c1c9a85ae9cc57315c4f6.png)
Then the actual access will be as follows:
If the bandwidth reaches 11 Gbps in the Chinese mainland and 4 Gbps outside the Chinese mainland, a 404 error will be returned for access requests from all users in the Chinese mainland, while users outside the Chinese mainland can still enjoy the acceleration service.

