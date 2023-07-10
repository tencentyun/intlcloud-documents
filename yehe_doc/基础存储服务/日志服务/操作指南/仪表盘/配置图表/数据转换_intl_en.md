Data conversion allows you to perform further processing of search results, including modifying data types, selecting fields for chart creation, and merging groups. This satisfies your chart creation needs without modifying SQL statements.

## Enabling Data Conversion

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Search and Analysis** to go to the search and analysis page.
3. Select the **Chart Analysis** tab and set **Data Conversion** below to ![](https://qcloudimg.tencent-cloud.cn/raw/90402f86446bf0509031d128da8dddc9.png).

4. On the **Dashboard Chart Editing** page, select the **Data Conversion** tab and set **Data Conversion** to ![](https://qcloudimg.tencent-cloud.cn/raw/90402f86446bf0509031d128da8dddc9.png).


## Use Cases



After executing a SQL analysis statement, you may want to visualize the results on different types of charts. As different charts require different attributes and numbers of fields, a problem will occur if the attributes and number of fields of the statement results are different from those required by the chart. In this case, you can modify the SQL statement to adapt it to the requirements of the chart. You can also configure data conversion to further process the results in order to meet the requirements for chart creation.

## Using Data Conversion

### Selecting fields for chart creation


After using a SQL statement to find the results in the above list, you can select fields from the field list to create a chart based on the selected fields. This operation is equivalent to `SELECT`. Below is the result after some fields are selected:

### Converting the field type



In the SQL statistics results, each field has a default type. Fields of the `# (numeric)` type will be identified as metrics, fields of the `t (string)` type will be identified as common dimensions, and fields of the `time type` will be identified as time dimensions based on the chart type. Then, they will be matched with the field attributes required for chart creation. For example, in a sequence diagram, the time dimension field needs to be the X-axis, and the metric field needs to be the Y-axis.

The `time` field in the above figure is treated as a common dimension, which doesn't meet the requirements for field attributes of a sequence diagram. If you modify the `time` field attribute to the time type, you can see that the `time` field changes to the time format (this operation is equivalent to the `CAST` function). At this point, you can use a sequence diagram.

The `histogram` function is usually used to process fields, and the result can be in a non-standard time format. Therefore, if the default field attribute is common dimension, the sequence diagram cannot be used. You need to use the `CAST` function to convert the field to the time type or use data conversion to change the field attribute to the time dimension.



### Merging groups



After using a SQL statement to find the above results, you can group them by `server_addr` and `server_name` and collect the PV and UV of each group. If you want to merge the results by `server_name`, you can hide the `server_addr` field and merge the results in the selected `server_name` dimension. This operation is equivalent to the `GROUP BY` function.
