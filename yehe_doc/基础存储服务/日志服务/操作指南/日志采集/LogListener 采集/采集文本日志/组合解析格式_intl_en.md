## Overview

If your log structure is too complex and involves multiple log parsing modes, and a single parsing mode (such as the NGINX mode, full regex mode, or JSON mode) cannot meet log parsing requirements, you can use LogListener to parse logs in combined parsing mode. You can enter code (in JSON format) in the console to define the pipeline logic for log parsing. You can add one or more LogListener plugins to process configurations, and the LogListener plugins are executed in the configuration processing order.

## Prerequisites

Assume that the raw data of a log is as follows:

```plaintext
1571394459,http://127.0.0.1/my/course/4|10.135.46.111|200,status:DEAD,
```
The content of a custom plugin is as follows:

 ```
 {
  "processors": [
    {
      "type": "processor_split_delimiter",
      "detail": {
        "Delimiter": ",",
        "ExtractKeys": [ "time", "msg1","msg2"]
      },
      "processors": [
        {
          "type": "processor_timeformat",
          "detail": {
            "KeepSource": true,
            "TimeFormat": "%s",
            "SourceKey": "time"
           }
        },
        {
          "type": "processor_split_delimiter",
          "detail": {
            "KeepSource": false,
            "Delimiter": "|",
            "SourceKey": "msg1",
            "ExtractKeys": [ "submsg1","submsg2","submsg3"]
           },
           "processors": []
        },
        {
          "type": "processor_split_key_value",
          "detail": {
            "KeepSource": false,
            "Delimiter": ":",
            "SourceKey": "msg2"
          }
        }
      ]
    }
  ]
}
 ```

After being structured by CLS, the log is changed to the following:

```plaintext
time: 1571394459
submsg1: http://127.0.0.1/my/course/4
submsg2: 10.135.46.111
submsg3: 200
status: DEAD
```

## Configuration Instructions

### Custom plugin types

<table>
	<tbody>
		<tr>
			<td><strong>Plugin Feature</strong></td>
			<td><strong>Plugin Name</strong></td>
			<td><strong>Feature Description</strong></td>
		</tr>
		<tr>
			<td>Field extraction</td>
			<td>processor_log_string</td>
			<td>Performs multi-character (line breaks) parsing of fields, typically for single-line logs.</td>
		</tr>
		<tr>
			<td>Field extraction</td>
			<td>processor_multiline</td>
			<td>Performs first-line regex parsing of fields (full regex mode), typically for multi-line logs.</td>
		</tr>
		<tr>
			<td>Field extraction</td>
			<td>processor_multiline_fullregex</td>
			<td>Performs first-line regex parsing of fields (full regex mode), typically for multi-line logs; extracts regexes from multi-line logs.</td>
		</tr>
		<tr>
			<td>Field extraction</td>
			<td>processor_fullregex</td>
			<td>Extracts fields (full regex mode) from single-line logs.</td>
		</tr>
		<tr>
			<td>Field extraction</td>
			<td>processor_json</td>
			<td>Expands field values in JSON format.</td>
		</tr>
		<tr>
			<td>Field extraction</td>
			<td>processor_split_delimiter</td>
			<td>Extracts fields (single-/multi-character separator mode).</td>
		</tr>
		<tr>
			<td>Field extraction</td>
			<td>processor_split_key_value</td>
			<td>Extracts fields (key-value pair mode).</td>
		</tr>
		<tr>
			<td>Field processing</td>
			<td>processor_drop</td>
			<td>Discards fields.</td>
		</tr>
		<tr>
			<td>Field processing</td>
			<td>processor_timeformat</td>
			<td>Parses time fields in raw logs to convert time formats and set parsing results as log time.</td>
		</tr>
	</tbody>
</table>

### Custom plugin parameters

<table>
<tbody>
<tr>
<td><strong>Plugin Name</strong></td>
<td><strong>Support Subitem Parsing</strong></td>
<td><strong>Plugin Parameter</strong></td>
<td><strong>Required</strong></td>
<td><strong>Feature Description</strong></td>
</tr>
<tr>
<td>processor_multiline</td>
<td>No</td>
<td>BeginRegex</td>
<td>Yes</td>
<td>Defines the first-line matching regex for multi-line logs.</td>
</tr>
<tr>
<td rowspan=3>processor_multiline_fullregex</td>
<td rowspan=3>Yes</td>
<td><p>BeginRegex</p></td>
<td>Yes</td><td>Defines the first-line matching regex for multi-line logs.</td>
</tr>
<tr>
<td>ExtractRegex</td>
<td>Yes</td>
<td >Defines the extraction regex after multi-line logs are extracted.</td>
</tr>
<tr>
<td>ExtractKeys</td>
<td>Yes</td>
<td>Defines the extraction keys.</td>
</tr>
<tr>
<td rowspan="2">processor_fullregex</td>
<td rowspan="2">Yes</td>
<td>ExtractRegex</td>
<td>Yes</td>
<td>Defines the extraction regex.</td>
</tr>
<tr>
<td>ExtractKeys</td>
<td>Yes</td>
<td>Defines the extraction keys.</td>
</tr>
<tr>
<td rowspan="2">processor_json</td>
<td rowspan="2">Yes</td>
<td>SourceKey</td>
<td>No</td>
<td>Defines the name of the upper-level processor key processed by the current processor.</td>
</tr>
<tr>
<td>KeepSource</td>
<td>No</td>
<td>Defines whether to retain `SourceKey` in the final key name.</td>
</tr>
<tr>
<td rowspan="4">processor_split_delimiter</td>
<td rowspan="4">Yes</td>
<td>SourceKey</td>
<td>No</td>
<td>Defines the name of the upper-level processor key processed by the current processor.</td>
</tr>
<tr>
<td>KeepSource</td>
<td>No</td>
<td>Defines whether to retain `SourceKey` in the final key name.</td>
</tr>
<tr>
<td>Delimiter</td>
<td>Yes</td>
<td>Defines the separator (single or multiple characters).</td>
</tr>
<tr>
<td>ExtractKeys</td>
<td>Yes</td>
<td>Defines the extraction keys after separator splitting.</td>
</tr>
<tr>
<td rowspan="3">processor_split_key_value</td>
<td rowspan="3">No</td>
<td>SourceKey</td>
<td>No</td>
<td>Defines the name of the upper-level processor key processed by the current processor.</td>
</tr>
<tr>
<td>KeepSource</td>
<td>No</td>
<td>Defines whether to retain `SourceKey` in the final key name.</td>
</tr>
<tr>
<td>Delimiter</td>
<td>Yes</td>
<td>Defines the separator between the `Key` and `Value` in a string.</td>
</tr>
<tr>
<td>processor_drop</td>
<td>No</td>
<td>SourceKey</td>
<td>Yes</td>
<td>Defines the name of the upper-level processor key processed by the current processor.</td>
</tr>
<tr>
<td rowspan=2>processor_timeformat</td>
<td rowspan=2>No</td>
<td>SourceKey</td>
<td>Yes</td>
<td>Defines the name of the upper-level processor key processed by the current processor.</td>
</tr>
<tr>
<td><span>TimeFormat</span></td>
<td>Yes</td>
<td>Defines the time parsing format for the `SourceKey` value (time data string in logs).</td>
</tr>
</tbody>
</table>

