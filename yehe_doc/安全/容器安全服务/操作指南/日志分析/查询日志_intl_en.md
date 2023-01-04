1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Security Operations** > **Log Analysis** on the left sidebar.
2. On the **Log Analysis** page, filter log analysis results and perform appropriate operations. 
 - Filter logs by time or type: At the top of the **Log Analysis** page, filter log analysis results by time (last 15 minutes, last hour, last 12 hours, last 24 hours, today, last 7 days, last 14 days, last 30 days, last 90 days, or a custom period) or by log type and click **OK**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/f59d2c3a1f66d25273739b7d5c5af5f1.png)
 - Filter logs by record field: At the top of the **Log Analysis** page, filter logs by field, which can be entered manually or automatically.
    - Manually enter the field: Enter the target field in the format of field name and field value and click **Search**. The search syntax description is as shown below.
<img src="https://qcloudimg.tencent-cloud.cn/raw/b362b6452cbe097762c3376f76786b67.png" style="zoom:67%;" />
    - Automatically enter the field: Click **Filter templates** and select the target template name, or click the historical record in the input box as shown above. To reuse a query template, click **Save filter** when manually entering a query statement to save the current configuration (log type and keyword).
<img src="https://qcloudimg.tencent-cloud.cn/raw/27cb4f6d94464d96037b1fb74bd8e1ae.png" style="zoom:67%;" />
 - Quickly view the log trend chart:
     - Method 1: To view logs within a specified period, scroll the mouse wheel to quickly view the blue bar chart above the log trend chart, which displays the statistical period and number of logs.
     - Method 2: Click the blue bar chart above the log trend chart to view more details.
3. On the **Log Analysis** page, fields are displayed in the log list based on the **Displayed fields**. If **Displayed fields** is **Raw log (_source)**, all log fields are listed. Up to 60,000 data entries can be listed in the console.
 - Customize fields to be displayed or hidden:
    - Add to view: Move the cursor to a hidden field and click **Add to view** on the right to add it to the displayed fields. Only selected displayed fields are listed, and hidden fields are not.
    ![](https://qcloudimg.tencent-cloud.cn/raw/f7f3c785abc34056c879b3f19a02f1a2.png)
    - Hide: Move the cursor to a displayed field and click **Remove** on the right to remove it from the displayed fields. The list on the right will no longer display this field.
    ![](https://qcloudimg.tencent-cloud.cn/raw/26d04db0a01e55fb9dd17580a701eb1d.png)
 - Export: Click **Export all** in the top-left corner of the field details, and log analysis will export 60,000 logs meeting the search condition as a file and download it through the browser to a local directory.
![](https://qcloudimg.tencent-cloud.cn/raw/16f963218161b19d0ce728f1701e42b5.png)
 - Switch the display mode: Click **Switch view** in the top-right corner of the field details to display the displayed fields in a table column.
![](https://qcloudimg.tencent-cloud.cn/raw/fafd6db8b797121d89a0fa4260d5e7aa.png)