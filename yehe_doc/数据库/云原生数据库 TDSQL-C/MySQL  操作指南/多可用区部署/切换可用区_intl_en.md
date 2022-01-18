TDSQL-C for MySQL allows you to change the primary and secondary AZs manually or automatically. You can use this feature to migrate the compute nodes of your database cluster to other AZs.

## Use Cases
The primary/secondary AZ switch feature is suitable for use cases such as disaster recovery and device failure recovery.
![](https://qcloudimg.tencent-cloud.cn/raw/dc53b3292eb2e84eee7e665885a9097e.png)

## Notes
- The connection will be disconnected for about 2 to 5 seconds during the primary/secondary AZ switch. We recommend that you switch during off-peak hours and that your application has a reconnection mechanism.
- The data does not need to be migrated if the target AZ is a secondary AZ. The system simply needs to switch the database compute nodes, allowing for a rapid cross-data center switch. This is often used in disaster recovery drills.
- The entire cluster is switched; that is, both read-write and read-only nodes are switched (partial node switch is not supported).
- The read-write and read-only addresses will not be changed after the switch.

## Directions
### Automatic switch
This feature supports automatic primary/secondary AZ switch in case of AZ failures, ensuring your business continuity and protecting your database.

### Manual switch
You can manually switch the cluster's primary and secondary AZs as needed by your business.
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a cluster name in the cluster list or **Manage** in the **Operation** column to enter the cluster details page.
2. In the **Availability Info** module on the cluster details page, click **Switch AZs**.
![](https://qcloudimg.tencent-cloud.cn/raw/41ecb8c0427a64728e04bd72a38537b8.jpg)
3. In the pop-up window, select **Switch now** or **During maintenance time**, click **Switching AZs will cause a momentary disconnection. Please ensure that your business has the reconnection mechanism.**, and click **OK**.
>?
>- Switching AZs will cause a momentary disconnection. Ensure that your business has the reconnection mechanism.
>- Select the **Instance List** page, click the target instance ID to enter the instance details page, and click **Edit** after **Maintenance Info** to set or modify the maintenance time.
>
![](https://qcloudimg.tencent-cloud.cn/raw/41c7d2c1ca0c1248b66ca7dea492ef72.png)
4. When the cluster status becomes **Running**, you can view the information of the switched AZ in **Availability Info** on the cluster details page.
![](https://qcloudimg.tencent-cloud.cn/raw/805366eed831de388d4d171e97e48fc1.png)

## FAQs
#### How long does it take to complete an AZ switch?
If the target AZ is a secondary AZ, the data does not need to be migrated when the primary AZ changes. The system simply needs to switch the database compute nodes, allowing for a rapid cross-data center switch.

#### Will the read-write address be changed after the entire cluster is switched?
When the entire cluster is switched, all read-write and read-only nodes will be switched, but the read-write and read-only addresses will remain unchanged.

#### After manual/automatic switch, if an instance is upgraded, will the upgrade affect or reset the information of the primary and secondary AZs?
No.

