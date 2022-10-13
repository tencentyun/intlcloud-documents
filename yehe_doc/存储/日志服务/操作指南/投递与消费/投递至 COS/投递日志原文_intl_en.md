## Overview

This document describes how to ship the collected raw log to COS. Currently, only logs collected in a single line, in multiple lines, or with certain separators are supported in this scenario.

## Notes

You can configure CSV shipping to COS to ship certain raw logs. The following table describes the options of **CSV** shipping to COS but doesn't apply to JSON or Parquet shipping.


| Log Collection Format      | Support for Raw Log Shipping     | User Raw Log    |CLS Storage Format      | Format for Shipping to COS                    |
| ----------------- | ------------------------------------- |----------------- | ------------------------------------- | ------------------------------------- |
| Full text in a single line          | Yes. For more information, see [Logs collected in a single line](#1). | yourlog | \_\_CONTENT\_\_:yourlog | yourlog  |
| Full text in multiple lines          | Yes. For more information, see [Logs collected in multiple lines](#1).  |yourlog|\_\_CONTENT\_\_:yourlog| yourlog  |
| Separator (CSV) format | It depends. For more information, see [CSV format](#2). Only space, tab, comma, semicolon, and vertical bar are supported as raw log separators. | V1 separator V2 separator V3 separator...Vn </br>For example, V1,V2,V3...Vn|K1:V1 K2:V2 K3:V3...Kn:Vn | V1 separator V2 separator V3 separator...Vn  </br>For example, V1,V2,V3...Vn|
| JSON format         | No | K1:V1 K2:V2 K3:V3...Kn:Vn|  K1:V1 K2:V2 K3:V3...Kn:Vn | V1,V2,V3...Vn differs from the original JSON. |
| Full regex          | No  | V11V22V33...Vnn  |  K1:V1 K2:V2 K3:V3...Kn:Vn  |  V1,V2,V3...Vn differs from the raw log. |

<span id="1"></span>

## Directions
### Log collected in a single line or multiple lines

For logs collected in a single line or multiple lines, you can configure parameters based on [CSV shipping](https://intl.cloud.tencent.com/document/product/614/31582) to implement raw log shipping.

1. Complete the first step of **Basic Configuration** as instructed in [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582).  
2. Set **Shipping Format** to **CSV**, retain the `__CONTENT__` field, delete other fields, set **Separator** to **Space**, set **Escape Character** to **Space**, set **Invalid Field Filling** to **None**, and disable **Key in First Line**.
The parameters are described as follows:
<table>
<thead>
<tr><th>Configuration Item</th><th>Description</th><th>Remarks</th></tr>
</thead>
<tbody><tr>
<td>Key</td>
<td><code>__CONTENT__</code></td>
<td>For full text in a single line or multiple lines, <code>__CONTENT__</code> is used as the default key, and the raw log is used as the value. When the raw log is shipped, only the <code>__CONTENT__</code> field is retained.</td>
</tr>
<tr>
<td>Separator</td>
<td>Space</td>
<td>Set **Separator** to **Space** for the full text in a single line or multiple lines.</td>
</tr>
<tr>
<td>Escape Character</td>
<td>None</td>
<td>To prevent the raw log from being modified due to escape characters, set **Escape Character** to **None**.</td>
</tr>
<tr>
<td>Invalid Field Filling</td>
<td>None</td>
<td>Set **Invalid Field Filling** to **None**.</td>
</tr>
<tr>
<td>Key in First Line</td>
<td>Disabled</td>
<td>You don't need to add a description of the field name in the first line of the CSV file for raw log shipping.</td>
</tr>
</tbody></table>
3. Click **OK** to enable shipping.  


<span id="2"></span>
### Logs collected in CSV format

>! [CSV shipping](https://intl.cloud.tencent.com/document/product/614/31582) supports limited types of separators, including space, tab, comma, semicolon, and vertical bar. Therefore, you can ship log data in the raw format only when the separator in the raw log content is supported by CSV shipping.  
>

1. Complete the first step of **Basic Configuration** as instructed in [CSV Shipping](https://intl.cloud.tencent.com/document/product/614/31582).  
2. Set **Shipping Format** to **CSV**. During field configuration, you need to delete CLS metadata fields. 

The parameters are described as follows:  
<table>
   <tr>
      <th>Configuration Item</th>
      <th>Value</th>
      <th>Description</th>
   </tr>
   <tr>
      <td>Key</td>
      <td>Keys</td>
      <td>Only the user field is retained.</td>
   </tr>
   <tr>
      <td>Separator</td>
      <td>A value selected from the drop-down list</td>
      <td>Select the separator of the raw log content. If separators are different, raw log shipping is not supported. Currently, only space, tab, comma, semicolon, and vertical bar are supported.</td>
   </tr>
   <tr>
      <td>Escape Character</td>
      <td>None</td>
      <td>To prevent the raw log from being modified due to escape characters, set **Escape Character** to **None**.</td>
   </tr>
   <tr>
      <td>Invalid Field Filling</td>
      <td>None</td>
      <td>Set **Invalid Field Filling** to **None**.</td>
   </tr>
   <tr>
      <td>Key in First Line</td>
      <td>Disabled</td>
      <td>You don't need to add a description of the field name in the first line of the CSV file for raw log shipping.</td>
   </tr>
</table>  
3. Click **OK** to enable shipping.  