## Directions

### Logging in to the console

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Topic** to go to the log topic management page.

### Creating a log topic

1. Click **Create Log Topic**.
2. In the pop-up dialog box, enter `define-log` as **Log Topic Name** and click **Confirm**.

### Managing the machine group

1. After the log topic is created successfully, click its name to go to the log topic management page.
2. Click the **Collection Configuration** tab, click **Add** in the **LogListener Collection Configuration** area, and select the format in which you need to collect logs.
3. On the **Machine Group Management** page, select the machine group to which to bind the current log topic and click **Next** to proceed to collection configuration.
For more information, see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).


### Configuring collection

#### Configuring the log file collection path

On the **Collection Configuration** page, set **Collection Path** according to the log collection path format.
Log collection path format: `[directory prefix expression]/**/[filename expression]`.

After the log collection path is entered, LogListener will match all common prefix paths that meet the **[directory prefix expression]** rule and listen for all log files in the directories (including subdirectories) that meet the **[filename expression]** rule. The parameters are as detailed below:

| Parameter     | Description       |
| -------- | ------------------------------------------------------------ |
| Directory Prefix | Directory prefix for log files, which supports only the wildcard characters `\*` and `?`\*` indicates to match any multiple characters. `?` indicates to match any single character. |
| /**/     | Current directory and all its subdirectories.                                  |
| File Name   | Log file name, which supports only the wildcard characters `\*` and `?`. `\*` indicates to match any multiple characters. `?` indicates to match any single character. |

Common configuration modes are as follows:
- [Common directory prefix]/\*\*/[common filename prefix]\*
- [Common directory prefix]/\*\*/\*[common filename suffix]
- [Common directory prefix]/\*\*/[common filename prefix]\*[common filename suffix]
- [Common directory prefix]/\*\*/\*[common string]\*

Below are examples:

| No. | Directory Prefix Expression | Filename Expression | Description                                                         |
| ---- | -------------- | ------------ | ------------------------------------------------------------ |
| 1.   | /var/log/nginx | access.log   | In this example, the log path is configured as `/var/log/nginx/**/access.log`. LogListener will listen for log files named `access.log` in all subdirectories in the `/var/log/nginx` prefix path. |
| 2.   | /var/log/nginx | \*.log       | In this example, the log path is configured as `/var/log/nginx/**/*.log`. LogListener will listen for log files suffixed with `.log` in all subdirectories in the `/var/log/nginx` prefix path. |
| 3.   | /var/log/nginx | error\*      | In this example, the log path is configured as `/var/log/nginx/**/error*`. LogListener will listen for log files prefixed with `error` in all subdirectories in the `/var/log/nginx` prefix path. |

>!
> - Only LogListener 2.3.9 and later support adding multiple collection paths.
> - The system does not support uploading logs with contents in multiple text formats, which may cause write failures, such as `key:"{"substream":XXX}"`.
> - We recommend you configure the collection path as `log/*.log` and rename the old file after log rotation as `log/*.log.xxxx`.
> - By default, a log file can only be collected by one log topic. If you want to have multiple collection configurations for the same file, add a soft link to the source file and add it to another collection configuration.
> 

#### Configuring the combined parsing mode

On the **Collection Configuration** page, select **Combined Parsing** as the **Extraction Mode**.

#### Configuring the collection policy

- Full collection: When LogListener collects a file, it starts reading data from the beginning of the file.
- Incremental collection: When LogListener collects a file, it collects only the newly added content in the file.


## Use Limits
- If the combined parsing mode is used for data parsing, LogListener will consume more resources. We recommend you not use overly complex plug-in combinations to process data.
- If the combined parsing mode is used, the collection and filter features of the text mode will become invalid, but some of these features can be implemented through relevant user-defined plug-ins.
- If the combined parsing mode is used, the feature of uploading logs that fail to be parsed is enabled by default. For logs that fail to be parsed, the input name is the `Key` and the original log content is the `Value` for log uploading.


## Related Operations

#### Log search
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Search and Analysis** to go to the search and analysis page.
3. Select the region, logset, and log topic as needed, and click **Search and Analysis** to search for logs according to the set query rules.


