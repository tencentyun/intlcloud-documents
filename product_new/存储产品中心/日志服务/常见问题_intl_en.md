### What is Cloud Log Service (CLS)?

CLS is an one-stop log data service platform provided by Tencent Cloud with the following features:

- Log collection: Supports multiple access methods like LogListener, API, etc.;
- Log storage: Stores and manages log data unifiedly;
- Search analysis: Provides log query and filtering features;
- Shipping consumption: Provides the log shipping/consumption features for further log data processing.
- CLS integrates seamlessly with various cloud products of Tencent Cloud.

### How does CLS define a log?

In CLS, a complete log contains mainly the log timestamp, the log content and the metadata:
- Log timestamp: The basic time attribute of logs
- Log content: Data content of key-value pairs
- Metadata: The basic meta information such as the log source IP address, log source file path, etc.

### How long can the log be kept?

CLS provides log lifecycle management. When you create a logset, you may assign an effective storing cycle for the log, beyond which the data is cleared without generating further storage cost. If you need to store for a longer time, please apply by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

In addition, data shipped to the COS (Cloud Object Storage) follows the lifecycle management of the destination bucket, and the charge rules also follow the billing rules of the COS.


### What are the main differences between a logset and a log topic?

CLS provides two levels of conceptual logic: logset and log topic. A logset contains multiple log topics, similar to a project containing multiple application services. Generally, the log format for each service is different. Therefore, a log topic is the smallest unit for configuration management like collection and search.


### What are the differences between the full-text index and the key-value index?

- Full-text index: Divides a complete log into multiple segments by delimiters, and then performs a keyword query based on the segments.
- Key-value index: Divides a complete log into multiple key-value pairs by format, and then performs a field query based on the key-value.


### Is CLS available for services not on Tencent Cloud?

Yes, it is. CLS does not restrict log sources. Logs are collected to CLS provided that the log source is reachable to our server through the network.


### Can LogListener upload data to multiple log topics?

LogListener can collect data for multiple intra-region log topics, but not for log topics in different regions.
