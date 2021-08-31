## Overview
[Tencent Cloud Monitor](https://intl.cloud.tencent.com/product/cm) (CM) provides load and performance monitoring metrics for various Tencent Cloud services such as CVM and TencentDB. You can use the CM console and APIs to get relevant monitoring data. Tencent Cloud Monitor app is an application plugin adapted to the open-source software Grafana. By calling [Tencent Cloud Monitor API 3.0](https://intl.cloud.tencent.com/document/product/248/33873), it can get and display monitoring data on custom dashboards. It supports:

- Data sources of [CVM](https://intl.cloud.tencent.com/document/product/248/6843) monitoring metrics
- Data sources of [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/248/11006) monitoring metrics
- Data sources of [TencentDB for PostgreSQL](https://intl.cloud.tencent.com/document/product/248/17945) monitoring metrics
- Data sources of [VPC - NAT Gateway](https://intl.cloud.tencent.com/document/product/248/10991) monitoring metrics
- Data sources of [VPC - peering connection](https://intl.cloud.tencent.com/document/product/248/10986) monitoring metrics
- Data sources of [public network CLB](https://intl.cloud.tencent.com/document/product/248/10997) monitoring metrics
- Data sources of [layer-4 private network CLB protocol](https://intl.cloud.tencent.com/document/product/248/39529) monitoring metrics
- Data sources of [layer-7 CLB protocol](https://intl.cloud.tencent.com/document/product/248/39530) monitoring metrics
- Data sources of [TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/248/35671) monitoring metrics
- Data sources of [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/248/39507) monitoring metrics
- Data sources of [CDN](https://intl.cloud.tencent.com/document/product/248/39554) monitoring metrics
- Data sources of [BWP](https://intl.cloud.tencent.com/document/product/248/34645) monitoring metrics
- Data sources of [CKafka](https://intl.cloud.tencent.com/document/product/248/17297) monitoring metrics
- Data sources of [EIP](https://intl.cloud.tencent.com/document/product/248/34646) monitoring metrics
- Data sources of [CFS](https://intl.cloud.tencent.com/document/product/248/34644) monitoring metrics
- Data sources of [SCF](https://intl.cloud.tencent.com/document/product/248/34638) monitoring metrics
- Typical [dashboard templates](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/tree/master/src/dashboards) are provided for CVM, TencentDB for MySQL, and CLB
- Data sources of monitoring metrics for more Tencent Cloud services will be supported in the future

## Installation and Update
There are many ways to install this plugin as shown below:

>!The Tencent Cloud Monitor app plugin runs on Grafana 6.x or above. Please start by setting up a Grafana environment. For more information, please see [Download Grafana](https://grafana.com/grafana/download).


## tc-monitor-cli Usage
[tc-monitor-cli](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/blob/master/bin/tc-monitor-cli) is a script encapsulated based on [grafana-cli](http://docs.grafana.org/plugins/installation/#installing-plugins-manually). It can be used in the following steps:
### Installation
You can manually download and run [this script](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/blob/master/bin/tc-monitor-cli) or use the following cURL or Wget command to install it:
#### cURL command
```bash
$ curl -o- https://raw.githubusercontent.com/TencentCloud/tencentcloud-monitor-grafana-app/master/bin/tc-monitor-cli | bash -s install
```
#### Wget command
```bash
$ wget -qO- https://raw.githubusercontent.com/TencentCloud/tencentcloud-monitor-grafana-app/master/bin/tc-monitor-cli | bash -s install
```

Running any of the above commands will download a script and install the latest version of the plugin. If you want to install a specific version, you only need to add the version number at the end of the command. For example, if you want to install version 1.4.0, run:
```bash
$ curl -o- https://raw.githubusercontent.com/TencentCloud/tencentcloud-monitor-grafana-app/master/bin/tc-monitor-cli | bash -s install 1.4.0
```
All version numbers can be viewed in [GitHub Releases](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/releases).

### Enabling plugin
After the installation, Grafana should be restarted. Hover over the **gear** icon on the left sidebar and click **Plugins** to enter the plugin management page. If the `Tencent Cloud Monitor` app plugin is displayed in the plugin list, it indicates that the plugin has been installed successfully. You can enter the application details page and click **Enable** button to enable this plugin.

### Update
Before the update, the script will back up the current version. You can run any of the following commands to update the plugin to the latest version:
#### cURL command
```bash
$ curl -o- https://raw.githubusercontent.com/TencentCloud/tencentcloud-monitor-grafana-app/master/bin/tc-monitor-cli | bash -s upgrade
```
#### Wget command
```bash
$ wget -qO- https://raw.githubusercontent.com/TencentCloud/tencentcloud-monitor-grafana-app/master/bin/tc-monitor-cli | bash -s upgrade
```

Restart Grafana after the update.

### Rollback
If you need to roll back the plugin to the last version before the update, run any of the following commands:
#### cURL command
```bash
$ curl -o- https://raw.githubusercontent.com/TencentCloud/tencentcloud-monitor-grafana-app/master/bin/tc-monitor-cli | bash -s rollback
```
#### Wget command
```bash
$ wget -qO- https://raw.githubusercontent.com/TencentCloud/tencentcloud-monitor-grafana-app/master/bin/tc-monitor-cli | bash -s rollback
```


### More options
For more parameters, run the following command to view the help:
#### cURL command
```bash
$ curl -o- https://raw.githubusercontent.com/TencentCloud/tencentcloud-monitor-grafana-app/master/bin/tc-monitor-cli | bash -s -- --help
```
#### Wget command
```bash
$ wget -qO- https://raw.githubusercontent.com/TencentCloud/tencentcloud-monitor-grafana-app/master/bin/tc-monitor-cli | bash -s -- --help
```




## zip Usage for Decompression to Plugin Directory

1. Download the latest version of Tencent Cloud Monitor app plugin code in [GitHub Releases](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/releases) (the resource name is `tencentcloud-monitor-app-[x.x.x].zip`) and place the decompressed code in the plugin directory of Grafana, which is `${GRAFANA_HOME}/data/plugins` by default. You can configure the plugin directory in `${GRAFANA_HOME}/conf/default.ini` or `${GRAFANA_HOME}/conf/custom.ini`. For more information on the plugin directory, please see [plugins](https://grafana.com/docs/grafana/latest/administration/configuration/#plugins).
2. Restart Grafana.
3. Hover over the **gear** icon on the left sidebar and click **Plugins** to enter the **Plugins** page. If the `Tencent Cloud Monitor` app plugin is displayed in the plugin list, it indicates that the plugin has been installed successfully.
4. Enter the app details page and click **Enable**. After the Tencent Cloud Monitor app plugin is enabled successfully, you can use it in Grafana.

## Data Source Configuration

The Tencent Cloud Monitor app plugin gets the monitoring metric data of Tencent Cloud services by calling [CM APIs](https://intl.cloud.tencent.com/document/product/248/33873). You can configure the data sources of the corresponding Tencent Cloud services in the following steps.    

1. Hover over the **gear** icon on the left sidebar and click **Data Sources** to enter the data source management page.
   ![](https://main.qcloudimg.com/raw/edbe5606fbf9a3b3db8d4d8fce9bde4c.png)
2. Click **Add data source** in the top-right corner and then click **Tencent Cloud Monitor Datasource** to enter the data source configuration page.
   ![](https://main.qcloudimg.com/raw/5f9744954fec35e8ca6b811bc5a2766c.png)
3. `Name` is the data source name, which can be customized and is `Tencent Cloud Monitor Datasource` by default.
4. `SecretId` and `SecretKey` are security certificate information required for CM API calls, which can be obtained on the [TencentCloud API Key](https://console.cloud.tencent.com/cam/capi) page in the Tencent Cloud console.
5. Select a Tencent Cloud service for which to get monitoring data.
6. Click **Save & Test** to test whether the data source is configured correctly, and if so, you can use it in the dashboard.
   ![](https://main.qcloudimg.com/raw/ca1f15285c1e7fed7fe9033d8162e180.png)

## Dashboard Creation

You can create a dashboard in the following three methods: 

### Quick creation

Hover over the **plus sign** on the left sidebar and click **+Dashboard** to create a dashboard.

### Management page

Hover over the **grid** icon on the left sidebar and click **Manage** to enter the dashboard management page. Click **New Dashboard** to create a dashboard. You can also perform various dashboard management operations on this page, such as creating folders, moving dashboards, or importing dashboards.

### Template import

Hover over the **gear** icon on the left sidebar and click **Plugins** to enter the plugin management page. Click **Tencent Cloud Monitor** to enter the app details page, switch to the **Dashboards** tab, and select a dashboard template to import.
![](https://main.qcloudimg.com/raw/e9fcdc874430e835461bdcb8506ab300.png)


## Panel Data Configuration

After creating a dashboard, you can configure the panel information to get the monitoring data from Tencent Cloud Monitor. The following describes how to do so by taking Graph as an example.

### CVM

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of CVM.
2. Select the configured Tencent Cloud Monitor data source that includes CVM monitoring from the `Queries to` data source list.
3. Use the input parameters of the CVM monitoring API for the configuration items here. For more information on the configuration items, please see [CVM](https://intl.cloud.tencent.com/document/product/248/6843).
   - `Namespace`: select a namespace. The namespace of CVM monitoring is `QCE/CVM`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance ID**. You can also select `As InstanceName` (as the instance name), `As PrivateIpAddress` (as the private IP of the primary ENI), or `As PublicIpAddress` (as the public IP of the primary ENI).
     - For more information on how to get the instance list, please see [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.

>!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.


![](https://main.qcloudimg.com/raw/254858c5b66092b1078119d5f743b07a.png)

### TencentDB for MySQL

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of TencentDB for MySQL.
2. Select the configured Tencent Cloud Monitor data source that includes TencentDB monitoring from the `Queries to` data source list.
3. Use the input parameters of the TencentDB for MySQL monitoring API for the configuration items here. For more information on the configuration items, please see [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/248/11006).
   - `Namespace`: select a namespace. The namespace of CVM monitoring is `QCE/CDB`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance ID**. You can also select `As InstanceName` (as the instance name) or `As Vip` (as the private IP).
     - For more information on how to get the instance list, please see [DescribeDBInstances](https://intl.cloud.tencent.com/document/api/236/15872). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.

>!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.  

![](https://main.qcloudimg.com/raw/954d31a383d67307028d26a96434595f.png)

### CLB
1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of CLB.
2. Select the configured Tencent Cloud Monitor data source that includes CLB monitoring from the `Queries to` data source list.
3. CLB metrics are divided into three namespaces: public network CLB monitoring metrics (Namespace=QCE/LB_PUBLIC), private network layer-4 CLB protocol monitoring metrics (Namespace=QCE/LB_PRIVATE), and layer-7 protocol monitoring metrics (Namespace=QCE/LOADBALANCE). You can select a value in `Namespace` as needed.
4. Use the input parameters of the CVM monitoring API for the configuration items here. For more information on the configuration items, please see [Public Network CLB](https://intl.cloud.tencent.com/document/product/248/10997).
   - `Namespace`: select a namespace, such as `QCE/LB_PUBLIC`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As LoadBalancerId` by default, meaning that the instance list is displayed as **instance ID**. You can also select `As LoadBalancerName` (as the instance name) or `As LoadBalancerVips` (as the IP).
     - For more information on how to get the instance list, please see [DescribeLoadBalancers](https://intl.cloud.tencent.com/document/product/214/33830). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.
     >!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.  
   - `Listener`: select a listener, which is **optional**. At this time, the instance dimension is used for request, which corresponds to the `Listener.N` field of the input parameter. The list will be automatically obtained.
     - To adapt to the habits of different users, the listener list is displayed as different fields, which is `As ListenerId` by default, meaning that the listener list is displayed as **listener ID**. You can also select `As ListenerName` (as the listener name) or `As Port` (as the port).
     - For more information on how to get the listener list, please see [DescribeListeners](https://intl.cloud.tencent.com/document/product/214/33831).

![](https://main.qcloudimg.com/raw/c49f2ee8a3a430aed60373475f20fc3e.png)

### TencentDB for MongoDB

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of TencentDB for MongoDB.
2. Select the configured Tencent Cloud Monitor data source that includes TencentDB for MongoDB monitoring from the `Queries to` data source list.
3. Use the input parameters of the TencentDB for MongoDB monitoring API for the configuration items here. For more information on the configuration items, please see [TencentDB for MongoDB](https://intl.cloud.tencent.com/document/product/248/35671).
   - `Namespace`: select a namespace, such as `QCE/CMONGO`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance ID**. You can also select `As InstanceName` (as the instance name).
     - For more information on how to get the instance list, please see [DescribeDBInstances](https://intl.cloud.tencent.com/document/product/240/34702). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.

>!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.  

![](https://main.qcloudimg.com/raw/c5f07505cbcebbc2678d86ee0568fde6.png)

### TencentDB for Redis

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of TencentDB for Redis.
2. Select the configured Tencent Cloud Monitor data source that includes TencentDB for Redis monitoring from the `Queries to` data source list.
3. TencentDB for Redis metrics are divided into two namespaces: Memory Edition (5-second) (Namespace=QCE/REDIS_MEM) and CKV Edition and Memory Edition (1-minute) (Namespace=QCE/REDIS). You can select a value in `Namespace` as needed.
4. Use the input parameters of the TencentDB for Redis monitoring API for the configuration items here. For more information on the configuration items, please see [Memory Edition (5-Second)](https://intl.cloud.tencent.com/document/product/248/39507).
   - `Namespace`: select a namespace, such as `QCE/REDIS_MEM`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance ID**. You can also select `As InstanceName` (as the instance name).
     - For more information on how to get the instance list, please see [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.

>!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.  

![](https://main.qcloudimg.com/raw/d04580797c4d2359e9110e1b35312f05.png)

### CDN

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of CDN.
2. Select the configured Tencent Cloud Monitor data source that includes CDN monitoring from the `Queries to` data source list.
3. CDN metrics are divided into two namespaces: domain name in the Chinese mainland (Namespace=QCE/CDN) and domain name outside the Chinese mainland (Namespace=QCE/OV_CDN). You can select a value in `Namespace` as needed.
4. Use the input parameters of the CDN monitoring API for the configuration items here. For more information on the configuration items, please see [Chinese Mainland Domain](https://intl.cloud.tencent.com/document/product/248/39554).
   - `Namespace`: select a namespace, such as `QCE/CDN`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As Domain` by default, meaning that the instance list is displayed as **domain name**. You can also select `As ProjectId` (as the project ID).
     - For more information on how to get the domain name list, please see [DescribeDomains](https://intl.cloud.tencent.com/document/product/228/34020). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.

>!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.  


### BWP

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of BWP.
2. Select the configured Tencent Cloud Monitor data source that includes BWP monitoring from the `Queries to` data source list.
3. Use the input parameters of the BWP monitoring API for the configuration items here. For more information on the configuration items, please see [BWP](https://intl.cloud.tencent.com/document/product/248/34645).
   - `Namespace`: select a namespace, such as `QCE/BWP`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As BandwidthPackageId` by default, meaning that the instance list is displayed as **package ID**. You can also select `As BandwidthPackageName` (as the package name).
     - For more information on how to get the domain name list, please see [DescribeBandwidthPackages](https://intl.cloud.tencent.com/document/product/215/36919). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.

>!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.  

![](https://main.qcloudimg.com/raw/3c4fd46849f29b749ccf149863a7d8fa.png)

### CKafka
1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of CKafka.
2. Select the configured Tencent Cloud Monitor data source that includes CKafka monitoring from the `Queries to` data source list.
3. Use the input parameters of the CKafka monitoring API for the configuration items here. For more information on the configuration items, please see [Instance](https://intl.cloud.tencent.com/document/product/248/17297).
   - `Namespace`: select a namespace, such as `QCE/CKAFKA`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As InstanceId` by default, meaning that the instance list is displayed as **instance ID**. You can also select `As InstanceName` (as the instance name).
     - For more information on how to get the instance list, please see [DescribeInstances](https://intl.cloud.tencent.com/document/product/597/35357). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 10` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.


   >!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.  


![](https://main.qcloudimg.com/raw/b785c3bd601ded982bd32fccf852a6b5.png)

### EIP

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of EIP.
2. Select the configured Tencent Cloud Monitor data source that includes EIP monitoring from the `Queries to` data source list.
3. Use the input parameters of the EIP monitoring API for the configuration items here. For more information on the configuration items, please see [EIP](https://intl.cloud.tencent.com/document/product/248/34646).
   - `Namespace`: select a namespace, such as `QCE/LB`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As AddressId` by default, meaning that the instance list is displayed as **instance address ID**. You can also select `As AddressName` (as the address name) or `As AddressIp` (as the address IP).
     - For more information on how to get the instance list, please see [DescribeAddresses](https://intl.cloud.tencent.com/document/api/215/16702). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.

>!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.  

![](https://main.qcloudimg.com/raw/58ca7f13a2892871d4c0cfd96094207a.png)

### CFS

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of CFS.
2. Select the configured Tencent Cloud Monitor data source that includes CFS monitoring from the `Queries to` data source list.
3. Use the input parameters of the CFS monitoring API for the configuration items here. For more information on the configuration items, please see [CFS](https://intl.cloud.tencent.com/document/product/248/34644).
   - `Namespace`: select a namespace, such as `QCE/CFS`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As FileSystemId` by default, meaning that the instance list is displayed as **file system ID**. You can also select `As FsName` (as the file system name).
     - For more information on how to get the instance list, please see [DescribeCfsFileSystems](https://intl.cloud.tencent.com/document/product/582/34514). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.

>!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.  


![](https://main.qcloudimg.com/raw/fe5081dacbc5a1936f90a1e75fa7e7de.png)

### SCF

1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the **Query** tab on the left, configure the options to get the monitoring data of SCF.
2. Select the configured Tencent Cloud Monitor data source that includes SCF monitoring from the `Queries to` data source list.
3. Use the input parameters of the SCF monitoring API for the configuration items here. For more information on the configuration items, please see [SCF](https://intl.cloud.tencent.com/document/product/248/34638).
   - `Namespace`: select a namespace, such as `QCE/SCF_V2`.
   - `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
   - `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options.
   - `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
   - `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained.
     - To adapt to the habits of different users, the instance list is displayed as different fields, which is `As FunctionId` by default, meaning that the instance list is displayed as **function ID**. You can also select `As FunctionName` (as the function name).
     - For more information on how to get the instance list, please see [ListFunctions](https://intl.cloud.tencent.com/document/api/583/18582). You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
     - The `Show Details` button is displayed only when a non-template variable is selected.

>!In this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click **Add Query** in the top-right corner to add new queries.  

![](https://main.qcloudimg.com/raw/2db681ea42ff1918a71913984dd8eb03.png)

## Template and Variables

[Templates and variables](https://grafana.com/docs/reference/templating/) are dashboard optimization features offered by Grafana to create highly reusable and interactive dashboards. They generally allow Grafana to get different metrics from data sources and provide a way to dynamically modify them without modifying dashboards. The Tencent Cloud Monitor app currently provides variables such as region, CVM instance, and TencentDB for MySQL instance. The provided templates and variables are as shown below:  

| Variable    | Example   | Description |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Region                      | Namespace=QCE/CVM&Action=DescribeRegions                     | See [DescribeRegions](https://intl.cloud.tencent.com/document/product/213/15708). `Action` is fixed at `DescribeRegions`. `Namespace` is the namespace of the corresponding Tencent Cloud service, such as `QCE/CVM` or `QCE/CDB`. Only one region can be selected. If multiple regions or the `All` option are selected, the first region value will be used by default. |
| CVM instance              | Namespace=QCE/CVM&Region=ap-beijing&Action=DescribeInstances&InstanceAlias=PublicIpAddresses | See [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258). `Namespace` is fixed at `QCE/CVM`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `InstanceId` by default and can also be `InstanceName`, `PrivateIpAddresses`, or `PublicIpAddresses`. One or more CVM instances can be selected. |
| TencentDB for MySQL instance       | Namespace=QCE/CDB&Region=ap-beijing&Action=DescribeInstances&InstanceAlias=InstanceId | See [DescribeDBInstances](https://intl.cloud.tencent.com/document/product/236/15872). `Namespace` is fixed at `QCE/CDB`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `InstanceId` by default and can also be `InstanceName` or `Vip`. One or more TencentDB instances can be selected. |
| TencentDB for PostgreSQL instance       | Namespace=QCE/POSTGRES&Region=ap-beijing&Action=DescribeInstances&InstanceAlias=DBInstanceId | See [DescribeDBInstances](https://intl.cloud.tencent.com/document/product/409/16773). `Namespace` is fixed at `QCE/CDB`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `DBInstanceId` by default and can also be `DBInstanceName`, `PrivateIpAddresses`, or `PublicIpAddresses`. One or more TencentDB instances can be selected. |
| VPC NAT Gateway instance | Namespace=QCE/NAT_GATEWAY&Region=ap-beijing&Action=DescribeInstances&InstanceAlias=NatGatewayId | See [DescribeNatGateway](https://intl.cloud.tencent.com/document/product/215/34752). `Namespace` is fixed at `QCE/NAT_GATEWAY`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `NatGatewayId` by default and can also be `NatGatewayName`. One or more NAT Gateway instances can be selected. |
| VPC peering connection instance      | Namespace=QCE/PCX&Region=ap-beijing&Action=DescribeInstances&InstanceAlias=peeringConnectionId | See [Introduction](https://intl.cloud.tencent.com/document/api/215/15754). `Namespace` is fixed at `QCE/PCX`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `peeringConnectionId` by default and can also be `peeringConnectionName`. One or more peering connection instances can be selected (if it is CLB, then only one or multiple listeners can be selected). |
| CLB instance              | Namespace=QCE/LB_PRIVATE&Action=DescribeInstances&Region=$region&InstanceAlias=LoadBalancerId | See [DescribeLoadBalancers](https://intl.cloud.tencent.com/document/product/214/33830). `Namespace` can be `QCE/LB_PRIVATE`, `QCE/LB_PUBLIC`, or `QCE/LOADBALANCE`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-guangzhou` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `LoadBalancerId` by default and can also be `LoadBalancerName` or `LoadBalancerVips`. One or more CLB instances can be selected. |
| CLB listener              | Namespace=QCE/LB_PRIVATE&Action=DescribeListeners&Region=$region&Instance=$instance&listenerAlias=ListenerId | See [DescribeListeners](https://intl.cloud.tencent.com/document/product/214/33831). `Namespace` can be `QCE/LB_PRIVATE`, `QCE/LB_PUBLIC`, or `QCE/LOADBALANCE`. `Action` is fixed at `DescribeListeners`. `Region` is the region parameter, which can be a specific region value such as `ap-guangzhou` or a variable value such as `$region`. `Instance` is the instance ID, which can be a specific instance ID such as `lbl-rbw529fz` or a variable value such as `$instance`. `listenerAlias` is the display field of the listener, which is `ListenerId` by default and can also be `ListenerName` or `Port`. One or more CLB listeners can be selected. |
| TencentDB for MongoDB       | Namespace=QCE/CMONGO&Region=$region&Action=DescribeInstances | See [DescribeDBInstances](https://intl.cloud.tencent.com/document/product/240/34702). `Namespace` is fixed at `QCE/CMONGO`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `InstanceId` by default and can also be `InstanceName`. One or more TencentDB for MongoDB instances can be selected. |
| TencentDB for Redis       | Namespace=QCE/REDIS&Region=$region&Action=DescribeInstances | See [DescribeInstances](https://intl.cloud.tencent.com/document/product/239/32065). `Namespace` is fixed at `QCE/REDIS`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `InstanceId` by default and can also be `InstanceName`. One or more TencentDB for Redis instances can be selected. |
| CDN       | Namespace=QCE/CDN&Region=$region&Action=DescribeInstances | See [DescribeDomains](https://intl.cloud.tencent.com/document/product/228/34020). `Namespace` is fixed at `QCE/CDN`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `Domain` by default and can also be `ProjectId`. One or more CDN instances can be selected. |
| BWP       | Namespace=QCE/BWP&Region=$region&Action=DescribeInstances | See [DescribeBandwidthPackages](https://intl.cloud.tencent.com/document/product/215/36919). `Namespace` is fixed at `QCE/BWP`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `BandwidthPackageId` by default and can also be `BandwidthPackageName`. One or more BWP instances can be selected. |
| CKafka       | Namespace=QCE/CKAFKA&Region=$region&Action=DescribeInstances | See [DescribeInstances](https://intl.cloud.tencent.com/document/product/597/35357). `Namespace` is fixed at `QCE/CKAFKA`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `InstanceId` by default and can also be `InstanceName`. One or more CKafka instances can be selected. |
| EIP       | Namespace=QCE/LB&Region=$region&Action=DescribeInstances | See [DescribeAddresses](https://intl.cloud.tencent.com/document/product/215/16702). `Namespace` is fixed at `QCE/LB`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `AddressId` by default and can also be `AddressName` or `AddressIp`. One or more EIP instances can be selected. |
| CFS       | Namespace=QCE/CFS&Region=$region&Action=DescribeInstances | See [DescribeCfsFileSystems](https://intl.cloud.tencent.com/document/product/582/34514). `Namespace` is fixed at `QCE/CFS`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `FileSystemId` by default and can also be `FsName`. One or more CFS instances can be selected. |
| SCF       | Namespace=QCE/SCF_V2&Region=$region&Action=DescribeInstances | See [ListFunctions](https://intl.cloud.tencent.com/document/product/583/18582). `Namespace` is fixed at `QCE/SCF_V2`. `Action` is fixed at `DescribeInstances`. `Region` is the region parameter, which can be a specific region value such as `ap-beijing` or a variable value such as `$region`. `InstanceAlias` is the display field of the instance, which is `FunctionId` by default and can also be `FunctionName`. One or more SCF instances can be selected. |



### Creating variable

1. Go to a dashboard and click the **gear** icon in the top-right corner to enter the dashboard settings page.
2. Click **Variables** on the left to enter the variable configuration page and then click **+ Add variable** to enter the variable editing page.

### Editing variable

- `Name`: variable name, which is typically an English string and can be used to replace the original specific value in the dashboard.
- `Label`: visible label of the variable, which is used to describe the variable name more explicitly. For example, if `Name` is set to "region", `Label` can be set to "Region".
- `Type`: variable query method. Here, only `Query` can be selected, which means to send a request to the data source to get the variable list.
- `Data source`: data source from which to get the variable list. You can select any configured Tencent Cloud Monitor data source.
- `Refresh`: variable refresh method, which defines when the variable data is refreshed.
- `Query`: variable query statement. For more information, please see the variable examples and descriptions in the above table.

After all the variable information is completed, you can preview the variable values obtained from a query at the bottom of the page. If they are correct as expected, you can click **Add** to add the variable. After the variable is added successfully, click **Save** in the right menu to save it in the dashboard configuration.

The following shows how to configure the region and CVM instance variables by taking the CVM single-instance monitoring dashboard as an example:
![](https://main.qcloudimg.com/raw/0d7748ac3b23c8db01e1c6030d02029d.png)
![](https://main.qcloudimg.com/raw/a621bfccdde342fbab6f036db8284387.png)

### Using variable

After the variables are created, selection boxes will be displayed in the top-left corner of the dashboard page, where you can switch the variable values. Variables can be imported with two syntaxes: `$varname` and `[[varname]]`. Variables are often used in panel query statements. The following shows how to use variables in queries by taking the CVM single-instance monitoring dashboard as an example. In addition, variables can also be used in panel titles and text panels.
![](https://main.qcloudimg.com/raw/3911b142bd3fd72d5ea5cce1156e3714.png)
![](https://main.qcloudimg.com/raw/f07f7f5fdb39f2f6a4db5487e72d5898.png)


## Local Development

1. Clone this project to the local system:
```bash
$ git clone https://github.com/TencentCloud/tencentcloud-monitor-grafana-app.git
```
2. Install dependencies:
```bash
$ npm install
```
3. Start the development environment:
```bash
$ npm run analyze
```

### Docker support (recommended)

For faster development and testing, the [docker-compose.yml](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/blob/master/docker-compose.yml) file has been added. You just need to run:

```bash
$ docker-compose up
```

Then, visit http://localhost:3000


### Running on local Grafana

In addition, you can also clone this project to the local Grafana plugin directory and restart the local Grafana. Please make sure that its version is above 6.x.

## License

Tencent Cloud Monitor app plugin is provided under [Apache License 2.0](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/blob/master/LICENSE).

