## 前提条件
BOT 流量管理需要购买 WAF [对应实例的增值服务](https://intl.cloud.tencent.com/document/product/627/47799)。

## 操作步骤
1. 登录 [Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/tea-botconfig)，在左侧导航栏中，选择**配置中心** > **BOT 与业务安全**，进入 BOT 与业务安全页面。
2. 在 BOT 与业务安全页面，左上角选择需要防护的域名，单击 BOT 管理规则的![](https://qcloudimg.tencent-cloud.cn/raw/0b613028c41243c1b53951862a3284e9.png)，即可开启 BOT 流量分析。
![](https://qcloudimg.tencent-cloud.cn/raw/bb5032ca5dcbbfaa400a5a44bc8d9d3f.png)
**字段说明**
 - **BOT 管理规则开关**： 默认关闭，可根据需要开启。
>?当且仅当域名 WAF 开关开启时，BOT 流量分析功能生效。

 - **生效场景**：展示当前域名下，开启了多少个 BOT 分析的场景模块，BOT场景中包含：前端对抗、威胁情报、AI 模型、智能统计等。
 - **场景总数**：展示当前域名下，存在多少个 BOT 分析的场景模块。
 - **当前全局场景**：展示当前域名下，生效的全局场景名称
 - **自定义总数规则**： 展示当前开启了多少个 BOT 的自定义规则。