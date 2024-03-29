﻿
- 包年包月预付费：云数据库 MySQL 申请退货退款，按照非全额退款处理。
- 按量计费后付费：云数据库 MySQL 直接清退资源，无法申请退款。
包年包月实例和按量计费实例均可在 [云数据库 MySQL 控制台](https://console.tencentcloud.com/cdb/instance?language=en) 的实例列表进行自助退货操作。

## 自助退还说明
- 包年包月实例自助退还后，实例的状态一旦变为隔离中时，就不再产生与该实例相关的费用。
- 实例彻底销毁后数据将无法找回，请提前备份实例数据。
- 实例彻底销毁后数据库备份将被删除，请提前下载数据库备份。
- 实例彻底销毁后数据库审计将被删除，请提前下载数据库审计日志。
- 包年包月实例彻底销毁后 IP 资源同时释放，实例无法访问。如果该实例有相关的只读或灾备实例：
  - 只读实例将同时被销毁。
  - 灾备实例将会断开同步连接，自动升级为主实例。
- 包年包月实例自助退还后，实例被移入云数据库回收站保留7天，此时实例无法访问。如您想恢复已经自助退还的包年包月实例，可以在云数据库回收站进行续费恢复。
- 如出现疑似异常/恶意退货，腾讯云有权拒绝您的退货申请。
- 某些活动资源不支持自助退还，具体以官网展示为准。

## 普通自助退还
普通自助退还将扣除您已使用的费用，退款金额将按购买支付使用的现金和赠送金支付比例退还至您的腾讯云账号。

#### 普通自助退还规则
**退款金额 = 当前有效订单金额 + 未开始订单金额 - 资源已使用价值**

- 当前有效订单金额：指生效中订单的付款金额，不包含折扣和代金券。
- 未开始订单金额：将来生效订单的付款金额，不包含代金券。
- 资源已使用价值按照如下策略计算：
 - 已使用部分，发起退费当天已满整月按整月扣除，不满整月则按量计费扣除。
 - 已使用部分精确到秒。
 - 退款金额 ≤ 0，按0计算并清退资源。

>!
>- 抵扣或代金券不予以退还。
>- 退还金额将按购买使用的现金和赠送金支付比例返还到您的腾讯云账户。

## 相关操作
如需在控制台自助退还按量计费和包年包月实例，请参见 [销毁实例](https://www.tencentcloud.com/document/product/236/31895?lang=en&pg=)。