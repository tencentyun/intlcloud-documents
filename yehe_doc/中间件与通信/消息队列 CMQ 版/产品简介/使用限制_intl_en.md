This document lists the limits of certain metrics and performance in TDMQ for CMQ. Be careful not to exceed the limits during use so as to avoid exceptions.
<style>
table th:nth-of-type(1) {
width: 50%;        
}
</style>

### Queue

| Limit | Description | 
|---------|---------|
| Maximum number of queues per root account | 10,000 |
| Message lifecycle | 1 minute–15 days |
| Long polling wait time for message reception | 0–30 seconds
| Hidden duration of fetched message | 1 second–12 hours |
| Maximum message length | 1 MB |
| Maximum number of retained messages | 1 million–100 million per queue |
| Production QPS limit | 5,000 |
| Consumption QPS limit | 5,000 |
| Traffic limit | 400 Mbps |

### Topic

| Limit | Description | 
|---------|---------|
| Maximum number of topics per root account | 10,000 |
| Message lifecycle | 24 hours by default, which cannot be modified currently |
| Maximum message length | 1 MB |
| Message retention size | 100 GB |
| Production QPS limit | 5,000 |
| Consumption QPS limit | 5,000 |
| Traffic limit | 400 Mbps |

### Subscriber

| Limit | Description | 
|---------|---------|
| Maximum number of subscribers per topic | 1,000 |

>!If you need higher production QPS, consumption QPS, and traffic, you can [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to apply for increasing the upper limits.

