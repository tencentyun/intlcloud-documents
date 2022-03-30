云数据库 PostgreSQL 支持内网地址和外网地址两种地址类型，默认提供内网地址供您内部访问实例，如果需要外网访问，您可通过控制台开启外网地址。

>?
>
>- 当前北京、上海、广州、成都地域支持外网安全组功能，支持通过控制台开启外网地址。

## 通过控制台开启外网地址
1. 登录 [PostgreSQL 控制台](https://console.cloud.tencent.com/postgres)，选择地域，在实例列表，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
3. 在**实例详情**页的**基本信息** > **外网IPv4地址**后，单击**开启**。
![](https://qcloudimg.tencent-cloud.cn/raw/a43ee5972d95fce9c3369cf714f15028.png)
4. 在弹出的对话框，阅读注意事项后，单击**确定**。
5. 待实例状态更新为**运行中**，即可在实例详情页查看外网地址。

>

### 配置 PodtgreSQL 安全组
1. 登录 [PodtgreSQL 控制台](https://console.cloud.tencent.com/postgres)，选择地域，在实例列表，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。

2. 在实例管理页面，选择**安全组**页，单击**配置安全组**，配置安全组规则为放通全部端口，确认安全组允许外部 IP 访问，详细配置方法请参见 [管理安全组](https://intl.cloud.tencent.com/document/product/409/40112)。

  ![](https://qcloudimg.tencent-cloud.cn/raw/5d34fb75a326af1e882f29c1fc967987.png)
  ![](https://qcloudimg.tencent-cloud.cn/raw/789e573631f0eb9806f6e755c6400520.png)

### 验证外网连通性
通过任意外网客户端工具访问 PodtgreSQL。具体操作方法可参考 [连接 PostgreSQL 实例](https://intl.cloud.tencent.com/document/product/409/34626)。


