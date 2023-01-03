This document lists the limits of certain metrics and performance in different TDMQ for Pulsar cluster types. Be careful not to exceed the limits during use to avoid exceptions.

<style>
table th:nth-of-type(1) {
width: 50%;        
}
</style>

### Cluster

| Limit | Virtual Cluster | Pro Cluster |
| -------------------- | ----------------- | ----------------- |
| Maximum number of clusters in a single region | 5         | Unlimited           |
| Maximum cluster name length | 128 characters | 128 characters |
| Maximum storage capacity | 100 GB | 20 TB |


### Namespace

| Limit | Virtual Cluster | Pro Cluster |
| ------------------------ | -------- | -------- |
| Maximum number of namespaces per cluster | 100 | Subject to the cluster specification |


### Topic

| Limit | Virtual Cluster | Pro Cluster |
| -------------------------- | ----------------- | ----------------- |
| Maximum number of topics per cluster | 1,000 | Subject to the cluster specification |
| Maximum number of topic partitions per cluster | 6,000 | 6,000 |
| Maximum number of partitions per topic        | 32                | 32 |
| Maximum topic name length | 128 characters | 128 characters |
| Maximum production TPS per topic partition | 5,000              | Subject to the cluster specification |
| Maximum production bandwidth per topic partition  | 40 Mbps           | Subject to the cluster specification |
| Maximum consumption TPS per topic partition | 5,000              | Subject to the cluster specification |
| Maximum consumption bandwidth per topic partition  | 40 Mbps           | Subject to the cluster specification |
| Maximum number of producers per topic | 1,000 | 1,000 |
| Maximum number of subscriptions per topic | 2,000 | 2,000 |
| Maximum number of consumers per topic | 2,000 | 2,000 |


### Message

| Limit | Virtual Cluster | Pro Cluster |
| ------------------------ | -------- | -------- |
| Maximum message retention period | 15 days          | 15 days          |
| Maximum message delay     | 10 days         | 10 days         |
| Maximum message size | 5 MB | 5 MB |
| Consumption offset reset     | 15 days         | 15 days         |
| Maximum number of received but unacknowledged messages | 5,000 | Subject to the cluster specification |
| Maximum number of messages per query | 65,536 | 65,536 |
