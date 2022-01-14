## Issue Description

Message consumption is slow.

## Possible Causes

- High server load
- Traffic throttling
- Client load issue
- Consumer’s consumption capability
- Network issue

## Solutions

- **High server load**
If you want to check whether it is a server issue, you can view the consumption time in **Advanced Monitoring** in the console, which indicates the time it takes for the server to process requests. If there is a server load issue, the time values in the statistical periods are relatively high as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/834c4f984f1a7967c09b06b27a222339.png)

- **Traffic throttling**
If you want to check whether it is caused by traffic throttling, you can configure an alarm for excessive bandwidth and then check whether the bandwidth peak of the instance has been reached in **Monitoring** > **Instance**; if so, you need to upgrade the bandwidth peak. For more information on how to upgrade the instance configuration, see [Upgrading Instance](https://intl.cloud.tencent.com/document/product/597/40650).

- **Client load issue**
If the server doesn't have a performance issue, there is a high probability that the consumption capacity of the client is insufficient. First, take a look at the correspondence between partitions and consumers as shown below. If a consumer consumes too many partitions, we recommend you add more consumers, so that one consumer consumes one partition.
![](https://qcloudimg.tencent-cloud.cn/raw/6ce8f40164c09c12cd9f9cc932c1730f.png)

- **Consumer’s consumption capability**
If the assignment relationship between consumers and partitions is normal, you can add more partitions in the console to increase the concurrency of data consumption as shown below. Adding partitions in the console is instant and lossless, so your business won’t be affected.
<img src="https://qcloudimg.tencent-cloud.cn/raw/ca5dee194de499929b6e2a2883ba445d.png" width="600">

- **Network issue**
Check the client load metrics, such as the client CPU, memory size, and network interface. If it is a Java process, you should pay attention to GC and heap memory usage.
