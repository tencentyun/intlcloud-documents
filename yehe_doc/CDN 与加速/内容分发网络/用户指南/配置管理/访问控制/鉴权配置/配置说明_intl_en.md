## Configuration
Generally, content delivered over CDN are public resources by default, which can be accessed by users with URLs. To prevent malicious users from hotlinking your content for profit, you can configure advanced timestamp authentication in addition to access control policies such as referer blocklist/allowlist, IP blocklist/allowlist, and IP access frequency limit.

>After timestamp hotlink protection is configured, the client needs to calculate the signature as configured and carry it to the server when initiating a request. The CDN node will authenticate the signature on the server, which will pass only after successful authentication.

## Configuration Guide
### Viewing the configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to access its configuration page. Under the **Security Configuration** tab, find the authentication configuration, which is disabled by default:
![](https://main.qcloudimg.com/raw/77831beaa25a77dd26b60e1f401c8dd3.png)

### Modifying the configuration
#### 1. Modify the configuration
CDN provides four authentication signature calculation models of your choice. You can open the **Authentication Calculator** at the top to view these models. For more information on the configuration effect and algorithms, please see the specific algorithm documents for [TypeA](https://intl.cloud.tencent.com/document/product/228/35222), [TypeB](https://intl.cloud.tencent.com/document/product/228/35223), [TypeC](https://intl.cloud.tencent.com/document/product/228/35224), and [TypeD](https://intl.cloud.tencent.com/document/product/228/35225):
![](https://main.qcloudimg.com/raw/ffd60184fa759b4c7a82a5a49634b8c3.png)

#### 2. Disable the configuration
You can toggle the authentication configuration switch to disable this feature. When the switch is off, any existing configuration will not take effect in the production environment. If you toggle the switch on, a message will be displayed asking for your confirmation before the configuration takes effect across the entire network.
![](https://main.qcloudimg.com/raw/5bb10025c5887793807e6b41dbea48a6.png)

#### 3. Add a region-specific configuration
If your acceleration domain name is configured for global acceleration and you want acceleration in and outside mainland China to have different authentication configurations, you can click **Add Special Configuration** under the configuration.
![](https://main.qcloudimg.com/raw/391372dbf734e813c45640dace716793.png)

>Currently, an added region-specific configuration item cannot be deleted, and can only be disabled.

## Configuration Sample
Suppose the domain name `cloud.tencent.com` is configured for global acceleration and the authentication configuration is as follows:
![](https://main.qcloudimg.com/raw/6f432b21603b61e4a1d9c17048a675bf.png)
Then, the actual effect will be as follows:

1. A user in mainland China can access the resource `http://cloud.tencent.com/1.jpg` by directly initiating a request.
2. A user outside mainland China can access the resource `http://cloud.tencent.com/1.jpg` by initiating a request with a URL in the format of `http://cloud.tencent.com/509301d10da7b862052927ed7a947f43/5e561139/1.jpg`.
