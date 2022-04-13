## Overview
The EdgeOne overview page allows you to quickly view the overall status of the current site and access feature pages and product documentation through quick links. It contains the acceleration and security service data, site management, service status, FAQs, and documentation modules.

>? Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Service Overview** on the left sidebar.
2. On the service overview page, **All sites** is selected by default. You can select a specific site to view its details.
![](https://qcloudimg.tencent-cloud.cn/raw/42be6a98fa149ebad9b58cc3abf419e3.png)
3. On the service overview page, you can view workflows, site management information, data overview, FAQs, and documentation.

### Workflow
On the top of the page, you can see the different service modules, core features, and connection status of the selected site. You can quickly view its enabled and disabled product services and enter core feature pages through quick links.
>? If **All sites** is selected, the connection statuses of different service modules don't change dynamically. They will change dynamically only when a specific site is selected.

### Site management
1. In the site management module, you can view the site's status and package information.
 - Status:
    - Enabled: It is detected that the NS or CNAME record of a connected site has been updated successfully and pointed to EdgeOne.
    - Ineffective: A site has been added, but its NS or CNAME record has not been updated.
    - Disabled: All EdgeOne services (DNS, acceleration, and security protection services) have been disabled for a previously enabled site.
  - Package information: Package version and expiration time of each site.
2. In the site management module, you can click **Manage** to enable, disable, and delete a site.
 - Enable: Enable all EdgeOne services again for a disabled site.
>!After enabling the site, check whether the services take effect (you may need to modify the NS or CNAME record).

 - Disable: Disable all EdgeOne services for an enabled site.

>!Check and confirm your site's DNS.

 - Delete: Delete a site. Once the site is deleted, all its configuration data will be cleared. To use the site again, you need to connect it again.

>!You must disable the site service first before deleting a site.


### Data overview
The data overview module displays the overview of business access and security protection data of all sites. As data aggregation has a delay, all data is for reference only. For detailed data, see [Data Analysis](https://intl.cloud.tencent.com/document/product/1145/46196).
![](https://qcloudimg.tencent-cloud.cn/raw/467bb3a78b1582cc51be6efec0cac579.png)

>! All data is client access log data (i.e., application layer data), which may differ from the data used for billing. The volume of data generated during actual network transfer will be greater than that of application layer data. For specific billable usage, the actual bill shall prevail.

### FAQs
The FAQs module displays FAQs about product services.

### Documentation
The documentation module lists product service documents.
