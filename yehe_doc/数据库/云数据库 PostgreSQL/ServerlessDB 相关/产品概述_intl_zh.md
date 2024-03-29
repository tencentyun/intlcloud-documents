## 简介
PostgreSQL for Serverless（ServerlessDB）是一款基于 PostgreSQL 数据库实现的按需分配资源的数据库产品，其数据库将根据您的实际请求数来自动分配资源。

传统数据库实例需要根据业务实际使用情况手动调整数据库规格，而手动管理数据库容量需要占用宝贵的时间，也可能因为数据库资源的不饱和使用而造成浪费。
PostgreSQL for Serverless 仅需创建实例，即可正常使用，您无需关心数据库实例规格，仅需要在数据库处于活动状态期间按照实际用量进行付费，不需要为数据库的闲时进行付费。

>?PostgreSQL for Serverless 目前为免费公测阶段，可直接通过云 API 接口 [CreateServerlessDBInstance](https://intl.cloud.tencent.com/document/product/409/38880) 创建实例。

## 系统架构
用户连接数据库后，通过 PostgreSQL for Serverless Proxy 层统一进行请求转发，然后进行数据操作。当用户请求数增加时，数据库将自动响应。当前设定单用户最高支持 QPS 40000/s。
![](https://main.qcloudimg.com/raw/85f9c5aa5403f17f3d4d21f45690ce91.png)

## 产品特性
### 高可用
PostgreSQL for Serverless 支持一主一备高可用，当主实例出现意外导致不可用时，数据库将自动启动备用实例，此时业务连接将转移至备用实例当中，避免业务因意外情况而导致数据库无法使用。

### 自动备份
PostgreSQL for Serverless 会在每日凌晨1:00自动对数据库进行全量备份。每15分钟或者日志文件达到60个时，备份一次数据库日志，所有备份将保存7天。
备份功能于后台自动执行，当前并未开放备份查看下载与数据恢复功能。
