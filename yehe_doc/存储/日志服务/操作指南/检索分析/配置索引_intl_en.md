## Overview

Index configuration is a necessary condition for using CLS for log search and analysis; that is, log search and analysis can be performed only after index is enabled. In addition, different index rules can lead to different search and analysis results. This document describes how to configure an index and how it works.




The core of index configuration is to [segment](https://intl.cloud.tencent.com/document/product/614/45409) raw logs so that logs can be quickly and conveniently searched based on specific search conditions. In addition, you can enable statistics for specific fields in index configuration to facilitate statistical analysis of logs using SQL. CLS provides the following three types of indexes:
<table>
<thead>
<tr>
<th width=15%>Category</th>
<th>Description</th>
<th>Configuration Method</th>
</tr>
</thead>
<tbody><tr>
<td>Full-Text Index</td>
<td>A raw log is split into multiple segments, and indexes are created based on the segments. You can query logs based on keywords (full-text search). <br>For example, entering <code>error</code> means to search for logs that contain the keyword <code>error</code>.</td>
<td>Console: Enable full-text index on the index configuration page.</td>
</tr>
<tr>
<td>Key-Value Index</td>
<td>A raw log is split into multiple segments based on a field (key:value), and indexes are created based on the segments. You can query logs based on key-value (key-value search). <br>For example, entering <code>level:error</code> means to search for logs with a <code>level</code> field whose value contains <code>error</code>.</td>
<td>Console: On the index configuration page, enable key-value index and enter the field name (`key`), such as <code>level</code>.</td>
</tr>
<tr>
<td>Metadata Index</td>
<td>A metadata index is also a key-value index, but the field name is prefixed with <code>__TAG__</code>. Metadata indexes are usually used to classify logs.<br>For example, entering <code>__TAG__.region:"ap-beijing"</code> means to search for logs with a <code>region</code> field whose value is <code>ap-beijing</code>.</td>
<td>Console: On the index configuration page, enable key-value index and enter the metadata field name (`key`), such as <code>__TAG__.region</code>.</td>
</tr>
</tbody></table>

>!
>- Index configuration will incur any index traffic and index storage fees. For more billing information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/614/37509). For how to save product use costs, see [Saving Product Use Costs](https://intl.cloud.tencent.com/document/product/614/45245).
>- Log data collected cannot be searched when index is disabled. It takes about one minute for the log search and analysis feature to become available after index is enabled.
>- Only fields for which **Enable Statistics** is toggled on in the key-value index configuration support SQL statistical analysis.
>- Index rule changes (including adding, modifying, and deleting fields, and adjusting delimiter configuration) take effect only for newly written logs. Existing data is not updated.
>

## Prerequisites

For log collection using LogListener, if the extraction mode in the collection configuration is set to full text in a single line or full text in multi lines, the original log is stored under the `__CONTENT__` field and supports only full-text index configuration. If you need to configure key-value indexes for some content in the log or enable statistics, you need to perform [log structuring](https://intl.cloud.tencent.com/document/product/614/31652) and use log extraction modes other than full text in a single line or full text in multi lines.

## Full-Text Index

A raw log is split into multiple segments, and indexes are created based on the segments. You can query logs based on keywords (full-text search).
<table>
<thead>
<tr>
<th width=15%>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Full-Text Delimiter</td>
<td>A set of characters that split the raw log into segments. Only English symbols are supported. Default delimiters in the console are <code>@&amp;?|#()='",;:&lt;&gt;[]{}/ \n\t\r</code>. <br><dx-alert infotype="notice" title="">If a segment is too long, an index will be created only for the first 10,000 characters, and the excessive part cannot be found. However, the complete log will be stored.</dx-alert></td>
</tr>
<tr>
<td>Case Sensitivity</td>
<td>Specifies whether log search is case-sensitive.<br>For example, if a log is <code>Error</code> and log search is case-sensitive, the log cannot be matched by <code>error</code>.</td>
</tr>
<tr>
<td>Allow Chinese Characters</td>
<td>This feature can be enabled when logs contain Chinese characters and the Chinese characters need to be searched. <br>For example, if the original text of a log is in Chinese, and this feature is disabled, you cannot query the log by using a Chinese keyword contained in the original text. The query can be successful only if you use the exact raw log text to query the log. However, if you enable this feature, you can query the log by using a Chinese keyword contained in the raw log text. </td>
</tr>
</tbody></table>


For example, a complete log is as shown below:
```
10.20.20.10;[2018-07-16 13:12:57];GET /online/sample HTTP/1.1;200
```
If you use the [Separator Format](https://intl.cloud.tencent.com/document/product/614/32285) to extract log fields, the structured log uploaded to CLS will be as follows:
```
IP: 10.20.20.10
request: GET /online/sample HTTP/1.1
status: 200
time: [2018-07-16 13:12:57]
```
If the full-text delimiter is <code>@&()='",;:&lt;>[]{}/ \n\t\r</code> (including space), all field values in the raw log will be segmented into the following keywords (each line denotes a keyword):
```
10.20.20.10
GET
online
sample
HTTP
1.1
200
2018-07-16
13
12
57
```
Under the above index configuration, the following results are obtained using the following search conditions:
- Search condition A:
```
\/online\/login
```
  - `\` is used to escape the `/` symbol (this symbol is a reserved symbol of the search syntax and therefore needs to be escaped).
  - The escaped `/` symbol is a delimiter, so the actual search condition is `online OR login`. A log containing `online` **or** `login` is considered to meet the search condition.
  - The example log provided above **meets** the search condition.
- Search condition B:
```
"/online/login"
```
  - Being enclosed by double quotation marks, the `/` symbol does not need to be escaped.
  - The content in the double quotation marks is also divided into two words. However, the double quotation marks indicate that only a log that **contains both the two words in the exact order** as that in the search condition is considered to meet the search condition.
  - The example log provided above does not contain `login` and therefore **does not meet** the search condition.
- Search condition C:
```
"/online/sample"
```
  - The example log provided above contains both `online` and `sample` in the exact order as that in the search condition and therefore is considered to **meet** the search condition.




## Key-Value Index

A raw log is split into multiple segments based on a field (key:value), and indexes are created based on the segments. You can query logs based on key-value (key-value search). To perform a key-value search, you must specify the field name in the syntax format of `key:value`, for example, `status:200`. If no field name is specified, a full-text search will be performed.

To meet basic log search requirements, CLS automatically creates key-value indexes for some built-in reserved fields, which does not incur index traffic fees. Details are as follows:

| Built-in Reserved Field    | Description                                                         |
| :-------------- | :----------------------------------------------------------- |
| `__FILENAME__`  | Filename for log collection, which can be used to search for logs in a specified file. For example, you can use `__FILENAME__:/"var/log/access.log"` to search for logs from the `/var/log/access.log` file. |
| `__SOURCE__`    | Source IP for log collection, which can be used to search for logs of a specified server. For example, you can use `__SOURCE__:192.168.10.10` to search for the logs of the server whose IP is `192.168.10.10`. |
| `__HOSTNAME__`	| The server name of the log, which can be used to search for logs of a specified server. Only LogListener 2.7.4 or later can collect this field. |
| `__TIMESTAMP__` | Log timestamp (UNIX timestamp in milliseconds). When a log is searched by time range, the system automatically searches for the log by this time and displays the time as the log time on the console. |
| `__PKG_LOGID__` | Log ID in a [log group](https://intl.cloud.tencent.com/document/product/614/38888). This ID is used for [context search](https://intl.cloud.tencent.com/document/product/614/39795). You are not recommended to use this ID alone. |


<table>
<thead>
<tr>
<th width=15%>Configuration Item</th>
<th>Description</th>
<th width=25%>Remarks</th>
</tr>
</thead>
<tbody><tr>
<td>Field Name</td>
<td>Field name in <a href="https://intl.cloud.tencent.com/document/product/614/31652">Collection Overview</a> <br><dx-alert infotype="notice" title="">
You can add up to 300 fields for a key-value index of a log topic.
</dx-alert>
<td>-</td>
</tr>
<tr>
<td>Data Type</td>
<td>Data type of the field. There are three types: <code>text, long, and double</code>. The <code>text</code> type supports fuzzy search by wildcard, while the <code>long and double</code> types support range search. <dx-alert infotype="notice" title="">
1. Fields of the `long` type support a data range of -1E15 to 1E15. Data out of the range may lose certain decimal places or not be matched. In the case of index configuration for a super long numeric field, we recommend that you:<ul><li>store the field as the `text` type if you don't need to search for it by comparing it with the numeric range.</li><li>store the field as the `double` type if you need to do so, which may lose certain decimal places.</li></ul>
2. Fields of the `double` type support a data range of -1.79E+308 to +1.79E+308. If the number of code characters of the floating-point number exceeds 64, decimal places will be lost.</dx-alert></td>
<td>long - Integer type (Int 64) <br>double - Floating point (64 bit) double  <br>text - String</td>
</tr>
<tr>
<td>Delimiter</td>
<td>A set of characters that split the field value into segments. Only English symbols are supported. <dx-alert infotype="notice" title="">
If a segment is too long, an index will be created only for the first 10,000 characters, and the excessive part cannot be found. However, the complete log will be stored.
</dx-alert></td>
<td>Default delimiters in the console: <code>@&amp;?|#()='",;:&lt;&gt;[]{}/ \n\t\r</code></td>
</tr>
<tr>
<td>Allow Chinese Characters</td>
<td>This feature can be enabled when fields contain Chinese characters and the Chinese characters need to be searched. <br>For example, if the original text of a log is in Chinese, and this feature is disabled, you cannot query the log by using a Chinese keyword contained in the original text. The query can be successful only if you use the exact raw log text to query the log. However, if you enable this feature, you can query the log by using a Chinese keyword contained in the raw log text. </td>
<td>-</td>
</tr>
<tr>
<td>Enable Statistics</td>
<td>After it is toggled on, SQL statistical analysis can be performed on the field, such as <code>group by ${key}</code> and <code>sum(${key})</code>. <dx-alert infotype="notice" title="">If it is toggled on for a field of the `text` type and the value is too long, only the first 32,766 characters will be included in the statistical calculation (SQL). If the field contains Chinese characters, the log will be lost if the value contains more than 32,766 characters. We recommend that you toggle the feature off in this case.</dx-alert></td>
<td>This feature is part of the key-value index feature and therefore is not billed separately.</td>
</tr>
<tr>
<td>Case Sensitivity</td>
<td>Specifies whether log search is case-sensitive.<br>For example, if a log is <code>level:Error</code> and log search is case-sensitive, the log cannot be matched by <code>level:error</code>.</td>
<td>-</td>
</tr>
</tbody></table>

For example, a complete log is as shown below:
```
10.20.20.10;[2018-07-16 13:12:57];GET /online/sample HTTP/1.1;200
```
If you use the [Separator Format](https://intl.cloud.tencent.com/document/product/614/32285) to extract log fields, the structured log uploaded to CLS will be as follows:
```
IP: 10.20.20.10
request: GET /online/sample HTTP/1.1
status: 200
time: [2018-07-16 13:12:57]
```
Assume that the key-value index configuration is as follows:

| Field Name| Field Type | Delimiter                                    | Allow Chinese Characters | Enable Statistics |
| -------- | -------- | ----------------------------------------- | -------- | -------- |
| IP       | text     | <code>@&()='",;:&lt;>[]{}/ \n\t\r </code> | No       | Yes       |
| request  | text     | <code>@&()='",;:&lt;>[]{}/ \n\t\r </code> | No       | Yes       |
| status   | long     | None                                        | No       | Yes       |
| time     | text     | <code>@&()='",;:&lt;>[]{}/ \n\t\r </code> | No       | Yes       |

Under the above index configuration, the following results are obtained using the following search conditions:

- Search condition A:
```
request:\/online\/login
```
  - `\` is used to escape the `/` symbol (this symbol is a reserved symbol of the search syntax and therefore needs to be escaped).
  - The escaped `/` symbol is a delimiter, so the actual search condition is `online OR login`. A log containing `online` **or** `login` is considered to meet the search condition.
  - The example log provided above **meets** the search condition.
- Search condition B:
```
request:"/online/login"
```
  - Being enclosed by double quotation marks, the `/` symbol does not need to be escaped.
  - The content in the double quotation marks is also divided into two words. However, the double quotation marks indicate that only a log that **contains both the two words in the exact order** as that in the search condition is considered to meet the search condition.
  - The example log provided above does not contain `login` and therefore **does not meet** the search condition.
- Search condition C:
```
request:"/online/sample"
```
  - The example log provided above contains both `online` and `sample` in the exact order as that in the search condition and therefore is considered to **meet** the search condition.

For fields with the statistics feature enabled, you can also use SQL to perform statistical analysis on logs.
- Search and analysis statement A:
```
request:"/online/login" | select count(*) as logCounts
```
Count the number of logs whose value of `request` is "/online/login".
- Search and analysis statement B:
```
* | select count(*) as logCounts,request group by request order by count(*) desc limit 10
```
Get the top 10 requests with the largest number of log entries.







## Metadata Index

When a log is uploaded to CLS, its metadata is passed through the `LogTag` field (for more information, see the `LogTag` field in [Uploading Log via API](https://intl.cloud.tencent.com/document/product/614/50267)), while the raw log content is passed through the `Log` field. A metadata index needs to be configured for all data which is passed via `LogTag`. A metadata index is a key-value index in essence, adopting the same indexing rules and configuration methods as key-value indexes. The only difference is that the metadata field in a metadata index is identified by the specific prefix `__TAG__. `. For example, the `region` metadata field is indexed as `__TAG__.region`.

For example, a complete log is as shown below:
```
10.20.20.10;[2018-07-16 13:12:57];GET /online/sample HTTP/1.1;200
```
If you use the [Separator Format](https://intl.cloud.tencent.com/document/product/614/32285) to extract log fields with the metadata `region:ap-beijing`, the structured log uploaded to CLS will be as follows:
```
IP: 10.20.20.10
request: GET /online/sample HTTP/1.1
status: 200
time: [2018-07-16 13:12:57]
__TAG__.region:ap-beijing
```
If the rules for metadata indexing are as follows:

| Field Name           | Delimiter                                   |
| ------------------ | ---------------------------------------- |
| \_\_TAG\_\_.region | <code>@&()='",;:&lt;>[]{}/ \n\t\r</code>|

Sample search: if you enter `__TAG__.region:"ap-beijing"`, the sample log can be returned.

## Advanced Settings

To meet the needs in some special use cases, the index configuration feature provides the following advanced settings. We recommend you adopt the recommended configurations in practical uses, which will also be used by default when an index configuration is created in the console.

| Configuration Item | Description | Recommended Configuration |
| -------------------------- | ------------------------------------------------------------ | -------- |
| Include built-in reserved fields in full-text index | **Contain**: The full-text index contains built-in fields `__FILENAME__`, `__HOSTNAME__`, and `__SOURCE__`, and full-text search and key-value search are supported, such as `"/var/log/access.log"` and `__FILENAME__:"/var/log/access.log"`.<br />**Not contain**: The full-text index does not contain the aforementioned built-in fields, and only key-value search can be used, such as `__FILENAME__:"/var/log/access.log"`.                   | Contain     |
| Include metadata fields in full-text index   | **Contain**: The full-text index contains all metadata fields (those prefixed with `__TAG__`), and log fields can be searched for directly with full-text search, such as `ap-beijing`.<br />**Not contain**: The full-text index does not contain any metadata fields, and log fields can be searched for only with key-value search, such as `__TAG__.region:ap-beijing`. Key-value search is not supported for infrequent log topics, and fields cannot be searched for in this case.<br />**Contain only metadata fields with key-value index enabled**: The full-text index contains metadata fields with key-value index enabled but not metadata fields with key-value index disabled. This option is not available for infrequent log topics. | Contain     |
| Log storage rule in case of index creation exception | In case of any exception during index creation for logs, CLS will store raw logs in `__RAWLOG__` to avoid log loss. If index creation fails only for certain fields, the failed part can be stored in the specified field (which is `RAWLOG_FALL_PART` by default). For more information, see [Handling rule for a log index creation exception](#CreateExceptionLogRule). | Enable |


## Directions

### Modifying index configuration

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Topic** to enter the log topic list page.
3. Click the target log topic ID/name to enter the log topic management page.
4. Click the **Index Configuration** tab and click **Edit** to enter the index configuration page. 

5. Modify the index configuration as needed and click **OK**.
When modifying index configuration, you can also click **Auto Configure** to enable the system to automatically get the latest log collected as a sample and parse the fields in it into key-value indexes. You can perform fine tuning on the basis of automatic configuration to quickly obtain the final index configuration information.


### Importing the index configuration

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Topic** to enter the log topic list page.
3. Click the target log topic ID/name to enter the log topic management page.
4. Click the **Index Configuration** tab and click **Import Configuration Rule**.

5. In the dialog box, select the log topic whose index configuration is to be imported and click **OK**. The index configuration of the selected log topic is automatically filled into the index configuration of the current log topic.

6. After confirming that everything is correct, click **OK**.

## Appendix

<span id="JSON"></span>
### JSON field parsing rules

During the storage process, logs may fail to be stored because there are too many JSON field levels, objects, or object types. To solve this problem, CLS will parse nested JSON fields only to the levels for which indexes are configured (existing log topics whose index configuration remains unchanged will not be affected), and the rest levels will be stored and displayed as strings. This feature upgrade affects only the search results of raw logs (search statements contain only search criteria but not SQL statements) and does not affect the statistical analysis results (SQL results).


The following uses an actual log as an example to describe the parsing rule in detail.

**Sample log:**

The log contains three fields, where `kye1` is a common field, and `kye2` and `kye3` are nested JSON fields.
```
{
	"kye1": "http://www.example.com",
	"kye2": {
		"address": {
			"country": "China",
			"city": {
				"name": "Beijing",
				"code": "065001"
			}
		},
		"contact": {
			"phone": {
				"home": "188xxxxxxxx",
				"work": "187xxxxxxxx"
			},
			"email": "xxx@xxx.com"
		}
	},
	"kye3": {
		"address": {
			"country": "China",
			"city": {
				"name": "Beijing",
				"code": "065001"
			}
		},
		"contact": {
			"phone": {
				"home": "188xxxxxxxx",
				"work": "187xxxxxxxx"
			},
			"email": "xxx@xxx.com"
		}
	}
}
```

**Index configuration**

The following figure shows the key-value index configuration. Key-value index is configured for the `kye1` and `kye2.address` fields but not the `kye3` field.



**Search and analysis effect on the console**


- `kye2.address` is displayed as a string, and its attributes and objects are not further expanded.
- Although `kye2.contact` is not configured with a key-value index, because `kye2.address` is configured with an index, `kye2.contact` as an object at the same level as `kye2.address` is also displayed as a string.
- `kye3` is not configured with a key-value index, and therefore its attributes and objects are not expanded.

The console provides the JSON formatting feature to display string-type JSON fields in a hierarchical manner, but this feature is only a display effect on the console, and the actual fields are still strings, as shown in the **API-based log search and analysis effect** section below.




**API-based log search and analysis effect**

If you use the [SearchLog](https://intl.cloud.tencent.com/document/product/614/42788) API, the value of the `Results` parameter in the output parameters is as follows (other parameters are not affected and remain unchanged):
```
{
  "Time": 1645065742008,
  "TopicId": "f813385f-aee0-4238-xxxx-c99b39aabe78",
  "TopicName": "TestJsonParse",
  "Source": "172.17.0.2",
  "FileName": "/root/testLog/jsonParse.log",
  "PkgId": "5CB847DA620DB3D4-10D",
  "PkgLogId": "65536",
  "HighLights": [],
  "Logs": null,
  "LogJson": "{\"kye1\":\"http://www.example.com\",\"kye2\":{\"address\":\"{\\\"country\\\":\\\"China\\\",\\\"city\\\":{\\\"name\\\":\\\"Beijing\\\",\\\"code\\\":\\\"065001\\\"}}\",\"contact\":\"{\\\"phone\\\":{\\\"home\\\":\\\"188xxxxxxxx\\\",\\\"work\\\":\\\"187xxxxxxxx\\\"},\\\"email\\\":\\\"xxx@xxx.com\\\"}\"},\"kye3\":\"{\\\"address\\\":{\\\"country\\\":\\\"China\\\",\\\"city\\\":{\\\"name\\\":\\\"Beijing\\\",\\\"code\\\":\\\"065001\\\"}},\\\"contact\\\":{\\\"phone\\\":{\\\"home\\\":\\\"188xxxxxxxx\\\",\\\"work\\\":\\\"187xxxxxxxx\\\"},\\\"email\\\":\\\"xxx@xxx.com\\\"}}\"}"
}
```

- `kye2.address` is a string, so its value is escaped as a string.
- `kye2.contact` is an object at the same level as `kye2.address`, and although `kye2.contact` is not configured with a key-value index, its value is also escaped as a string.
- `kye3` is not configured with a key-value index and is escaped as a string as a whole.

**If you use code to process the output parameters of the [SearchLog](https://intl.cloud.tencent.com/document/product/614/42788) API, note the escape characters to avoid processing logic exceptions.** To help you compare the API output parameters before and after the feature upgrade, the API output parameters before the upgrade are provided below:
```
{
  "Time": 1645065742008,
  "TopicId": "f813385f-aee0-4238-xxxx-c99b39aabe78",
  "TopicName": "zhengxinTestJsonParse",
  "Source": "172.17.0.2",
  "FileName": "/root/testLog/jsonParse.log",
  "PkgId": "25D0A12F620DBB64-D3",
  "PkgLogId": "65536",
  "HighLights": [],
  "Logs": null,
  "LogJson": "{\"kye1\":\"http://www.example.com\",\"kye2\":{\"address\":\"{\\\"city\\\":{\\\"code\\\":\\\"065001\\\",\\\"name\\\":\\\"Beijing\\\"},\\\"country\\\":\\\"China\\\"}\",\"contact\":{\"phone\":{\"work\":\"187xxxxxxxx\",\"home\":\"188xxxxxxxx\"},\"email\":\"xxx@xxx.com\"}},\"kye3\":{\"address\":{\"country\":\"China\",\"city\":{\"code\":\"065001\",\"name\":\"Beijing\"}},\"contact\":{\"phone\":{\"work\":\"187xxxxxxxx\",\"home\":\"188xxxxxxxx\"},\"email\":\"xxx@xxx.com\"}}}"
}
```


[](id:CreateExceptionLogRule)
### Handling rule for a log index creation exception

If the raw log format is abnormal or the index configuration and raw log do not match, index creation may fail. In this case, CLS will store the raw log in 	`__RAWLOG__` for exception handling. This avoids log loss. `__RAWLOG__` supports only full-text search (full-text index needs to be enabled) but not key-value search, key-value index, and statistical analysis. After full-text index is enabled, index traffic, index storage, and fees will still be calculated according to the full text of the raw log for the abnormal log, without additional fees.

Index creation exceptions divide into two cases:

1. Index creation according to the index configuration fails for all fields in the log. In this case, the log has only the `__RAWLOG__` field, and only full-text search can be used.


2. Index creation fails for some fields and succeeds for the others in the log. In this case, the log has both the `__RAWLOG__` field and certain fields with a successfully created index (these fields support properly configuring key-value index and statistical analysis). In **Index Configuration** > **Advanced Settings**, you can also store abnormal fields in the specified field (which is `RAWLOG_FALL_PART` by default and supports configuring key-value index and statistical analysis).


CLS will keep optimizing the compatibility of index configuration with raw logs to avoid the abovementioned log exceptions. As the product iterates, specific exception handling rules may change.
