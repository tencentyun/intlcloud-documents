## Issue Description
The consumer cannot pull messages.

## Cause
Check whether the consumer group has a heap. If there is no heap, an empty message will be returned after the `fetch.max.wait` time elapses. This parameter is configured by the consumer client and 500 ms by default as shown below:
```
# Fetch request wait time.
fetch.max.wait.ms=500
```

![](https://qcloudimg.tencent-cloud.cn/raw/eb6f5565a35eff67ee44e7b64104be98.png)

## Solutions
- If messages heap up, but no messages are pulled, we recommend you check the client SDK version. If the SDK version is low, upgrade it as instructed in [SDK Overview](https://intl.cloud.tencent.com/document/product/597/41028).
- You can also [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance.





