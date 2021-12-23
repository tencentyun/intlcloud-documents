This document lists the limits of certain metrics and performance in TDMQ for RabbitMQ. Be careful not to exceed the limits during use so as to avoid exceptions.

<style>
table th:nth-of-type(1) {
width: 50%;        
}
</style>



### Cluster
| Limit | Description | 
| --------------------------- | ---------- |
| Maximum number of clusters per region | 5 |
| Cluster name length | 3–64 characters |

### Vhost
| Limit | Description | 
| --------------------------- | ---------- |
| Vhost name length              | 3–64 characters    |
| Maximum TPS per vhost           | 8,000       |
| Maximum number of client connections per vhost | 8,000       |
| Maximum number of vhosts per cluster      | 10         |


### Exchange
| Limit | Description | 
| --------------------------- | ---------- |
| Exchange name length              | 3–64 characters    |
| Maximum number of exchanges per cluster | 1,000 |



### Queue
| Limit | Description | 
| --------------------------- | ---------- |
| Maximum number of queues per cluster | 1,000 |
| Queue name length              | 3–64 characters    |


### Message
| Limit | Description | 
| --------------------------- | ---------- |
| Maximum message retention period | 15 days |
| Maximum message delay | 40 days |
| Maximum message size | 5 MB |
| Consumption offset reset | 15 days |


### Channel
| Limit | Description | 
| --------------------------- | ---------- |
| Maximum number of channels per connection | 1,000 |

