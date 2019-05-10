## API Key

API key is a security credential for user authentication and access to Tencent Cloud API. An API key consists of SecretId and SecretKey. A user can create multiple cloud API keys by visiting [Cloud API Key Console](https://console.cloud.tencent.com/capi). Users must have API keys to call cloud APIs.

- SecretId is used to identify the API caller.
- SecretKey is a key used for signature string encryption, and signature string verification by the server.

## Region

Region refers to Cloud Log Service (CLS) IDC's region. Users can select CLS region based on latency, cost and other considerations. We recommend users choose the nearest region based on their business location and environment.

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

Log topic is the basic and the minimum management unit of CLS. A log topic corresponds to an application or a service. Log collection, indexing, and shipping are all based on topics. A logset can contain multiple log topics.



