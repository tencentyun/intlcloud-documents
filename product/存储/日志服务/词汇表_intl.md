## API Key

API key is the security credential used for authentication when a user accesses a Tencent Cloud API. An API key consists of SecretId and SecretKey. Multiple cloud API keys can be created under one user account. A user who does not have a cloud API key needs to create one by going to the [Cloud API Key Console](https://console.cloud.tencent.com/capi), otherwise he or she will be unable to call the cloud APIs.

- SecretId is used to identify the API caller.
- SecretKey is a key used for signature string encryption, and signature string verification by the server.

## Region

Region refers to the region where the CLS IDC resides. You can select the CLS region based on latency, cost and other factors. It is recommended to select the nearest region based on your business scenario.

## Server Group

Server group is a list of servers for which log collection is needed. A log topic can bind to multiple server groups, and a server group can also be bound to multiple log topics.

## Key-Value Index

Key-value index is another index type for retrieval analysis. The key-value index splits the original log into multiple key-value pairs, and a unique key name needs to be defined for each key-value pair. The query syntax for a key-value index is Key:Value.

## LogListener

LogListener is a proprietary collection Agent provided by CLS. The LogListener that is installed successfully can maintain a long-term heartbeat connection with CLS.

## Full-Text Index

Full-text index is an index type for query retrieval. The full-text index splits the original log into multiple word segments, which are the basis of log retrieval. You can input the keywords to make queries.


## Logset

Logset is a project management logic concept provided by CLS. A logset corresponds to a project.

## Log Topic

Log topic is the basic and the minimum management unit provided by CLS. Log collection, log indexing, and log shipping are all based on topics. A log topic corresponds to an application or a service, and a logset can contain multiple log topics.



