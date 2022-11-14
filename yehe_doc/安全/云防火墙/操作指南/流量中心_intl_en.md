Traffic Monitoring provides incoming access statistics, outgoing access analysis, and inter-VPC activities tabs based on inbound, outbound, and inter-VPC traffic. This topic describes how to view the traffic status and understand the visual information on the three tabs in Traffic Monitoring.

## [Incoming access statistics](id:out)
On the **Incoming access statistics** page, you can view the IP addresses, access count, and volume of the inbound traffic. You can also view details about the access to specific assets in different time periods in specified regions on the map, and view the ranking of traffic in different regions.

#### Directions

1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw), click **Traffic Monitoring** in the left navigation pane, and click the **Incoming access statistics** tab.
2. In the **Incoming access statistics** tab, click **All assets** to view the access to each asset in the current region. You can also view the traffic in different time periods, such as the last 24 hours or the last 7 days.
![](https://qcloudimg.tencent-cloud.cn/raw/e5483d1a0764228f23c16ff98427b217.png)
3. View the incoming access to assets in regions around the world and within China on the map.
	- Select **All regions** to view the distribution of traffic in each country or region around the world.
	- Select **China** to view the distribution of traffic in each province of China.
>!
>- The carousel slider on the left side displays the top 5 countries/regions or provinces with the highest traffic volume and access count. You can hover the mouse cursor over a country/region or province to view the access by IP addresses.
>- The color depth on the map indicates the traffic volume in each region. A darker color indicates higher traffic. You can hover the mouse cursor over a country/region or province to view details.
>- The icons on the right side are used to refresh data in the carousel slider, reset the map to the initial position, expand the map, and zoom in and out the map.

![](https://qcloudimg.tencent-cloud.cn/raw/942d94ad61fec3fd1c9f10d0d8d6b5ce.png)
4. On the right side of the map, click <img src="https://main.qcloudimg.com/raw/2b3a0dcde8a1f294cfb8d9ba532d8810.png" style="margin:0;"> to view the traffic statistics in the global mode.
5. In the global mode, view the rankings in different dimensions.
  - The carousel slider on the left side of the map displays top 10 countries/regions or provinces with the highest traffic volume and access count.
  - The carousel slider on the right side of the map displays the top 5 ports with the most visits, the protocol distribution of incoming access, the top 5 assets with the most visits, and the top 5 assets with the highest traffic volume.
>? When a specific asset is selected, the asset ranking is not displayed in the carousel slider on the right side.

  - The line chart below the map shows the traffic bandwidth of incoming access within the current time range. You can also view the peak bandwidth in and the total traffic volume in the last 7 days or 24 hours.
    ![](https://qcloudimg.tencent-cloud.cn/raw/d9f08b227831e50bc946fe6a061ed139.png)
6. In the lower part of the page, view details of the incoming access IP addresses.
>? For brevity, the list only displays the access information of top 500 IP addresses by default.

The features of the **Incoming access** list under **Internet access** are described below, and those of other lists are similar.
1. In the **Incoming access** list, enter an **exact** IP address of an access source in the **External address** search box, enter an **exact** IP address of an asset in the **Destination port** search box, or enter an **exact or fuzzy** place name in the **Location** search box, and then click **Start search** to search for access details. 
	![](https://qcloudimg.tencent-cloud.cn/raw/bca7279c3e8078e054412a4f40a114a8.png)
2. View data details. You can view traffic logs, threat profile, or asset details in the access list.
	- View traffic logs
		1. Click **Traffic logs** in the action column on the right.
		2. On the **Traffic logs** page, you can view details about the access between specified IP addresses. You can also filter the results by access source and access destination to obtain the details about the access from the same source to the same asset.
	- View the threat profile
		1. Select **More** -> **Threat profile** in the action column on the right.
		2. On the **Threat profile** page, view the threat profile of the external address and then perform tracing and auditing.    
   - View asset details
		1. Select **More** -> **Asset details** in the action column on the right.
		2. On the **Asset details** page, view exposed assets and security events about the asset.

## Outgoing access analysis
You can view details about the outgoing access from assets in the last 7 days, and learn about the outgoing traffic, outgoing domain names, and outgoing destinations on the **Outgoing access** page.
#### Directions

1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw), click **Traffic Monitoring** in the left navigation pane, and click the **Outgoing access** tab.
	- In the **Outgoing access overview** module, you can view the access status of outbound traffic in the last 7 days or 24 hours. You can also filter the results by time and asset to obtain the outgoing access statistics of specific assets within a time range.
	- On the left side of the **Outgoing access overview** module, you can view the outgoing domain names and outgoing destinations of assets, the number of outgoing assets, and the number of alerts. You can select an asset from the **All assets** drop-down list to view the outgoing access of the asset.
	- In the line chart in the lower part, you can view the bandwidth in the last 7 days or 24 hours. Hover the mouse cursor over the line chart to view the bandwidth at a point in time.
	- On the right side of the **Outgoing access overview** module, you can view the top 5 most requested domain names, the top 5 most requested addresses, the address with the most access traffic, the top 5 assets with the most outgoing access requests, and the top 5 assets with the highest outgoing traffic in the last 7 days or 24 hours.
   ![](https://qcloudimg.tencent-cloud.cn/raw/12040c3c9b10c4878f7dadf17fb373d3.png)
2. You can view the access statistics of outgoing traffic, outgoing domain names, outgoing destinations, and outgoing assets in the lists below. Access details are available in all the lists except the **Outgoing traffic**.
![](https://qcloudimg.tencent-cloud.cn/raw/fcfcb2c5f67fb9259ffa2b856e24e204.png)
3. The **Outgoing destination** list is used as an example of how to view access details. Click **Outgoing destination**, and click **Access details** in the action column on the right side of an IP address to enter the **Outgoing destination details** page.
![](https://qcloudimg.tencent-cloud.cn/raw/49dd462ea216973123289f8cd8e95a52.png)
4. On the **Outgoing destination details** page, you can view the access count and traffic volume of assets to the IP address in the last 7 days or 24 hours, and the location of the IP address. You can also view the assets accessed from the IP address. To learn more about the traffic logs and threat profile, please see [Incoming access statistics](#out).
<img src="https://qcloudimg.tencent-cloud.cn/raw/55b8f086540c1e6125f1ece425cc15c3.png" style="zoom: 50%;" />
5. To learn more about the outgoing access of an asset in the list, click **Traffic logs** or **Outgoing details** in the action column on the right side of the instance list to view the traffic logs of the asset or the IP addresses and domain names accessed by the asset in the last 7 days or 24 hours.
<img src="https://qcloudimg.tencent-cloud.cn/raw/068476bccdb0256d38647ae1a50bc4f4.png" style="zoom:67%;" />


## Inter-VPC activities
You can view traffic access between VPCs and the protocol distribution on the **Inter-VPC activities** page.
#### Directions

1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw), click **Traffic Monitoring** in the left navigation pane, and click the **Inter-VPC Activities** tab.
2. In the **Inter-VPC activities** tab, select a VPC instance from the filter box in the upper part and select a time period.
![](https://qcloudimg.tencent-cloud.cn/raw/006e6d789602e2a008ea3319a6dd8aed.png)
3. Hover the mouse cursor over the line chart of traffic statistics to view the bandwidth at a specific time. Hover the mouse cursor over the donut chart of protocol distribution on the right to view the distribution of protocols.
    ![](https://qcloudimg.tencent-cloud.cn/raw/a4e3e1e1f53c3c80de4753f93f1b21c8.png)
4. In the lower part of the page, view the IP addresses in access between VPCs, and view the access source, access destination, and access count of IP addresses in the VPCs. Enter an access source, access destination, or destination port in the search boxes to start an exact search. For more information, please see [Incoming access statistics](#out).
![](https://qcloudimg.tencent-cloud.cn/raw/0cdc8b71579007abe01eb55efffaac2d.png)

## More information
For questions about Traffic Monitoring, please see [Bandwidth](https://intl.cloud.tencent.com/document/product/1160/49825).
