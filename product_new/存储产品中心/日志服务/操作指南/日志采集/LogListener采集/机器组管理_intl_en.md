A server group is a server object configured to collect logs by LogListener in Tencent Cloud CLS. Generally, different server groups are configured based on various business scenarios to help you manage CLS.

## Creating a Server Group
You can quickly create a server group on the CLS Console as instructed below:
1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Click **Server Group Management** on the left sidebar.
3. Select the region of your log service, e.g. Guangzhou, and then click **Create Server Group**.
![](https://main.qcloudimg.com/raw/95220e6cb971a91ac4e490b39f6e5068.png)
4. Enter the server group name and the server IP address, and click **Confirm** after confirmation to complete the creation of the server group.
![](https://main.qcloudimg.com/raw/5a5372e04930018fb1a1a51653d5eab8.png)
>!
> - Enter one IP in a line. Windows system is not supported.
> - If you are using Tencent Cloud servers in the same region, you can enter private IPs directly, with one IP per line.


## Viewing Server Status
The heartbeat mechanism is employed to maintain the connection between the server group and the CLS system. Heartbeat is sent regularly to CLS from the server group with LogListener installed.
1. Click the **View** button to check the status of the server group to see if the server is running normally.
![](https://main.qcloudimg.com/raw/b1b9f577f6ca595c5a6aaffd8169fd40.png)
2. If the status is normal, the server communicates with Tencent Cloud CLS normally.
![](https://main.qcloudimg.com/raw/69d87f0aa09637c03f58190a366178ce.png)

## Deleting a Server Group
1. Log in to the [CLS Console](https://console.cloud.tencent.com/cls).
2. Select the server group to be deleted, and click the **Delete** button.
![](https://main.qcloudimg.com/raw/c5cb4b37df17cc3b01f15e363d7dacd2.png)
3. Click **OK** to delete the server group.
![](https://main.qcloudimg.com/raw/d94ecda2fd201698859dd9eee5bfd5c4.png)
>!Once a server group is deleted, logs are no longer collected under the bound log topics.
