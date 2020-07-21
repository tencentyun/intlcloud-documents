SCF uses concurrent instances (also called concurrences or instances) to process requests or events.

## Concurrence Overview
Currently, an SCF concurrent instance processes only one event at a time, and subsequent events or requests will not be received by the instance if it is still processing the current event and has not received the returned information. When the SCF platform receives sync/async requests and delivers them to a concurrent instance for processing, this logic always applies as detailed below:
- **Async request**: async events will first enter a queue on the SCF platform, where they will be processed in a FIFO manner. The system will select an appropriate concurrence processing method based on the conditions such as queue length and current number of concurrent instances of the function to pull sufficient concurrences and process the events in sequence.
- **Sync request**: after sync requests arrive at the SCF platform, the platform will check whether there are any idle concurrent instances, and if so, the events will be immediately sent to instances for processing; otherwise, the platform will start new concurrent instances to process them.


## Concurrence Limits
- Currently, the maximum total number of concurrent instances for a single function is 300, which means that a function can start up to 300 concurrent instances.
- The limit on the number of concurrent instances is shared by all versions of the function; for example, if 200 concurrent instances are being used by v1 of a function, v2 can start only 100 new concurrent instances.


## Concurrence Expansion
If the current number of concurrent instances of a function is insufficient to process request events, the SCF platform will start new ones to process them.

The maximum expansion speed of new concurrent instances in a region under one account is 500 instances/minute, that is, up to 500 new concurrent instances can be started in one minute. If the limit is reached in one minute, no more new instances will be started until the minute elapses, during which a limited expansion error will occur if new instance expansion requests are initiated.

## Concurrence Reuse
After a concurrent instance processes a request event, it will not be repossessed immediately; instead, it will be retained for a certain period of time. During the retention duration, if there are new request events that need to be processed, the retained concurrent instance will be used first, so the events can be processed quickly with no need to wait for start of new concurrent instances. The concurrent instance retention duration is dynamically adjusted by the SCF platform as needed; therefore, you cannot assume a certain retention duration when writing the function business code.


## Concurrence Monitoring

When a concurrent instance of a function is processing actual requests, it will be marked as running concurrent instance. In SCF monitoring information, you can query the running concurrent instances of a function, a specific function version, or an alias. As there are certain intervals in running instance information collection, if a function's execution time is very short and its number of concurrent instances is high, the current monitoring data may not be completely accurate.
