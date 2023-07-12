## Overview
CLS supports log collection for self-built Kubernetes clusters. Before performing log collection on a self-built Kubernetes cluster, you need to use a custom resource definition (CRD) to define log collection configuration (LogConfig), and deploy Log-Provisioner, Log-Agent, and LogListener on the cluster. If you are a Tencent Kubernetes Engine (TKE) user, you can quickly access and use the CLS service by referring to [Enabling log collection](https://intl.cloud.tencent.com/document/product/457/32419).


## Prerequisites

- You have created a cluster of Kubernetes 1.10 or above.
- You have configured TencentCloud API permissions required for self-built Kubernetes log collection. For more information, see [Examples of Custom Access Policies](https://intl.cloud.tencent.com/document/product/614/45004).
- You have enabled CLS, created a logset and a log topic, and obtained the log topic ID (`topicId`).
For more information, see [Managing Log Topic](https://intl.cloud.tencent.com/document/product/614/34239).
- You have obtained the domain name (`CLS_HOST`) of the region of your log topic.
For details of the CLS domain name list, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).
- You have obtained the API key ID (`TmpSecretId`) and API key (`TmpSecretKey`) required for CLS authentication.
To obtain the API key and API key ID, go to [Manage API Key](https://console.cloud.tencent.com/cam/capi).


## Kubernetes Log Collection Principles
Log collection on a Kubernetes cluster requires the following:
- LogConfig: CRD of log collection configuration, which defines where logs are collected, how they are parsed, and to which CLS log topic they are shipped after being parsed.
- Log-Agent: component used to listen for changes in LogConfig and containers on nodes and dynamically calculate the actual positions of log files in containers on node hosts.
- Log-Provisioner: component used to synchronize the log collection configuration defined in LogConfig to CLS.
- LogListener: component used to collect log file content from node hosts, parses it, and uploads it to CLS.


## Flowchart
<dx-steps>

- <a href="#install_LogListener">Install LogListener in a self-built Kubernetes cluster</a>
- <a href="#logconfig_def">Define the LogConfig object</a>
- <a href="#logconfig_create">Create a LogConfig object</a>
</dx-steps>

## Directions

### Step 1. Install LogListener in a self-built Kubernetes cluster[](id:install_LogListener)

First, you need to install the LogListener component in the self-built Kubernetes cluster as instructed [here](https://intl.cloud.tencent.com/document/product/614/43573) to collect logs to CLS.


### Step 2. Define the LogConfig object[](id:logconfig_def)

Define log collection configuration in the LogConfig object via CRD. Run the `wget` command to download the `LogConfig.yaml` CRD declaration file, using the master node path `/usr/local/` as an example.

```shell
wget https://mirrors.tencent.com/install/cls/k8s/LogConfig.yaml
```
The `LogConfig.yaml` declaration file consists of the following two parts:
- `clsDetail`: The configuration for shipping to CLS.
- `inputDetail`: Log source configuration.

```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig                               ## Default value
metadata:
  name: test						      	## CRD resource name, which is unique in the cluster.
spec:
  clsDetail:							  	## The configuration for shipping to CLS
    ...
  inputDetail:                                ## Log source configuration
    ...
```

#### clsDetail (the configuration for shipping to CLS) field description


```yaml
  clsDetail:
    # You need to specify the logset and topic names to automatically create a log topic, which cannot be modified after being defined.
    logsetName: test                      	## The name of the CLS logset. If there is no logset with this name, one will be created automatically. If there is such a logset, a log topic will be created under it.
    topicName: test             	   ## The name of the CLS log topic. If there is no log topic with this name, one will be created automatically.
	# Select an existing logset and log topic. If the logset is specified but the log topic is not, a log topic will be created automatically, which cannot be modified after being defined.
    logsetId: xxxxxx-xx-xx-xx-xxxxxxxx  	 ## The ID of the CLS logset. The logset needs to be created in advance in CLS.
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx  	 ## The ID of the CLS log topic. The log topic needs to be created in advance in CLS and not occupied by other collection configurations.
    region: ap-xxx                  	   ## Topic region for cross-region shipping
    # Define the log topic configuration when a log topic is created automatically. The configuration cannot be modified after being defined.
    period: 30					        	## Lifecycle in days. Value range: 1–3600. `3640` indicates permanent storage.
    storageType: hot.             		  ## Log topic storage class. Valid values: `hot` (STANDARD); `cold` (STANDARD_IA). Default value: `hot`.
    HotPeriod: 7                              ## Transition cycle in days. Value range: 1–3600. It is valid only if `storageType` is `hot`.
    partitionCount:                	## The number (an integer) of log topic partitions. Default value: `1`. Maximum value: `10`.
    autoSplit: true					   	## Whether to enable auto-split (Boolen type). Default value: `true`.
    maxSplitPartitions:	10		     	## The maximum number (an integer) of partitions
    tags:                             		## Tag description list. This parameter is used to bind a tag to a log topic. Up to nine tag key-value pairs are supported, and a resource can be bound to only one tag key.
      - key: xxx						  	## Tag key
        value: xxx                        	## Tag value
    # Define collection rules
    logType: json_log  			   		## Log parsing format. Valid values: `json_log` (JSON); `delimiter_log` (separator); `minimalist_log` (full text in a single line); `multiline_log` (full text in multi lines); `fullregex_log` (single line - full regex); `multiline_fullregex_log` (multiple lines - full regex). Default value: `minimalist_log`.
    logFormat: xxx                        	## Log formatting method
    excludePaths:                     		## Collection path blocklist
      - type: File							## Type. Valid values: `File`, `Path`. 
        value: /xx/xx/xx/xx.log           	## The value of `type`
    userDefineRule: xxxxxx             	   ## Custom collection rule, which is a serialized JSON string.
    extractRule: {}                   		## Extraction and filter rule. If `ExtractRule` is set, `LogType` must be set. For more information, see the extractRule description.
    AdvancedConfig:				   		## Advanced collection configuration
      MaxDepth: 1					     	## Maximum number of directory levels
      FileTimeout: 60				     	## File timeout attribute
    # Define index configuration, which cannot be modified then.
    indexs: 							  	## You can customize the index method and field when creating a topic.
      - indexName:   				 		## The field for which to configure the key value or meta field index. You don't need to add the `__TAG__.` prefix to the key of the meta field and can just use that of the corresponding field when uploading a log, as the `__TAG__.` prefix will be automatically added for display in the Tencent Cloud console.
        indexType:  		      			## Field type. Valid values: `long`, `text`, `double`.
        tokenizer:  				  		## Field delimiter. Each character represents a delimiter. Only English symbols and \n\t\r are supported. For `long` and `double` fields, leave it empty. For `text` fields, we recommend that you use @&?|#()='",;:<>[]{}/ \n\t\r\ as the delimiter.
        sqlFlag:   				   		## Whether the analysis feature is enabled for the field (Boolen)
        containZH: 	       				## Whether Chinese characters are contained (Boolen)
```

**extractRule description**

| Name | Type | Required | Description |
| -------------- | --------------- | ------ | ------------------------------------------------------------ |
| timeKey        | String          | No     | The specified field in the log to be used as the log timestamp. If the configuration is empty, the actual log collection time will be used. `time_key` and `time_format` must appear in pairs. |
| timeFormat | String | No | Time field format. For more information, see the output parameters of the time format description of the `strftime` function in C programming language. |
| delimiter | String | No | The delimiter for delimited logs, which is valid only if `log_type` is `delimiter_log`. |
| logRegex | String | No | Full log matching rule, which is valid only if `log_type` is `fullregex_log`. |
| beginningRegex | String | No | First-line matching rule, which is valid only if `log_type` is `multiline_log` or `multiline_fullregex_log`. |
| unMatchUpload | String | No | Whether to upload the logs failed to be parsed. Valid values: `true` (yes); `false` (no). |
| unMatchedKey | String | No | The key of the log failed to be parsed. |
| backtracking | String | No | The size of the data to be rewound in incremental collection mode. Valid values: `-1` (full collection); `0` (incremental collection). Default value: `-1`. |
| keys | Array of String | No | The key name of each extracted field. An empty key indicates to discard the field. This parameter is valid only if `log_type` is `delimiter_log`, `fullregex_log`, or `multiline_fullregex_log`. `json_log` logs use the key of JSON itself. |
| filterKeys | Array of String | No | Log keys to be filtered, which correspond to `FilterRegex` by subscript. |
| filterRegex | Array of String | No | The `regex` of the log keys to be filtered, which corresponds to `FilterKeys` by subscript. |
| isGBK | String | No | Whether it is GBK-encoded. Valid values: `0` (no); `1` (yes).<br>Note: This field may return null, indicating that no valid values can be obtained. |



#### Log collection rule configuration sample

#### <dx-tabs>
::: Full text in a single line [](id:single_line)
In "full text in a single line" mode, a line is a full log. When CLS collects logs, it uses the line break `\n` to mark the end of a log. For easier structural management, a default key value `\_\_CONTENT\_\_` is given to each log, but the log data itself will no longer be structured, nor will the log field be extracted. The time attribute of a log is determined by the collection time.

Assume that the raw data of a log is as follows:
```
Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64
```

A sample of LogConfig configuration is as follows:
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  clsDetail:
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
    # Single-line log
    logType: minimalist_log
```

The data collected to CLS is as follows:
```
__CONTENT__:Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64
```
:::
::: Full text in multi lines [](id:multi_line)
In "full text in multi lines" mode, a log may span multiple lines (such as Java stacktrace), and the line break `\n` cannot be used to mark the end of a log. To help CLS distinguish between logs, a first-line regular expression is used for matching. When a line of a log matches the preset regular expression, it is considered as the beginning of the log, and the log ends before the next matching line.

In the "full text in multi lines" mode, a default key `\_\_CONTENT\_\_` is also set, but the log data itself is not structured, and no log fields are extracted. The time attribute of a log is determined by the collection time.

Assume that the raw data of a multi-line log is:
```
2019-12-15 17:13:06,043 [main] ERROR com.test.logging.FooFactory:
java.lang.NullPointerException
    at com.test.logging.FooFactory.createFoo(FooFactory.java:15)
    at com.test.logging.FooFactoryTest.test(FooFactoryTest.java:11)
```

A sample of LogConfig is as follows:
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  clsDetail:
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
    # Multi-line log
    logType: multiline_log
    extractRule:
      # Only a line that starts with a date time is considered the beginning of a new log. Otherwise, add the line break `\n` to the end of the current log.
      beginningRegex: \d{4}-\d{2}-\d{2}\s\d{2}:\d{2}:\d{2},\d{3}\s.+
```

The data collected to CLS is as follows:
```
__CONTENT__:2019-12-15 17:13:06,043 [main] ERROR com.test.logging.FooFactory:\njava.lang.NullPointerException\n    at com.test.logging.FooFactory.createFoo(FooFactory.java:15)\n    at com.test.logging.FooFactoryTest.test(FooFactoryTest.java:11)
```
:::
::: Single line - full regex [](id:single_full_regex)
The "single line - full regex" mode is often used to process structured logs. It parses a full log by extracting multiple key-value pairs based on a regex. 

Assume that the raw data of a log is as follows:
```
10.135.46.111 - - [22/Jan/2019:19:19:30 +0800] "GET /my/course/1 HTTP/1.1" 127.0.0.1 200 782 9703 "http://127.0.0.1/course/explore?filter%5Btype%5D=all&filter%5Bprice%5D=all&filter%5BcurrentLevelId%5D=all&orderBy=studentNum" "Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0"  0.354 0.354
```

A sample of LogConfig is as follows:
```
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  clsDetail:
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
    # Full Regex
    logType: fullregex_log
    extractRule:
      # Regular expression, in which the corresponding values will be extracted based on the `()` capture groups
      logRegex: (\S+)[^\[]+(\[[^:]+:\d+:\d+:\d+\s\S+)\s"(\w+)\s(\S+)\s([^"]+)"\s(\S+)\s(\d+)\s(\d+)\s(\d+)\s"([^"]+)"\s"([^"]+)"\s+(\S+)\s(\S+).*
      beginningRegex: (\S+)[^\[]+(\[[^:]+:\d+:\d+:\d+\s\S+)\s"(\w+)\s(\S+)\s([^"]+)"\s(\S+)\s(\d+)\s(\d+)\s(\d+)\s"([^"]+)"\s"([^"]+)"\s+(\S+)\s(\S+).*
      # List of extracted keys, which are in one-to-one correspondence with the extracted values
      keys:  ['remote_addr','time_local','request_method','request_url','http_protocol','http_host','status','request_length','body_bytes_sent','http_referer','http_user_agent','request_time','upstream_response_time']
```

The data collected to CLS is as follows:
```
body_bytes_sent: 9703
http_host: 127.0.0.1
http_protocol: HTTP/1.1
http_referer: http://127.0.0.1/course/explore?filter%5Btype%5D=all&filter%5Bprice%5D=all&filter%5BcurrentLevelId%5D=all&orderBy=studentNum
http_user_agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0
remote_addr: 10.135.46.111
request_length: 782
request_method: GET
request_time: 0.354
request_url: /my/course/1
status: 200
time_local: [22/Jan/2019:19:19:30 +0800]
upstream_response_time: 0.354
```
:::
::: Multiple lines - full regex [](id:multi_full_regex)
In "multiple lines - full regex" mode, multiple key-value pairs can be extracted from a complete piece of log data that spans multiple lines in a log text file (such as Java program logs) based on a regular expression. If you don't need to extract key-value pairs, please configure it by referring to the "full text in multi lines" mode.

Assume that the raw data of a log is as follows:
```
[2018-10-01T10:30:01,000] [INFO] java.lang.Exception: exception happened
   at TestPrintStackTrace.f(TestPrintStackTrace.java:3)
   at TestPrintStackTrace.g(TestPrintStackTrace.java:7)
   at TestPrintStackTrace.main(TestPrintStackTrace.java:16)
```

A sample of LogConfig is as follows:
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec: 
  clsDetail: 
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
        # Multiple lines - full regex
        logType: multiline_fullregex_log
        extractRule: 
          # The first-line full regular expression: only a line that starts with a date time is considered the beginning of a new log. Otherwise, add the line break `\n` to the end of the current log.
          beginningRegex: \[\d+-\d+-\w+:\d+:\d+,\d+\]\s\[\w+\]\s.*
          # Regular expression, in which the corresponding values will be extracted based on the `()` capture groups
          logRegex: \[(\d+-\d+-\w+:\d+:\d+,\d+)\]\s\[(\w+)\]\s(.*)
          # List of extracted keys, which are in one-to-one correspondence with the extracted values
          keys: ['time','level','msg']
```

Based on the extracted key, the data collected to CLS is as follows:
```
time: 2018-10-01T10:30:01,000`
level: INFO`
msg: java.lang.Exception: exception happened
   at TestPrintStackTrace.f(TestPrintStackTrace.java:3)
   at TestPrintStackTrace.g(TestPrintStackTrace.java:7)
   at TestPrintStackTrace.main(TestPrintStackTrace.java:16)
```
:::
::: JSON format [](id:json)
A JSON log automatically extracts the key at the first layer as the field name and the value at the first layer as the field value to implement structured processing of the entire log. Each complete log ends with a line break `\n`.

Assume the raw data of a JSON log is as follows:
```
{"remote_ip":"10.135.46.111","time_local":"22/Jan/2019:19:19:34 +0800","body_sent":23,"responsetime":0.232,"upstreamtime":"0.232","upstreamhost":"unix:/tmp/php-cgi.sock","http_host":"127.0.0.1","method":"POST","url":"/event/dispatch","request":"POST /event/dispatch HTTP/1.1","xff":"-","referer":"http://127.0.0.1/my/course/4","agent":"Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0","response_code":"200"}
```

A sample of LogConfig is as follows:
```
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  clsDetail:
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
    # JSON log
    logType: json_log
```

The data collected to CLS is as follows:
```
agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0
body_sent: 23
http_host: 127.0.0.1
method: POST
referer: http://127.0.0.1/my/course/4
remote_ip: 10.135.46.111
request: POST /event/dispatch HTTP/1.1
response_code: 200
responsetime: 0.232
time_local: 22/Jan/2019:19:19:34 +0800
upstreamhost: unix:/tmp/php-cgi.sock
upstreamtime: 0.232
url: /event/dispatch
xff: -
```
:::
::: Separator format [](id:delimiter)
For a log in separator format (separator log), the entire log data can be structured according to the specified separator, and each complete log ends with a line break `\n`. When CLS processes separator logs, you need to define a unique key for each separate field.

Assume the raw data of a log is as follows:
```
10.20.20.10 ::: [Tue Jan 22 14:49:45 CST 2019 +0800] ::: GET /online/sample HTTP/1.1 ::: 127.0.0.1 ::: 200 ::: 647 ::: 35 ::: http://127.0.0.1/
```

A sample of LogConfig is as follows:
```
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  clsDetail:
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
    # Separator log
    logType: delimiter_log
    extractRule:
      # Separator
      delimiter: ':::'
      # List of extracted keys, which are in one-to-one correspondence to the separated fields
      keys: ['IP','time','request','host','status','length','bytes','referer']
```

The data collected to CLS is as follows:
```
IP: 10.20.20.10
bytes: 35
host: 127.0.0.1
length: 647
referer: http://127.0.0.1/
request: GET /online/sample HTTP/1.1
status: 200
time: [Tue Jan 22 14:49:45 CST 2019 +0800]
```
:::
</dx-tabs>


#### inputDetail (log source) field description

```yaml
  inputDetail:
    type: container_stdout   			    	## Log collection type. Valid values: `container_stdout` (container standard output); `container_file` (container file); `host_file` (host file).
    containerStdout:        				 	## Container standard output configuration, which is valid only if `type` is `container_stdout`.
      namespace: default   			 	 	## The Kubernetes namespace of the container to be collected. Separate multiple namespaces by `,`, for example, `default,namespace`. If this field is not specified, it indicates all namespaces. Note that this field cannot be specified if `excludeNamespace` is specified.
      excludeNamespace: nm1,nm2   		   	## The Kubernetes namespace of the container to be excluded. Separate multiple namespaces by `,`, for example, `nm1,nm2`. If this field is not specified, it indicates all namespaces. Note that this field cannot be specified if `namespace` is specified.
	  nsLabelSelector: environment in (production),tier in (frontend) ## The namespace label for filtering namespaces
      allContainers: false      			 	## Whether to collect the standard output of all containers in the specified namespace. Note that if `allContainers=true`, you cannot specify `workload`, `includeLabels`, and `excludeLabels` at the same time.
      containerOperator: in                      ## Container selection method. Valid values: `in` (include); `not in` (exclude).
      container: xxx             				## The name of the container to be or not to be collected
      includeLabels:  					   	## The labels of the Pods to be collected. This field cannot be specified if `workload` is specified.
        key: value1   					   	## Pods with multiple values of the same key can be matched. For example, if you enter `environment = production,qa`, Pods with the `production` or `qa` value of the `environment` key will be matched. Separate multiple values by comma. If `excludeLabels` is also specified, Pods in the intersection will be matched.
      excludeLabels:  						   ## The labels of the Pods to be excluded. This field cannot be specified if `workload`, `namespace`, and `excludeNamespace` are specified.
        key2: value2  					   	## Pods with multiple values of the same key can be matched. For example, if you enter `environment = production,qa`, Pods with the `production` or `qa` value of the `environment` key will be excluded. Separate multiple values by comma. If `includeLabels` is also specified, Pods in the intersection will be matched.
      metadataLabels:            				## The Pod labels to be collected as metadata. If this field is not specified, all Pod labels will be collected as metadata.
      - label1
      metadataContainer:					 	## The container environments of the metadata to be collected. If this field is not specified, metadata (`namespace`, `pod_name`, `pod_ip`, `pod_uid`, `container_id`, `container_name`, and `image_name`) of all container environments will be collected.
      - namespace
      customLabels:              				## Custom metadata
        label: l1
      workloads:						 		## The workloads of the specified workload types in the specified namespaces of the containers of the logs to be collected
      - container: xxx    			   		## The name of the container to be collected. If this field is not specified, all containers in the workload Pod will be collected.
        containerOperator: in                      ## Container selection method. Valid values: `in` (include); `not in` (exclude).
        kind: deployment  			   		## Workload type. Valid values: `deployment`, `daemonset`, `statefulset`, `job`, `cronjob`.
        name: sample-app  			   		## Workload name
        namespace: prod   			   		## Workload namespace
		
    containerFile:  				 			## Container file configuration, which is valid only if `type` is `container_file`.
      namespace: default      			   	## The Kubernetes namespace of the container to be collected. You must specify a namespace.	  
      excludeNamespace: nm1,nm2   	       	## The Kubernetes namespace of the container to be excluded. Separate multiple namespaces by `,`, for example, `nm1,nm2`. If this field is not specified, it indicates all namespaces. Note that this field cannot be specified if `namespace` is specified.
      nsLabelSelector: environment in (production),tier in (frontend) ## The namespace label for filtering namespaces
      containerOperator: in                      ## Container selection method. Valid values: `in` (include); `not in` (exclude).
      container: xxx          			   	## The name of the container to be collected. If it is `*`, it indicates the names of all containers to be collected.
      logPath: /var/logs      			   	## Log folder. Wildcards are not supported.
      filePattern: app_*.log 					## Log filename. Wildcards `*` and `?` are supported. `*` indicates to match any number of characters, while `?` indicates to match any single character.
      includeLabels:  					   	## The labels of the Pods to be collected. This field cannot be specified if `workload` is specified.
        key: value1   					   	## The `metadata` will be carried in the log collected based on the collection rule and reported to the consumer. Pods with multiple values of the same key can be matched. For example, if you enter `environment = production,qa`, Pods with the `production` or `qa` value of the `environment` key will be matched. Separate values by comma. If `excludeLabels` is also specified, Pods in the intersection will be matched.
      excludeLabels:  					   	## Pods with the specified labels will be excluded. This field cannot be specified if `workload` is specified.
        key2: value2 							## Pods with multiple values of the same key can be matched. For example, if you enter `environment = production,qa`, Pods with the `production` or `qa` value of the `environment` key will be excluded. Separate multiple values by comma. If `includeLabels` is also specified, Pods in the intersection will be matched.
      metadataLabels:        		        	## The Pod labels to be collected as metadata. If this field is not specified, all Pod labels will be collected as metadata.
      - namespace
      metadataContainer:				     	## The container environments of the metadata to be collected. If this field is not specified, metadata (`namespace`, `pod_name`, `pod_ip`, `pod_uid`, `container_id`, `container_name`, and `image_name`) of all container environments will be collected.
      customLabels:   					   	## Custom metadata
        key: value
      workload:
    	container: xxx    	  			 	## The name of the container to be collected. If this field is not specified, all containers in the workload Pod will be collected.
        containerOperator: in                      ## Container selection method. Valid values: `in` (include); `not in` (exclude).
        kind: deployment  				   	## Workload type. Valid values: `deployment`, `daemonset`, `statefulset`, `job`, `cronjob`.
        name: sample-app  					   ## Workload name
        namespace: prod					  	## Workload namespace

    hostFile:                					## Node file path, which is valid only if `type` is `host_file`.
      filePattern: '*.log'   					## Log filename. Wildcards `*` and `?` are supported. `*` indicates to match any number of characters, while `?` indicates to match any single character.
      logPath: /tmp/logs     					## Log folder. Wildcards are not supported.
      customLabels:          					## Custom metadata
        label1: v1
```

### Log source configuration sample

<dx-tabs>
::: Standard container output [](id:pod_stdout)
Sample 1: collecting the standard output of all containers in the default namespace

```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: container_stdout
    containerStdout:
      namespace: default
      allContainers: true
 ...
```

Sample 2: collecting the container standard output in the Pod that belongs to ingress-gateway deployment in the production namespace
```
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: container_stdout
    containerStdout:
      allContainers: false
      workloads:
      - namespace: production
        name: ingress-gateway
        kind: deployment
  ...
```

Sample 3: collecting the container standard output in the Pod whose Pod labels contain "k8s-app=nginx" in the production namespace
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: container_stdout
    containerStdout:
      namespace: production
      allContainers: false
      includeLabels:
        k8s-app: nginx
  ...
```
:::
::: Container file [](id:pod_file)
Sample 1: collecting the `access.log` file in the `/data/nginx/log/` path in the NGINX container in the Pod that belongs to ingress-gateway deployment in the production namespace
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: container_file
    containerFile:
      namespace: production
      workload:
        name: ingress-gateway
        kind: deployment
      container: nginx
      logPath: /data/nginx/log
      filePattern: access.log
  ...
```

Sample 2: collecting the `access.log` file in the `/data/nginx/log/` path in the NGINX container in the Pod whose pod labels contain "k8s-app=ingress-gateway" in the production namespace
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: container_file
    containerFile:
      namespace: production
      includeLabels:
        k8s-app: ingress-gateway
      container: nginx
      logPath: /data/nginx/log
      filePattern: access.log
  ...
```
:::
::: Host file [](id:node_file)
Sample: collecting all `.log` files in the host path `/data/`
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
spec:
  inputDetail:
    type: host_file
    hostFile:
      logPath: /data
      filePattern: *.log
  ...
```
:::
:::
</dx-tabs>

### Step 3. Create a LogConfig object [](id:logconfig_create)

As the `LogConfig.yaml` declaration file is defined in [Step 2. Define the LogConfig object](#logconfig_def), you can run the kubectl command to create a LogConfig object based on the file.

```shell
kubectl create -f /usr/local/LogConfig.yaml
```
## Related Operations

After the deployment for cluster log collection is completed, you can go to [CLS console > Search and Analysis](https://console.cloud.tencent.com/cls/search) to view collected logs.

