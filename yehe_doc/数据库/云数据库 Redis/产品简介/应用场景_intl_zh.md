

### 游戏场景
游戏场景中，可以将非角色数据，例如积分排行榜，存储在 Redis 中进行快速访问，Redis 原生自带的 SortedSet 数据类型能帮助您对玩家数据排序。
![](https://main.qcloudimg.com/raw/e76810228c64a3d085d999f4537162ee.svg)

### 互联网 App
互联网、App 应用产品中，可以将用户的基础资料缓存至 Redis 中，提高读写性能。同时也可以将静态的图片，资源缓存到 Redis 中，提高应用加载速度。
![](https://main.qcloudimg.com/raw/5ec0c42091bced4415a7d54b2b6d112d.svg)

### 电商展示场景
电商展示中，可以将商品展示、购物推荐等数据存储在 Redis 中进行快速访问，同时在大型促销秒杀活动中，Redis 达千万级的 QPS 能轻松应对高并发访问。
![](https://qcloudimg.tencent-cloud.cn/raw/6cd55d3dd73a1a8977b2266939e34f8c.png)
