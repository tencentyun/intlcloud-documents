## Scenarios

To manage domain names connected to Tencent Cloud CDN, go to the [CDN console](https://console.cloud.tencent.com/cdn) and select **Domain Management** from the left sidebar.

You can adjust the list column, batch enable/disable acceleration service for domain names, and batch change domain name projects, tags, and configurations.

## Directions

### Adjusting list volumes

Click the ![img](https://main.qcloudimg.com/raw/c8528c5a51cbea35ecb7e0414b51267e.png) icon on the right of the search bar to open the list field option list. You can choose to display or hide fields and adjust their display order:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Qa5H894_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423164718.png)


### Exporting the configuration list

Click the ![img](https://main.qcloudimg.com/raw/16b5654ecd298d7cadc63b243413a31d.png) icon on the right of the search bar to export an Excel file of the domain name list content. You can select up to 1000 domain names to export each time.



### Changing the related project

You can change the projects of normally-running domain names.

- Single domain name: Click **More** -> **Modify Project**.
  ![](https://staticintl.cloudcachetci.com/yehe/backend-news/knXR199_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423164814.png)
- Batch change the project: Select target domain names and click **More Actions** -> **Edit Project** on the top. Up to 50 domain names can be selected at a time.
  ![](https://staticintl.cloudcachetci.com/yehe/backend-news/adjh960_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423170306.png)



### Editing tags

- Single domain name: Click the target domain name to enter its configuration page, open the **Basic Configuration** tab, click the pencil icon on the right of **Tag** in the **Basic Information** section.
- Batch editing: Select domain names to modify, and click **More Actions** -> **Edit Tag** on the top. Up to 50 domain names are supported. Refresh the page to check the updated tags. 	



### Disabling the acceleration service

When you disable the acceleration service for a domain name, it is deactivated on CDN cache nodes across the entire network. All access requests to the domain name get 404. Therefore, before disabling a domain name, make sure that its CNAME record is resolved to a non-CDN CNAME address.

> !Consumption will no longer be generated after the acceleration service is completely disabled.

- Single domain name:  **More** -> **Disable**.
- Batch disable: Select domain names to disable, click **More Actions** -> **Disable Acceleration** on the top.



### Enabling the acceleration service

When the acceleration service is enabled for a domain name, the domain name configuration is distributed to cache nodes across the entire network.

- Single domain: Click **More** -> **Enable**.
- Batch enable: Select domain names to enable, and click **More Actions** -> **Enable Acceleration** on the top.

> !If an enabled domain name has no operations or consumption for 3 months, it will be considered inactive and CDN will automatically disable its acceleration service.



### Deleting domain names

To delete an accelerated domain name, you need to disable it first. After the deletion, all data of the domain names will be cleared and cannot be restored. You can no longer check their statistical data.

- Single domain name: Locate the domain name, click **More** -> **Delete**.
- Batch delete: Select domain names to delete, and click **More Actions** -> **Delete** on the top.



### Batch changing configurations	

The Batch Change Configuration feature allows you to change a configuration item of multiple domain names at the same time. For more information, please see [Batch Changing Configuration](https://www.tencentcloud.com/document/product/228/39911).	
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Sb5V462_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423165446.png)



### Copying configurations

The Copy Configuration feature allows you to duplicate configurations of an existing acceleration domain name to one or multiple new acceleration domain names. For more information, please see [Copying Configuration](https://www.tencentcloud.com/document/product/228/38936).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/t7Ja848_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423165303.png)


### Purging all caches

To purge all cached resources on the CDN nodes under the current domain name, click **More** on the right of the domain name, and click **Purge all caches** in the pop-up window. 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/jRTu897_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423165158.png)