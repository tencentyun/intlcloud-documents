## Overview
You can configure log collection in the console as instructed in [Collect container logs to CLS](https://intl.cloud.tencent.com/document/product/457/32419) or through CustomResourceDefinitions (CRDs). CRDs support collecting container standard output, container files, and host files in different formats and shipping them to CLS, CKafka, or other consumers.

## Prerequisites
You have enabled log collection in [**Ops Feature Management**](https://console.cloud.tencent.com/tke2/ops/list?rid=8) in the TKE console as instructed in [Collect container logs to CLS](https://www.tencentcloud.com/document/product/457/32419).


## CRD Overview

### Structure overview

```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig                 ## Default value
metadata:
  name: test					## CRD resource name, which is unique in the cluster.
spec:
  clsDetail:					## The configuration for shipping to CLS
    ...
  inputDetail:                  ## Data source configuration for collection
    ...
  kafkaDetail:					## The configuration for shipping to a CKafka or self-built Kafka cluster
    ...
status:							## CRD resource status
  status: ""
  code: ""						## The error code returned by the called API
  reason: ""					## Error cause
```


### clsDetail description

>! You cannot modify a specified topic.


```yaml
  clsDetail:
    ## A log topic is created automatically, and both the logset and topic names need to be specified.
    logsetName: test                    ## The name of the CLS logset. If there is no logset with this name, one will be created automatically. If there is such a logset, a log topic will be created under it.
    topicName: test                     ## The name of the CLS log topic. If there is no log topic with this name, one will be created automatically.
	
	# Select an existing logset and log topic. If the logset is specified but the log topic is not, a log topic will be created automatically.
    logsetId: xxxxxx-xx-xx-xx-xxxxxxxx  ## The ID of the CLS logset. The logset needs to be created in advance in CLS.
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx   ## The ID of the CLS log topic. The log topic needs to be created in advance in CLS and not occupied by other collection configurations.
	
    logType: json_log  ## Log collection format. Valid values: `json_log` (JSON); `delimiter_log` (delimited); `minimalist_log` (full text in a single line); `multiline_log` (full text in multiple lines); `fullregex_log` (full regular expression). Default value: `minimalist_log`.
	logFormat: xxx                      ## Log formatting method
	period: 30					        ## Lifecycle in days. Value range: 1–3600. `3640` indicates permanent storage.
	partitionCount:                     ## The number (an integer) of log topic partitions. Default value: `1`. Maximum value: `10`.
	tags:                             ## Tag description list. This parameter is used to bind a tag to a log topic. Up to nine tag key-value pairs are supported, and a resource can be bound to only one tag key.
	 - key: xxx							  ## Tag key
	 value: xxx                      ## Tag value
	autoSplit: false					## Whether to enable automatic split (Boolean type). Default value: `true`.
	maxSplitPartitions:
	storageType: hot.                  ## Log topic storage class. Valid values: `hot` (STANDARD); `cold` (STANDARD_IA). Default value: `hot`.
	excludePaths:                      ## Collection path blocklist
	  - type: File						  ## Type. Valid values: `File`, `Path`. 
	      value: /xx/xx/xx/xx.log         ## The value of `type`
	indexs: 							 ## You can customize the indexing method and field when creating a topic.
	  - indexName:   ## The field for which to configure the key value or meta field index. You don't need to add the `__TAG__.` prefix to the key of the meta field and can just use that of the corresponding field when uploading a log, as the `__TAG__.` prefix will be automatically added for display in the Tencent Cloud console.
	      indexType:  ## Field type. Valid values: `long`, `text`, `double`.
	      tokenizer:  ## Field delimiter. Each character represents a delimiter. Only English symbols and \n\t\r are supported. For `long` and `double` fields, leave it empty. For `text` fields, we recommend you use @&?|#()='",;:<>[]{}/ \n\t\r\ as the delimiter.
	      sqlFlag:   ## Whether the analysis feature is enabled for the field (Boolean)
	      containZH: ## Whether Chinese characters are contained (Boolean)
	region: ap-xxx                     ## Topic region for cross-region shipping
    userDefineRule: xxxxxx             ## Custom collection rule, which is a serialized JSON string
    extractRule: {}                    ## Extraction and filter rule. If `ExtractRule` is set, `LogType` must be set.
```

### inputDetail description
```yaml
  inputDetail:
    type: container_stdout                  ## Log collection type, including `container_stdout` (container standard output), `container_file` (container file), and `host_file` (host file).

    containerStdout:                        ## Container standard output
      namespace: default    ## The Kubernetes namespace of the container to be collected. Separate multiple namespaces by comma, for example, `default,namespace`. If this field is not specified, it indicates all namespaces. Note that this field cannot be specified if `excludeNamespace` is specified.
      excludeNamespace: nm1,nm2   ## The Kubernetes namespace of the container to be excluded. Separate multiple namespaces by comma, for example, `nm1,nm2`. If this field is not specified, it indicates all namespaces. Note that this field cannot be specified if `namespace` is specified.
	  nsLabelSelector: environment in (production),tier in (frontend) ## Filter namespaces by namespace label
      allContainers: false       ## Whether to collect the standard output of all containers in the specified namespace. Note that if `allContainers=true`, you cannot specify `workload`, `includeLabels`, and `excludeLabels` at the same time.
      container: xxx             ## The name of the container to be collected. If this field is empty, it indicates the names of all containers to be collected. 
      excludeLabels:  ## Pods with the specified labels will be excluded. This field cannot be specified if `workload`, `namespace`, and `excludeNamespace` are specified.
        key2: value2  ## Pods with multiple values of the same key can be matched. For example, if you enter `environment = production,qa`, Pods with the `production` or `qa` value of the `environment` key will be excluded. Separate multiple values by comma. If you also specify `includeLabels`, Pods in the intersection will be matched.

      includeLabels:  ## Pods with the specified labels will be collected. This field cannot be specified if `workload`, `namespace`, and `excludeNamespace` are specified.
        key: value1   ## The `metadata` will be carried in the log collected based on the collection rule and reported to the consumer. Pods with multiple values of the same key can be matched. For example, if you enter `environment = production,qa`, Pods with the `production` or `qa` value of the `environment` key will be matched. Separate multiple values by comma. If you also specify `excludeLabels`, Pods in the intersection will be matched.
		
      metadataLabels:            ## Specify the Pod labels to be collected as the metadata. If this field is not specified, all Pod labels will be collected as the metadata.
      - label1
      customLabels:              ## Custom metadata
        label: l1
	  
      workloads:
      - container: xxx    ## The name of the container to be collected. If this field is not specified, all containers in the workload Pod will be collected.
        kind: deployment  ## Workload type. Valid values: `deployment`, `daemonset`, `statefulset`, `job`, `cronjob`.
        name: sample-app  ## Workload name
        namespace: prod   ## Workload namespace
		
    containerFile:  ## Container file
      namespace: default      ## The Kubernetes namespace of the container to be collected. You must specify a namespace.	  
      excludeNamespace: nm1,nm2   ## The Kubernetes namespace of the container to be excluded. Separate multiple namespaces by comma, for example, `nm1,nm2`. If this field is not specified, it indicates all namespaces. Note that this field cannot be specified if `namespace` is specified.
      nsLabelSelector: environment in (production),tier in (frontend) ## Filter namespaces by namespace label
      container: xxx          ## The name of the container to be collected. If this field is empty, it indicates the names of all containers to be collected.
      logPath: /var/logs      ## Log folder. Wildcards are not supported.
      filePattern: app_*.log                ## Log filename. Wildcards `*` and `?` are supported. `*` indicates to match any number of characters, while `?` indicates to match any single character.
      customLabels:   ## Custom metadata
        key: value
      excludeLabels:  ## Pods with the specified labels will be excluded. This field cannot be specified if `workload` is specified.
        key2: value2  ## Pods with multiple values of the same key can be matched. For example, if you enter `environment = production,qa`, Pods with the `production` or `qa` value of the `environment` key will be excluded. Separate multiple values by comma. If you also specify `includeLabels`, Pods in the intersection will be matched.

      includeLabels:  ## Pods with the specified labels will be collected. This field cannot be specified if `workload` is specified.
        key: value1   ## The `metadata` will be carried in the log collected based on the collection rule and reported to the consumer. Pods with multiple values of the same key can be matched. For example, if you enter `environment = production,qa`, Pods with the `production` or `qa` value of the `environment` key will be matched. Separate multiple values by comma. If you also specify `excludeLabels`, Pods in the intersection will be matched.
      metadataLabels:            ## Specify the Pod labels to be collected as the metadata. If this field is not specified, all Pod labels will be collected as the metadata.
      - label1               ## Pod label
      workload:
        container: xxx    ## The name of the container to be collected. If this field is not specified, all containers in the workload Pod will be collected.
        name: sample-app  ## Workload name

    hostFile:                ## Node file path
      filePattern: '*.log'   ## Log filename. Wildcards `*` and `?` are supported. `*` indicates to match any number of characters, while `?` indicates to match any single character.
      logPath: /tmp/logs     ## Log folder. Wildcards are not supported.
      customLabels:   ## Custom metadata
        label1: v1
```

**extractRule description**

| Name | Type | Required | Description |
|---------|---------|---------|---------|
| timeKey | String | No | The key name of the time field. `time_key` and `time_format` must appear in pairs. |
| timeFormat | String | No | Time field format. For more information, see the output parameters of the time format description of the `strftime` function in C language. |
| delimiter | String | No | The delimiter for delimited logs, which is valid only if `log_type` is `delimiter_log`. |
| logRegex | String | No | Full log matching rule, which is valid only if `log_type` is `fullregex_log`. |
| beginningRegex	 | String | No | First-line matching rule, which is valid only if `log_type` is `multiline_log` or `fullregex_log`. |
| unMatchUpload | String | No | Whether to upload the logs failed to be parsed. Valid values: `true` (yes); `false` (no). |
| unMatchedKey | String | No | Unmatched log key. |
| backtracking | String | No | The size of the data to be rewound in incremental collection mode. Valid values: `-1` (full collection); `0` (incremental collection). Default value: `-1`. |
| keys | Array of String | No | The key name of each extracted field. An empty key indicates to discard the field. This parameter is valid only if `log_type` is `delimiter_log`. `json_log` logs use the key of JSON itself. |
| filterKeys | Array of String | No | Log keys to be filtered, which correspond to `FilterRegex` by subscript. |
| filterRegex | Array of String | No | The `regex` of the log keys to be filtered, which corresponds to `FilterKeys` by subscript. |
| isGBK | String | No | Whether it is GBK-encoded. Valid values: `0` (no); `1` (yes).<br>Note: This field may return null, indicating that no valid values can be obtained. |
| jsonStandard | String | No | Whether it is standard JSON. Valid values: `0` (no); `1` (yes).<br>Note: This field may return null, indicating that no valid values can be obtained. |


### kafkaDetail description
``` yaml
  kafkaDetail:
    brokers: x.x.x.x:p    ## (Required) The broker address. Generally, it is domain name:port. If there is more than one address, separate them by comma.
    topic: test		      ## 
    kafkaType: CKafka     ## Kafka type. Valid values: `CKafka` (CKafka); `SelfBuildKafka` (self-built Kafka).
    instanceId: xxxx      ## The ID of the CKafka instance when `kafkaType` is `CKafka`
	   logType: minimalist_log ## The type of the parsed Kafka log. Valid values: `minimalist_log` or `""` (full text in a single line); `multiline_log` (full text in multiple lines); `json` (JSON).
    timestampFormat: xxx   ## Timestamp format. Default value: `double`.
    timestampKey: xxx      ## Timestamp key. Default value: `@timestamp`.
	metadata:
	  formatType: default   ## Metadata format. Valid values: `default` (default, the same as the EKS Kafka collector); `filebeat` (Filebeat); `fluent-bit` (Fluent Bit).
    messageKey:            ## Specify a key to ship logs to the specified partition. This parameter is not enabled by default, and logs are shipped randomly. When it is enabled, logs with the same key will be shipped to the same partition. You can select the Pod field as the key. For example, if you enter a Pod name, select Field>metadata.name.
      value: Field        ## Topic ID, which is required
      valueFrom:
        fieldRef: 
          fieldPath: metadata.name ## If the key is `Field`, you can select `metadata.name`, `metadata.namespace`, `spec.nodeName`, and `spec.serviceAccountName`.
```



### status description

| status | Description |
|---------|---------|
| Empty | Initial status |
| Synced | Configured the collection successfully |
| Stale | Failed to configure the collection |


## Sample CRD
### Sample CRD for the configuration of the container standard output
<dx-tabs>
::: All containers
**Specify a namespace**

```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
metadata:
  name: "test"
spec:
  clsDetail:
    .......
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
  inputDetail:
    containerStdout:
      allContainers: true
      namespace: default,kube-public
    type: container_stdout

```

**Exclude a namespace**

```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
metadata:
  name: "test"
spec:
  clsDetail:
    ........
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
  inputDetail:
    containerStdout:
      allContainers: true
      excludeNamespace: kube-system,kube-node-lease
    type: container_stdout

```
:::
::: Specifying a workload
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
metadata:
  name: "test"
spec:
  clsDetail:
    ......
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
  inputDetail:
    containerStdout:
      allContainers: false
      workloads:
      - container: prod
        kind: deployment
        name: sample-app
        namespace: kube-system
    type: container_stdout
```

:::
::: Specifying Pod labels
``` yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
metadata:
  name: test
spec:
  clsDetail:
    ......
    topicId: xxxxxx-xx-xx-xx-xxxxxxxx
  inputDetail:
    containerStdout:
      container: prod
      excludeLabels:
        key2: v2
      includeLabels:
        key1: v1
      namespace: default,kube-system
    type: container_stdout
```
:::
</dx-tabs>


### Sample CRD for the configuration of the container file path
<dx-tabs>
::: Specifying a workload

```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
metadata:
  name: test
spec:
  clsDetail:
    .......
    topicId: xxxx-xx-xx-xx-xxxx
  inputDetail:
    containerFile:
      container: prod
      filePattern: '*.log'
      logPath: /tmp/logs
      namespace: kube-system
      workload:
        kind: deployment
        name: sample-app
    type: container_file
```
:::
::: Specifying Pod labels
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
metadata:
  name: test
spec:
  clsDetail:
    .......
    topicId: xxxx-xx-xx-xx-xxxx
  inputDetail:
    containerFile:
      container: prod
      filePattern: '*.log'
      includeLabels:
        key1: v1
      excludeLabels:
        key2: v2
      logPath: /tmp/logs
      namespace: default,kube-public
    type: container_file
```
:::
</dx-tabs>

### Sample CRD for the configuration of the node file path
```yaml
apiVersion: cls.cloud.tencent.com/v1
kind: LogConfig
metadata:
  creationTimestamp: "2022-03-13T12:48:49Z"
  generation: 4
  name: test
  resourceVersion: "11729531"
  selfLink: /apis/cls.cloud.tencent.com/v1/logconfigs/test
  uid: 233f4b72-cfef-4a43-abb8-e4d033185097
spec:
  clsDetail:
    .......
    topicId: xxxx-xx-xx-xx-xxxx
  inputDetail:
    hostFile:
      customLabels:
        testmetadata: v1
      filePattern: '*.log'
      logPath: /var/logs
    type: host_file
```
