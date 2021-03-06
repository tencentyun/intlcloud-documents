
## 命名空间


Namespace=QCE/ECM

## 监控指标
>?拉取计算和网络监控指标数据时，Region 请统一选择“广州”地域。

| 指标英文名    | 指标中文名         | 指标含义                                                     | 单位 | 维度 |
| ------------- | ------------------ | ------------------------------------------------------------ | ---- | ---- |
| CpuUsage      | CPU 使用率         | CPU 利用率是通过 CVM 子机内部监控组件采集上报，数据更加精准     | %    | UUID |
| CpuLoadavg    | CPU 平均负载       | 1分钟内 CPU 平均负载，取 /proc/loadavg 第一列数据（Windows 操作系统无此指标），依赖 [监控组件](https://intl.cloud.tencent.com/document/product/248/6211) 采集 | -    | UUID |
| MemUsed       | 内存使用量         | 使用的内存量，不包括系统缓存和缓存区占用内存，依赖 [监控组件](https://intl.cloud.tencent.com/document/product/248/6211) 采集 | MB   | UUID |
| BaseCpuUsage  | 基础 CPU 使用率      | 基础 CPU 使用率通过宿主机采集上报，无须安装监控组件即可查看数据，子机高负载情况下仍可持续采集上报数据 | %    | UUID |
| MemUsage      | 内存利用率         | 用户实际使用的内存量与总内存量之比，不包括缓冲区与系统缓存占用的内存 | %    | UUID |
| LanOuttraffic | 内网出带宽         | 内网网卡的平均每秒出流量                                     | Mbps | UUID |
| LanIntraffic  | 内网入带宽         | 内网网卡的平均每秒入流量                                     | Mbps | UUID |
| LanOutpkg     | 内网出包量         | 内网网卡的平均每秒出包量                                     | 个/s | UUID |
| LanInpkg      | 内网入包量         | 内网网卡的平均每秒入包量                                     | 个/s | UUID |
| TcpCurrEstab  | TCP 连接数         | 处于 ESTABLISHED 状态的 TCP 连接数量，依赖监控组件安装采集   | 个   | UUID |
| WanOuttraffic | 外网出带宽         | 外网平均每秒出流量，最小粒度数据为，10秒总流量/10秒计算得出   | Mbps | UUID |
| WanIntraffic  | 外网入带宽         | 外网平均每秒入流量                                           | Mbps | UUID |
| WanOutpkg     | 外网出包量         | 外网平均每秒出包量                                           | 个/s | UUID |
| WanInpkg      | 外网入包量         | 外网平均每秒入包量                                           | 个/s | UUID |
| AccOuttraffic | 外网网卡每秒出流量 | 外网网卡的平均每秒出流量                                     | MB   | UUID |
|RegionIspIntraffic|地域 ISP 外网入口带宽|每个区域每个 ISP 外网使用入口带宽|Mbps|Region、ISP|
|RegionIspOuttraffic|地域 ISP 外网出口带宽|每个区域每个 ISP 外网使用出口带宽|Mbps|Region、ISP|


> ?每个指标的统计粒度（Period）可取值不一定相同，可通过DescribeBaseMetrics接口获取每个指标支持的统计粒度

## 各维度对应参数总览

| 参数名称                       | 维度名称 | 维度解释 | 格式                                                      |
| ------------------------------ | -------- | -------- | --------------------------------------------------------- |
| Instances.N.Dimensions.0.Name  | UUID     | 实例 UUID | 输入 String 类型维度名称：uuid                             |
| Instances.N.Dimensions.0.Value | UUID     | 实例 UUID | 输入具体 UUID，例如：4ef19d31-3117-455c-ae8e-2029a07d8999 |
| Instances.N.Dimensions.0.Name | Region | ECM 地域 | 输入 String 类型维度名称：Region|
| Instances.N.Dimensions.0.Value | Region | ECM 地域，可在 ECM 产品中使用 DescribeNode接口查询 Region 列表 | 输入 ECM 具体地域，例如：ap-zhengzhou-ecm |
| Instances.N.Dimensions.1.Name | ISP | 节点运营商 | 输入 String 类型维度名称：ISP |
| Instances.N.Dimensions.1.Value | ISP | 节点具体运营商，可在 ECM 产品中使用 DescribeNode接口查询 Region 支持的 ISP 列表 | 输入节点具体运营商，例如："CTCC"电信;"CUCC"联通;"CMCC"移动 |



## 入参说明

#### 1. 查询计算和网络监控数据，入参取值如下：
&Namespace=QCE/ECM
&Instances.N.Dimensions.0.Name=UUID
&Instances.N.Dimensions.0.Value=具体实例 UUID

#### 2. 查询地域 ISP 外网出、入口带宽指标监控数据，入参取值如下：
&Namespace=QCE/ECM
&Instances.N.Dimensions.0.Name=Region
&Instances.N.Dimensions.0.Value=ECM 具体地域
&Instances.N.Dimensions.1.Name=ISP
&Instances.N.Dimensions.1.Value=节点具体运营商
