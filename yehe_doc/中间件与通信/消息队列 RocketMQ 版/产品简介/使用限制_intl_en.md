This document lists the limits of certain metrics and performance in TDMQ for RocketMQ. Be careful not to exceed the limits during use so as to avoid exceptions.

<style>
table th:nth-of-type(1) {
width: 50%;        
}
</style>

### Cluster

| Limit | Description | 
|---------|---------|
| Maximum number of clusters per region | 5 |
| Cluster name length | 3–64 characters | 

### Namespace

| Limit | Description | 
|---------|---------|
| Maximum number of namespaces per cluster | 10 | 
| Maximum TPS per namespace | 8,000 |
| Maximum bandwidth (production + consumption) per namespace | 400 Mbps |
| Namespace name length | 3–64 characters |

### Topic

| Limit | Description | 
|---------|---------|
| Maximum number of topics per namespace | 1,000 |
| Topic name length | 3–64 characters |
| Maximum number of producers per topic | 1,000 |
| Maximum number of consumers per topic | 500 | 

### Group

| Limit | Description | 
|---------|---------|
| Maximum number of groups per namespace | 10,000 |
| Group name length | 3–64 characters |

### Message

| Limit | Description | 
|---------|---------|
| Maximum message retention period | 15 days |
| Maximum message delay | 40 days |
| Maximum message size | 5 MB |
| Consumption offset reset | 15 days |

