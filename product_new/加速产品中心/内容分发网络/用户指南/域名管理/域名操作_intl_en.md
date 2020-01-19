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
![](https://main.qcloudimg.com/raw/e3d608f08832ce6fa7e01a7fb238ec01.png)
### Enabling domain names by batches
Select multiple domain names and click **Activate CDN** above the list of domain names.
![](https://main.qcloudimg.com/raw/051ea70275127c1be7394f904ad9d2b1.png)

## Closing an acceleration domain name
You can **close** an **activated** domain name with the following steps. After a domain name is closed, it will no longer be accelerated, but its configuration will be retained for future reuse. It takes about 5 minutes to close the acceleration service.
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to stop the acceleration service:
### Closing a single domain name
Right-click the domain name and select **Close CDN**.
![](https://main.qcloudimg.com/raw/e38cd358d057f746ae3d62b10b2ee169.png)

### Closing domain names by batches
Select multiple domain names and click **Close CDN** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/cfd1471f736552d89569a4646a279aa7.png)

## Deleting an acceleration domain name
You can delete a **closed** domain name. **Its configuration will not be retained upon deletion and the deletion cannot be undone.**
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to delete a domain name:

### Deleting a single domain name
Right-click the domain name you want to delete and select **Delete**.
![](https://main.qcloudimg.com/raw/d859905654d49fda9fec4da90052349a.png)
### Deleting domain names by batches
Select the domain names you want to delete and click **Delete** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/bcd2de467e0008574996bbc881c6822e.png)
## Modifying Project
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to modify a project:

### Modifying a single domain name
Right-click the domain name and select **Modify Project**.
![](https://main.qcloudimg.com/raw/988859a20a66cddc48350b67bbe5d186.png)

### Modifying domain names by batches
Select multiple domain names and click **Modify Project** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/215a768ad5b45ec7965e1187ff38de1b.png)
Modify the current project to the target one.
![](https://main.qcloudimg.com/raw/c11fb5f4de5bf484093e38d064cf6b22.png)
