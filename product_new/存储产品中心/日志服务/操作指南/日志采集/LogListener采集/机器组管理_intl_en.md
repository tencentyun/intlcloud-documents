A server group is a server object configured to collect logs by LogListener in Tencent Cloud CLS. Generally, different server groups are configured based on various business scenarios to help you manage CLS.

## Creating a Server Group
You can quickly create a server group on the CLS Console as instructed below:
1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Server Group Management** on the left sidebar.
3. Select the region of your log service, e.g. Guangzhou, and then click **Create Server Group**.
![](https://main.qcloudimg.com/raw/ff00993bbf5151c23c7f0c0e2048a664.png)
4. Enter the server group name and the server IP address, and click **Confirm** after confirmation to complete the creation of the server group.
![](https://main.qcloudimg.com/raw/acd1cf6a8e3208176364160b836ce532.png)
>!
> - Enter one IP in a line. Windows system is not supported.
> - If you are using Tencent Cloud servers in the same region, you can enter private IPs directly, with one IP per line.


## Viewing Server Status
The heartbeat mechanism is employed to maintain the connection between the server group and the CLS system. Heartbeat is sent regularly to CLS from the server group with LogListener installed.
1. Click the **View** button to check the status of the server group to see if the server is running normally.
![](https://main.qcloudimg.com/raw/4163e320b011c1593c345b80cb52e0ed.png)
2. If the status is normal, the server communicates with Tencent Cloud CLS normally.
![](https://main.qcloudimg.com/raw/f3c7d75d5282758fadecded57bdedb1a.png)

## Deleting a Server Group
1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Select the server group to be deleted, and click the **Delete** button.
![](https://main.qcloudimg.com/raw/a5499d33aa8c2323697388334dc27584.png)
3. Click **OK** to delete the server group.
![](https://main.qcloudimg.com/raw/e99130ce78d418e04c4f573fbcd112d0.png)
>!Once a server group is deleted, logs are no longer collected under the bound log topics.
