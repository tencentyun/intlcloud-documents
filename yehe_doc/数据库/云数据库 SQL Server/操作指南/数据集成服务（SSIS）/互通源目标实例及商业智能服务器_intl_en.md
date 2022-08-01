Before using the SSIS feature, you need to interconnect the source instance, target instance, and business intelligence server.

The interworking group management feature is used to sustain interconnection between instances. Therefore, in the same account and region, all database instances and the business intelligence server in an SSIS project need to be added to the same interworking group, and the interworking IP for business intelligence services needs to be enabled for each of them before they can access each other.

This document describes how to add/manage instances in a interworking group.

## Adding an Instance to an Interworking Group
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select **Interworking Group Management** on the left sidebar, select a region at the top of the page, and click **Add Instance**.
3. In the **Add Instance** window, select the target database instances and business intelligence server, enable interworking IP for business intelligence services for each of them by toggling on the switch, and click **Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/3ce498d8bf0ec4a3e06faa31fd6fcfab.png"  style="zoom:50%;">
4. Confirm the information of the configured instances and click **OK** to add them to the interworking group.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f173e341cae9e2371b6911b72e9effdd.png"  style="zoom:50%;">
5. Return to the **Interworking Group Management** page. After the status of the instances just added to the interworking group becomes **Added to interworking group**, the instances are successfully added.
After adding instances successfully, you can view the following information in the instance list on the **Interworking Group Management** page.
![](https://qcloudimg.tencent-cloud.cn/raw/b669b0e6851e57d1b81ce368aaf920d8.png)
 - Instance ID/Name: ID/name of the instance. You can rename the instance here.
 - Status: You can filter instances by interworking status, including **Enabling interworking IP**, **Enabled interworking IP**, **Added to interworking group**, **Reclaiming interworking IP**, and **Reclaimed interworking IP**.
 - Version: Instance version information, which can be filtered.
 - Interworking IP for Business Intelligence Services: The interworking IP for business intelligence services is displayed here.
 - AZ: AZs in the current region, which can be filtered.
 - Private Network Address: Private network address of the TencentDB for SQL Server instance.
 - Operation (Remove): You can remove an instance from the interworking group. Once removed, the instance cannot interconnect with other instances in the group.

## Removing an Instance from an Interworking Group
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select **Interworking Group Management** on the left sidebar and select a region at the top of the page.
3. On the **Interworking Group Management** page, select the target instance in the instance list and click **Remove** in the **Operation** column.
4. In the pop-up window, confirm the selected instance and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/3323d071e947149352f59987c7902b61.png)
5. After removing the instance, click **OK** in the pop-up window, and the removed instance will no longer be displayed in the instance list.
![](https://qcloudimg.tencent-cloud.cn/raw/e4fa36f28aa3960c89f97cbdb34596f2.png)
>? 
>- Once removed, the instance cannot interconnect with other instances in the group.
>- To make the instance interconnect with other instances in the group, add it back to the group.

