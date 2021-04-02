You can write an SCF function to process the logs collected in the CLS service. By passing the collected logs as a parameter, the function can be invoked and the function code can process and analyze the data or dump it to other Tencent Cloud services.

Characteristics of CLS triggers:
- **Push model**: CLS monitors the specified log topic, aggregates data within a certain period of time, and invokes the associated function to push the event data to the function.
- **Async invocation**: a CLS trigger always invokes a function asynchronously, and the result is not returned to the invoker. For more information on invocation types, please see "Invocation Types" in [How It Works](https://intl.cloud.tencent.com/document/product/583/9694).

## CLS Trigger Attributes

- **Logset**: configure the CLS logset you want to connect to. It can only be a logset in the same region as the function.
- **Log topic**: configure the CLS log topic you want to connect to, which is the smallest unit for managing and configuring CLS triggers.
- **Maximum waiting time**: configure the longest waiting time for a single event pull.


## CLS Trigger Consumption and Message Delivery

After consuming messages, the CLS backend consumption module will encapsulate them into event structures according to the **max waiting time**, **delivery process**, and **message body size** and then initiate async function invocation. The applicable limits are as follows:
- **Maximum waiting time**: at present, the SCF backend consumption module requires this value to be between 3s and 300s to avoid an excessive latency before consumption. For example, if the maximum waiting time is set to 60s, the consumption template will aggregate log data once every 60s and deliver it to the function.
- **Event size limit for async invocation**: 128 KB. For more information, please see [Limits](https://intl.cloud.tencent.com/document/product/583/11637). If a message of the log topic is large (for example, if the message body size exceeds 128 KB after being compressed by the backend component within the maximum waiting time), then due to the limit of 128 KB for async invocation, the system will extract and deliver the message body of 128 KB after being compressed by gzip in sequence from the event structure passed to the function instead of using the data aggregated within the maximum waiting time.
- **Delivery process**: if a non-retriable error occurs during the delivery process, such as `AccessDeniedException` or `ResourceNotFoundException`, the CLS trigger will pause the transfer retry logic.

>?
>- In the message delivery process, the time aggregation may vary by combination; that is, the number of messages in each event structure ranges from **1 to the maximum waiting time**. If the configured maximum waiting time is too long, there may be cases where the aggregation time in an event structure will never reach the maximum aggregation time.
>- After the event content is obtained by the function, each message can be guaranteed for processing by loop handling, and it is not assumed that the message time passed each time is constant.


## Event Message Structure for CLS Trigger

When the specified CLS trigger receives a message, the CLS backend consumption module will consume the message and encapsulate it to asynchronously invoke your function. In order to ensure the efficiency of data transfer in a single triggering action, the value of the data field is a Base64-encoded Gzip document.

```
{
  "clslogs": {
    "data": "ewogICAgIm1lc3NhZ2VUeXBlIjogIkRBVEFfTUVTU0FHRSIsCiAgICAib3duZXIiOiAiMTIzNDU2Nzg5MDEyIiwKICAgICJsb2dHcm91cCI6I..."
  }
} 
```

After being decoded and decompressed, the log data will look like the following JSON body (using decoded CLS Logs message data as an example):
```
{
	"topic_id": "xxxx-xx-xx-xx-yyyyyyyy",
	"topic_name": "testname",
	"records": [{
		"timestamp": "1605578090000000",
		"content": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
	}, {
		"timestamp": "1605578090000000",
		"content": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
	}]
}
```

The data structures are as detailed below:

| Structure | Description |
| ---------- | --- |
| topic_id | Log topic ID |
| topic_name   | 	Log topic name |
| timestamp | Log production time (timestamp at the microsecond level) |
| content | Log content |
