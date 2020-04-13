
## Configuration Scenario
Generally, content delivered over CDN is public resource by default, which can be accessed by users with URLs. To prevent malicious users from hotlinking your content for profit, you can configure advanced timestamp authentication to avoid hotlinking, in addition to access control policies such as referer blacklist/whitelist, IP blacklist/whitelist, and IP access frequency limit.

>After timestamp hotlink protection is configured, the client needs to calculate the signature as configured and carry it to the server when initiating a request. The CDN node will authenticate the signature on the server, which will pass only after successful authentication.

## Configuration Guide
### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Security Configuration** tab, find the authentication configuration, which is disabled by default:
![](https://main.qcloudimg.com/raw/77831beaa25a77dd26b60e1f401c8dd3.png)

### Modifying configuration
#### 1. Modify the configuration
CDN provides four authentication signature calculation modes. You can open the **Calculator** at the top to view these modes and the configuration effects. For more information on the algorithms, please see the specific documents below:
![](https://main.qcloudimg.com/raw/ffd60184fa759b4c7a82a5a49634b8c3.png)

#### 2. Disable the configuration
You can switch to disable the authentication configuration feature. When the switch is off, it will not take effect in the production environment even if there is an existing configuration. When you turn on the switch, a message will be displayed to confirm whether to enable this feature before the configuration takes effect across the entire network.
![](https://main.qcloudimg.com/raw/5bb10025c5887793807e6b41dbea48a6.png)

#### 3. Add region-specific configuration
If your acceleration domain name is configured for global acceleration and you want acceleration in and outside Mainland China to have different authentication configurations, you can click **Add Special Configuration** under the configuration.
![](https://main.qcloudimg.com/raw/391372dbf734e813c45640dace716793.png)

>After a region-specific configuration item is added, it cannot be directly deleted for the time being. You can only disable it.

## Configuration Sample
Suppose the domain name `cloud.tencent.com` is configured for global acceleration and the authentication configuration is as follows:
![](https://main.qcloudimg.com/raw/6f432b21603b61e4a1d9c17048a675bf.png)
Then, the actual effect will be as follows:
1. A user in Mainland China can access the resource `http://cloud.tencent.com/1.jpg` by directly initiating a request.
2. A user outside Mainland China can access the resource `http://cloud.tencent.com/1.jpg` by initiating a request with a URL in the format of `http://cloud.tencent.com/509301d10da7b862052927ed7a947f43/5e561139/1.jpg`.

