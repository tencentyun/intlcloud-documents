This document lists the limits of certain metrics and performance in TDMQ for Pulsar. Be careful not to exceed the limits during use so as to avoid exceptions.

<style>
table th:nth-of-type(1) {
width: 50%;        
}
</style>


### Cluster

| Limit | Description |
| -------------------- | ---------------- |
| Maximum number of clusters per region | 5 |
| Maximum cluster name length | 64 characters |
| Maximum storage capacity | 100 GB |


### Namespace

| Limit | Description |
| ------------------------------- | -------- |
| Maximum number of namespaces per cluster | 100 |
| Maximum TPS per namespace | 10,000 |
| Maximum bandwidth (production + consumption) per namespace | 400 Mbps |


### Topic

| Limit | Description |
| --------------------------- | ---------------- |
| Maximum number of topics per cluster | 1,000 |
| Maximum topic name length | 64 characters |
| Maximum number of producers per topic | 1,000 |
| Maximum number of consumers per topic | 500 |


### Message

| Limit | Description |
| ------------------------ | -------- |
| Maximum message retention period | 15 days |
| Maximum message delay | 10 days |
| Maximum message size | 5 MB |
| Consumption offset reset | 15 days |
| Maximum number of received but unacknowledged messages | 5,000 |
| Maximum number of messages per query | 65,536 |
