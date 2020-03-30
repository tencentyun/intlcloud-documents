## 1. 接口描述

接口：GetMonitorData

接口请求域名： monitor.tencentcloudapi.com

获取云产品的监控数据。传入产品的命名空间、对象维度描述和监控指标即可获得相应的监控数据。 

接口调用频率限制为：20次/秒，1200次/分钟。 单请求最多可支持批量拉取10个实例的监控数据，单请求的数据点数限制为1440个。

若您需要调用的指标、对象较多，可能存在因限频出现拉取失败的情况，建议尽量将请求按时间维度均摊。

查询云服务器监控数据，入参取值如下：

&Namespace=QCE/CVM

&Instances.N.Dimensions.0.Name=InstanceId

&Instances.N.Dimensions.0.Value=云服务器的具体ID


## 2. 输入参数

以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见[公共请求参数](https://intl.cloud.tencent.com/document/api/248/4478)页面。

### 2.1输入参数

| 参数名称 | 是否必选 | 类型 | 描述 |
| ----------- | ---- | ---------------------------------------- | ---------------------------------------- |
| Action | 是 | String | 公共参数，本接口取值：GetMonitorData |
| Version | 是 | String | 公共参数，本接口取值： 2018-07-24 |
| Region | 否 | String | 公共参数，表示查询的是哪个地域实例的监控数据；支持的地域可查看云服务器支持的[地域列表](https://intl.cloud.tencent.com/document/api/213/15692) |
| Namespace | 是 | String | 命名空间，每个云产品会有一个命名空间,如：QCE/CVM |
| MetricName | 是 | String | 指标名称，具体名称见2.2 |
| Instances.N | 是 | Array of [Instance](https://intl.cloud.tencent.com/document/product/248/33883) | 实例对象的维度组合 |
| Period | 否 | Integer | 监控统计周期。默认为取值为300，单位为s |
| StartTime | 否 | Timestamp | 起始时间，如"2016-01-01 10:25:00"。 默认时间为当天的”00:00:00” |
| EndTime | 否 | Timestamp | 结束时间，默认为当前时间。 EndTime不能小于StartTime |

### 2.2 指标名称

每个指标的统计粒度（Period）可取值不一定相同，可通过[DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882)接口获取每个接口支持的统计粒度。

#### 2.2.1 不需要安装监控agent，就能获取数据的监控指标

| 指标名称 | 含义 | 单位 |
| ------------- | ----- | ---- |
| lanOuttraffic | 内网出带宽 | Mbps |
| lanIntraffic | 内网入带宽 | Mbps |
| lanOutpkg | 内网出包量 | 个/秒 |
| lanInpkg | 内网入包量 | 个/秒 |
| WanOuttraffic | 外网出带宽 | Mbps |
| WanIntraffic | 外网入带宽 | Mbps |
| AccOuttraffic | 外网出流量 | MB |
| WanOutpkg | 外网出包量 | 个/秒 |
| WanInpkg | 外网入包量 | 个/秒 |

#### 2.2.2 安装监控agent才能获取数据的监控指标

| 指标名称 | 指标中文名称 | 计算方式 | 指标含义 | 单位 | 统计粒度（period） |
| ------------ | ------- | ---------------------------------------- | --------------------------- | ---- | ------------- |
| CPUUsage | CPU使用率 | CPU的user+nice+system+irq+softirq+idle+iowait时间占总的时间的百分比 | 机器运行期间实时占用的CPU百分比 | % | 10s、60s、300s |
| CPULoadAvg | CPU平均负载 | 分析/proc/loadavg中的数据，以10s为间隔采集过去1分钟内系统平均负载
(windows机器没有此指标) | 一段时间内正在使用和等待使用CPU的平均任务数 | - | 10s、60s、300s |
| MemUsed | 内存使用量 | windows：调用GlobalMemoryStatusEx
Linux：调用psutil.virtual_memory()
计算：总内存 - 可用内存（包括buffers与cached）得到内存使用量数值，不包含buffers和cached | 用户实际使用的内存量，不包括缓冲区与系统缓存占用的内存 | MB | 10s、60s、300s |
| MemUsage | 内存利用率 | 除去缓存、buffer和剩余，用户实际使用内存与总内存之比 | 用户实际使用的内存量，不包括缓冲区与系统缓存占用的内存 | % | 10s、60s、300s |
| TcpCurrEstab | TCP连接数 | windows:调用GetTcpTable获取状态值为MIB_TCP_STATE_ESTAB的tcp数 linux:从/proc/net/snmp获取CurrEstab的值 | 处于 ESTABLISHED 状态的 TCP 连接数量 | 个 | 10s、60s 、300s |

注：安装agent才能获取的指标上报、展示、告警时间为客户云服务器的本地时间。若客户云服务器本地时间非东八区时间，将导致该云服务器的监控数据的时间为非东八区的子机本地时间。

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
| ---------- | --------------------- | ---------------------------------------- |
| MetricName | String | 监控指标 |
| StartTime | Timestamp | 数据点起始时间 |
| EndTime | Timestamp | 数据点结束时间 |
| Period | Integer | 数据统计周期 |
| DataPoints | Array of PointsObject | 监控数据列表 |
| RequestId | String | 唯一请求ID，每次请求都会返回。定位问题时需要提供该次请求的RequestId。 |

## 4. 示例

### 示例1 拉取单个实例监控数据示例

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CVM
&MetricName=CPUUsage
&Period=300
&StartTime=2018-08-24T10:40:23+08:00
&EndTime=2018-08-24T10:50:23+08:00
&Instances.0.Dimensions.0.Name=InstanceId
&Instances.0.Dimensions.0.Value=ins-j0hk02zo
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"DataPoints": [
{
"Dimensions": [
{
"Name": "InstanceId",
"Value": "ins-j0hk02zo"
}
],
"Timestamps": [
1535079000,
1535079300,
1535079600
],
"Values": [
2.566,
2.283,
6.316
]
}
],
"EndTime": "2018-08-24 10:50:00",
"MetricName": "CPUUsage",
"Period": 300,
"RequestId": "d96ec542-6547-4af2-91ac-fee85c1b8b85",
"StartTime": "2018-08-24 10:40:00"
}
}
```

### 示例2 拉取多个实例监控数据示例

#### 输入示例

```
https://monitor.tencentcloudapi.com/?Action=GetMonitorData
&Namespace=QCE/CVM
&MetricName=CPUUsage
&Period=300
&StartTime=2018-09-22T10:40:23+08:00
&EndTime=2018-09-22T10:50:23+08:00
&Instances.0.Dimensions.0.Name=InstanceId
&Instances.0.Dimensions.0.Value=ins-j0hk02zo
&Instances.1.Dimensions.0.Name=InstanceId
&Instances.1.Dimensions.0.Value=ins-o8vv2w10
&<公共请求参数>
```

#### 输出示例

```
{
"Response": {
"DataPoints": [
{
"Dimensions": [
{
"Name": "InstanceId",
"Value": "ins-j0hk02zo"
}
],
"Timestamps": [],
"Values": []
},
{
"Dimensions": [
{
"Name": "InstanceId",
"Value": "ins-o8vv2w10"
}
],
"Timestamps": [],
"Values": []
}
],
"EndTime": "2018-09-22 10:50:00",
"MetricName": "CPUUsage",
"Period": 300,
"RequestId": "9ac53ccc-fbab-483d-980b-b763bcc2f83f",
"StartTime": "2018-09-22 10:40:00"
}
}
```