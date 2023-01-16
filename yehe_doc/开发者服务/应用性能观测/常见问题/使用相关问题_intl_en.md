
### How do I migrate from SkyWalking to APM?
APM is compatible with the SkyWalking protocol, so you only need to replace the reporting token and address of SkyWalking to start monitoring in APM.


### What should I do if no data is displayed in the application list and tracing server but the resource management section shows that Go application data is reported?
You need to configure the `span.kind` tag in the code and specify `server` or `client` in `Value`.
`span.kind` differentiates the server from the client, which is required when the topology is drawn. If it is not configured, the topology data in the application list will be empty.
![](https://main.qcloudimg.com/raw/ff6795585b9a1b19bf92dfc8e3f1c851.jpg)

### Why are some services grayed out in the APM topology when data is successfully reported?
From the service provider's perspective, a service will be grayed out if it is inactive, that is, it doesn't receive requests in the specified time range.

### Why is there only trace data but no metric data?
Most probably, it is due to the `span.kind`. APM scrapes `span.kind` of the **client**, **server**, **consumer**, and **producer** types only. Make sure that your `span.kind` is one of them.

### How does APM calculate the average error rate?
Average error rate = total number of error spans/total number of requests.
The average error rate is calculated by span. An error will be marked if any span is in the error status, which can be `error` or `status.code` in APM.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yNQ8010_2.png)

>? APM will support the custom calculation of errors in the future.

### What should I do if APM's private network address is unpingable during reporting over the private network?
1. Check whether the server and APM business system are in the same region.
2. Check whether the server address and port are pingable, and if not, submit a ticket for assistance.
