## Prerequisites
The Tencent Cloud Monitor App plugin runs on Grafana 7.3 or above. Please start by setting up a Grafana environment. For more information, please see [Download Grafana](https://grafana.com/grafana/download).

## Step 1. Install and update

### Installation
There are many ways to install this plugin as shown below:

#### Using Grafana CLI

Check all versions of the plugin.

```bash
grafana-cli plugins list-versions tencentcloud-monitor-app
```

Install the latest version of the plugin.

```bash
grafana-cli plugins install tencentcloud-monitor-app
```
**If a plugin installation directory is customized, use the `--pluginsDir` parameter to configure the directory.**

Restart Grafana.
```bash
systemctl restart grafana-server
```

For more information, please see [Install Grafana plugins](https://grafana.com/docs/grafana/latest/plugins/installation/).

>!Grafana CLI is the only way of installation that is guaranteed to work. Any alternative methods should be considered as a workaround, as they do not ensure backward compatibility.

#### Using GitHub releases
Download the latest version of the Tencent Cloud Monitor App plugin code in [GitHub Releases](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/releases) (the resource name is `tencentcloud-monitor-app-[x.x.x].zip`) and place the decompressed code in the plugin directory of Grafana, which is `${GRAFANA_HOME}/plugins` by default. You can configure the plugin directory in `${GRAFANA_HOME}/conf/grafana.ini` (Linux/macOS) or `${GRAFANA_HOME}/conf/custom.ini` (Windows/macOS). For more information on the plugin directory, please see [plugins](https://grafana.com/docs/grafana/latest/administration/configuration/#plugins). After successful installation, restart Grafana.

#### Using source code
If you want to build the software package yourself or provide help, please see [here](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/blob/master/CONTRIBUTING.md).

### Update

```bash
grafana-cli plugins update tencentcloud-monitor-app
```

Restart Grafana.
```bash
systemctl restart grafana-server
```

#### Upgrading from version 1.x to 2.x
```bash
grafana-cli plugins upgrade tencentcloud-monitor-app
```

>!After the upgrade, you need to delete the old data source and configure a new one.

### More options
If you need more help, please see [Grafana CLI](https://grafana.com/docs/grafana/latest/administration/cli/) or run the following command:

```bash
grafana-cli plugins --help
```


## Step 2. Enable the plugin

1. Hover over the **gear** icon on the left sidebar and click **Plugins** to enter the plugin management page. If the Tencent Cloud Monitor App plugin is displayed in the plugin list, it indicates that the plugin has been installed successfully.
![](https://main.qcloudimg.com/raw/a658f09d212f374ccc54b8d394b5e635.png)
2. Enter the app details page and click **Enable**. After the Tencent Cloud Monitor App plugin is enabled successfully, you can use it in Grafana.
![](https://main.qcloudimg.com/raw/2cc428c778007aa30737b170b7cf7bbe.png)

## Step 3. Configure a data source

The Tencent Cloud Monitor App plugin gets the monitoring metric data of Tencent Cloud services by calling CM APIs. You can configure the data sources of the corresponding Tencent Cloud services in the following steps.    
1. Hover over the **gear** icon on the left sidebar and click **Data Sources** to go to the data source management page.
![](https://main.qcloudimg.com/raw/5e2c922ebb1b8c6c6f5c2769cd7b8b59.png)
2. Click **Add data source** in the top-right corner and then click **Tencent Cloud Monitoring** to enter the data source configuration page.
![](https://main.qcloudimg.com/raw/51d09bf84540ecb6f1730912a5d5bdf9.png)
3. Set `Name`: data source name, which can be customized and is `Tencent Cloud Monitoring` by default.  
4. Set `SecretId` and `SecretKey`: security certificate information required for CM API calls, which can be obtained on the [TencentCloud API Key](https://console.cloud.tencent.com/cam/capi) page in the Tencent Cloud console.
5. Select Tencent Cloud services whose monitoring data you want to get.  
6. Click **Save & Test** to test whether the data source is configured correctly, and if so, you can use it in the dashboard.
![](https://main.qcloudimg.com/raw/85ed048d5a163c8028e9cfe19b4d35d1.png)

## Step 4. Create a dashboard


You can create a dashboard in any of the following ways:

### Quick creation

Hover over the **plus sign** on the left sidebar and click **+Dashboard** to create a dashboard.

### Management page

Hover over the **grid** icon on the left sidebar and click **Manage** to enter the dashboard management page. Click **New Dashboard** to create a dashboard. You can also perform various dashboard management operations on this page, such as creating folders, moving dashboards, or importing dashboards.

### Template import

Hover over the **gear** icon on the left sidebar and click **Plugins** to go to the plugin management page. Click **Tencent Cloud Monitor** to enter the application details page, switch to the `Dashboards` tab, and select a dashboard template to import.
![](https://main.qcloudimg.com/raw/c2678540c0eeb27b2d6acca5712ba2c5.png)


## Step 5. Configure panel data

![](https://main.qcloudimg.com/raw/8bcee2cb5f8b1f8b1e5c7683841d434a.png)

After creating a dashboard, you can configure the panel information to get the monitoring data from Tencent Cloud Monitor. The following describes how to do so by taking Graph as an example.
1. Click **Add Query** in **New Panel** to enter the panel configuration page. On the `Query` tab on the left, select the Tencent Cloud Monitor data source configured above.
2. Set `Namespace`: select a namespace. For example, the namespace of CVM monitoring is `QCE/CVM`. Click [here](https://intl.cloud.tencent.com/zh/document/product/248/40019) to view the namespaces of other Tencent Cloud services.
3. Set `Region`: select a region. The region list will be automatically obtained according to the `Namespace` option.
4. Set `MetricName`: select a metric name. The metric list will be automatically obtained according to the `Namespace` and `Region` options. Click [here](https://intl.cloud.tencent.com/zh/document/product/248/40019) to view the metric documents of different Tencent Cloud services.
5. Set `Period`: select a statistical period. The period list will be automatically obtained according to the `MetricName` option.
6. Set `Instance`: select an instance, which corresponds to the `Instances.N` field of the input parameter. The instance list will be automatically obtained. Click [here](https://intl.cloud.tencent.com/zh/document/product/248/40019) to view the instance list API documents of different Tencent Cloud services.
   - To adapt to the habits of different users, the instance list is displayed as different fields, which is the **ID** of the corresponding service by default.
   - The `Show Details` button is visible only when you select a non-template variable. You can toggle `Show Details` to `true` to display the instance request parameters, which are `Offset = 0` and `Limit = 20` by default. If you need to change the instance query criteria, you can configure corresponding parameters as instructed in the API documentation.
   - **Note:** in this application, a single query to get the monitoring data is an atomic operation, i.e., querying the monitoring data of a certain metric of a certain instance. Therefore, you can select only one instance at a time. If you need to query the monitoring data of multiple instances, you can click `+ Query` at the bottom to add new queries.
