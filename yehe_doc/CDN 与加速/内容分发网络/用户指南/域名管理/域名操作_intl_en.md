## Operation Scenarios
After you connect a domain name to Tencent Cloud CDN, you can log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and <br/>select **Domain Management** on the left sidebar to view the acceleration domain or activate/disable acceleration service.

CDN allows you to customize the domain list page to display multiple basic configuration items and adjust their order as needed. In addition, you can activate or disable in batches the acceleration service for domains, improving business management efficiency.

## Operation Guide
### List operations
#### 1. Customize the list display
Click the **Customize** icon to the right of the search box to display the customization option box:
![](https://main.qcloudimg.com/raw/790ae4b6c47b8b5ccd72e517701d34db.png)
You can choose to display or hide fields and adjust their display order:
![](https://main.qcloudimg.com/raw/1d123a3948ee2450204fa8cc78a11a36.png)

You can customize the following fields:

+ Domain: required and cannot be hidden.
+ Service type: static acceleration, download acceleration, or streaming VOD acceleration.
+ Status: domain service status (activated, disabled, or deploying).
+ CNAME: CNAME record of the domain.
+ Origin type: external origin server or COS origin server.
+ Service region: Mainland China, outside Mainland China, or global.
+ Project: name of the project to which the domain belongs.
+ Primary origin configuration: primary origin server address.
+ Hot backup origin configuration: backup origin server address.
+ HTTPS configuration: configured or not configured.
+ Origin-pull protocol: HTTP, HTTPS, or follow protocol.
+ Origin domain: origin-pull domain configuration.
+ Ignore query string: enabled or disabled.

#### 2. Export the configuration list

Click the **Export** icon to the right of the search box to export the domain list as an Excel file.

+ The exported content only contains domains and configuration items currently displayed on the domain list page, not all domains and all basic configuration items.
+ Up to 3,000 domains can be exported at a time.

![](https://main.qcloudimg.com/raw/8065bb602460bf3fcf9a8dbec9c3bd67.png)

### Domain operations
In the CDN Console, you can activate, disable, and delete the acceleration service or modify the projects for acceleration domains.

#### 1. Disable the acceleration service

After the acceleration service is disabled for a domain, its configurations will be deactivated on cache nodes across the entire network. If access requests to the domain are still redirected to CDN nodes, error 404 will be returned. Before disabling a domain, make sure that its CNAME record is pointing to a non-CDN CNAME address.

>
> - You can only disable activated acceleration domains. Domains in deployment cannot be disabled.
> - Configurations of disabled domains will be retained and take effect when the domains are reactivated.
>- Consumption will no longer be generated after the acceleration service is completely disabled.

You can click **Close** in the "Operation" column on the right of the domain to disable the service. You can also select multiple domains in **Activated** status and disable them in batches in **More Actions** at the top.

![](https://main.qcloudimg.com/raw/6536bf6c02870b792031a2c65645c31a.png)

#### 2. Enable the acceleration service

If a domain is in **Disabled** status, you can activate the acceleration service to distribute its configuration to cache nodes across the entire network again:

You can click **Activate** in the "Operation" column on the right of the domain to enable the service. You can also select multiple domains in **Disabled** status and activate them in batches in **More Actions** at the top.

>
>If an activated domain has no operation or consumption for 3 months, it will be considered as inactive. CDN will automatically disable its acceleration service.

![](https://main.qcloudimg.com/raw/fd6d029c82e516965ea6e093ef41c9f5.png)

#### 3. Delete acceleration domains

If a domain is in **Disabled** status, you can click **More** on the right to delete it. Note that once a domain is deleted, its configuration will be cleared and cannot be restored. Its statistical data can no longer be viewed.
![](https://main.qcloudimg.com/raw/bc58fc9c225efb79a0ec1454b6748e1c.png)

