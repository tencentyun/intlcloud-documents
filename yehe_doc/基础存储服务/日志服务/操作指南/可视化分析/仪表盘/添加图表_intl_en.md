CLS supports visual chart statistics of search and analysis results, and saves statistical charts to dashboards for continuous monitoring and viewing. A dashboard also provides an entry for creating statistical charts, supporting simple chart creation and custom chart creation.

## Directions

### Adding a chart via the Search and Analysis page

>! In this mode, you need to search for data to generate chart content. For more information, see [here](https://intl.cloud.tencent.com/document/product/614/37803).
>

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Search and Analysis** to go to the search and analysis management page.
3. Click the **Chart Analysis** tab and click **Add to Dashboard**.
4. In the pop-up window, enter information and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f7780847c352e5f244b57ae36417e704.png" style="width: 60%;" /></br>
<table>
<thead>
<tr>
<th align="left">Form Element</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Chart Name</td>
<td align="left">The chart name.</td>
</tr>
<tr>
<td align="left">Target Dashboard</td>
<td align="left">The dashboard type of the chart. If you select **To an existing dashboard**, the chart will be added to an existing dashboard. If you select **Create Dashboard**, you need to create a dashboard and add the chart to it.</td>
</tr>
<tr>
<td align="left">Dashboard</td>
<td align="left">The dashboard name.</td>
</tr>
</tbody></table>

### Adding a chart via the Dashboard page

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls/overview).
2. On the left sidebar, click **Dashboard** to enter the dashboard management page.
3. Click the ID/name of the target dashboard to enter the dashboard details page.
>? If you do not have a dashboard, [create one](https://intl.cloud.tencent.com/document/product/614/37886).
>
4. Click **Create** and select a chart type as needed to create a chart.
![](https://qcloudimg.tencent-cloud.cn/raw/629154e713c86586c6c5bdbb07d0c765.png)
 - Quick Chart: You can drag and drop to easily create charts. However, this mode supports weaker statistical and analytical features.
![](https://qcloudimg.tencent-cloud.cn/raw/d4abd28ea7ee6393a8b4c03054236046.png)
<table>
<thead>
<tr>
<th align="left">Chart Element</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Field</td>
<td align="left">The list of current log topic fields. You can click or drag and drop a field to the condition input box on the right.</td>
</tr>
<tr>
<td align="left">Metric</td>
<td align="left">A metric measures a certain characteristic of an item, generally a numeric field. You can drag and drop a field from the field list on the left or click the "+" icon to display a drop-down list to select a field. After adding a field, you can click the settings icon next to the field to modify the field's aggregate calculation mode, which is "AVG" by default.</td>
</tr>
<tr>
<td align="left">Dimension</td>
<td align="left">A dimension is the perspective for analyzing a metric. It is generally a string-type field describing the attributes of an item. You can drag and drop a field from the field list on the left or click the "+" icon to display a drop-down list to select a field.</td>
</tr>
<tr>
<td align="left">Filter</td>
<td align="left">A filter field filters data attributes. You can drag and drop a field from the field list on the left or click the "+" icon to display a drop-down list to select a field. After adding a field, you can click the settings icon next to the field to modify the field filter mode, which is "Exist" by default.</td>
</tr>
<tr>
<td align="left">Sort</td>
<td align="left">A sorting field sorts statistical results. Only specified condition fields can be sorted. We recommend you click the "+" icon to display a drop-down list to select a field. After adding a field, you can click the settings icon next to the field to modify the sorting mode, which is "Ascending" by default.</td>
</tr>
<tr>
<td align="left">Row quantity limit</td>
<td align="left">Row quantity limit filters the number of statistical results. After it is set, a certain number of statistical results will be displayed in reverse order. The valid range is 1–1,000, and the default value is `1000`.</td>
</tr>
</tbody></table>
 - Custom Chart: You can customize a search statement to create charts. This mode supports all statistical and analytical features.
Enter the search statement to automatically generate a chart.
![](https://qcloudimg.tencent-cloud.cn/raw/d8f95bab0eeda9116101cadc30a43978.png)
5. Check whether the data configuration meets the requirements. The system will automatically fill in data based on the chart data structure. If the data type doesn't match, you need to **convert the data** manually and adjust the configuration. For more information, see [Data conversion](https://intl.cloud.tencent.com/document/product/614/47787).
![](https://qcloudimg.tencent-cloud.cn/raw/9ecddd28dd4934e5b59043fc91c4cdd1.png)
6. Click **Save**.
