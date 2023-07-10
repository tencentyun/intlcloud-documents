
CLS provides a great variety of chart types. You can use SQL to flexibly collect system and business metrics in logs and display them in charts. You can also save chart analysis results to dashboards for long-term monitoring.

## Chart Types

<table>
<thead>
<tr><th style="width: 17%">Chart Type</th><th style="width: 66%">Use Cases</th><th style="width: 17%">Details</th></tr>
</thead>
<tbody><tr>
<td>Table</td>
<td>A table is the most common type of data display, where data is organized for comparison and counting. It is suitable for most scenarios.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/47778">Table</a></td>
</tr>
<tr>
<td>Sequence diagram</td>
<td>A sequence diagram requires statistics to have a time series field, so that it can organize and aggregate the metric in chronological order. It visually reflects the change trend of a metric over time. It is suitable for trend analysis scenarios, for example, analyzing the trend of the daily number of 404 errors in the past week.</td>
<td><a href="https://www.tencentcloud.com/document/product/614/47779">Sequence Diagram</a></td>
</tr>
<tr>
<td>Bar chart</td>
<td>A bar chart describes categorical data. It visually reflects the comparison of each category in size. It is suitable for category statistics scenarios, for example, collecting the numbers of each type of error codes in the last 24 hours.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/47780">Bar Chart</a></td>
</tr>
<tr>
<td>Pie chart</td>
<td>A pie chart describes the proportions of different types. It measures the proportion of each type by the slice size. It is suitable for proportion statistics scenarios, for example, analyzing the proportions of different error codes.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/47781">Pie Chart</a></td>
</tr>
<tr>
<td>Individual value plot</td>
<td>An individual value plot describes a single metric, typically a key metric of business value. It is suitable for collecting daily, weekly, or monthly metrics such as PV and UV.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/47782">Individual Value Plot</a></td>
</tr>
<tr>
<td>Gauge chart</td>
<td>A gauge chart describes a single metric. Unlike an individual value plot, it is generally used with a threshold to measure the metric status. It is suitable for rating scenarios, such as system health monitoring.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/47783">Gauge Chart</a></td>
</tr>
<tr>
<td>Map</td>
<td>A map shows the geographic location of data through the position of graphics. It is generally used to display the distribution of data in different geographic locations. It is suitable for geographic statistics scenarios, such as the geographic distribution of attacker IPs.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/47784">Map</a></td>
</tr>
<tr>
<td>Sankey diagram</td>
<td>A Sankey diagram is a special type of flow diagram used to describe the flow of one set of values to another set. It is suitable for directional statistics scenarios, such as firewall source and destination IP traffic.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/47785">Sankey Diagram</a></td>
</tr>
<tr>
<td>Word cloud</td>
<td>A word cloud is a visual representation of the frequency of words. It is suitable for audit statistics scenarios, such as high-frequency operations.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/47786">Word Cloud</a></td>
</tr>
</tbody></table>

## Common Features

<table>
<thead>
<tr><th style="width: 17%">Feature</th><th style="width: 66%">Description</th><th style="width: 17%">Details</th></tr>
</thead>
<tbody><tr>
<td>Data conversion</td>
<td>Data conversion allows you to perform further processing of search results, including modifying data types, selecting fields for chart creation, and merging groups. This satisfies your chart creation needs without modifying SQL statements.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/47787">Data Conversion</a></td>
</tr>
<tr>
<td>Unit conversion</td>
<td>Charts support automatic unit conversion. After you select an original unit, when the value meets the conversion factor, it will be automatically converted to the next higher unit. Units support decimal place configuration.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/47788">Unit Configuration</a></td>
</tr>
<tr>
<td>Adding chart to dashboard</td>
<td>You can save chart analysis results to a dashboard for long-term monitoring.</td>
<td><a href="https://cloud.tencent.com/document/product/614/63399">Adding Chart</a></td>
</tr>
</tbody></table>
