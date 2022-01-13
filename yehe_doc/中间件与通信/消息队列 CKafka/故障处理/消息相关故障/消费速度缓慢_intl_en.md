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
![](https://main.qcloudimg.com/raw/ec2f08922533ab6d9128351b577a29ba.png)

- **Traffic throttling**
If you want to check whether it is caused by traffic throttling, you can configure an alarm for excessive bandwidth and then check whether the bandwidth peak of the instance has been reached in **Monitoring** > **Instance**; if so, you need to upgrade the bandwidth peak. For more information on how to upgrade the instance configuration, see [Upgrading Instance](https://intl.cloud.tencent.com/document/product/597/40650).
![](https://main.qcloudimg.com/raw/fd0f26d24abebd1b1f6673d15a28ab75.png)

- **Client load issue**
If the server doesn't have a performance issue, there is a high probability that the consumption capacity of the client is insufficient. First, take a look at the correspondence between partitions and consumers as shown below. If a consumer consumes too many partitions, we recommend you add more consumers, so that one consumer consumes one partition.
![](https://main.qcloudimg.com/raw/2e53984a61efc0a742e92867673d3c7a.jpg)

- **Consumer’s consumption capability**
If the assignment relationship between consumers and partitions is normal, you can add more partitions in the console to increase the concurrency of data consumption as shown below. Adding partitions in the console is instant and lossless, so your business won’t be affected.
<img src="https://main.qcloudimg.com/raw/c1a1544ce98d2a3a0c95adbb2195c755.png" width="600">

- **Network issue**
Check the client load metrics, such as the client CPU, memory size, and network interface. If it is a Java process, you should pay attention to GC and heap memory usage.
