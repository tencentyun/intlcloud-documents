In the CDN Console, you can activate, close, and delete acceleration service or modify projects of accelerated domain names that have CDN service enabled:
- Activated: The acceleration service is provided normally.
- Disable: After a domain name is disabled, a 404 error will be returned when a user request reaches a CDN node. The custom configuration of the disabled domain name will be retained when the domain name is enabled again.
- Delete: This deletes a domain name from the domain name list. Only disabled domain names can be deleted.
- Project: The project of a domain name is used to distinguish sub-user permissions in CDN. Please be cautious when changing the project.
- If a domain name is idle and did not incur any traffic/bandwidth usage for 90 days, it will be repossessed (automatically deactivated).

## Activating Acceleration
You can **activate** a **closed** domain name with the following steps. It takes about 5 minutes to activate the acceleration service.
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to activate the acceleration service:
### Activating a Single Domain Name
Right-click the domain name and select **Activate CDN**.
![](https://main.qcloudimg.com/raw/ee20f5932cb8e459af089c7d7c4c602a.jpg)
### Batch Activating
Select multiple domain names and click **Activate CDN** above the list of domain names.
![](https://main.qcloudimg.com/raw/9531daee6ddf846b2ddd12df7ae79a3e.jpg)

## Stopping Acceleration
You can **close** an **activated** domain name with the following steps. After the domain name is closed, it will no longer be accelerated, but its configuration will be retained for future reuse. It takes about 5 minutes to close the acceleration service.
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to stop the acceleration service:
### Stopping a Single Domain Name
Right-click the domain name and select **Close CDN**.
![](https://main.qcloudimg.com/raw/81fa72b8ba7af7243eb3fa1e32298e2c.jpg)

### Batch Stopping
Select multiple domain names and click **Close CDN** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/6961c74da9ecfd60afc177e9e35ba837.jpg)

## Deleting an Accelerated Domain Name
You can **delete** a **disabled** domain name. Its configuration will not be retained upon deletion.
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to delete a domain name:

### Deleting a Single Domain Name
Right-click the domain name you want to delete and select **Delete**.
![](https://main.qcloudimg.com/raw/d82f80795b62cc47d2b180bfee5a9f30.jpg)
### Batch Deleting
Select the domain names you want to delete and click **Delete** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/952ecd62247568f7d0ce89643d72ee81.jpg)
## Modifying Project
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to modify a project:

### Modifying a Single Domain Name
Right-click the domain name and select **Modify Project**.
![](https://main.qcloudimg.com/raw/5cd9130e05f8989cf56673ed5aaec1ef.jpg)

### Batch Modification
Select multiple domain names and click **Modify Project** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/5cd9130e05f8989cf56673ed5aaec1ef.jpg)
Modify the current project to the desired one.
![](https://main.qcloudimg.com/raw/645a6acdf0922f7e1138652673fb8d74.jpg)
