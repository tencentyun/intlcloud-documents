
云数据库 Redis 多可用区实例和单可用区实例的访问方式一致，均是提供一个 VIP 给到业务访问。

## 跨可用区访问
云数据库 Redis 提供的 VIP 在整个地域下都可以访问，在同一个地域下的不同可用区去访问相同的 VIP，您都能够访问到同一个 Redis 实例。

VIP 可以屏蔽 Redis 服务的故障切换，在 Redis 服务节点发生故障切换后，Redis 服务将在后台自动更新 VIP 关联的后端服务进程，业务无需更换 VIP。

## 查看实例 VIP
您可以登录 [Redis 控制台](https://console.cloud.tencent.com/redis)，在实例列表查看实例 VIP。
![](https://main.qcloudimg.com/raw/3d4787cf07be40f20ca35a050e5424e0.png)
或者单击实例 ID，进入实例详情页查看实例 VIP。
![](https://main.qcloudimg.com/raw/c470985bf8dc39e46f483849202901ba.png)

## 访问多可用区实例
访问方式请参见 [连接 Redis 实例](https://intl.cloud.tencent.com/document/product/239/9897)。
