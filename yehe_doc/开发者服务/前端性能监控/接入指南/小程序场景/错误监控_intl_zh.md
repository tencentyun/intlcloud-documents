
前端性能监控的 Aegis 的实例会自动进行 JS 执行错误、Promise执行错误、Ajax（Fetch）请求异常等监控。本文将为您介绍各错误监控逻辑及处理方式。

<dx-alert infotype="notice" title="">
 Aegis 实例会对这些异常进行监控，当您只是引入了 SDK 而没有将其实例化时，Aegis 将不会上报数据。
</dx-alert>

## JS 执行错误

Aegis 通过监听  `wx` 对象上的 `onerror` 事件来获取项目中的报错，并且通过解析错误和分析堆栈，将错误信息自动上报到后台服务中。该上报的上报等级为 error ，所以当自动上报的错误达到阈值时，Aegis 将会自动告警，帮助您尽早发现异常。由于上报等级为 error ，自动上报也将影响项目的评分。

## request 请求异常

Aegis 将会改写 `wx.request`(`qq.request`) ，之后监听每次接口请求，当 `statusCode` 不存在或者大于等于 400 时认为该请求是一个失败的请求，抑或是接口超时，abort 和其他类型的失败。

如果您的项目中使用了一些库也会重写 `wx.request`(`qq.request`)，如：`miniprogram-api-promise` 或者自己有封装，请一定确保在引入这个库之前完成对 Aegis 的初始化，否则将无法监听到接口失败的情况。

>!Aegis SDK 在错误发生的时候，不会主动收集接口请求参数和返回信息，如果需要对进口信息进行上报，可以使用 API 参数里面的 apiDetail 进行开启。

<dx-codeblock>
:::  js
new Aegis({
  api: {
    apiDetail: true,
  },
});
:::
</dx-codeblock>

## retcode异常

Aegis 在改写 `wx.request`(`qq.request`)，在获得 API 返回的内容，并尝试在内容中获取到本次请求的 `retcode`，当 `retcode` 不符合预期的时候，会认为本次请求出现了异常，并进行上报。

<dx-alert infotype="explain" title="">
如何获取 `retcode` 以及哪些`retcode` 是正常的可以在 [配置文档](https://intl.cloud.tencent.com/document/product/1131/44539) 中查看。
</dx-alert>
