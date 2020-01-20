In the CDN Console, you can activate, close, and delete acceleration service or modify projects of acceleration domain names that have CDN service enabled:
- Activated: The acceleration service is provided.
- Disable: After a domain name is disabled, a 404 error will be returned when a user request reaches a CDN node. The custom configuration of the disabled domain name will be retained when the domain name is enabled again.
- Delete: The domain name is deleted from the domain name list. Only disabled domain names can be deleted.
- Project: Please note that the project of a domain name is used to distinguish sub-user permissions in CDN.
- If a domain name is idle and does not incur any traffic/bandwidth usage for 90 days, it will be repossessed (automatically deactivated).

## Enabling an acceleration domain name
You can **enable** a **disabled** domain name by following the steps below. It takes about 5 minutes to enable the acceleration service.
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to activate the acceleration service:
### Enabling a single domain name
Right-click the domain name and select **Activate CDN**.
![](https://main.qcloudimg.com/raw/1b43338bb791171551209cc46b0c547c.png)
### Enabling domain names by batches
Select multiple domain names and click **Activate CDN** above the list of domain names.
![](https://main.qcloudimg.com/raw/f75d9dbffe1cf66d05de404662d3f738.png)

## Closing an acceleration domain name
You can **close** an **activated** domain name with the following steps. After a domain name is closed, it will no longer be accelerated, but its configuration will be retained for future reuse. It takes about 5 minutes to close the acceleration service.
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to stop the acceleration service:
### Closing a single domain name
Right-click the domain name and select **Close CDN**.
![](https://main.qcloudimg.com/raw/f30849431436150df62e19f17808df2f.png)

### Closing domain names by batches
Select multiple domain names and click **Close CDN** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/9d80ed62526ad68ebe448927b0c204cf.png)

## Deleting an acceleration domain name
You can delete a **closed** domain name. **Its configuration will not be retained upon deletion and the deletion cannot be undone.**
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to delete a domain name:

### Deleting a single domain name
Right-click the domain name you want to delete and select **Delete**.
![](https://main.qcloudimg.com/raw/65b5a9d1e911a54de7fcbdb0b7363144.png)
### Deleting domain names by batches
Select the domain names you want to delete and click **Delete** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/d7508791ddf0f7e0d07d056670586608.png)
## Modifying Project
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to modify a project:

### Modifying a single domain name
Right-click the domain name and select **Modify Project**.
![](https://main.qcloudimg.com/raw/7642879cec12b07813fc02f5366c4222.png)

### Modifying domain names by batches
Select multiple domain names and click **Modify Project** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/e8388d3a886701a7f2180a7d1d437b42.png)
Modify the current project to the target one.
![](https://main.qcloudimg.com/raw/b618fd0aca8b5c568c382dfa8d140ff3.png)
