### What should I do if message consumption is slow?

**Error description**

Message consumption is slow.

**Possible causes**

High server load, traffic throttling, client load, insufficient consumer processing capacity, or network issues.

**Solution**

- If you want to check whether it is a server issue, you can view the consumption time in **Advanced Monitoring** in the console, which indicates the time it takes for the server to process requests. If there is a server load issue, the time values in the statistical periods are relatively high.

- If you want to check whether it is caused by traffic throttling, you can configure an alarm for excessive bandwidth and then check whether the bandwidth peak of the instance has been reached in **Monitoring** > **Instance**; if so, you need to upgrade the bandwidth peak. For more information on how to upgrade the instance configuration, please see [Upgrading Instance](https://intl.cloud.tencent.com/document/product/597/40650).
  ![](https://main.qcloudimg.com/raw/5e1f6110db1157e23cf1574b53775cab.png)

- If the server doesn't have a performance issue, there is a high probability that the consumption capacity of the client is insufficient. First, take a look at the correspondence between partitions and consumers as shown below. If a consumer consumes too many partitions, we recommend you add more consumers, so that one consumer consumes one partition.

  ![](https://main.qcloudimg.com/raw/5818999b8966e0182099b6fee34aa0da.png)

  If the assignment relationship between consumers and partitions is normal, you can add more partitions in the console to increase the concurrency of data consumption as shown below. Adding partitions in the console is instant and lossless, so you don't need to worry about any impact.

  <img src="https://main.qcloudimg.com/raw/390cec2a876e2f254fd95bb38bb6bb9c.png" width="600">

- You can also check the client load metrics, such as the client CPU, memory size, and network interface. If it is a Java process, you should pay attention to GC and heap memory usage.
