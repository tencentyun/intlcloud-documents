### 计费概述

预留实例计费（Reserved Instance Offering）是一种计费模式，是账户中按量计费实例所应用的一种折扣。按量计费必须在预留实例正常生命周期范围内且属性与预留实例完全匹配才能享受账单折扣。 预留实例相比按量计费模式价格更优惠。
>? 预留实例正在内测中，价格文档仅供参考，最终价格以账单为准。如有需要，请[联系商务](https://intl.cloud.tencent.com/contact-sales)。
>

> 预留实例计费目前不支持退款。
>
> 预留实例计费不支持调整配置，当与预留实例计费匹配的按量计费实例调整配置后，无法享受预留实例计费折扣。
>
> 当与预留实例计费相匹配的按量实例选择关机或强制关机后，该按量计费实例仍享受预留实例计费带来的折扣。


#### 上线时间

预留实例计费功能暂时处于白名单开放，请前往预留实例计费[内测申请](https://intl.cloud.tencent.com/apply/p/bvrqmrrp5ns)使用资格。 

#### 属性

- [地域](https://cloud.tencent.com/document/product/213/6091)：地域是指物理的数据中心的地理区域，例如硅谷
- [可用区](https://cloud.tencent.com/document/product/213/6091)：可用区（Zone）是指腾讯云在同一地域内电力和网络互相独立的物理数据中心，例如硅谷一区
- [实例类型](https://cloud.tencent.com/document/product/213/11518)：腾讯云提供多种实例类型，例如标准型
- [实例规格](https://cloud.tencent.com/document/product/213/11518)：预留实例计费机型规格，例如S4.SMALL1 
- 操作系统：Linux

> 按量计费必须在预留实例计费正常生命周期范围内且属性与预留实例完全匹配才能享受账单折扣。

#### 概念对比

| 对比项   | 预留实例计费      | 按量计费实例         |
| -------- | ---------- | ---------- |
| 形式     | 一种计费模式，一种按量实例的折扣。       | 以[按量计费](https://intl.cloud.tencent.com/document/product/213/2179)方式购买的实例，等同于一台实际运行的虚拟机。 |
| 使用方式 | 无法单独使用，需要匹配按量付费实例，抵扣按量付费实例账单。 | 可以独立管理、配置，既可以用作简单的Web服务器，也可以与其他腾讯云产品搭配提供强大的解决方案。 |

#### 使用限制

目前预留实例计费支持可购买的可用区以及实例规格请在API[列出可购买的预留实例计费](https://intl.cloud.tencent.com/document/product/213/30575)中查看

操作系统：目前腾讯云仅支持Linux操作系统预留实例计费

付款方式：提供全预付、部分预付、零预付三种付款方式

有效期限：1年(365天)

配额：每个用户在每个可用区最多可以持有20台预留实例计费
