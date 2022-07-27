This document lists the limits of certain metrics and performance in TDMQ for Pulsar. Be careful not to exceed the limits during use so as to avoid exceptions.

<style>
table th:nth-of-type(1) {
width: 50%;        
}
</style>

### Cluster

| Limit | Description |
| -------------------- | ----------------- |
| Maximum number of clusters per region | 5 |
| Maximum cluster name length | 128 characters |
| Maximum storage capacity | 100 GB |


### Namespace

| Limit | Description |
| ------------------------ | -------- |
| Maximum number of namespaces per cluster | 100 |


### Topic

| Limit | Description |
| -------------------------- | ----------------- |
| Maximum number of topics per cluster | 1,000 |
| Maximum number of topic partitions per cluster | 6,000 |
| Maximum number of partitions per topic        | 32                |
| Maximum topic name length | 128 characters |
| Maximum production TPS per topic partition | 5,000              |
| Maximum production bandwidth per topic partition  | 40 Mbps           |
| Maximum consumption TPS per topic partition | 5,000              |
| Maximum consumption bandwidth per topic partition  | 40 Mbps           |
| Maximum number of producers per topic | 1,000 |
| Maximum number of subscriptions per topic | 2,000 |
| Maximum number of consumers per topic | 2,000 |


### Message

| Limit | Description |
| ------------------------ | -------- |
| Maximum message retention period | 15 days |
| Maximum message delay | 10 days |
| Maximum message size | 5 MB |
| Consumption offset reset | 15 days |
| Maximum number of received but unacknowledged messages | 5,000 |
| Maximum number of messages per query | 65,536 |
