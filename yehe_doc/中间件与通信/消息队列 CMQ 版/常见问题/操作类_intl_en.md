### What should I do if message deletion fails? 
The failure to delete the message may be because the message handle has timed out. The queue attribute `visibilityTimeout` indicates the visibility time of the message. If the time difference between message consumption and message deletion exceeds this time, the message handler will become invalid, making it impossible to delete the message. 

### What should I do if the `10250 qps throttling` exception occurs when I call TDMQ for CMQ? 
This exception occurs because the QPS reaches the upper limit. The default value of QPS is 5,000, indicating that up to 5,000 messages can be sent (published) per second. The number of consumed messages is 1.1 times that of produced messages by default. If you need a higher QPS, you can [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to apply for increasing the QPS upper limit.

### What should I do if the SDK I need is not provided?
If there is no SDK for your programming language, you can assemble packets to call TDMQ for CMQ according to the specifications in the official documentation.

### How do I make an API key only valid for APIs of TDMQ for CMQ?
An API key is a global key. Currently, TDMQ for CMQ has been connected to CAM, so you can use CAM for access control.

