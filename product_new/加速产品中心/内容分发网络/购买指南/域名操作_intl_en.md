In the CDN Console, you can activate, close, and delete acceleration service or modify projects of accelerated domain names that have been connected to CDN:
- Activated: The acceleration service is provided normally.
- Disable: After a domain name is disabled, a 404 error will be returned when a user request reaches a CDN node. The custom configuration of the disabled domain name will be retained when the domain name is enabled again.
- Delete: This deletes a domain name from the domain name list. Only disabled domain names can be deleted.
- Project: The project of a domain name is used to distinguish sub-user permissions in CDN. Please be cautious when changing the project.
- If a domain name is idle with no traffic/bandwidth usage incurred for 90 days, it will be repossessed (automatically deactivated).

## Activating Acceleration
You can **activate** a **closed** domain name by following steps. It takes about 5 minutes to activate the acceleration service.
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to activate the acceleration service:
### Activating a Single Domain Name
Right-click the domain name for which you want to activate the acceleration service and select **Activate CDN**.
![](https://main.qcloudimg.com/raw/e3d608f08832ce6fa7e01a7fb238ec01.png)
### Batch Activating
Select the domain names for which you want to activate the service and click **Activate CDN** above the domain name section.
![](https://main.qcloudimg.com/raw/051ea70275127c1be7394f904ad9d2b1.png)

## Stopping Acceleration
You can **close** an **activated** domain name by following steps. After the domain name is closed, it will no longer be accelerated, but its configuration will be retained (for future reuse). It takes about 5 minutes to close the acceleration service.
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to stop the acceleration service:
### Stopping a Single Domain Name
Right-click the domain name for which you want to stop the acceleration service and select **Close CDN**.
![](https://main.qcloudimg.com/raw/e38cd358d057f746ae3d62b10b2ee169.png)

### Batch Stopping
Select the domain names for which you want to stop the service and click **Close CDN** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/cfd1471f736552d89569a4646a279aa7.png)

## Deleting an Accelerated Domain Name
You can **delete** a **disabled** domain name. Its configuration will not be retained upon deletion.
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to delete a domain name:

### Deleting a Single Domain Name
Right-click the domain name you want to delete and select **Delete**.
![](https://main.qcloudimg.com/raw/d859905654d49fda9fec4da90052349a.png)
### Batch Deleting
Select the domain names you want to delete and click **Delete** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/bcd2de467e0008574996bbc881c6822e.png)
## Changing Project
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** to enter the management page. There are two ways to modify a project:

### Modifying a Single Domain Name
Right-click the domain name for which you want to modify the project and select **Modify Project**.
![](https://main.qcloudimg.com/raw/988859a20a66cddc48350b67bbe5d186.png)

### Batch Modification
Select multiple domain names for which you want to modify the project and click **Modify Project** in the **More Actions** drop-down list.
![](https://main.qcloudimg.com/raw/215a768ad5b45ec7965e1187ff38de1b.png)
Modify the current project to the desired one.
![](https://main.qcloudimg.com/raw/c11fb5f4de5bf484093e38d064cf6b22.png)
