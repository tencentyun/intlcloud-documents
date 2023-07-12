This document describes LogListener's capabilities and limits of file collection, configuration, resources, performance, and error handling related to data collection.

## File Collection Capabilities and Limits

| Item | Capability and Limit |
|---------|---------|
| File encoding | Supports UTF8 and GBK codec.</br>Note: only LogListener v2.6.2 and above support GBK codec. |
| Soft link | Supported. |
| Size of a single log | The size of a single-line log is limited to 512 KB. If the size of a single-line log exceeds 512 KB, the log will be truncated and only the first 512 KB is retained. For a multi-line log, after it is divided according to the first-line regular expression, the maximum limit for a single log is 1 MB. |
| Regular expression | Perl-compatible regular expressions are supported. |
| First log collection behavior | LogListener supports full/incremental collection policies:<ul  style="margin: 0;"><li>Full collection: after LogListener is started for the first time after installation, all logs that meet requirements are collected, including files that have not been written.</li><li>Incremental collection: after LogListener is started for the first time after installation, existing files will be collected from the latest position.</li></ul>**Note:** Full/Incremental collection policies are available starting from LogListener v2.6.2. |
| Log file rotation | Supported. (It is recommended that the file name after rotation not be matched by the wildcard collection path.) |
| Collection behavior when log parsing fails | We recommend you enable the feature of uploading parsing-failure logs. If the feature is enabled, parsing-failure logs will be uploaded to the preset index in the format of full text in a single line. Otherwise, the logs will be discarded. |
| File opening | LogListener opens files when reading files for log collection and closes the files when the reading is completed. |


## Checkpoint Management Capabilities and Limits

| Item | Capability and Limit |
|---------|---------|
| Checkpoint storage location | The default save path is the `data` directory in the LogListener installation directory. You can customize a save path in the `loglistener.conf` file. |
| Checkpoint storage policy | LogListener stores two copies of checkpoint metadata: <ul  style="margin: 0;"><li>One copy records the information only of checkpoints where upload is completed, and the information is persisted to a disk in real time.</li><li>The other copy records the information of checkpoints where upload is completed and checkpoints where upload is not completed, and the information is periodically persisted to a disk. Persistence takes precedence when the program exits. </li></ul>  |


## Resource and Performance Capabilities and Limits


| Item | Capability and Limit |
|---------|---------|
| Default CPU resource limits  | LogListener does not limit CPU resources by default. You can configure CPU resource limits in the configuration file.</br>Without CPU resource limits, the current implementation architecture of LogListener can achieve a maximum CPU usage of 110% (up to 100% for a single business thread and about 10% for a control thread).   |
| Default memory resource limits  | LogListener's default memory threshold is 2 GB. You can change the threshold to 300 MB or higher as needed.   |
| Default bandwidth resource limits  | LogListener does not limit bandwidth resources by default. You can configure bandwidth resource limits in the `loglistener.conf` file.   |
| Resource overrun handling policy  | If LogListener overruns CPU and memory resources for more than 5 minutes, LogListener will be forced to restart automatically.   |
| Log compression  | Collected logs are shipped as compact logs by default. You can modify log compression configuration in the `loglistener.conf` file.   |
| Number of monitored directories  | The recommended maximum number of monitored directories is 5,000. If this limit is exceeded, log collection may fail.   |
| Number of monitored files  | The recommended maximum number of monitored files is 10,000. If this limit is exceeded, log collection may fail.   |


## Error Handling

| Item | Capability and Limit |
|---------|---------|
| Network error handling  | Except exceptions requiring special handling (such as log topic deletion), all other errors (such as network exceptions, timeout, frequency control, and overdue payment) will be retried.   |
| Maximum retry timeout duration   | If data fails to be sent after retrying for more than 1 hour, the system discards the data.</br>The default behavior is to retry at an interval, and the retry interval becomes longer and longer until the maximum retry timeout duration is exceeded.   |
| Maximum number of retries  | The maximum number of retries can be set in the `loglistener.conf` configuration file and is not set by default. By default, the system retries until the maximum retry duration is exceeded, and then discards the data.</br>If the maximum number of retries is set, the system retries until the maximum number of retries is exceeded, and then discards the data.   |


## File Collection Rules

| Item | Capability and Limit |
|---------|---------|
| Log upload policy  |  LogListener automatically aggregates and uploads logs of the same file when any of the following aggregation conditions is met: 10,000 logs, the total logset size reaching 1 MB, or the log collection time exceeding 3 seconds. |
| File collection handling policy  | A single target file (a file that can be matched by the collection path) can be uploaded to only one log topic. The same file cannot be matched by the collection paths of multiple topics.</br>If you need to upload a file to multiple topics, use soft links. You can create different soft links for the same target file so that it can be collected to different topics via different soft links.   |
| Log collection delay  |  In the case of real-time collection, data collection, transmission, and storage to disks will be completed within 1 minute, and the logs are retrievable in the console.</br>If the log volume is large, or LogListener can use only a limited amount of resources, there will be some collection delay.  |


## Machine Group Related Rules

| Item | Capability and Limit |
|---------|---------|
| Machine group logic  | At present, machine groups are divided into the following two categories, and their usage methods are independent of and incompatible with each other. If the two usage methods are used together, LogListener will not be able to pull the correct collection configuration, resulting in no collection.<ol  style="margin: 0;"><li>IP machine group: a machine IP must be manually added to the machine group in the console, and the `group_label` field in `loglistener.conf` on the corresponding machine must be empty.</li><li>Label machine group: the machine group label is set in the console, and the `group_label` field in `loglistener.conf` on the corresponding machine must be set to the same label.</li></ol> |
| Relationships between machine groups and log topics  |  <ul  style="margin: 0;"><li>A single log topic can be bound to multiple machine groups.</li><li>A single machine group can be bound to multiple log topics.</li></ul>  |
| Relationships between machine groups and machines  |  <ul  style="margin: 0;"><li>A single machine can be added to multiple machine groups.</li><li>For an IP machine group, there is no limit to the number of machine groups that a machine can join.</li><li>For a label machine group, the maximum number of machine groups that a machine can join is 20.</li></ul>  |
| Limits on the labels of label machine groups  | <ul  style="margin: 0;"><li>Currently, the label of a label machine group can contain up to 32 characters.</li><li>Up to 20 labels can be configured for a single label machine group.</li></ul>  |



## Collection Path/Collection Blocklist Usage


| Item | Capability and Limit |
|---------|---------|
| Collection blocklist  | This feature is used to specify the content to ignore in the collection path. Currently, collection blocklists support two modes:<ul  style="margin: 0;"><li>FILE mode: specify the files to ignore in the collection path.</li><li>PATH mode: specify the subdirectories to ignore in the collection path. Wildcard filtering is supported.</li></ul>**Notes:**<ul  style="margin: 0;"><li>The FILE and PATH modes can be used together.</li><li>A collection blocklist is to exclude content from the collection path, and for both the FILE and PATH modes, the specified path to exclude must be a subset of the collection path.</li></ul>  |




