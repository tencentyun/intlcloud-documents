CKafka 推出 Datahub 数据中心接入服务模块，负责从业务数据源获取数据，并进行一些预处理工作，分发给离线/在线处理平台，构建数据源和数据处理系统间的桥梁，将数据处理系统同业务侧的数据源解耦。

Datahub 支持接入各种数据源产生的不同类型的数据，统一管理，再分发给下游的离线/在线处理平台，构建清晰的数据通道。

## 数据源

DataHub 的数据源可以分为：主动上报、服务类和日志类。

- **主动上报类**：支持 HTTP 数据主动上报至 CKafka。详细操作参见 [主动上报](https://intl.cloud.tencent.com/document/product/597/46807)。
- **异步拉取-服务类：**支持 MongoDB，日志服务 CLS 和 DTS。
  - MongoDB：支持 MongoDB 数据接入 CKafka。详细操作参见 [MongoDB](https://intl.cloud.tencent.com/document/product/597/46810)。
  - 数据传输服务 DTS：支持 DTS 数据接入 CKafka。详细操作参见 [数据传输服务 DTS](https://intl.cloud.tencent.com/document/product/597/46811)。

> ?日志类数据源的数据接入在日志投递方的控制台进行操作，CKafka 控制台不进行展示。



## 数据接入

数据接入具体操作主要分为以下两个部分：

### 主动上报

提供 SDK，使用流程为：
![](https://qcloudimg.tencent-cloud.cn/raw/1e6792185d7c1f8bd135cd6df1e3965a.png)

### 异步拉取

服务类、日志类、接口类，提供完整的产品化配置界面，用户无需关心底层实现。
