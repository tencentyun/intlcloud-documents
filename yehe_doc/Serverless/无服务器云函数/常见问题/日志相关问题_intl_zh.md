### 日志查询报错 “A query error has occurred”

通常是函数关联的日志主题索引配置异常，请参考 [日志投递配置](https://intl.cloud.tencent.com/document/product/583/39778#configuring-index) 调整索引配置后重试。

>! 
>- 日志索引配置生效时间一般有60s延时。
>- 索引配置更新后仅对新写入的数据生效。

### 日志查询报错 “server response timeout”

通常是函数关联的日志主题日志量过大引起的查询接口超时，请尝试缩短日志查询的时间范围后重试。

