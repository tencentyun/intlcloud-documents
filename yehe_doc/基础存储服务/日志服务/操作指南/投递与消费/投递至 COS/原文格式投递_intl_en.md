## Overview

You can log in to the [CLS Console](https://console.cloud.tencent.com/cls) and ship data in the log source format to Cloud Object Storage (COS). This topic describes how to create a source format shipping task.

Currently, COS to which CLS ships log files supports two basic formats: CSV and JSON. Based on basic format shipping, source format shipping leverages special parameters to restore original logs. Not all log source formats support source format shipping. See the following table for details.

| Log Source Format      | Source Format Shipping Supported                      |
| ----------------- | ------------------------------------- |
| Full text in a single line          | Yes. See [Source format shipping with full text in a single line](#1).     |
| Full text in multi lines          | Yes. See [Source format shipping with full text in multi lines](#1).    |
| JSON format         | No.                                |
| Separator (CSV) format | Uncertain. See [Source format shipping with CSV](#2). |
| Full RegEx          | No.                                |

<span id="1"></span>

## Directions
### Source format shipping with full text in a single line (or in multi lines)

For full text in a single line or in multi lines, you can set special parameters in advanced configuration to ship log data in its source format based on [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582).

1. On the **Basic Configuration** tab page, set parameters according to the instructions in [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582).
2. On the **Advanced Configuration** tab page, set **Shipping Format** to **csv**, **Key** to `__CONTENT__`, **Separator** to **Space**, **Escape character** to **None**, **Invalid Field Filling** to **None**, and disable **Key in First Line**. See the figure below.
![image](https://main.qcloudimg.com/raw/67572d3e6658b5ca3c5dd155a17831d8.png)
The parameters are described as follows:

| Parameter          | Value          | Description                                                     |
| --------------- | ------------- | ------------------------------------------------------------ |
| Key | `__CONTENT__` | For full text in a single line or in multi lines, the system uses `__CONTENT__` as the key and the log source content as the value. For source format shipping, enter `__CONTENT__` as the key. |
| Separator          | Space          | For full text in a single line or in multi lines, set **Separator** to **Space**.                |
| Escape character          | None            | To prevent source content from being modified by escape characters, set **Escape character** to **None**.                    |
| Invalid Field Filling        | None            | Set **Invalid Field Filling** to **None**.                                               |
| Key in First Line         | Disabled            | You do not need to add a description of the field name in the first line of the CSV file for source format shipping.                |

3. Click **OK**. The shipping task is enabled.
![img](https://main.qcloudimg.com/raw/6a2aea81506294684fdabbb15de45e7b.png)


<span id="2"></span>


### Source format shipping with CSV

>! [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582) supports limited types of separators, including spaces, tabs, commas (,), semicolons (;), and vertical bars (|). Therefore, you can ship log data in its source format only when the separator in the log source content is supported by CSV shipping. Otherwise, source format shipping is not supported.

1. On the **Basic Configuration** tab page, set parameters according to the instructions in [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582).
2. On the **Advanced Configuration** tab page, set **Shipping Format** to **csv** and set other parameters according to the following table.

<table>
   <tr>
      <th>Parameter</th>
      <th>Value</th>
      <th>Description</th>
   </tr>
   <tr>
      <td>Key</td>
      <td>Keys</td>
      <td>Enter the key of each key-value pair in the source content in order.</td>
   </tr>
   <tr>
      <td>Separator</td>
      <td>Select a value from the drop-down list.</td>
      <td>Select the separator used in the source content. If there is no such option, source format shipping is not supported.</td>
   </tr>
   <tr>
      <td>Escape character</td>
      <td>None</td>
      <td>To prevent source content from being modified due to escape characters, set **Escape character** to **None**.</td>
   </tr>
   <tr>
      <td>Invalid Field Filling</td>
      <td>None</td>
      <td>Set **Invalid Field Filling** to **None**.</td>
   </tr>
   <tr>
      <td>Key in First Line</td>
      <td>Disabled</td>
      <td>You do not need to add a description of the field name in the first line of the CSV file for source format shipping.</td>
   </tr>
</table>

For example, the raw log is as follows:
```
10.20.20.10;[Tue Jan 22 14:49:45 CST 2019 +0800];GET /online/sampleHTTP/1.1;127.0.0.1;200;647;35;http://127.0.0.1/
```
Define a semicolon (;) as the separator and define a key for each field, as shown in the following figure.
![image](https://main.qcloudimg.com/raw/d0c49e56caf8ee578ad94f7a0eea9e79.png)
To ship data in its source format, set **Separator** to **Semicolon** for the CSV shipping format on the **Advanced Configuration** tab page. The following figure shows the complete configuration.
![image](https://main.qcloudimg.com/raw/050222943d4411c6ec5854d1f2b9d51a.png)

3. Click **OK**. The shipping task is enabled.
![img](https://main.qcloudimg.com/raw/dd0904dcaf9492ee07e4b87956c6b7df.png)
