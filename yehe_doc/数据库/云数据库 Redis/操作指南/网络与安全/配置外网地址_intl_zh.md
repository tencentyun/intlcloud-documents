本文为您介绍如何通过 Redis 控制台，手动开启或关闭外网地址，来实现外网访问 Redis 实例，用户使用系统分配的域名和端口，即可 [通过外网访问云数据库 Redis](https://intl.cloud.tencent.com/document/product/239/47571)。开启外网后，可方便日常测试和管理，提升用户开发和使用的便利性。

>?
>- 外网访问出现的故障，不会计入 Redis 服务的整体可用性计算。
>- 云数据库 Redis 外网访问会降低实例的安全性，仅推荐用于管理、测试或辅助管理数据库，不提供可用性 SLA 保证，业务访问请使用内网访问。
>

## 注意事项
1. 启用后，您可以使用系统分配的域名和端口通过外网访问腾讯云数据库 Redis，生效时间大概需要5分钟。
2. 外网访问仅用于开发或辅助管理数据库，业务访问请使用内网访问。
3. 外网访问开通后将受到安全组网络访问策略的控制，请在安全组入站规则中配置访问数据库的来源信息，并放通协议端口（需同时放开内网和外网端口，内网端口默认为6379）。具体操作，请参见 [Redis 安全组配置](https://intl.cloud.tencent.com/document/product/239/31945)。
4. 外网访问的出现故障，不会计入 Redis 服务的整体可用性计算。

## 前提条件
- 仅支持私有网络 VPC 的实例开通外网地址功能。如果为基础网络，请先 [切换基础网络为私有网络](https://intl.cloud.tencent.com/document/product/239/31944)，再开启外网访问。
- 目前仅以下地域暂支持外网地址功能：成都、北京、上海、广州。其他地域如需外网访问，可通过 [iptable 转发](https://intl.cloud.tencent.com/document/product/239/9897) 的方式来实现外网访问 Redis 实例。
- 开通外网地址功能需关闭 [免密码访问](https://intl.cloud.tencent.com/document/product/239/32548)。

## 开启外网地址
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，单击实例 ID，进入实例详情页。
2. 在实例详情页右侧的**网络信息**模块中，单击**外网地址**处的**开启**。
>!外网访问开通后将受到安全组网络访问策略的控制，请在安全组入站规则中配置访问数据库的来源信息，并放通协议端口（需同时放开内网和外网端口，内网端口默认为6379）。具体操作，请参见 [Redis 安全组配置](https://intl.cloud.tencent.com/document/product/239/31945)。
>
![](https://qcloudimg.tencent-cloud.cn/raw/e321411f59c98cb56089da38f5daec81.png)
3. 在弹出的对话框，确认无误后，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/68286671abbbff9a56a73b7890b7b9bf.png)
4. 返回实例详情页，实例状态变为**开通外网中**，表示实例正在开启外网地址。若实例状态长时间不改变，请重新刷新网页。
5. 当**外网地址**处显示包含域名和端口的外网地址，表明成功开启外网地址，使用外网可正常访问 Redis 数据库。
![](https://qcloudimg.tencent-cloud.cn/raw/0e7954a9edb62be93308250c125c8387.png)

## 关闭外网地址
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表，单击实例 ID，进入实例详情页。
2. 在实例详情页右侧的**网络信息**模块中，单击**外网地址**处的**关闭**。
![](https://qcloudimg.tencent-cloud.cn/raw/c4e569e1f967c6da605fe8e5a4206a1a.png)
3. 在弹出的对话框，确认无误后，单击**确定**。
4. 返回实例详情页，实例状态变为**外网关闭中**，**外网地址**处不再显示外网地址，外网功能即关闭。

## 相关 API

| API接口 | 说明 |
|---------|---------|
| [AllocateWanAddress](https://intl.cloud.tencent.com/document/product/239/46976) | 开通外网接口 |
| [ReleaseWanAddress](https://intl.cloud.tencent.com/document/product/239/46975) | 关闭外网接口 |

