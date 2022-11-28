This document lists the limits of certain metrics and performance in TDMQ for RocketMQ. Be careful not to exceed the limits during use to avoid exceptions.

<style>
table th:first-of-type {
    width: 50%;
}
table th:nth-of-type(2) {
    width: 10%;
}
table th:nth-of-type(3) {
    width: 40%;
}
</style>


### Cluster

| Limit Type             | Virtual Cluster | Exclusive Cluster |
| -------------------- | ------------ | ----------------- |
| Maximum number of clusters in a single region | 10         | Unlimited           |
| Cluster name length         | 3–64 characters   | 3–64 characters   |

### Namespace

| Limit Type                        | Virtual Cluster | Exclusive Cluster                    |
| ------------------------------- | ------------ | -------------------------------- |
| Maximum number of namespaces per cluster        | 10         | 10                             |
| Maximum TPS per namespace             | 4,000         | Over 4,000, depending on the node specification   |
| Maximum production and consumption bandwidth per namespace | 40 Mbps       | 80 Mbps, depending on the node specification                         |
| Namespace name length                | 3-64 characters   | 3-64 characters |

### Topic

| Limit Type                | Virtual Cluster | Exclusive Cluster |
| ----------------------- | ------------ | ------------ |
| Maximum number of topics per cluster | 150          | 200-500      |
| Topic name length          | 3-64 characters   | 3-64 characters   |
| Maximum number of producers per topic | 1,000         | 1,000         |
| Maximum number of consumers per topic | 500          | 500          |

### Group

| Limit Type                | Virtual Cluster | Exclusive Cluster |
| ----------------------- | ------------ | ------------ |
| Maximum number of groups per cluster | 1,500         | 2,000-5,000    |
| Group name length          | 3-64 characters   | 3-64 characters   |

### Message


| Limit Type         | Virtual Cluster | Exclusive Cluster |
| ---------------- | ------------ | ------------ |
| Maximum message retention period | 3 days          | 3 days          |
| Maximum message delay     | 40 days         | 40 days         |
| Message size         | 5 MB          | 5 MB          |
| Consumption offset reset     | 15 days         | 15 days         |

