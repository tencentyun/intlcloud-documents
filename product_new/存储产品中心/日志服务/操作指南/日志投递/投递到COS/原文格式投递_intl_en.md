## Overview

You can log in to the [CLS Console](https://console.cloud.tencent.com/cls) and ship data of the log source to Cloud Object Storage (COS). This topic describes how to create a task of log source shipping.

COS of CLS supports the CSV and JSON formats. However, source format shipping indicates that special parameters are set to restore the source log based on the basic format shipping. The following table describes whether source format shipping is supported.

| Log source format      | Whether source format shipping is supported                      |
| ----------------- | ------------------------------------- |
| Full text in a single line          | Yes. Please see [Source Format Shipping with Full Text in a Single Line](#1).     |
| Full text in multi lines          | Yes. Please see [Source Format Shipping with Full Text in Multi Lines](#1).    |
| JSON format         | No.                                |
| Separator (CSV) format | Uncertain. Please see [Source Format Shipping with CSV](#2). |
| Full RegEx          | No.                                |

<span id="1"></span>

## Directions
### Source format shipping with full text in a single line (or in multi lines)

For full text in a single line or in multi lines, you can set special parameters in advanced configuration to ship log data in the source format based on [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582).

1. Complete **basic configuration** according to the instructions in [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582).
2. In advanced configuration, set the shipping format to **CSV**, enter `__CONTENT__` in the key name, set **Space** as the separator, set the escape character as **Space**, and **Invalid Field Filling** to **None**, and then disable **Key in First Line**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/67572d3e6658b5ca3c5dd155a17831d8.png)
The following table describes the parameters

| Parameter          | Content          | Description                                                     |
| --------------- | ------------- | ------------------------------------------------------------ |
| Key | `__CONTENT__` | For full text in a single line or in multi lines, the system uses `__CONTENT__` as the key while the log source as the value. During source format shipping, enter `__CONTENT__` in the key name. |
| Separator          | Space          | For full text in a single line or in multi lines, select **Space** for the separator.                |
| Escape character          | None            | To prevent source content from being modified by escape characters, set the escape character to **None**.                    |
| Invalid Field        | None            | Set the invalid field to **None**.                                               |
| Key in First Line         | Disable            | You do not need to add description of the field name in the first line of the CSV file for source format shipping.                |

3. Click **OK**. The shipping is then enabled.
![](https://main.qcloudimg.com/raw/6a2aea81506294684fdabbb15de45e7b.png)


<span id="2"></span>


### Source format shipping with CSV

>! [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582) supports limited separators, including spaces, tabs, commas (,), semicolons (;), and vertical bars (|). Therefore, you can ship in the source format only when separators in the log source are the same as those supported by CSV shipping. Otherwise, you cannot ship in the source format.

1. Complete **basic configuration** according to the instructions in [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582).
2. In advanced configuration, set the shipping format to **CSV** and configure other items as follows.

<table>
   <tr>
      <th>Configuration Item</th>
      <th>Content</th>
      <th>Description</th>
   </tr>
   <tr>
      <td>Key name</td>
      <td>Key Name</td>
      <td>Enter the key name of each key-value pair in the source file successively.</td>
   </tr>
   <tr>
      <td>Separator</td>
      <td>A value selected from the list</td>
      <td>Select the corresponding separator in the source file. If there are no same separators in the source file, you cannot ship data in the source format.</td>
   </tr>
   <tr>
      <td>Escape character</td>
      <td>None</td>
      <td>To prevent source content from being modified due to escape characters, set **Escape Character** to **None**.</td>
   </tr>
   <tr>
      <td>Invalid Field</td>
      <td>None</td>
      <td>Set the invalid field to **None**.</td>
   </tr>
   <tr>
      <td>Key in First Line</td>
      <td>Disable</td>
      <td>You do not need to add description of the field name in the first line of the CSV file for source format shipping.</td>
   </tr>
</table>

For example, the raw log is as follows:
```
10.20.20.10;[Tue Jan 22 14:49:45 CST 2019 +0800];GET /online/sampleHTTP/1.1;127.0.0.1;200;647;35;http://127.0.0.1/
```
Define semicolons (;) as the separator and define a key name for each field, as shown in the following figure.
![](https://main.qcloudimg.com/raw/d0c49e56caf8ee578ad94f7a0eea9e79.png)
To ship data in the source format, you need to set the separator of the CSV format to **Semicolon** in the advanced shipping configuration. The following figure shows the complete configurations.
![](https://main.qcloudimg.com/raw/050222943d4411c6ec5854d1f2b9d51a.png)
3. Click **OK**. The shipping is then enabled.
![](https://main.qcloudimg.com/raw/dd0904dcaf9492ee07e4b87956c6b7df.png)
