## Issue Description

There are always heaped messages in some partitions as displayed on the monitoring page.

## Possible Causes

- The producer keeps producing messages to the partition while the consumer never consumes these messages.
- There are insufficient consumers in the consumer group or the consumption speed is too slow.
- The consumer does not consume messages in certain partitions due to bugs.

## Solutions


- **The producer keeps producing messages to the partition while the consumer never consumes these messages**
You can restart the client if messages in some partitions are not consumed. If the problem persists, you can either check the client logs first or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

- **There are insufficient consumers in the consumer group or the consumption speed is too slow**
Try increasing the number of consumers to improve consumption speed.

- **The consumer does not consume messages in certain partitions due to bugs**
Check the local logs of the consumer to see whether exceptions exist.





