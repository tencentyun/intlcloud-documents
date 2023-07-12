## Overview

CLS can be connected to Grafana to export the raw log data and SQL aggregate analysis results for display in Grafana. To display the results in Grafana, you only need to install the Tencent Cloud Monitor Grafana App and enter search and analysis statements in Grafana.

This document describes how to install and configure Grafana on CentOS.

## Directions

### Installing Grafana

1. For more information on how to install Grafana 8.0 or later, see [Install Grafana](https://grafana.com/docs/grafana/latest/installation/).
If your Grafana version is earlier than 8.0, configuration backup and upgrade are required. For details, see [Upgrade Grafana](https://grafana.com/docs/grafana/latest/installation/upgrading/).
The following example shows how to install Grafana 8.4.3 ([click here to get the latest version address](https://grafana.com/grafana/download?pg=get&plcmt=selfmanaged-box1-cta1&edition=oss)) on CentOS:
```
sudo yum install initscripts urw-fonts wget
wget https://dl.grafana.com/oss/release/grafana-8.4.3-1.x86_64.rpm
sudo yum install grafana-8.4.3-1.x86_64.rpm
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl status grafana-server
sudo systemctl enable grafana-server
```
2. After installation, we recommend you modify the [dataproxy] configuration in the `grafana.ini` file.
The default timeout period of Grafana is 30s. When you search for a large amount of data, a timeout may occur. For more information, see [Grafana proxy queries timeout after 30s with dataproxy.timeout and dataproxy.keep_alive_seconds to > 30s #35505](https://github.com/grafana/grafana/issues/35505). We recommend you set the timeout period to 60s to maximize the CLS capabilities. Modify the configuration as follows:
```markdown
[dataproxy]
timeout = 60
dialTimeout = 60
keep_alive_seconds = 60
```
To install more visual panels (such as pie and graph panels), install Grafana panel plugins by running the corresponding commands.
For example, if you want to install the pie panel, you can run the following command:
```
grafana-cli plugins install grafana-piechart-panel
service grafana-server restart
```
For information on more plugins, see [Grafana Plugins](https://grafana.com/grafana/plugins?type=panel).


### Installing Tencent Cloud Monitor Grafana App

#### Installation from the official plugin library

1. Go to the Grafana page.
2. On the **Configuration** > **Plugin** page, search for **Tencent Cloud Monitor** and click it to install it.
![](https://qcloudimg.tencent-cloud.cn/raw/0edf0fe478d2d3364a1c5cc5b9045824.png)


#### Installation on the command line

1. Install [Tencent Cloud Monitor Grafana App](https://grafana.com/grafana/plugins/tencentcloud-monitor-app/).
```sh
grafana-cli plugins install tencentcloud-monitor-app
# If the plugin cannot be found after the installation, it may be because that the plugin directory is not set to the default directory. In this case, go to the plugin installation directory and run the following command.
# If your CVM instance is not on CentOS, confirm the location of the Grafana plugin directory first and go to the directory for installation.
grafana-cli --pluginsDir ./  plugins install tencentcloud-monitor-app

# If you want to install an unofficial latest version of the plugin or install a beta version, run the following command:
grafana-cli --pluginUrl https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/archive/refs/tags/${VERSION}.zip plugins install tencentcloud-monitor-app
```
2. Run the following command to restart the Grafana service:
```sh
service grafana-server restart
```


### Configuring log data source

1. Enter `http://${Grafana IP address}:3000` (3000 is the default port number) in your browser to log in to Grafana.
2. On the left sidebar, select the **Settings** icon to go to the **Plugins** page. Select **Tencent Cloud Monitor** and click **Enable** on the **Config** page to enable the plugin.
3. On the **Data Sources** page, click **Add data source**.
4. Select **Tencent Cloud Monitor**, enter the data source name and Tencent Cloud [access key](https://console.cloud.tencent.com/cam/capi) as instructed, select **Cloud Log Service (cls)**, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/a1649f5eecf14583ba7b34292a98c58b.png)

### Trying out the CLB-DEMO preset dashboard

To quickly try out Tencent Cloud Monitor Grafana App, we recommend you use the [demo log](https://intl.cloud.tencent.com/document/product/614/43572) feature.

After creating a log topic, you can go to the preset `CLB Demo Access Log` dashboard to view preset content.
![](https://qcloudimg.tencent-cloud.cn/raw/5c9470f472d3b56d64993fb7e2196d52.png)


### Manually configuring dashboard

1. On the left sidebar, click **Create Dashboards**.
2. On the dashboard page, click **Add new panel**.
3. Select a data source, a **region**, and a **log topic**, and enter the corresponding search and analysis statement.
4. Click the time in the upper-right corner and refresh. Then you can view the requested data on the dashboard.

### Using log analysis to enter SQL statements for chart drawing and display

For the native charts on Grafana, data visualization is driven by data type. You can determine if and how a chart can be drawn based on the field type.

1. Draw a table.
Tables have no special requirements for data formats, and any content returned for the SQL statement can be displayed.
2. Draw a sequence diagram. The content returned for the SQL statement contains two fields, `analytic_time` of the time type and `log_count` of the numeric type, which can be used to complete the drawing.
```sql
* | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as analytic_time, count(*) as log_count group by analytic_time order by analytic_time limit 1000
```
3. Draw pie charts (Pie, Gauge, BarGauge, or Stat) (note that the `Value Options - show` chart configuration item on the right must be set to `All values`).
```sql
* | select try_cast(status as varchar) as status, count(*) as log_count group by status
```
The content returned for the SQL statement contains two fields: `status` of the character type and `log_count` of the numeric type. Grafana automatically selects the character type as the tag for drawing.
>! 
> - If `try_cast` is not used for type conversion, the chart drawing effect will be affected.
> - If the content field types returned for the SQL statement do not meet your chart drawing requirements, in addition to using the type conversion function in SQL, you can use the **Convert field type** feature on the **Transform** tab page of Grafana for visual display.
> 


### Viewing raw logs

For search scenarios, we recommend you use the Logs plugin to display data.
![](https://qcloudimg.tencent-cloud.cn/raw/4d0a45a5c2d6f2a8005d59df893bfc0a.png)

If you are using Grafana v8.3 or later, you can also use the **Extract fields** feature on the **Transform** tab page of Grafana to extract fields from the content returned for the search and view data in **Table**.
![](http://zuohaotu.com/Download/061616164532_01032b82797a2045fb8b17af2c32a6d6e.png?_gl=1*1kk2qfe*_ga*MTY3MzY1ODg3My4xNjU1MzY3MjU0*_ga_ZN9652QSEY*MTY1NTM2NzI1NC4xLjEuMTY1NTM2NzQwNi4w)


## Other Usage Guidelines for the Plugin
- [Git repository for Tencent Cloud Monitor Grafana App](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app)
- [CLS documentation](https://github.com/TencentCloud/tencentcloud-monitor-grafana-app/blob/master/%E6%97%A5%E5%BF%97%E6%9C%8D%E5%8A%A1.md)
- [CM data source template variables](https://intl.cloud.tencent.com/document/product/248/40024)
