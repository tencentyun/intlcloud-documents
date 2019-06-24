A server group is a server object configured to collect logs by LogListener in Tencent Cloud CLS. Generally, different server groups are configured based on various business scenarios to help you manage CLS.

## Creating Server Group
You can quickly create a server group on CLS console as follows:
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Click **Server Group** in the left navigation bar, select the region of your CLS, such as Guangzhou, and then click the **Create Server Group** button.
![](https://main.qcloudimg.com/raw/7a1ab71883e898cf3f75783871370c35.png)
3. Enter the server group name and the server's IP address, and click **OK** after confirmation to complete the creation of the server group.
![](https://main.qcloudimg.com/raw/0c67289db75e1617358f4220ea056ca8.png)

> **Note**:
> Only Linux server is supported by CLS. Enter the private IP for IP address. IP address range is not supported.

## Viewing Server Status
The heartbeat mechanism is employed to maintain the connection between the server group and CLS system. Heartbeat is sent regularly to CLS from the server group installed with LogListener.
1. Click the **View** button and check the status of the server group to see if the server is running normally.
![](https://main.qcloudimg.com/raw/9b3223064ff5c145389fd4aa90cb8ca1.png)
2. If the status is normal, the server communicates with Tencent Cloud CLS normally.
![](https://main.qcloudimg.com/raw/68a3cfeed73a1f8823fba7a18afe2e3b.png)

## Deleting Server Group
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. Select the server group to be deleted, and click the **Delete** button.
![](https://main.qcloudimg.com/raw/2be211ff2b79aa836a768237ca2137a4.png)
3. Click **OK** to delete the server group.
![](https://main.qcloudimg.com/raw/ec46a79a0aa54b21d2beea95190d332b.png)
> **Note:**
> Once the server group is deleted, logs are no longer collected under the associated log topics.

