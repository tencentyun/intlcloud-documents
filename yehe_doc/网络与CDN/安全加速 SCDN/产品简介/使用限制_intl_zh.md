## 接入安全加速

接入腾讯云 SCDN 的域名需要首先接入腾讯云 CDN/ECDN，且开通 SCDN 的服务地域，需要同时启动 CDN/ECDN 服务。使用 CDN 服务，接入域名的相关限制，请参考 [CDN 使用限制](https://intl.cloud.tencent.com/document/product/228/32981) 。

## 安全加速服务

| 类型         | 限制说明                                                     |
| ------------ | ------------------------------------------------------------ |
| 安全加速域名 | 安全加速套餐内含 20 个基础防护域名数量。如需增加上限，需购买域名扩展包，提升上限为120个。 安全加速域名，在 CDN 的对应服务区域的状态需要为“已启动”。如关闭对应区域 CDN 服务，安全加速服务也会关闭。 暂不支持泛域名接入。 |
| 数据统计     | 默认提供近 1 年的整体攻击数据查询，部分特别说明的数据项除外。 |
| 事件日志     | 支持查询近 7 天的攻击事件日志。 创建成功的日志下载任务保留 7 天。 单个任务最多支持下载 1000 条日志。 每日允许创建 100 个下载任务。 |