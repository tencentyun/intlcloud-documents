CLS supports visual chart statistics of search and analysis results, and saves statistical charts to dashboards for continuous monitoring and viewing. A dashboard also provides an entry for creating statistical charts, supporting simple chart creation and custom chart creation.


## Directions

### Adding a chart via the **Search and Analysis** page

>! In this mode, you need to search for data to generate chart content. For more information, see [here](https://intl.cloud.tencent.com/document/product/614/37803).
>

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Search and Analysis** to go to the search and analysis management page.
3. Click the **Chart Analysis** tab and click **Add to Dashboard**.
4. In the pop-up window, enter information and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/f7780847c352e5f244b57ae36417e704.png)
<table>
	<tr><th>Parameter</th><th>Description</th></tr>
	<tr><td>Chart Name</td><td>Name of the chart.</td></tr>
	<tr><td>Target Dashboard</td><td>Type of the dashboard to which the chart is to be added.<ul style="margin: 0;"><li>If you select an existing dashboard, the chart will be added to an existing dashboard.</li><li>If you choose to create a dashboard, you need to create a dashboard and add the chart to it.</li></ul></td></tr>
	<tr><td>Dashboard</td><td>Name of the dashboard.</td></tr>
</table>


### Adding a chart via the Dashboard page

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. In the left sidebar, click **Dashboard** to go to the dashboard management page.
3. Click the ID/name of the target dashboard to go to the dashboard details page.
>? If you do not have a dashboard, please [create one](https://intl.cloud.tencent.com/document/product/614/37886).
>
4. Click **Create** and select a chart type as needed to create a chart.
![](https://qcloudimg.tencent-cloud.cn/raw/629154e713c86586c6c5bdbb07d0c765.png)
 - Quick Chart: you can drag and drop to easily create charts. However, this mode supports weaker statistical and analytical features.
![](https://qcloudimg.tencent-cloud.cn/raw/d4abd28ea7ee6393a8b4c03054236046.png)
 <table>
	<tr><th>Chart Element</th><th>Description</th></tr>
	<tr><td>Field list</td><td>A list of log topic fields. You can click or drag and drop a field to add it to the condition input boxes on the right.</td></tr>
	<tr><td>Metric</td><td>A metric is a parameter that measures a certain characteristic of an item, generally a numeric field. You can drag and drop a field from the field list on the left or click the "+" icon to display a drop-down list to select a field. After adding a field, you can click the settings icon next to the field to modify the field's aggregate calculation mode, which is **AVG** by default.</td></tr>
	<tr><td>Dimension</td><td>A dimension is perspective for analyzing a metric. It is generally a string-type field describing the attributes of an item. You can drag and drop a field from the field list on the left or click the "+" icon to display a drop-down list to select a field.</td></tr>
	<tr><td>Filter</td><td>A filter field is used to filter the attributes of data. You can drag and drop a field from the field list on the left or click the "+" icon to display a drop-down list to select a field. After adding a field, you can click the settings icon next to the field to modify the field filter mode, which is **Exist** by default.</td></tr>
	<tr><td>Sort</td><td>A sorting field is used to sort statistical results. Only specified condition fields (metrics) can be sorted. You are advised to click the "+" icon to display a drop-down list to select a field. After adding a field, you can click the settings icon next to the field to modify the sorting mode, which is **Ascending** by default.</td></tr>
	<tr><td>Max Rows</td><td>This row limit is used for quantitative filtering of statistical results. After a number is specified, the specified number of (or less) rows of statistical results will be displayed in ascending order. This parameter supports values ranging from 1 to 1,000 and defaults to **1000**.</td></tr>
</table>
 - Custom Chart: you can customize a search statement to create charts. This mode supports all statistical and analytical features.
![](https://qcloudimg.tencent-cloud.cn/raw/d8f95bab0eeda9116101cadc30a43978.png)
Enter the search and analysis statement and click **Generate Chart**.
5. Check whether the data configuration meets your requirements. The system automatically fills the data according to the chart data structure requirements. You can manually adjust the data structure if necessary.
![](https://qcloudimg.tencent-cloud.cn/raw/9ecddd28dd4934e5b59043fc91c4cdd1.png)
6. Click **Save**.




## FAQs

#### What should I do if no chart is generated when I click **Generate Chart** or switch the chart type after completing the configuration?

When the structure of the searched data matches the data structure required by the chart, the system automatically populates data by default. If the data structures are inconsistent, the chart will not be generated due to missing necessary fields (for example, the time field is missing in the case shown in the figure below). When this happens, check whether data meets requirements.

