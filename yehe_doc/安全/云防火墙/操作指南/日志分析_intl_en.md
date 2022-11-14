Log Analysis allows you to view details of all traffic logs of the login account stored in Cloud Firewall for the past 6 months, query logs with search statements, and use reporting and analysis services. This topic describes how to use Log Analysis.

## Viewing log analysis data
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/search) and click **Log Analysis** in the left navigation pane.
2. Drag your mouse on the bar chart in blue to quickly select a time range to search and click a bar to check the logs.
>?
>- Cancel: Click **Cancel** in the upper right corner of the bar chart and the bar chart will show the number of logs for today by default.
>- If you change the time and log type or enter new keywords to search again, the bar chart will show the number of logs for today by default.

![](https://qcloudimg.tencent-cloud.cn/raw/da651d6375efaf780be963e05d0ae1a1.png)
3. The log list displays the field details of each traffic log in the order the fields appear in **Display fields**. When the **Display fields** module only contains **source**, the list displays the field details of each traffic log in the order the fields appear in **Hide fields**.
![](https://qcloudimg.tencent-cloud.cn/raw/33766da06f62adabe56804066bdfdc37.png)
 - **Show**: Hover your mouse over a hidden field and click **Show**. This field will appear under **Display fields** and its details will be displayed in the log list on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/9cb866ce797a3ba0948f01b49e205a36.png)
 - **Hide**: Hover your mouse over a displayed field and click **Hide**. This field will be deleted from **Display fields**and its details will not be displayed in the log list on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/b4022fd64a0916447c403b5052bbb590.png)
## Log shipping
You can use log shipping to automatically ship Cloud Firewall logs to specified Cloud Kafka (CKafka) instances. This section describes how to use the log shipping feature of Log Analysis.
### Background
- You can ship logs to specified CKafka topics based on Cloud Firewall log types.
- Log shipping supports two network access methods: public domain name and supported environment.
	- For access via public domain name, logs are shipped through the public network.
	- For access via supported environment, logs are shipped through Tencent Cloud private network, which effectively enhances the performance.

### Prerequisites
- You need to [purchase Cloud Kafka instances](https://console.cloud.tencent.com/ckafka/index?rid=1) first, and set the bandwidth of the CKafka instance based on the Cloud Firewall bandwidth.
- Please see [Cloud Kafka](https://intl.cloud.tencent.com/document/product/597) for more information, and [contact us](https://intl.cloud.tencent.com/contact-us) to enable the allowlist for "access via public domain name" or "access via supported environment”.
- You can only use one CKafka account for log shipping.

### Configurations
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/search) and click **Log Analysis** in the left navigation pane.
2. Click **Log shipping** in the upper left corner.
![](https://qcloudimg.tencent-cloud.cn/raw/f39b7fce2fc876ae3fcf3e5e18fab089.png)
3. Configure the initial settings on the log shipping page.
	1. Select the network access method: public domain name or supported environment.
		- **Method 1**: Select **Public domain name** and then select the message queue instance and public domain name. Enter the user name and password of the selected instance.
		![](https://qcloudimg.tencent-cloud.cn/raw/1ed083eb69c7eb0f24c0e772d2473b58.png)
		- **Method 2**: Select **Supported environment** (Tencent Cloud products that you purchased and can be used with CKafka), and then select the message queue instance and IP port.
![](https://qcloudimg.tencent-cloud.cn/raw/0604b976e8d2464cce14fb8dcc354ec2.png)
	2. Associate a CKafka topic on the log shipping page.
>? You can ship multiple types of Cloud Firewall logs to their specified CKafka topics. One CKafka topic can only be associated with one Cloud Firewall log type.

![](https://qcloudimg.tencent-cloud.cn/raw/2252f6fbba3fdc0d2ef69c9ab7f20ff3.png)

	3. Click **OK**, and you will see a prompt showing that the log shipping has been configured.

4. After configuration, you can view the log shipping details.
![](https://qcloudimg.tencent-cloud.cn/raw/896dcdd057e341be18753795c9ac7ab1.png)
- **Basic info**: shows the basic information of CKafka instances.
>! When you see **Unhealthy** in the **Status** field, click **View monitoring** to check whether CKafka is abnormal or whether the quota is insufficient.

- **Shipping status**: Toggles the log shipping on/off to control a specified log type.
	- Method 1: Toggle on or off under **Shipping status** on the right side of each log type.
	- Method 2: Disable/enable in batch. You can select **Enable all** or **Disable all**.
- **Change CKafka topic**: In the action column on the right side of a log type, click **Edit** to configure it individually. You can select a CKafka topic not associated with other Cloud Firewall log types in the specified CKafka instance.
>? One CKafka topic can only be associated with one Cloud Firewall log type.

- **View monitoring**: In the action column on the right side of a log type, click **View monitoring** to go to the monitoring page of the CKafka console, where you can view network traffic, peak bandwidth, message quantity, disk usage, etc.
- **Change configuration**: Click **Change configuration** above the log type list, and then select the message queue instance to ship, network access method, and user name/password.
>! This will interrupt the current shipping process.

- **Change password**: click **Change password** above the log type list to modify the user name and password of CKafka.

