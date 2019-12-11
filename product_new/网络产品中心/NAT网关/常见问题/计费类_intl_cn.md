
### NAT 网关如何计费？
NAT 网关服务费用包含以下部分：
- 网关费用（按小时计费）。
- 访问 Internet 产生的流量费用。

详情请参见 [计费概述](https://intl.cloud.tencent.com/document/product/1015/30248)。
有关私有网络的更多计费信息，详情请参见 [私有网络价格总览](https://intl.cloud.tencent.com/doc/product/215)。

### 用户创建的 NAT 网关没有使用为什么还会扣费？
由于 NAT 网关具备双机热备的特性，系统每 3 秒会分别给 NAT 网关的主备服务器发送一个 5 KB的探测包，因此每天会产生 0.2747 GB的流量。

### 路由表配置了某子网内通过 NAT 网关访问公网，但是该子网内的云服务器又配置了弹性 IP，这些云服务器是通过 NAT 网关还是弹性 IP 访问公网？
当路由表中存在多条路由规则时，路由优先级由高至低分别为：

- 私有网络内流量。
- 最精确路由。
- 公网 IP。

详情请参见 [路由规则优先级说明](https://intl.cloud.tencent.com/document/product/215/4954) 。
