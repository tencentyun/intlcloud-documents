本文将为您介绍异常登录的功能和操作。

## 概述
当检测到存在异常地域登录、异常用户名登录、异常登录时间、异常IP登录等可疑情况，主机安全将根据智能算法将登录记录标记为“可疑”或“高危”，系统会向您提供实时告警通知。

## 限制说明
- 已安装主机安全客户端的主机（客户端在线），均可使用异常登录功能。
- 主机安全控制台仅保留近6个月的异常登录事件，过期的事件数据将不再展示。

## 操作指南
1. 登录 [主机安全控制台](https://console.intl.cloud.tencent.com/cwp) 。
2. 单击左侧导航中的**入侵检测**>**异常登录**，各功能说明如下。

### 事件列表
在**事件列表**中，可查看并处理主机安全监测到的异常登录风险。
![](https://qcloudimg.tencent-cloud.cn/raw/2e913ad2862ac39f18b5611e1c0ed6f9.png)
字段说明：
- 服务器IP/名称：被异常登录的服务器。
- 来源 IP：登录来源 IP，一般是公司网络出口 IP 或网络代理 IP。
- 来源地：登录来源 IP 所在的地域。
- 登录用户名：成功登录服务器时使用的登录用户名。
- 登录时间：成功登录服务器的时间（服务器上的时区时间）。
- 危险等级：可疑/高危。
- 状态
  - 异常登录：本次登录存在异常地域、异常用户名、异常登录时间或异常IP登录。
  - 已加入白名单：登录来源已被添加为白名单（登录源 IP、登录用户名、登录时间及常用登录地）。
  - 已处理：用户已手动处理，并将该事件标记为已处理。
  - 已忽略：用户已忽略本次告警事件。
- 操作
  - 处理
    - 标记已处理：若您已人工对该风险事件进行处理，可将事件标记为已处理。
    - 加入白名单：加入白名单操作后，当再次发生相同事件时将不再进行告警，请谨慎操作。
    - 忽略：仅将本次告警事件进行忽略，若再有相同事件发生依然会进行告警。
    - 删除记录：删除该事件记录，控制台将不再显示，无法恢复记录，请慎重操作。

### 白名单管理
在**白名单管理**中，可增/删/改/查异常登录的白名单。
![](https://qcloudimg.tencent-cloud.cn/raw/0ebc346662503b301c1b2fce64c80613.png)
字段说明：
- 服务器IP/名称：该白名单生效的服务器。
- 来源IP：加白名单的来源IP。
- 常用登录地：加白名单的登录地。
- 登录用户名：加白名单的用户名。
- 登录时间：加白名单的时间。
- 创建时间：该白名单的创建时间。
- 修改时间：最近一次修改白名单的时间。
- 操作
   - 编辑：可重新编辑登录源ip、登录用户名、登录时间、常用登录地、生效范围等。
   - 删除：可对白名单进行删除操作。
