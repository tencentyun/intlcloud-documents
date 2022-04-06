During the operation of Tencent Cloud direct connect, each tunnel takes different traffic load for different business. If the tunnel is full of business traffic, the connection will be unavailable. To solve this issue, Tencent Cloud direct connect launches the traffic analysis feature at the gateway granularity to inform you the IPs of traffic in "Top N" ranklist and the traffic details and help you adjust your business.


## Prerequisite
- You have created a direct connect gateway as instructed in [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).
- Business traffic has flowed in the gateway.


## Directions
1. Log in to the [Direct Connect Gateway console](https://console.cloud.tencent.com/dc/dc), and click **Direct Connect Gateway** in the left sidebar.
2. Select a region and VPC at the top of the **Direct Connect Gateway** page. Click the **ID/Name** of the target direct connect gateway to enter its details page.
![]()
3. Click **Traffic Analysis** on the details page and enable the **Traffic collection task**.
![]()
	When enabling, the system will collect statistics on all data traffic passing through the gateway and display the statistical result in about 3-5 minutes.
4. View the traffic analysis result.
![]()
 - Settings of time period and time granularity
    - For time period, you can select **3 minutes ago**, **1 hour ago** or **7 days ago**.
    - For time granularity, you can select **1 minute**, **1 hour** or **1 day**. This indicates the traffic statistics is collected every minute/hour/day.
>?  
>- If you estimate that the traffic analysis time is about 0-30 minutes, we recommend that you select **1 minute** for time granularity. If the analysis time is more than 30 minutes, we recommend that you select **1 hour**.
>- If you need more accurate and fine-grained traffic statistics and analysis within 3 minutes, we recommend that you select **3 minutes ago** for time period and set 1 hour for custom time span (for example, 2021-08-06 14:18 to 2021-08-06 15:17) and select **1 minute** for time granularity.
> 
 - View the "TOP N" information  
The tunnel traffic ranklist can be displayed in four ways, including **Top 5**, **TOP 20**, **TOP 50** and custom top N. If you want to view the traffic of a specified IP, you can enter the IP address in the input box on the right.
