Tencent Cloud Mesh provides end-to-end observability between north-south and east-west services.

The collection of observation data depends on reporting of the [envoy sidecar proxy](https://www.envoyproxy.io) (data plane) of a service that has been injected with sidecars. You can flexibly control the production and calculation of observable data on the data plane through Tencent Cloud Mesh. Tencent Cloud Mesh integrates the observation data into suitable monitoring products to provide you with the observability of traffic between services at the edge of a mesh and services inside the mesh.

![](https://qcloudimg.tencent-cloud.cn/raw/6362fa7abea064f1ee2f6d5262b7f6ac.png)
Tencent Cloud Mesh provides three types of observable data:

| Type | Description |
|---	|---	|
| Metric | Metrics provide you with traffic observation data of services or gateways, and are suitable for developers of a single service to focus on. |
| Trace | Call tracing can link multi-layer calls of a service request into a call trace, which is convenient for you to observe the call structure, perform performance analysis, and locate exceptions. |
| Access log | Access logs completely record each request generation by the Envoy proxy, including information about the request layer and the sidecar proxy layer, which is convenient for operations personnel to conduct access auditing and fault troubleshooting. |

The three types of observable data are described as follows: 

| Observable Data | Recorded Information | Applicable Scenario or Role |
| ----- | ----- | ----- |
| Metric | Traffic observation data of a single service or gateway, including but not limited to metrics such as latency, number of requests, and request size. For more metric information, see [Istio Standard Metrics](https://istio.io/latest/docs/reference/config/metrics/). | Developers of a single service monitor the operating status of the service.  |
| Trace | Call dependencies between services. Compared with metric information, trace information further includes URL information. The recorded data is generally sampled. | Overall service developers perform call dependencies and performance analysis of all services. |
| Access log | Complete information about each request, including rich information output at the sidecar proxy layer. For more information, see [Envoy Access Logging](https://www.envoyproxy.io/docs/envoy/latest/configuration/observability/access_log/usage). | Mesh operations personnel conduct access auditing and fault troubleshooting. |



