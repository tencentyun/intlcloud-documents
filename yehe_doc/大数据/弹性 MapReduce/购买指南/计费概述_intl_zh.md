## 计费模式
按量计费：集群的全部节点计费模式均为按量计费，节点类型详细介绍请参见 [节点类型说明](https://intl.cloud.tencent.com/document/product/1026/31094)。

购买弹性 MapReduce 集群时，集群单价按小时呈现，结算时按实际使用秒数计价，费用四舍五入，精确到小数点后2位；计费的起点以集群创建开始的时间点为准，终点以您发起销毁集群完成操作的时间点为准。 

购买按量计费集群时，会预先冻结当前配置使用2个小时的费用，并在每个整点（北京时间）进行一次结算，根据在上一个小时集群实际使用时长进行扣费。

按量计费节点配置调整时，购买时冻结的费用将解冻，并重新按最新配置的单价进行费用冻结，冻结均为2小时的费用。销毁按量计费集群时，系统会对冻结的费用进行解冻。


## 价格说明
EMR 提供的弹性计算集群能力，允许用户选择多种规格进行自定义组合。EMR 产品收取的费用由各集群中的全部节点构成。

北京、上海、广州、地域的节点价格如下：
>!
>1. 官网价格会根据情况做适当调整，具体价格请参考官网，此处不作为长期有效数据。
>2. 磁盘类型价格请参考 [云硬盘价格总览](https://intl.cloud.tencent.com/document/product/362/2413)。
>3. 以下价格仅为 CPU 内存的配置费用，不包含镜像、系统云盘、数据云盘以及带宽费用。
>4. 根据实际情况部分机型已售罄，具体可参见购买页机型列表。


###  第一阶梯按量计费（美元/小时）

| 机型                | CPU  | 内存（GB） | 北上广 |
| ------------------- | ---- | ---------- | ------ |
| 标准型S2            | 2    | 4          | 0.12   |
| 标准型S2            | 4    | 8          | 0.23   |
| 标准型S2            | 4    | 16         | 0.34   |
| 标准型S2            | 8    | 16         | 0.45   |
| 标准型S2            | 8    | 32         | 0.67   |
| 标准型S2            | 12   | 24         | 0.67   |
| 标准型S2            | 16   | 32         | 0.89   |
| 标准型S2            | 16   | 64         | 1.33   |
| 标准型S2            | 24   | 48         | 1.33   |
| 标准型S2            | 24   | 96         | 1.99   |
| 标准型S2            | 32   | 64         | 1.77   |
| 标准型S2            | 32   | 128        | 2.65   |
| 标准型S2            | 48   | 125        | 3.05   |
| 高IO型I2            | 8    | 16         | 0.45   |
| 高IO型I2            | 8    | 32         | 0.67   |
| 高IO型I2            | 12   | 24         | 0.67   |
| 高IO型I2            | 16   | 32         | 0.89   |
| 高IO型I2            | 16   | 64         | 1.33   |
| 高IO型I2            | 24   | 96         | 1.99   |
| 高IO型I2            | 32   | 64         | 1.77   |
| 高IO型I2            | 32   | 128        | 2.65   |
| 内存型M2            | 2    | 16         | 0.23   |
| 内存型M2            | 8    | 64         | 0.91   |
| 内存型M2            | 12   | 96         | 1.36   |
| 内存型M2            | 16   | 128        | 1.81   |
| 内存型M2            | 24   | 192        | 2.71   |
| 内存型M2            | 32   | 256        | 3.61   |
| 计算型C2            | 4    | 8          | 0.33   |
| 计算型C2            | 4    | 16         | 0.5    |
| 计算型C2            | 16   | 32         | 1.31   |
| 计算型C2            | 16   | 60         | 1.89   |
| 计算型C2            | 32   | 120        | 3.78   |
| 大数据型D1          | 8    | 32         | 0.72   |
| 大数据型D1          | 16   | 64         | 1.44   |
| 大数据型D1          | 24   | 96         | 2.16   |
| 大数据型D1          | 32   | 128        | 2.88   |
| 大数据型D1          | 56   | 224        | 5.03   |
| 大数据型D2          | 8    | 32         | 0.68   |
| 大数据型D2          | 16   | 64         | 1.36   |
| 大数据型D2          | 24   | 96         | 2.04   |
| 大数据型D2          | 32   | 128        | 2.72   |
| 大数据型D2          | 64   | 256        | 5.44   |
| 大数据型D2          | 76   | 320        | 6.68   |
| 内存型M4            | 2    | 4          | 0.11   |
| 内存型M4            | 4    | 32         | 0.46   |
| 内存型M4            | 8    | 64         | 0.91   |
| 内存型M4            | 12   | 96         | 1.36   |
| 内存型M4            | 12   | 144        | 1.85   |
| 内存型M4            | 16   | 128        | 1.81   |
| 内存型M4            | 16   | 192        | 2.47   |
| 内存型M4            | 32   | 256        | 3.61   |
| 内存型M4            | 32   | 384        | 4.94   |
| 内存型M4            | 64   | 512        | 7.22   |
| 内存型M4            | 72   | 648        | 8.86   |
| 标准型S3            | 2    | 4          | 0.12   |
| 标准型S3            | 2    | 8          | 0.17   |
| 标准型S3            | 4    | 8          | 0.23   |
| 标准型S3            | 4    | 16         | 0.34   |
| 标准型S3            | 8    | 16         | 0.45   |
| 标准型S3            | 8    | 32         | 0.67   |
| 标准型S3            | 16   | 32         | 0.89   |
| 标准型S3            | 16   | 64         | 1.33   |
| 标准型S3            | 24   | 48         | 1.33   |
| 标准型S3            | 24   | 96         | 1.99   |
| 标准型S3            | 32   | 64         | 1.77   |
| 标准型S3            | 32   | 128        | 2.65   |
| 标准型S3            | 48   | 96         | 2.65   |
| 标准型S3            | 48   | 192        | 3.98   |
| 标准型S3            | 64   | 128        | 3.54   |
| 标准型S3            | 64   | 256        | 5.3    |
| 高IO型I3            | 8    | 32         | 0.68   |
| 高IO型I3            | 16   | 64         | 1.35   |
| 高IO型I3            | 24   | 96         | 2.02   |
| 高IO型I3            | 32   | 128        | 2.69   |
| 高IO型I3            | 48   | 192        | 4.03   |
| 高IO型I3            | 64   | 256        | 5.38   |
| 高IO型I3            | 80   | 320        | 6.72   |
| 标准型S4            | 1    | 4          | 0.09   |
| 标准型S4            | 2    | 4          | 0.12   |
| 标准型S4            | 2    | 8          | 0.17   |
| 标准型S4            | 4    | 8          | 0.23   |
| 标准型S4            | 4    | 16         | 0.34   |
| 标准型S4            | 8    | 16         | 0.46   |
| 标准型S4            | 8    | 32         | 0.68   |
| 标准型S4            | 16   | 32         | 0.91   |
| 标准型S4            | 16   | 64         | 1.35   |
| 标准型S4            | 24   | 48         | 1.36   |
| 标准型S4            | 24   | 96         | 2.02   |
| 标准型S4            | 32   | 64         | 1.81   |
| 标准型S4            | 32   | 128        | 2.69   |
| 标准型S4            | 48   | 96         | 2.71   |
| 标准型S4            | 48   | 192        | 4.03   |
| 标准型S4            | 64   | 128        | 3.61   |
| 标准型S4            | 64   | 256        | 5.38   |
| 标准型S4            | 72   | 288        | 6.05   |
| 大数据型DS2         | 8    | 32         | 0.68   |
| 大数据型DS2         | 16   | 64         | 1.36   |
| 大数据型DS2         | 24   | 96         | 2.04   |
| 大数据型DS2         | 32   | 128        | 2.72   |
| 标准网络优化型SN3ne | 2    | 4          | 0.12   |
| 标准网络优化型SN3ne | 4    | 8          | 0.23   |
| 标准网络优化型SN3ne | 4    | 16         | 0.34   |
| 标准网络优化型SN3ne | 8    | 16         | 0.46   |
| 标准网络优化型SN3ne | 8    | 32         | 0.68   |
| 标准网络优化型SN3ne | 12   | 24         | 0.68   |
| 标准网络优化型SN3ne | 16   | 32         | 0.91   |
| 标准网络优化型SN3ne | 16   | 64         | 1.35   |
| 标准网络优化型SN3ne | 24   | 48         | 1.36   |
| 标准网络优化型SN3ne | 24   | 96         | 2.02   |
| 标准网络优化型SN3ne | 32   | 64         | 1.81   |
| 标准网络优化型SN3ne | 32   | 128        | 2.69   |
| 标准网络优化型SN3ne | 48   | 96         | 2.71   |
| 标准网络优化型SN3ne | 64   | 128        | 3.61   |
| 标准网络优化型SN3ne | 64   | 192        | 4.49   |
| 标准网络优化型SN3ne | 64   | 256        | 5.38   |
| 标准网络优化型SN3ne | 72   | 288        | 6.05   |
| 标准网络优化型SN3ne | 76   | 192        | 4.84   |
| 标准网络优化型SN3ne | 76   | 256        | 5.72   |
| 内存型M5            | 2    | 16         | 0.23   |
| 内存型M5            | 4    | 32         | 0.46   |
| 内存型M5            | 8    | 64         | 0.91   |
| 内存型M5            | 12   | 96         | 1.36   |
| 内存型M5            | 32   | 256        | 3.61   |
| 标准型S5            | 2    | 4          | 0.07   |
| 标准型S5            | 2    | 8          | 0.11   |
| 标准型S5            | 4    | 8          | 0.14   |
| 标准型S5            | 4    | 16         | 0.21   |
| 标准型S5            | 8    | 16         | 0.28   |
| 标准型S5            | 8    | 32         | 0.41   |
| 标准型S5            | 16   | 32         | 0.55   |
| 标准型S5            | 16   | 64         | 0.82   |
| 标准型S5            | 24   | 48         | 0.82   |
| 标准型S5            | 24   | 64         | 0.95   |
| 标准型S5            | 24   | 96         | 1.23   |
| 标准型S5            | 32   | 64         | 1.09   |
| 标准型S5            | 32   | 128        | 1.63   |
| 标准型S5            | 48   | 96         | 1.63   |
| 标准型S5            | 48   | 192        | 2.45   |
| 标准型S5            | 64   | 192        | 2.72   |
| 标准型S5            | 64   | 256        | 3.26   |
| 标准型S5            | 76   | 256        | 3.46   |
| 高IO型IT3           | 16   | 64         | 1.44   |
| 高IO型IT3           | 32   | 128        | 2.88   |
| 高IO型IT3           | 64   | 256        | 5.75   |
| 高IO型IT3           | 76   | 160        | 4.67   |
| 计算网络增强型CN3   | 4    | 8          | 0.28   |
| 计算网络增强型CN3   | 4    | 16         | 0.42   |
| 计算网络增强型CN3   | 8    | 16         | 0.56   |
| 计算网络增强型CN3   | 8    | 32         | 0.83   |
| 计算网络增强型CN3   | 16   | 32         | 1.11   |
| 计算网络增强型CN3   | 16   | 64         | 1.66   |
| 计算网络增强型CN3   | 32   | 64         | 2.21   |
| 计算网络增强型CN3   | 32   | 128        | 3.32   |
| 标准型SA2           | 2    | 4          | 0.14   |
| 标准型SA2           | 4    | 4          | 0.07   |
| 标准型SA2           | 4    | 8          | 0.09   |
| 标准型SA2           | 8    | 8          | 0.14   |
| 标准型SA2           | 8    | 16         | 0.18   |
| 标准型SA2           | 16   | 32         | 0.36   |
| 标准型SA2           | 16   | 64         | 0.53   |
| 标准型SA2           | 32   | 64         | 0.71   |
| 标准型SA2           | 64   | 128        | 1.41   |
| 标准型SA2           | 64   | 192        | 1.77   |
| 标准型SA2           | 80   | 160        | 1.77   |
| 标准型SA2           | 128  | 256        | 2.82   |
| 标准型SA2           | 160  | 320        | 3.53   |
| 计算型C3            | 4    | 8          | 0.35   |
| 计算型C3            | 4    | 16         | 0.52   |
| 计算型C3            | 8    | 16         | 0.69   |
| 计算型C3            | 8    | 32         | 1.04   |
| 计算型C3            | 16   | 32         | 1.38   |
| 计算型C3            | 16   | 64         | 2.08   |
| 计算型C3            | 32   | 64         | 2.76   |
| 计算型C3            | 32   | 128        | 4.16   |

使用 EMR 可能产生的其他费用项包括：网络流量、元数据存储和对象存储。

- **网络流量**
  集群的 Master.1 节点默认开启外网访问功能，以实现在集群外访问 Hadoop 众多组件的 WebUI 界面。流量费用即访问这些页面产生的数据交互流量费用，流量绝大多数情况都非常少。因此默认使用按流量计费的方案，相比按带宽付费更节约成本。
- **元数据存储**
  EMR（2.x 及以下版本）的 Hive 等元数据存储使用了腾讯云关系型数据 TencentDB，该部分费用包含在购买页中的费用总和。
- **对象存储**
  当您使用对象存储来实现集群的计算存储分离时，会因集群计算请求拉取对象存储中的数据，而产生数据存储和请求费用（可参见 [COS 产品定价](https://intl.cloud.tencent.com/document/product/436/6239)）。同时，在计算中，也可能因结果数据存放或者备份等目的，而在对象存储中产生新的数据。





