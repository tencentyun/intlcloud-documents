## Use Cases

After you connect a domain name to Tencent Cloud CDN, you can log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar to view the acceleration domain name list.

You can adjust the displayed columns, batch enable/disable the acceleration service for domain names and batch change domain name projects, tags, and configurations.

## Operations Guide

### Adjusting displayed columns

Click the ![img](https://main.qcloudimg.com/raw/c8528c5a51cbea35ecb7e0414b51267e.png) icon on the right of the search bar to see all the available columns. Choose the columns you want to display, cancel the ones you want to hide an adjust their order:
![img](https://main.qcloudimg.com/raw/790ae4b6c47b8b5ccd72e517701d34db.png)



### Exporting the configuration list

Click the ![img](https://main.qcloudimg.com/raw/16b5654ecd298d7cadc63b243413a31d.png) icon on the right of the search bar to export the domain name list details in an Excel file. You can select up to 1000 domain names to export each time.



### Changing projects

You can change the projects of running domain names.

- Change the project of one domain name: on the right of the target domain name, click **More** -> **Modify Project**.

- Batch change the projects of multiple domain names: tick target domain names and click **More Actions** -> **Edit Project** on the top. You can change the projects of up to 50 domain names at a time.




### Editing tags

- Change the tag of one domain name: click the target domain name to enter its configuration page, open the **Basic Configuration** tab, click the pencil icon on the right of **Tag** in the **Basic Information** section.
- Batch change the tags of multiple domain names: tick target domain names and click **More Actions** -> **Edit Tag** on the top. You can change the tags of up to 50 domain names at a time. The changes do not take effect immediately, please refresh to view the new tags.	



### Disabling the acceleration service

You can disable the acceleration service for normally-running domain names. After the acceleration service is disabled for a domain name, its configurations will be deactivated on CDN cache nodes across the entire network. If access requests to the domain name are still redirected to CDN nodes, a 404 error will be returned. Therefore, before disabling a domain name, make sure that its CNAME record is resolved to a non-CDN CNAME address.

> !Consumption will no longer be generated after the acceleration service is completely disabled.

- Disable the acceleration service for one domain name: on the right of the target domain name, click **More** -> **Disable**.
- Batch disable the acceleration service for multiple domain names: tick enabled domain names and click **More Actions** -> **Disable Acceleration** on the top.



### Enabling the acceleration service

You can enable the acceleration service for disabled domain names to distribute their configurations to cache nodes across the entire network again.

- Enable the acceleration service for one domain name: on the right of a disabled domain name, click **More** -> **Enable**.
- Batch enable the acceleration service for multiple domain names: tick disabled domain names and click **More Actions** -> **Enable Acceleration** on the top.

> !If an enabled domain name has no operations or consumption for 3 months, it will be considered inactive and CDN will automatically disable its acceleration service.



### Deleting acceleration domain names

If the domain names are in **Disabled** status, you can delete them. Once they are deleted, their configurations will be cleared and cannot be restored, and their statistical data can no longer be viewed. Please operate with caution.

- Delete one domain name: on the right of the target domain name, click **More** -> **Delete**.
- Batch delete multiple domain names: tick disabled domain names and click **More Actions** -> **Delete** on the top.



### Batch changing configurations	

The Batch Change Configuration feature allows you to change a configuration item of multiple domain names at the same time. For more information, please see [Batch Changing Configuration](https://intl.cloud.tencent.com/document/product/228/39911).	




### Copying configurations

The Copy Configuration feature allows you to duplicate configurations of an existing acceleration domain name to one or multiple new acceleration domain names. For more information, please see [Copying Configuration](https://intl.cloud.tencent.com/document/product/228/38936).






