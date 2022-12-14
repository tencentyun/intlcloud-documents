云数据库 MySQL 上线了全新数据库代理版本，为了支持全新数据库代理版本的全部能力，腾讯云数据库团队提供了新的接口服务用于替换升级、配置数据库代理，您可参考以下列表替换升级新的接口服务。

## 变更时间
2022年11月17日（周四）起。

## 接口替换列表

| 下线接口 | 替换接口 | 接口功能 |
|---------|---------|---------|
| UpgradeCDBProxy | [AdjustCdbProxy](https://intl.cloud.tencent.com/document/product/236/45187) | 升级数据库代理配置 |
| ModifyCDBProxy | [AdjustCdbProxyAddress](https://intl.cloud.tencent.com/document/product/236/45194) | 配置数据库代理读写分离 |
