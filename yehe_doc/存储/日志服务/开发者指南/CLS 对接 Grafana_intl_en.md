## Overview

CLS can be connected to Grafana to export the raw log data and SQL aggregate analysis results for display in Grafana. To display the results in Grafana, you only need to install the Grafana plugins for CLS and enter search and analysis statements in Grafana.

You can log in to [Grafana](http://106.53.153.13:3000/d/r6mrhEbGz/cls-demo) by using the following username and password for trial.
- Username: Viewer
- Password: clsdemo

This document describes how to install and configure Grafana on CentOS.

## Directions

### Installing Grafana

For more information on how to install Grafana, please see [Install Grafana](https://grafana.com/docs/grafana/latest/installation/).
The following uses installing Grafana grafana 8.3.3 on CentOS as an example ([click](https://grafana.com/grafana/download?pg=get&plcmt=selfmanaged-box1-cta1&edition=oss) to download the latest version):
```
sudo yum install initscripts urw-fonts wget
wget https://dl.grafana.com/oss/release/grafana-8.3.3-1.x86_64.rpm 
sudo yum install grafana-8.3.3-1.x86_64.rpm
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl status grafana-server 
sudo systemctl enable grafana-server  
```
To install more visual panels (such as pie and graph panels), please install Grafana panel plugins by running the corresponding commands.
For example, if you want to install the pie panel, you can run the following command:
```
grafana-cli plugins install grafana-piechart-panel
service grafana-server restart
```
For information on more plugins, please see [Grafana Plugins](https://grafana.com/grafana/plugins?type=panel).

### Installing and configuring Grafana plugins for CLS

1. Install Grafana plugins for CLS in the `/var/lib/grafana/plugins/` plugin directory.
```
cd /var/lib/grafana/plugins/
wget https://github.com/TencentCloud/cls-grafana-datasource/releases/latest/download/tencent-cls-grafana-datasource.zip
unzip tencent-cls-grafana-datasource
```
>? 
> - If your CVM instance is not on CentOS, please confirm the location of the Grafana plugin directory first and go to the directory for installation.
> - You need to install Grafana 7.0 or above. If your Grafana version is lower than 7.0, configuration backup and upgrade are required. For details, see [Upgrade Grafana](https://grafana.com/docs/grafana/latest/installation/upgrading/).
> 
2. Open the `grafana.ini` configuration file on the server where Grafana has been deployed.
 - The file path on macOS is `/usr/local/etc/grafana/grafana.ini`.
 - The file path on Linux is `/etc/grafana/grafana.ini`.
3. Set the `allow_loading_unsigned_plugins` parameter in **plugins**.
```
allow_loading_unsigned_plugins = tencent-cls-grafana-datasource
```
4. Run the following command to restart the Grafana service:
```
   service grafana-server restart
```
<span id="ConfigLogDataSource"></span>
### Configuring log data source
1. Log in to Grafana by accessing the following URL from your browser.
>? The default port of Grafana is `3000`.
>
```
http://Grafana IP address: 3000
```
2. On the left sidebar, select the **Settings** icon to go to the **Data Sources** page.
3. On the **Data Sources** page, click **Add data source**.
4. Select **Tencent Cloud Log Service Datasource** and configure the data source as instructed below.
![image-20201229200229285](https://main.qcloudimg.com/raw/275835ded7a0826d6027984ab9aa0b84.png)
<table>
<tr><th>Configuration Item</th><th>Description</th><tr>
<tr><td>Security Credentials</td><td> <b>SecretId</b> and  <b>SecretKey</b>: API request key, which is used for authentication. You can go to the <a href="https://console.cloud.tencent.com/cam/capi">API Key Management</a> page to get a key.</td><tr>
<tr><td>Log Service Info</td><td><ul><li><b>Region</b>: abbreviation of the CLS region. For example, enter `ap-beijing` for the Beijing region.</br>For the complete list of regions, please see <a href="https://intl.cloud.tencent.com/document/product/614/18940">Available Regions</a>.</li><li><b>TopicId</b>: log topic ID.</li></ul></td></tr>
</table>

### Configuring dashboard

1. On the left sidebar, click <b>Create Dashboards</b>.
2. On the dashboard page, click <b>Add new panel</b>.
3. Select the log data source you just created as the data source as shown below:
   ![image-20201229200254913](https://main.qcloudimg.com/raw/b0981c7c5e43d803d0eb694f3b737060.png)
4. Enter the query statement, select the format according to the panel type to be displayed, and the system will automatically convert the data for display in Grafana.
<table>
<tr><th>Format</th><th>Description</th><th>Configuration Item</th><tr>
<tr><td>Log panel</td><td>Log panel is used to shown log search results. Query syntax supports searching by keyword and fuzzy match. For more information, see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439). Eg. status:400</td><td><b>limit</b>: specifies the number of log search results to be returned.</td><tr>
<tr><td>Table panel</td><td>Table panel automatically shows the results of whatever columns and rows your query returns.</td><td>None</td><tr>
<tr><td>Graph,Pie,Gauge panel</td><td>In this pattern, there is a format transformation where data will be adapted to graph,pie,gauge panel. </td><td><ul><li><b>Metrics</b>: metrics to be collected.</li><li><b>Bucket</b>: (optional) name of the aggregate column.</li><li><b>Time</b>: (optional) if the result returned by a query is continuous time data, you need to specify the <b>Time</b> field; otherwise, leave it empty.</li></ul></td></tr>
</table>


## Samples

### Graph

A graph shows the PV and UV curves as shown below:

You can configure it according to the following information:

- The query statement is entered as shown below:

```
* | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as time, count(*) as pv,count( distinct remote_addr) as uv group by time order by time limit 1000

```
- **Format**: select **Graph,Pie,Gauge panel**.
- **Metrics**: **pv, uv**.
- **Bucket**: **leave it empty** if there are no aggregate columns.
- **Time**: **time**.

### Pie

A pie shows the distribution of request status codes as shown below:

You can configure it according to the following information:
- The query statement is entered as shown below:

```
* | select count(*) as count, status group by status

```
- **Format**: select **Graph,Pie,Gauge panel**.
- **Metrics**: **count**.
- **Bucket**: **status**.
- **Time**: **leave it empty** if it is not continuous time data.

### Bar gauge

A bar gauge shows the top 10 pages in terms of access latency as shown below:

You can configure it according to the following information:
- The query statement is entered as shown below:

```
* | select http_referer,avg(request_time) as lagency group by http_referer order by lagency desc limit 10
```
- **Format**: select **Graph,Pie,Gauge panel**.
- **Metrics**: **latency**.
- **Bucket**: **http_referer**.
- **Time**: **leave it empty** if it is not continuous time data.

### Table

A table shows the top 10 users in terms of access requests as shown below:

You can configure it according to the following information:
- The query statement is entered as shown below:

```
* | select remote_addr,count(*) as count group by remote_addr order by count desc limit 10

```
- **Format**: **Table**.



