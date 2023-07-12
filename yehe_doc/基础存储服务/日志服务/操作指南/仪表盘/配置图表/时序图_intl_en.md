A sequence diagram requires statistics to have a time series field, so that it can organize and aggregate the metric in chronological order. It visually reflects the change trend of a metric over time. It is suitable for trend analysis scenarios, for example, analyzing the trend of the daily number of 404 errors in the past week.

## Chart Configuration

### General configuration



| Configuration Item | Description |
| -------- | ------------------------------------------------------------ |
| Chart Name | Set the display name of the table, which can be left empty.                                |
| Legend     | Set the chart legends. You can control the legend styles and positions and add comparison data to legends. |
| Tooltip | Control the content style of the bubble tip displayed when the mouse is hovered over. |
| Unit | Set the unit of all metric-type fields in the chart. For more information, see [Unit Configuration](https://intl.cloud.tencent.com/document/product/614/47788).     |


### Changes



| Configuration Item | Description |
| -------- | ------------------------------------------------------------ |
| Changes | After the changes feature is enabled, you can compare the data in a time period with the data in the same period X hours, days, months, or years ago. The comparison data is displayed as dotted lines in the chart. |



### Sequence diagram configuration



| Configuration Item | Description |
| ------ | ------------------------------------------------------------ |
| Sequence diagram | Drawing Style: Set the display style of data on coordinate axes. If you select a line, column, or dot, it will be a line chart, histogram, or scatter plot respectively. <br />Linear: Set whether to smooth the connections between points. <br />Line Width: Control the thickness of lines. <br />Fill: Control the transparency of the fill area. If this value is 0, there will be no fill. <br />Display Point: Display data points. If there is no data, no points will be displayed. <br />Null: Control the processing of a sequence point if there is no data on the point. This value is 0 by default. <br />Stack: Control whether to display data in a stack. |
| Axes | Show: Show/Hide axes. <br />MAX/MIN: Control the maximum and minimum values displayed on coordinate axes. Coordinate areas greater than the maximum value or smaller than the minimum value will not be displayed. |

Sample drawing style:
![](https://qcloudimg.tencent-cloud.cn/raw/f6ea7fdde1dd41fe5738488faabbd06d.png)

Sample fill:
![](https://qcloudimg.tencent-cloud.cn/raw/f6ea7fdde1dd41fe5738488faabbd06d.png)

Sample null value:
![](https://qcloudimg.tencent-cloud.cn/raw/272e502e60446d620031b54abeacebc0.png)

### Threshold configuration



| Configuration Item | Description |
| -------- | ------------------------------------------------------------ |
| Threshold configuration | Threshold Point: Set the threshold points. You can add multiple threshold intervals. You can click a threshold color to open the color picker to customize the color. <br />Threshold Display: Control the style of threshold display, including three modes: threshold line, area filling, and both. If this option is disabled, no threshold will be used. |


## Chart Operations

### Time range

![](https://qcloudimg.tencent-cloud.cn/raw/0764c42fde7d9a739b493f0e879bda51.png)

Hover over the chart, press and hold the left mouse button, and drag to trigger the selector and use time in the selected area as the time range. This is suitable for scenarios such as drilling down into the time range of abnormal points.

## Use Cases

A sequence diagram requires fields of time type during creation and depends on various functions to process time fields during use. For more time functions for sequence diagram, see [Time and Date Functions](https://cloud.tencent.com/document/product/614/58981).

Calculate the PV and UV per minute:
```
* | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as time, count(*) as pv,count( distinct remote_addr) as uv group by time order by time desc limit 10000
```
![](https://qcloudimg.tencent-cloud.cn/raw/1c77605c14921b3768b04176b1817684.png)

Calculate the PV for each protocol type per minute:
```
* | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as time, protocol_type, count(*) as pv group by  time, protocol_type order by time desc limit 10000
```
![](https://qcloudimg.tencent-cloud.cn/raw/09400ef819ba330b6394b357badafe74.png)

Calculate the request failure rate (%) per minute:
```
* | select date_trunc('minute', __TIMESTAMP__) as time, round(sum(case when status = 404 then 1.00 else 0.00 end)/ cast(count(*) as double)*100,3) as "404 proportion", round(sum(case when status >= 500 then 1.00 else 0.00 end)/cast(count(*) as double)*100,3) as "5XX proportion", round(sum(case when status >= 400 and status < 500 then 1.00 else 0.00 end)/cast(count(*) as double)*100,3) as "4XX proportion", round(sum(case when status >= 400  then 1.00 else 0.00 end)/cast(count(*) as double)*100,3) as "total failure rate" group by time order by time limit 10000
```
![](https://qcloudimg.tencent-cloud.cn/raw/b74434e4c08111d570d04cf7ec8f9313.png)
