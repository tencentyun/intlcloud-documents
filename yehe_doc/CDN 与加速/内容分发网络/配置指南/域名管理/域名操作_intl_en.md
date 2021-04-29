## Overview

After a domain name is connected to Tencent Cloud CDN, if you need to view, enable, or disable domain names,
you can log in to the [CDN console](https://console.cloud.tencent.com/cdn), and then click **Domain Management** on the left sidebar for these operations.

CDN supports domain name list page customization for you to display multiple basic configurations and adjust their order as needed. In addition, you can batch enable or disable the acceleration service for domain names, improving business management efficiency.

## List Operation Guide

### Customizing the list fields

Click the <img src ="https://main.qcloudimg.com/raw/c8528c5a51cbea35ecb7e0414b51267e.png" style ="margin:0" data-nonescope="true"> icon on the right of the search bar to open the list field option list:
![](https://main.qcloudimg.com/raw/790ae4b6c47b8b5ccd72e517701d34db.png)
You can choose to display or hide fields and adjust their display order:
![](https://main.qcloudimg.com/raw/1d123a3948ee2450204fa8cc78a11a36.png)

You can customize the following fields:

+ Domain: required and cannot be hidden.
+ Service type: static acceleration, download acceleration, or streaming VOD acceleration.
+ Status: domain name service status (enabled, disabled, or deploying).
+ CNAME: CNAME record of the domain name.
+ Origin type: external origin server or COS origin server.
+ Service region: Chinese mainland, outside the Chinese mainland, or global.
+ Project: name of the project to which the domain name belongs.
+ Primary origin configuration: primary origin server address.
+ Secondary origin configuration: secondary origin server address.
+ HTTPS configuration: configured or not configured.
+ Origin-pull protocol: HTTP, HTTPS, or follow protocol.
+ Origin domain: origin-pull domain name settings.
+ Ignore query string: enabled or disabled.
+ Tag: custom key value for resource classification and management.

### Exporting the configuration list

Click the <img src ="https://main.qcloudimg.com/raw/16b5654ecd298d7cadc63b243413a31d.png" style ="margin:0" data-nonescope="true"> icon on the right of the search bar to export an Excel file of the domain name list content. You can select up to 1000 domain names to export each time.
![](https://main.qcloudimg.com/raw/8065bb602460bf3fcf9a8dbec9c3bd67.png)

## Domain Name Operation Guide

On the CDN console, you can enable, disable, and delete the acceleration service as well as modify the projects for acceleration domain names.

<span ID="close"></span>

### Disabling the acceleration service

After the acceleration service is disabled for a domain name, its configurations will be deactivated on CDN cache nodes across the entire network. If access requests to the domain name are still redirected to CDN nodes, error 404 will be returned. Therefore, before disabling a domain name, make sure that its CNAME record is resolved to a non-CDN CNAME address.

> !
> - You can only disable enabled acceleration domain names, the ones in deployment cannot be disabled.
> - Configurations of disabled domain names will be retained and take effect when they are enabled.
> - Consumption will no longer be generated after the acceleration service is completely disabled.

If the domain names are in **Enabled** status, you can disable them by clicking **Disable** or ticking multiple ones to disable them by the batch operation in **More Actions** on the top.

![](https://main.qcloudimg.com/raw/6536bf6c02870b792031a2c65645c31a.png)

### Enabling the acceleration service

If a domain name is in **Disabled** status, you can enable the acceleration service to distribute its configurations to cache nodes across the entire network again.

If the domain names are in **Disabled** status, you can enable them by clicking **Enable** or ticking multiple ones to enable them by the batch operation in **More Actions** on the top.

> !If an enabled domain name has no operations or consumption for 3 months, it will be considered inactive and CDN will automatically disable its acceleration service.

![](https://main.qcloudimg.com/raw/fd6d029c82e516965ea6e093ef41c9f5.png)


<span ID ="del"></span>
### Deleting an acceleration domain name

If the domain names are in **Disabled** status, you can delete them by clicking **More** -> **Delete**. Once they are deleted, their configurations will be cleared and cannot be restored, and their statistical data can no longer be viewed.
![](https://main.qcloudimg.com/raw/bc58fc9c225efb79a0ec1454b6748e1c.png)
