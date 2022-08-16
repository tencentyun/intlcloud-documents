By default, Tencent Cloud Mesh integrates Application Performance Management (APM) as the consumer end for call tracing. After the consumer end is enabled, Tencent Cloud Mesh will create an APM instance for you and report tracing data to the corresponding APM instance. On the Tencent Cloud Mesh console, you can view a complete call waterfall chart of a request in the mesh and tracing log information about calls at each layer, which can help you understand call dependencies of services and conduct latency analysis in the mesh. You can also view call data directly on the APM console.
In addition to APM, the mesh supports reporting the call data to the third-party Jaeger/Zpkin service. If the third-party tracing service is enabled, the Tencent Cloud Mesh console cannot display call tracing information, which needs to be viewed in the third-party service.

Call tracing data is collected and reported by sidecars, and the sidecars automatically generate trace spans. If you need to view the complete call trace information, you need to make few modifications on the service code to deliver the request context, so that Tencent Cloud Mesh can correctly associate the inbound and outbound spans to form a complete call trace. The headers that need to be delivered by the service include:

- x-request-id 
- x-b3-traceid 
- x-b3-spanid 
- x-b3-parentspanid 
- x-b3-sampled 
- x-b3-flags 
- x-ot-span-context 

For more information about Envoy-based tracing, see [Istio Distributed Tracing FAQ](https://istio.io/latest/faq/distributed-tracing/).

## Viewing Call Tracing

The procedure for viewing call tracing is as follows:

1. In the service list of the mesh, click the service whose call information needs to be focused on to enter the service details page.
![](https://qcloudimg.tencent-cloud.cn/raw/1ebfb534a3bfc951419f95d02e21897d.png)
2. On the service details page, click **Call trace**. You can view that the service is a callee, and view a list of called records and a statistical histogram of duration distribution of these records.
![](https://qcloudimg.tencent-cloud.cn/raw/66448bdc8b9bbe0df9356ed8bd199653.png)
3. Click the first column of the called record list to view a complete call trace waterfall chart related to the call. The first column records the URL of the call. The overview of the waterfall chart above can be zoomed through dragging.
![](https://qcloudimg.tencent-cloud.cn/raw/8fe5374211782f73fffca3c36e604395.png)
![](https://qcloudimg.tencent-cloud.cn/raw/2ebaa29d62627022bfa8218307501755.png)
4. Click the call whose details to be viewed. You can view the detailed tracing logs of the call.
![](https://qcloudimg.tencent-cloud.cn/raw/508448b4c3c1499cbff3ed0107e1f6f5.png)
5. Click the close button to close the span details page and return to the list of called records.
![](https://qcloudimg.tencent-cloud.cn/raw/a123555deb82a179abff52043c17cb21.png)
6. Tips for querying service's called records: You can filter the called records by duration, time span, source IP, trace ID, and return code. After filtering, you can sort the call records by **Latency** and **Start time**, so that you can easily choose the call you need to view.
![](https://qcloudimg.tencent-cloud.cn/raw/300692bd94c350159470cf9914d7719c.png)

## Configuring a Call Tracing Sampling Rate

A call tracing sampling rate is a sampling ratio of tracing data, and the resources consumed by sidecars during data collection and reporting are positively related to the bandwidth and sampling rate. Usually, in a production environment, it is not necessary to generate, collect, or report tracing data for all calls, so as to avoid excessive consumption of computing and bandwidth resources. Instead, only a certain proportion needs to be configured. It is recommended that a 100% sampling rate is configured for a development and test environment and a 1% sampling rate is configured for a production environment.

You can configure a sampling rate when creating a mesh.
![](https://qcloudimg.tencent-cloud.cn/raw/fb53d9ee7b9997b329a83c646b1e4e55.png)
Alternatively, you can modify sampling rate configurations on the basic information page of the mesh after the mesh is created.
![](https://qcloudimg.tencent-cloud.cn/raw/a0a893379ff38d874a4cbc2b10193462.png)
