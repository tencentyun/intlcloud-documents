## Overview

CLS provides quick statistical analysis of fields. You can quickly analyze field value distribution, trends over time, and numerical statistics without writing query statements. For example, you can quickly collect statistics on the top 5 request APIs and API response time trends.

## Prerequisite

You have enabled quick analysis feature for fields in index configuration.

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Search and Analysis** to go to the search and analysis page.
3. Click the drop-down lists of **Logset** and **Log Topic** to select the log topic to be searched.

4. Click **Log Time** and select a log time for search.
You can select **Recent Time** or **Relative Time** or customize the time range.
5. On the left sidebar, click the field name.

> ?
> - The quick analysis feature for fields of the string type (text) is slightly different from that for fields of the numeric type (long and double):
>   - String: supports field value distributed statistics, intelligent aggregated time line charts and top 5 values
>   - Numeric: supports intelligent aggregated time line charts and top 5 values
> - Gray fields, such as `__PKG_LOGID__` in the above figure, cannot be clicked because statistics are not enabled for them.
> 
6. In the pop-up quick analysis window, click a statistics chart to automatically generate the corresponding search statement and chart. You can query chart details here, and you can further modify the search statement and chart configuration to get an analysis chart that better fits your specific needs.


