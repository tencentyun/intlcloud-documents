You can perform the following operations on the Tencent Cloud service integration page:
- View available integrations
- Manage installed integrations
- Configure service roles

## Prerequisites
1. Log in to the [TCMG console](https://console.cloud.tencent.com/monitor/grafana).
2. Find the corresponding Grafana instance in the list and click its **instance ID** to enter the Grafana instance management page.
3. Click **Tencent Cloud Service Integration** on the left sidebar.

## Viewing Available Integrations
On the **Tencent Cloud Service Integration** page, you can view and search for the available integrations of the current instance and install and connect them. After they are connected successfully, their monitoring data will be displayed on the Grafana dashboard.
![](https://qcloudimg.tencent-cloud.cn/raw/97c03d65b8a1d30429c5c3336bbaaf6a.png)


### Prometheus
1. Click **Install** below **Prometheus** to enter the installation page.
2. Configure the data source:
 - Data Source Name: enter the Prometheus instance ID.
 - Data Source Address: enter the private network address of Prometheus such as `http://x.x.x.x:9090`.
 - UID: it is the unique data source ID. We recommend you enter the Prometheus instance ID.
 - Account: `Appid` of your Tencent Cloud account, i.e., the account on the Prometheus instance details page.
 - Password: token on the Prometheus instance details page.
 - Dashboard Configuration: the dashboards in the Prometheus integration center will be automatically installed through this optional parameter, so you don't need to enter it.

2. After completing the configuration, click **Save**. After the system is rebooted, you can view the installed Prometheus data source on the Grafana data source page.

### CM
1. Click **Install** below **CM** to enter the installation page.
2. Configure the data source:
 - Data Source Name: enter the data source name.
 - Authentication: select the authentication type.
    - With key:
      - SecretID: enter your `SecretID`.
      - SecretKey: enter your `SecretKey`.
      ![](https://qcloudimg.tencent-cloud.cn/raw/8524cf27df323ca942dee24be0ace15d.png)
    - With service role: this option requires you to configure the service role with corresponding permissions for your instance. For detailed directions, see [Service Role](https://intl.cloud.tencent.com/document/product/1124/43961).
    ![](https://qcloudimg.tencent-cloud.cn/raw/cf3611a9478563ef509a3ef7b9a729f9.png)
3. After completing the configuration, click **Save**. After the system is rebooted, you can view the installed CM data source on the Grafana data source page.

### CLS
1. Click **Install** below **CLS** to enter the installation page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/d9bf38b5b8ed5d6695c587bf7ee1cd5f.png)
2. Configure the data source:
 - Data Source Name: enter the data source name.
 - SecretID: enter your `SecretID`.
 - SecretKey: enter your `SecretKey`.
3. Configure CLS:
 - Region: region such as `ap-guangzhou`. For the complete list, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).
 - TopicId: log topic. For more information, see [Log Topic](https://intl.cloud.tencent.com/document/product/614/32849).
4. After completing the configuration, click **Save**. After the system is rebooted, you can view the installed CLS data source on the Grafana data source page.


## Managing Installed Integrations

Select **Integration List** to view the installed integrations, which may be installed by you or automatically by Tencent Cloud services through the binding relationship and can be deleted in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/1afadce4f33c829bbf6720f90f1bc854.png)
