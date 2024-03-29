TRTC 通过应用的形式来管理不同的业务或项目。您可以在实时音视频控制台中给不同的业务或项目分别创建不同的应用，从而实现业务或项目数据的隔离。

## 注意事项
每个腾讯云账号最多可以创建100个 TRTC 应用。 

## 创建应用
1. 登录 [实时音视频控制台](https://console.cloud.tencent.com/trtc)，单击左侧栏【应用管理】。
![](https://main.qcloudimg.com/raw/ee125318641e0016ea0bae0d6951a2e3.png)
2. 单击上方的【创建应用】，根据实际业务需求填写应用名称和配置标签。
![](https://main.qcloudimg.com/raw/3d1853c6540a47f1b02de37dccf01f74.png)
> ? 仅支持填写数字、中英文和下划线，且不得超过15个字符。
3. 单击【确定】即可成功创建。


## 查看应用列表
应用创建成功后，相应的应用信息会在应用列表中进行展示，其中展示的信息包括 SDKAppID、应用名称、标签、服务状态及创建时间。
![](https://main.qcloudimg.com/raw/617da5aea2eaa92a75c043f8d1e3b1d3.png)

| 信息项  | 说明  |
| ---------------------- | ---------------------- |
| SDKAppID | 应用创建成功后自动生成的 SDKAppID，是应用的唯一标识，调用语音 API 接口时，需要提供该参数。 |
| 应用名称 | 创建应用时自定义的应用名称。 |
| 标签 | 在 [应用信息](https://intl.cloud.tencent.com/document/product/647/39079) 中设置的标签值。<br/>用于标识和组织您在腾讯云的各种资源。例如：企业可能有多个业务部门，每个部门有1个或多个 TRTC 应用，这时，企业可以通过给 TRTC 应用添加标签来标记部门信息。 |
| 服务状态 | 当前应用的服务状态情况，包括**正常**、**已停用**两种状态。<br/>当服务状态显示“已停用”时，若非主动操作，请检查 [套餐包余量](https://console.cloud.tencent.com/trtc/package) 是否为0、[腾讯云账户](https://console.cloud.tencent.com/expense/overview) 是否欠费。 |
| 创建时间 | 应用成功创建的时间。                                         |
| 操作 | 支持进行【用量统计】、【功能配置】及【应用信息】等操作。     |



## 相关文档
- 若需在应用列表中搜索相关应用，具体操作请参见 [搜索应用](https://intl.cloud.tencent.com/document/product/647/39078)。
- 若需查看应用的基本信息，具体操作请参见 [应用信息](https://intl.cloud.tencent.com/document/product/647/39079)。
- 若需配置或查看应用的功能配置信息，具体操作请参见 [功能配置](https://intl.cloud.tencent.com/document/product/647/39080)。
- 若需在云端混流转码时设置自定义背景图片，可在素材管理中添加对应的图片素材，具体操作请参见 [素材管理](https://intl.cloud.tencent.com/document/product/647/39081)。
- 若需快速跑通应用配套的 Demo 源码，具体操作请参见 [快速上手](https://intl.cloud.tencent.com/document/product/647/39082)。
