When setting the **notification content** and **custom webhook configuration** in an **alarm policy**, you can use alarm notification variables to customize the notification content and include a clearer cause description.

## Getting Started
When [configuring an alarm policy](https://intl.cloud.tencent.com/document/product/614/39574), enter the following configuration information for the notification content:
```
Detailed log:
{{.QueryLog[0][0]}}
```
The configured information should be as follows:

When the alarm notification is received, the notification content will be automatically replaced with the following value, indicating the last detailed log when the alarm is triggered:

```
Detailed log:
{"content":{"body_bytes_sent":"33352","http_referer":"-","http_user_agent":"Mozilla/5.0 (Windows NT 6.2; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/30.0.1599.17 Safari/537.36","remote_addr":"201.80.83.199","remote_user":"-","request_method":"GET","request_uri":"/content/themes/test-com/images/header_about.jpg","status":"404","time_local":"01/Nov/2018:01:16:31"},"fileName":"/root/testLog/nginx.log","pkg_id":"285A243662909DE3-70A","source":"172.17.0.2","time":1653831150008,"topicId":"a54de372-ffe0-49ae-a12e-c340bb2b03f2"}
```


## Notification Variables
<table>
<thead>
<tr>
<th>Variable</th>
<th width="18%">Configuration</th>
<th>Sample Variable Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>{{.UIN}}</td>
<td>Account ID</td>
<td>100007xxx827</td>
<td>-</td>
</tr>
<tr>
<td>{{.Nickname}}</td>
<td>Account nickname</td>
<td>xx company</td>
<td>-</td>
</tr>
<tr>
<td>{{.Region}}</td>
<td>Region</td>
<td>Guangzhou</td>
<td>-</td>
</tr>
<tr>
<td>{{.Alarm}}</td>
<td>Alarm policy name</td>
<td>Too many NGINX error logs</td>
<td>-</td>
</tr>
<tr>
<td>{{.AlarmID}}</td>
<td>Alarm policy ID</td>
<td>notice-3abd7ad6-15b7-4168-xxxx-52e5b961a561</td>
<td>-</td>
</tr>
<tr>
<td>{{.ExecuteQuery}}</td>
<td>Executed Statement</td>
<td>["status:&gt;=400 | select count(*) as errorLogCount","status:&gt;=400 | select count(*) as errorLogCount,request_uri group by request_uri order by count(*) desc"]</td>
<td>It is an array. <code>{{.ExecuteQuery[0]}}</code> indicates the detailed log of the first query statement, <code>{{.ExecuteQuery[1]}}</code> the second, and so on.</td>
</tr>
<tr>
<td>{{.Condition}}</td>
<td>Trigger Condition</td>
<td>$1.errorLogCount &gt; 1</td>
<td>-</td>
</tr>
<tr>
<td>{{.HappenThreshold}}</td>
<td>Number of times the trigger condition needs to be constantly met before an alarm is triggered</td>
<td>1</td>
<td>-</td>
</tr>
<tr>
<td>{{.AlertThreshold}}</td>
<td>Alarm interval</td>
<td>15</td>
<td>Unit: Minute</td>
</tr>
<tr>
<td>{{.Topic}}</td>
<td>Log topic name</td>
<td>nginxLog</td>
<td>-</td>
</tr>
<tr>
<td>{{.TopicId}}</td>
<td>Log topic ID</td>
<td>a54de372-ffe0-49ae-xxxx-c340bb2b03f2</td>
<td>-</td>
</tr>
<tr>
<td>{{.StartTime}}</td>
<td>Time when the alarm is triggered for the first time</td>
<td>2022-05-28 18:56:37</td>
<td>Time zone: Asia/Shanghai</td>
</tr>
<tr>
<td>{{.StartTimeUnix}}</td>
<td>Timestamp when the alarm is triggered for the first time</td>
<td>1653735397099</td>
<td>UNIX timestamp in milliseconds</td>
</tr>
<tr>
<td>{{.NotifyTime}}</td>
<td>Time of this alarm notification</td>
<td>2022-05-28 19:41:37</td>
<td>Time zone: Asia/Shanghai</td>
</tr>
<tr>
<td>{{.NotifyTimeUnix}}</td>
<td>Timestamp of this alarm notification</td>
<td>1653738097099</td>
<td>UNIX timestamp in milliseconds</td>
</tr>
<tr>
<td>{{.NotifyType}}</td>
<td>Alarm notification type</td>
<td>1</td>
<td>Valid values: `1` (alarmed), `2` (resolved)</td>
</tr>
<tr>
<td>{{.ConsecutiveAlertNums}}</td>
<td>Number of consecutive alarms</td>
<td>2</td>
<td>-</td>
</tr>
<tr>
<td>{{.Duration}}</td>
<td>Alarm duration</td>
<td>0</td>
<td>Unit: Minute</td>
</tr>
<tr>
<td>{{.TriggerParams}}</td>
<td>Alarm trigger parameter</td>
<td>$1.errorLogCount=5;</td>
<td>-</td>
</tr>
<tr>
<td>{{.ConditionGroup}}</td>
<td>Group information when the alarm is triggered</td>
<td>{"$1.AppName":"userManageService"}</td>
<td>This is valid only when triggering by group is enabled in the alarm policy.</td>
</tr>
<tr>
<td>{{.DetailUrl}}</td>
<td>URL of the alarm details page</td>
<td>https://alarm.cls.tencentcs.com/MDv2xxJh</td>
<td>No login is required.</td>
</tr>
<tr>
<td>{{.QueryUrl}}</td>
<td>URL of the search and analysis statement in the first query statement</td>
<td>https://alarm.cls.tencentcs.com/T0pkxxMA</td>
<td>-</td>
</tr>
<tr>
<td>{{.Message}}</td>
<td>Notification content</td>
<td>-</td>
<td>It indicates the **notification content** entered in the alarm policy.</td>
</tr>
<tr>
<td>{{.QueryResult}}</td>
<td>Execution result of the query statement</td>
<td>For more information, see the <a href="#QueryResult">{{.QueryResult}}</a> remarks.</td>
<td>-</td>
</tr>
<tr>
<td>{{.QueryLog}}</td>
<td>Detailed log matching the search condition of the query statement</td>
<td>For more information, see the <a href="#QueryLog">{{.QueryLog}}</a> remarks.</td>
<td>-</td>
</tr>
<tr>
<td>{{.AnalysisResult}}</td>
<td>Multi-dimensional analysis result</td>
<td>For more information, see the <a href="#AnalysisResult">{{.AnalysisResult}}</a> remarks.</td>
<td>This variable is valid only when an alarm is triggered and becomes invalid when the alarm is cleared.</td>
</tr>
</tbody></table>

Below are relevant descriptions:
<dx-accordion>
::: {{.QueryResult}}[](id:QueryResult)

- **Description**: Execution result of the query statement
- **Remarks**: It is an array. `{{.QueryResult[0]}}` indicates the execution result of the first query statement, `{{.QueryResult[1]}}` the second, and so on.
- **Sample variable value**:
If there are two query statements in the alarm policy:
```plaintext
The first query statement: status:>=400 | select count(*) as errorLogCount
The second query statement: status:>=400 | select count(*) as errorLogCount,request_uri group by request_uri order by count(*) desc
```
Then the variable values are:
```
[
	[{
		"errorLogCount": 7
	}],
	[{
		"errorLogCount": 3,
		"request_uri": "/apple-touch-icon-144x144.png"
	}, {
		"errorLogCount": 3,
		"request_uri": "/feed"
	}, {
		"errorLogCount": 1,
		"request_uri": "/opt/node_apps/test-v5/app/themes/basic/public/static/404.html"
	}]
]
```

:::
::: {{.QueryLog}}[](id:QueryLog)

- **Description**: Detailed log matching the search condition of the query statement (excluding SQL filter condition)
- **Remarks**: It is an array. `{{.QueryLog[0]}}` indicates the detailed log of the first query statement, `{{.QueryLog[1]}}` the second, and so on. Up to last ten detailed logs can be contained in each query statement.
- **Sample variable value**:
```
[
	[{
		"content": {
			"__TAG__": {
				"pod": "nginxPod",
				"cluster": "testCluster"
			},
			"body_bytes_sent": "32847",
			"http_referer": "-",
			"http_user_agent": "Opera/9.80 (Windows NT 6.1; U; en-US) Presto/2.7.62 Version/11.01",
			"remote_addr": "105.86.148.186",
			"remote_user": "-",
			"request_method": "GET",
			"request_uri": "/apple-touch-icon-144x144.png",
			"status": "404",
			"time_local": "01/Nov/2018:00:55:14"
		},
		"fileName": "/root/testLog/nginx.log",
		"pkg_id": "285A243662909DE3-5CD",
		"source": "172.17.0.2",
		"time": 1653739000013,
		"topicId": "a54de372-ffe0-49ae-a12e-c340bb2b03f2"
	}, {
		"content": {
			"__TAG__": {
				"pod": "nginxPod",
				"cluster": "testCluster"
			},
			"body_bytes_sent": "33496",
			"http_referer": "-",
			"http_user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.93 Safari/537.36",
			"remote_addr": "222.18.168.242",
			"remote_user": "-",
			"request_method": "GET",
			"request_uri": "/opt/node_apps/test-v5/app/themes/basic/public/static/404.html",
			"status": "404",
			"time_local": "01/Nov/2018:00:54:37"
		},
		"fileName": "/root/testLog/nginx.log",
		"pkg_id": "285A243662909DE3-5C8",
		"source": "172.17.0.2",
		"time": 1653738975008,
		"topicId": "a54de372-ffe0-49ae-a12e-c340bb2b03f2"
	}]
]
```

:::
::: {{.AnalysisResult}}[](id:AnalysisResult)

- **Description**: Multi-dimensional analysis result
- **Remarks**: It is an object. The level-1 object corresponds to each multi-dimensional analysis result, with the `key` being the multi-dimensional analysis name and the `value` being the multi-dimensional analysis result. This variable is valid only when an alarm is triggered (that is, {{.NotifyType}}=1) and becomes invalid when the alarm is cleared (that is, {{.NotifyType}}=2).
- **Sample variable value**:
If there are three multi-dimensional analysis operations in the alarm policy:
```plaintext
Name: Top URL
Type: Top 5 field values by occurrence and their percentages
Field: request_uri

Name: Error log URL distribution
Type: Custom search and analysis
Analysis statement: status:>=400 | select count(*) as errorLogCount,request_uri group by request_uri order by count(*) desc

Name: Detailed error log
Type: Custom search and analysis
Analysis statement: status:>=400
```
Then the variable values are:
```
{
	"Top URL": [{
		"count": 77,
		"ratio": 0.45294117647058824,
		"value": "/"
	}, {
		"count": 20,
		"ratio": 0.11764705882352941,
		"value": "/favicon.ico"
	}, {
		"count": 7,
		"ratio": 0.041176470588235294,
		"value": "/blog/feed"
	}, {
		"count": 5,
		"ratio": 0.029411764705882353,
		"value": "/test-tile-service"
	}, {
		"count": 3,
		"ratio": 0.01764705882352941,
		"value": "/android-chrome-192x192.png"
	}],
	"Detailed error log": [{
		"content": {
			"__TAG__": {
				"pod": "nginxPod",
				"cluster": "testCluster"
			},
			"body_bytes_sent": "32847",
			"http_referer": "-",
			"http_user_agent": "Opera/9.80 (Windows NT 6.1; U; en-US) Presto/2.7.62 Version/11.01",
			"remote_addr": "105.86.148.186",
			"remote_user": "-",
			"request_method": "GET",
			"request_uri": "/apple-touch-icon-144x144.png",
			"status": "404",
			"time_local": "01/Nov/2018:00:55:14"
		},
		"fileName": "/root/testLog/nginx.log",
		"pkg_id": "285A243662909DE3-5CD",
		"source": "172.17.0.2",
		"time": 1653739000013,
		"topicId": "a54de372-ffe0-49ae-a12e-c340bb2b03f2"
	}, {
		"content": {
			"__TAG__": {
				"pod": "nginxPod",
				"cluster": "testCluster"
			},
			"body_bytes_sent": "33496",
			"http_referer": "-",
			"http_user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_8_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.93 Safari/537.36",
			"remote_addr": "222.18.168.242",
			"remote_user": "-",
			"request_method": "GET",
			"request_uri": "/opt/node_apps/test-v5/app/themes/basic/public/static/404.html",
			"status": "404",
			"time_local": "01/Nov/2018:00:54:37"
		},
		"fileName": "/root/testLog/nginx.log",
		"pkg_id": "285A243662909DE3-5C8",
		"source": "172.17.0.2",
		"time": 1653738975008,
		"topicId": "a54de372-ffe0-49ae-a12e-c340bb2b03f2"
	}],
	"Error log URL distribution": [{
		"errorLogCount": 3,
		"request_uri": "/apple-touch-icon-144x144.png"
	}, {
		"errorLogCount": 3,
		"request_uri": "/feed"
	}, {
		"errorLogCount": 1,
		"request_uri": "/opt/node_apps/test-v5/app/themes/basic/public/static/404.html"
	}]
}
```

:::
</dx-accordion>


## Variable Syntax

The variable syntax is similar to Go template syntax. It extracts and formats alarm notification variables so that they can be displayed more clearly in the alarm notification content. All variables and their syntaxes are within `{{ }}`, and text outside `{{ }}` won't be processed.

### Variable extraction

**Syntax format**:
```
{{.variable[x]}} or {{index .variable x}}
{{.variable.childNodeName}} or {{index .variable "childNodeName"}}
```
**Syntax description**:
- When the variable is an array, `{{.variable[x]}}` (equivalent to `{{index .variable x}}`) is used to extract array elements by subscript. Here, `x` is an integer greater than or equal to 0.
- When the variable is an object, `{{.variable.childNodeKey}}` (equivalent to `{{index .variable "childNodeName"}}`) is used to extract sub-object values (`value`) by sub-object name (`key`).
>! When a sub-object name contains spaces, use syntax in the format of `{{index .variable "childNodeName"}}`, such as `{{index .AnalysisResult "Top URL"}}`.
>

**Sample**:
The `{{.QueryResult}}` variable values are:
```
[
	[{
		"errorLogCount": 7 // Extract the value
	}],
	[{
		"errorLogCount": 3,
		"request_uri": "/apple-touch-icon-144x144.png"
	}, {
		"errorLogCount": 3,
		"request_uri": "/feed"
	}, {
		"errorLogCount": 1,
		"request_uri": "/opt/node_apps/test-v5/app/themes/basic/public/static/404.html"
	}]
]
```
Get the `errorLogCount` value of the first array through the following expression:
```
{{.QueryResult[0][0].errorLogCount}}
```
Returned result:
```
7
```


### Loop and traversal

**Syntax format**:
```
{{range .variable}}
Custom content{{.childNode1}}custom content{{.childNode2}}...
{{end}}
```
Or
```
{{range $key,$value := .variable}}
Custom content{{$key}}custom content{{$value}}...
{{end}}
```

**Syntax description**:

When the variable is an array or an object that contains multiple sub-objects, you can use this syntax to display each element/object in the specified format.

**Sample**:

The `{{.QueryResult}}` variable values are:
```
[
	[{
		"errorLogCount": 7
	}],
	[{
		"errorLogCount": 3,
		"request_uri": "/apple-touch-icon-144x144.png"
	}, {
		"errorLogCount": 3,
		"request_uri": "/feed"
	}, {
		"errorLogCount": 1,
		"request_uri": "/opt/node_apps/test-v5/app/themes/basic/public/static/404.html"
	}]
]
```
Display the `errorLogCount` value of each `request_uri` in the second array through the following expression:
```
{{range .QueryResult[1]}}
* {{.request_uri}} error log quantity: {{.errorLogCount}}
{{end}}
```
Returned result:
```

* /apple-touch-icon-144x144.png error log quantity: 3

* /feed error log quantity: 3

* /opt/node_apps/test-v5/app/themes/basic/public/static/404.html error log quantity: 1


```


### Condition judgment

**Syntax format**:
```
{{if boolen}}
xxx
{{end}}
```
Or
```
{{if boolen}}
xxx
{{else}}
xxx
{{end}}
```
Or
```
{{if boolen}}
xxx
{{else if boolen}}
xxx
{{end}}
```

**Syntax description**:

Execute the expressions based on the condition judgment result, where AND, OR, and NOT can be used for logical operations and values can be compared.
```
eq arg1 arg2: When arg1 == arg2, the value is `true`. 
ne arg1 arg2: When arg1 != arg2, the value is `true`. 
lt arg1 arg2: When arg1 < arg2, the value is `true`. 
le arg1 arg2: When arg1 <= arg2, the value is `true`. 
gt arg1 arg2: When arg1 > arg2, the value is `true`. 
ge arg1 arg2: When arg1 >= arg2, the value is `true`.
```

**Sample**:

The `{{.QueryResult}}` variable values are:
```
[
	[{
		"errorLogCount": 7
	}],
	[{
		"errorLogCount": 3,
		"request_uri": "/apple-touch-icon-144x144.png"
	}, {
		"errorLogCount": 3,
		"request_uri": "/feed"
	}, {
		"errorLogCount": 1,
		"request_uri": "/opt/node_apps/test-v5/app/themes/basic/public/static/404.html"
	}]
]
```
Display the `request_uri` that is ≥ 2 and ≤ 100 and its `errorLogCount` value in the second array through the following expression:
```
{{range .QueryResult[1]}}
{{if and (ge .errorLogCount 2) (le .errorLogCount 100)}}
* {{.request_uri}} error log quantity: {{.errorLogCount}}
{{end}}
{{end}}
```
Returned result:
```


* /apple-touch-icon-144x144.png error log quantity: 3



* /feed error log quantity: 3




```
You can also use `if` to check whether the field value exists. If the field value is an empty string or does not exist, it is equivalent to `false`. For example:
```
{{if .QueryLog[0][0].apple}}
apple exist, value is : {{.QueryLog[0][0].apple}}
{{else}}
apple is not exist
{{end}}
```



### Blank area removal

**Syntax format**:
```
{{- xxx}} or {{xxx -}}
```

**Syntax description**:

When the variable syntax is executed, its spaces, indents, line breaks, and other blank areas will be retained. For example, many blank lines are contained in the returned result of the samples for loop and traversal as well as condition judgment, adversely affecting the display effect. You can add `-` at the beginning or end in `{{ }}` to remove blank areas.

**Sample**:

Change the expression in the condition judgment sample to:
```
{{- range .QueryResult[1]}}
{{- if and (ge .errorLogCount 2) (le .errorLogCount 100)}}
* {{.request_uri}} error log quantity: {{.errorLogCount}}
{{- end}}
{{- end}}
```
Returned result:
```
* /apple-touch-icon-144x144.png error log quantity: 3
* /feed error log quantity: 3
```


## Variable Function

### Special symbol escaping

**Syntax format**:
```
{{escape .variable}}
```

**Syntax description**:

Many alarm variables contain special symbols. If these variables are directly concatenated into JSON strings for custom webhooks, the JSON format may be incorrect, leading to callback failures. In this case, you can escape the original variables before they are concatenated.

**Sample**:

The `{{.ExecuteQuery[0]}}` variable value is `status:>=400 | select count(*) as "error log quantity"`.
If escaping is not used, the request content in the custom webhook configuration will be:
```json
{
  "Query":"{{.ExecuteQuery[0]}}"
}
```
The returned result will be as follows, which is not a valid JSON string:
```json

{
   "Query":"status:>=400 | select count(*) as "error log quantity""
}

```
In this case, you can use escaping to change the request content in the custom webhook configuration to:
```json
{
  "Query":"{{escape .ExecuteQuery[0]}}"
}
```
The returned result will be as follows, which is in line with the JSON syntax:
```json
{
  "Query":"status:>=400 | select count(*) as \"error log quantity\""
}

```


### String extraction

#### Extraction by length

**Syntax format**:

```
{{substr .variable start}} or {{substr .variable start length}}
```

**Syntax description**:

Extract a string based on the specified start point and length (optional).

**Sample**:

The `{{.QueryLog[0][0].fileName}}` variable value is:
```
/root/testLog/nginx.log
```
Get a string starting from the sixth character and containing seven characters through the following expression:
```
{{substr .QueryLog[0][0].fileName 6 7 }}
```
Returned result:
```
testLog
```

#### Extraction based on the start and end characters

**Syntax format**:

```
{{extract .variable "startstring" ["endstring"]}}
```

**Syntax description**:

Extract a string based on the specified start and end characters (optional).

**Sample**:

The `{{.QueryLog[0][0].fileName}}` variable value is:
```
/root/testLog/nginx.log
```
Get a string between `/root/` and `/nginx` through the following expression:
```
{{extract .QueryLog[0][0].fileName "/root/" "/nginx"}}
```
Returned result:
```
testLog
```


### Specified string check

**Syntax format**:

```
{{containstr .variable "searchstring"}}
```

**Syntax description**:

Check whether the specified string is included in the variable value. The check result can be used in the condition judgment syntax.

**Sample**:

The `{{.QueryLog[0][0].fileName}}` variable value is:
```
/root/testLog/nginx.log
```
Get a string between `/root/` and `/nginx` through the following expression:
```
{{if containstr .QueryLog[0][0].fileName "test"}}
Test log
{{else}}
Non-test log
{{end}}
```
Returned result:
```
Test log
```


### UNIX timestamp conversion

**Syntax format**:
```
{{fromUnixTime .variable}} or {{fromUnixTime .variable "timezone"}}
```

**Syntax description**:

It is used to convert UNIX timestamps (in milliseconds or seconds) into readable dates and times. Here, the time zone is optional and is Asia/Shanghai by default.

**Sample**:

The `{{.QueryLog[0][0].time}}` variable value is:
```
1653893435008
```
Get the dates and times in different time zones through the following expressions:
```
{{fromUnixTime .QueryLog[0][0].time}}
{{fromUnixTime .QueryLog[0][0].time "Asia/Shanghai"}}
{{fromUnixTime .QueryLog[0][0].time "Asia/Tokyo"}}
```
Returned result:
```

2022-05-30 14:50:35.008 +0800 CST
2022-05-30 14:50:35.008 +0800 CST
2022-05-30 15:50:35.008 +0900 JST

```

### String concatenation

**Syntax format**:

```
{{concat .variable1 .variable2 ...}}
```

**Syntax description**:

Concatenate specified variables or strings.

**Sample**:

Concatenate the region and alarm policy name.
```
{{concat .Region .Alarm}}
```
Returned result:
```
Guangzhou alarmTest
```

### Base64/Base64URL/URL encoding and decoding

**Syntax format**:

```
{{base64_encode .variable}}
{{base64_decode .variable}}
{{base64url_encode .variable}}
{{base64url_decode .variable}}
{{url_encode .variable}}
{{url_decode .variable}}
```

**Syntax description**:

Encode or decode specified variables or strings. Here, the *"="* at the end will not be removed or added during Base64URL encoding and decoding.

**Sample**:

```
{{base64_encode "test"}}
{{base64_decode "dGVzdOa1i+ivlQ=="}}
{{base64url_encode "test"}}
{{base64url_decode "dGVzdOa1i-ivlQ=="}}
{{url_encode "https://console.cloud.tencent.com:80/cls?region=ap-chongqing"}}
{{url_decode "https%3A%2F%2Fconsole.cloud.tencent.com%3A80%2Fcls%3Fregion%3Dap-chongqing"}}
```

Returned result:

```
dGVzdOa1i+ivlQ==
test
dGVzdOa1i-ivlQ==
test
https%3A%2F%2Fconsole.cloud.tencent.com%3A80%2Fcls%3Fregion%3Dap-chongqing
https://console.cloud.tencent.com:80/cls?region=ap-chongqing
```

### MD5/SHA1/SHA256/SHA512 encryption

**Syntax format**:

```
{{md5 .variable}}
{{md5 .variable | base64_encode}}
{{md5 .variable | base64url_encode}}
{{sha1 .variable}}
{{sha1 .variable | base64_encode}}
{{sha1 .variable | base64url_encode}}
{{sha256 .variable}}
{{sha256 .variable | base64_encode}}
{{sha256 .variable | base64url_encode}}
{{sha512 .variable}}
{{sha512 .variable | base64_encode}}
{{sha512 .variable | base64url_encode}}
```

**Syntax description**:

Encrypt specified variables or strings using a certain encryption algorithm. By default, hexadecimal strings are returned, which can be converted into Base64 or Base64URL as needed.

**Sample**:

```
{{md5 "test"}}
{{md5 "test" | base64_encode}}
{{md5 "test" | base64url_encode}}
{{sha1 "test"}}
{{sha1 "test" | base64_encode}}
{{sha1 "test" | base64url_encode}}
{{sha256 "test"}}
{{sha256 "test" | base64_encode}}
{{sha256 "test" | base64url_encode}}
{{sha512 "test"}}
{{sha512 "test" | base64_encode}}
{{sha512 "test" | base64url_encode}}
```

Returned result:
```javascript
098F6BCD4621D373CADE4E832627B4F6
CY9rzUYh03PK3k6DJie09g==
CY9rzUYh03PK3k6DJie09g==
A94A8FE5CCB19BA61C4C0873D391E987982FBBD3
qUqP5cyxm6YcTAhz05Hph5gvu9M=
qUqP5cyxm6YcTAhz05Hph5gvu9M=
9F86D081884C7D659A2FEAA0C55AD015A3BF4F1B2B0B822CD15D6C15B0F00A08
n4bQgYhMfWWaL+qgxVrQFaO/TxsrC4Is0V1sFbDwCgg=
n4bQgYhMfWWaL-qgxVrQFaO_TxsrC4Is0V1sFbDwCgg=
EE26B0DD4AF7E749AA1A8EE3C10AE9923F618980772E473F8819A5D4940E0DB27AC185F8A0E1D5F84F88BC887FD67B143732C304CC5FA9AD8E6F57F50028A8FF
7iaw3Ur350mqGo7jwQrpkj9hiYB3Lkc/iBml1JQODbJ6wYX4oOHV+E+IvIh/1nsUNzLDBMxfqa2Ob1f1ACio/w==
7iaw3Ur350mqGo7jwQrpkj9hiYB3Lkc_iBml1JQODbJ6wYX4oOHV-E-IvIh_1nsUNzLDBMxfqa2Ob1f1ACio_w==
```

### HMAC_MD5/HMAC_SHA1/HMAC_SHA256/HMAC_SHA512 encryption

**Syntax format**:

```
{{hmac_md5 .variable "Secretkey"}}
{{hmac_md5 .variable "Secretkey" | base64_encode}}
{{hmac_md5 .variable "Secretkey" | base64url_encode}}
{{hmac_sha1 .variable "Secretkey"}}
{{hmac_sha1 .variable "Secretkey" | base64_encode}}
{{hmac_sha1 .variable "Secretkey" | base64url_encode}}
{{hmac_sha256 .variable "Secretkey"}}
{{hmac_sha256 .variable "Secretkey" | base64_encode}}
{{hmac_sha256 .variable "Secretkey" | base64url_encode}}
{{hmac_sha512 .variable "Secretkey"}}
{{hmac_sha512 .variable "Secretkey" | base64_encode}}
{{hmac_sha512 .variable "Secretkey" | base64url_encode}}
```

**Syntax description**:

Encrypt specified variables or strings using a certain encryption algorithm. By default, hexadecimal strings are returned, which can be converted into Base64 or Base64URL as needed. Here, `Secretkey` is the key in the HMAC encryption algorithm and can be modified as needed.

**Sample**:

```
{{hmac_md5 "test" "Secretkey"}}
{{hmac_md5 "test" "Secretkey" | base64_encode}}
{{hmac_md5 "test" "Secretkey" | base64url_encode}}
{{hmac_sha1 "test" "Secretkey"}}
{{hmac_sha1 "test" "Secretkey" | base64_encode}}
{{hmac_sha1 "test" "Secretkey" | base64url_encode}}
{{hmac_sha256 "test" "Secretkey"}}
{{hmac_sha256 "test" "Secretkey" | base64_encode}}
{{hmac_sha256 "test" "Secretkey" | base64url_encode}}
{{hmac_sha512 "test" "Secretkey"}}
{{hmac_sha512 "test" "Secretkey" | base64_encode}}
{{hmac_sha512 "test" "Secretkey" | base64url_encode}}
```

Returned result:

```javascript
E7B946D930658699AA668601E33E87CE
57lG2TBlhpmqZoYB4z6Hzg==
57lG2TBlhpmqZoYB4z6Hzg==
2AB64F124D932F5033EAC7AF392AC5CC4D52F503
KrZPEk2TL1Az6sevOSrFzE1S9QM=
KrZPEk2TL1Az6sevOSrFzE1S9QM=
FC49EBC05209B1359773D87C216BA85BCE0163FDE459EA37AB603EC9D8445D23
/EnrwFIJsTWXc9h8IWuoW84BY/3kWeo3q2A+ydhEXSM=
_EnrwFIJsTWXc9h8IWuoW84BY_3kWeo3q2A-ydhEXSM=
D18DF3D943F74769A8B66E43D7EF03639BB6B8B8A2EBC9976170DC58EEE58BE98478F3183E4B5AA3481DE12026AAE3843F8213B39D639EAC6EE93734EA667BC5
0Y3z2UP3R2motm5D1+8DY5u2uLii68mXYXDcWO7li+mEePMYPktao0gd4SAmquOEP4ITs51jnqxu6Tc06mZ7xQ==
0Y3z2UP3R2motm5D1-8DY5u2uLii68mXYXDcWO7li-mEePMYPktao0gd4SAmquOEP4ITs51jnqxu6Tc06mZ7xQ==
```


## Use Cases

#### Case 1: Displaying the last detailed log in the alarm notification

**Scenario**:
The last detailed log that meets the search condition of the query statement is added to the alarm notification in the format of `key:value`. There is a key in each row, and CLS preset fields and metadata fields are not included.

**Notification content configuration**:
```
{{range $key,$value := .QueryLog[0][0].content}}
{{if not (containstr $key "__TAG__")}}
{{- $key}}:{{$value}}
{{- end}}
{{- end}}
```
Here, `.QueryLog[0][0]` indicates the last detailed log that meets the search condition of the first query statement in the alarm policy. Its value is:
```
{
	"content": {
		"__TAG__": {
			"a": "b12fgfe",
			"c": "fgerhcdhgj"
		},
		"body_bytes_sent": "33704",
		"http_referer": "-",
		"http_user_agent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36",
		"remote_addr": "247.0.249.191",
		"remote_user": "-",
		"request_method": "GET",
		"request_uri": "/products/hadoop)",
		"status": "404",
		"time_local": "01/Nov/2018:07:54:08"
	},
	"fileName": "/root/testLog/nginx.log",
	"pkg_id": "285A243662909DE3-210B",
	"source": "172.17.0.2",
	"time": 1653908859008,
	"topicId": "a54de372-ffe0-49ae-a12e-c340bb2b03f2"
}
```

**Alarm notification content**:
```
remote_addr:247.0.249.191
time_local:01/Nov/2018:07:54:08
http_user_agent:Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/35.0.3319.102 Safari/537.36
remote_user:-
http_referer:-
body_bytes_sent:33704
request_method:GET
request_uri:/products/hadoop)
status:404
```


#### Case 2: Displaying the execution result of the query statement in the alarm notification

**Scenario**:
What meets the trigger condition in the execution result of the query statement is added to the alarm notification and displayed in a list.
The query statement of the alarm policy is `status:>=400 | select count(*) as errorLogCount,request_uri group by request_uri order by count(*) desc`.
The trigger condition is `$1.errorLogCount > 10`.

**Notification content configuration**:
```
{{range .QueryResult[0]}}
{{- if gt .errorLogCount 10}}
{{.request_uri}} error log quantity: {{.errorLogCount}}
{{- end}}
{{- end}}
```
Here, `.QueryResult[0]` indicates the execution result of the first query statement in the alarm policy. Its value is:
```
[{
	"errorLogCount": 161,
	"request_uri": "/apple-touch-icon-144x144.png"
}, {
	"errorLogCount": 86,
	"request_uri": "/opt/node_apps/test-v5/app/themes/basic/public/static/404.html"
}, {
	"errorLogCount": 33,
	"request_uri": "/feed"
}, {
	"errorLogCount": 26,
	"request_uri": "/wp-login.php"
}, {
	"errorLogCount": 10,
	"request_uri": "/safari-pinned-tab.svg"
}, {
	"errorLogCount": 7,
	"request_uri": "/mstile-144x144.png"
}, {
	"errorLogCount": 4,
	"request_uri": "/atom.xml"
}, {
	"errorLogCount": 3,
	"request_uri": "/content/plugins/prettify-gc-syntax-highlighter/launch.js?ver=3.5.2?ver=3.5.2"
}]
```

**Alarm notification content**:
```
/apple-touch-icon-144x144.png error log quantity: 161
/opt/node_apps/elastic-v5/app/themes/basic/public/static/404.html error log quantity: 86
/feed error log quantity: 33
/wp-login.php error log quantity: 26
```
