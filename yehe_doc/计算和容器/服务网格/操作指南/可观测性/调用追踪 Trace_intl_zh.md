服务网格默认集成应用性能观测 APM 作为调用追踪消费端，开启后网格将会为您创建一个 APM 实例并将 tracing 数据上报到对应的 APM 实例，您可以在服务网格控制台查看到请求在网格内的完整调用瀑布图和每层调用的 trace 日志信息，帮助您理解服务的调用依赖，以及做网格内的延迟分析。您也可以直接在 APM 控制台查看调用相关数据。
除了 APM 之外，网格支持将调用数据上报到第三方 Jaeger/Zpkin 服务，如果开启使用第三方 tracing 服务，则服务网格控制台将无法展示调用追踪相关信息，需要在第三方服务中查看。

调用追踪数据通过 sidecar 收集上报，sidecar 会自动生成 trace span。如果您需要查看完整调用链信息，需要在业务代码中做少量改造，传递请求上下文，以便 TCM 可以正确关联入站和出站的 span，形成完整调用链路。需要业务传递的 headers 包括：

- x-request-id 
- x-b3-traceid 
- x-b3-spanid 
- x-b3-parentspanid 
- x-b3-sampled 
- x-b3-flags 
- x-ot-span-context 

更多关于 Envoy-based tracing 的信息，请参见 [Istio Distributed Tracing FAQ](https://istio.io/latest/faq/distributed-tracing/)。

## 查看调用追踪

查看调用追踪的流程如下：

1. 需要关注网格某个服务的调用情况，在网格的服务列表页面单击该服务，进入服务详情页面。
![](https://qcloudimg.tencent-cloud.cn/raw/1ebfb534a3bfc951419f95d02e21897d.png)
2. 在服务详情页面单击**调用追踪**，您可以查看到该服务作为被调方，被调用的记录列表，以及这些调用记录的耗时分布统计直方图。
![](https://qcloudimg.tencent-cloud.cn/raw/66448bdc8b9bbe0df9356ed8bd199653.png)
3. 被调记录列表第一列记录了调用的 URL，单击即可查看该调用相关的完整调用链路瀑布图，上方瀑布图概览可以拖拽实现缩放。
![](https://qcloudimg.tencent-cloud.cn/raw/8fe5374211782f73fffca3c36e604395.png)
![](https://qcloudimg.tencent-cloud.cn/raw/2ebaa29d62627022bfa8218307501755.png)
4. 单击想要查看详情的调用，可以查看对应调用环节的详细 trace 日志。
![](https://qcloudimg.tencent-cloud.cn/raw/508448b4c3c1499cbff3ed0107e1f6f5.png)
5. 单击关闭按钮可关闭 span 详情，以及返回服务被调记录列表页。
![](https://qcloudimg.tencent-cloud.cn/raw/a123555deb82a179abff52043c17cb21.png)
6. 查询服务被调记录 Tips：您可以按照耗时、时间跨度、源端IP、Trace ID、返回码过滤被调记录，过滤完成后您可以按照**延时**和**开始时间**对调用记录排序，方便您选择查看需要关注的调用。
![](https://qcloudimg.tencent-cloud.cn/raw/300692bd94c350159470cf9914d7719c.png)

## 配置调用追踪采样率

调用追踪采样率是 trace 数据的采样比例，sidecar 采集与上报数据消耗资源与带宽和采样率成正相关。通常生产环境下，不需要为所有调用都生成 trace 数据并采集上报，避免过多消耗计算资源与带宽资源，只需要配置一定比例即可。建议开发测试环境可以配置100%采样率，生产环境配置1%采样率。

您可以在网格创建时配置采样率，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/fb53d9ee7b9997b329a83c646b1e4e55.png)
也可以在网格创建后，在网格基本信息页面修改采样率配置。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/a0a893379ff38d874a4cbc2b10193462.png)
