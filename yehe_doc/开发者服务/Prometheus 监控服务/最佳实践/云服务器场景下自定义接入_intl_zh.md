本文将详细为您介绍腾讯云云服务器（CVM）如何从0开始接入 Prometheus 监控服务。

## 购买 Prometheus
>?购买的 Prometheus 实例需跟监控的云服务器同一个 vpc 下，能实现网络互通。

1. 登录 [Prometheus 监控服务控制台](https://console.cloud.tencent.com/monitor/prometheus)，单击 **新建** 购买 Prometheus 实例 。 
![](https://qcloudimg.tencent-cloud.cn/raw/721c025fa3a82df239b240d1d2546471.png)
2. 在购买页中，选择合适的实例规格、网络。选择相同 vpc 网段，保证 Prometheus 能与需要采集的云服务器网段相同，才能采集到数据。实例规格，可根据自己的业务上报量进行选择。
![](https://qcloudimg.tencent-cloud.cn/raw/11d449cab6ebcb10501a63c9cff0c421.png)
3. 选择完后，单击立即购买并支付即可。



## 接入云服务器基础指标
1. 下载安装 node_expoter：
在需要上报的云服务器上，下载并安装 node_expoter（采集基础指标数据的 exporter），您可以单击进入 Prometheus 开源官网下载地址 [node_expoter](https://prometheus.io/download/#node_exporter)，也可以直接执行下列命令，下载解压：
```
wget https://github.com/prometheus/node_exporter/releases/download/v1.3.1/node_exporter-1.3.1.linux-amd64.tar.gz && tar -xvf node_exporter-1.3.1.linux-amd64.tar.gz
```
文件目录如下: 
![](https://qcloudimg.tencent-cloud.cn/raw/215bcb6ce3c069bd73eda5a9b1f8bdee.jfif)
2. 运行 node_exporter 采集基础监控数据：
 1. 进入相关文件夹，执行 node_exporter。
```
cd node_exporter-1.3.1.linux-amd64
./node_exporter
```
如下图所示即为成功采集到了基础监控数据。
![](https://qcloudimg.tencent-cloud.cn/raw/fb9bb9fcfb6f0e1a47ec2942e7215299.png)
 2. 可通过下列命令，将该基础监控数据暴露在9100 端口：
```
curl 127.0.0.1:9100/metrics
```
如下图为执行命令后看到的暴露出来的指标监控数据。
![](https://qcloudimg.tencent-cloud.cn/raw/4295420750699bf57711deb515319131.jfif)
3. 新增抓取任务：
登录 [Prometheus 监控服务控制台](https://console.cloud.tencent.com/monitor/prometheus)，进入 **集成中心**  > **选择云服务器**，在任务配置中根据页面提示进行配置。
抓取任务参考配置如下：
```
job_name: example-job-name
metrics_path: /metrics
cvm_sd_configs:
- region: ap-guangzhou
  ports:
  - 9100
  filters:         
  - name: tag:示例标签键
    values: 
    - 示例标签值
relabel_configs: 
- source_labels: [__meta_cvm_instance_state]
  regex: RUNNING
  action: keep
- regex: __meta_cvm_tag_(.*)
  replacement: $1
  action: labelmap
- source_labels: [__meta_cvm_region]
  target_label: region
  action: replace
```


4. 查看数据是否上报成功：
登录 [Prometheus 监控服务控制台](https://console.cloud.tencent.com/monitor/prometheus)，单击 Grafana 图标，进入 Grafana。
如下图所示，到 Explore 搜索下 `{job="cvm_node_exporter"}` 查看是否有数据，若有数据，则表示上报成功。
![](https://qcloudimg.tencent-cloud.cn/raw/5df4efbf12becadade7f2de2e64f220c.png)
5. 配置 Dashboard 界面：Dashboard 界面每个产品都会有一些现成的 json 文件，可以直接导入。  
 1. **下载 Dashboard 文件**：登录 [Dashboard 界面](https://grafana.com/grafana/dashboards/)，单击搜索 node_exporter，选择最新的 Dashboard 并下载。
![](https://qcloudimg.tencent-cloud.cn/raw/2198a3ab1f6243ce17addc73856614bb.png)
ii. **导入 Dashboard 的 json 文件**：登录 [Prometheus 监控服务控制台](https://console.cloud.tencent.com/monitor/prometheus)，进入**基本信息 > Grafana 地址**，单击进入 Grafana，在 Grafana 控制台 > Create > Import > 在 Upload JSON file 中上传 Dashboard 文件。
![](https://qcloudimg.tencent-cloud.cn/raw/a5c4a39697314f2cfcf107a8972fbacc.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3c9a7028eabc4a898e020837c74752d3.png)


## 接入云服务器业务层指标
Prometheus 根据监控的不同场景提供了 Counter、Gauge、Historgram、Summary 四种指标类型。Prometheus 社区提供了多种开发语言的 SDK，每种语言的使用方法基本上类似，主要是开发语言语法上的区别，下面主要以 Go 作为例子，使用 Counter 指标类型如何上报自定义监控指标数据。其余指标类型请参见 [自定义监控](https://intl.cloud.tencent.com/document/product/1116/43215)。

#### Counter
计数类型，数据是单调递增的指标，服务重启之后会重置。可以用 Counter 来监控请求数、异常数、用户登录数和订单数等。
1. 如何通过 Counter 来监控订单数：
```
package order

import (
    "github.com/prometheus/client_golang/prometheus"
    "github.com/prometheus/client_golang/prometheus/promauto"
)

// 定义需要监控 Counter 类型对象
var (
    opsProcessed = promauto.NewCounterVec(prometheus.CounterOpts{
        Name: "order_service_processed_orders_total",
        Help: "The total number of processed orders",
    }, []string{"status"}) // 处理状态
)

// 订单处理
func makeOrder() {
    opsProcessed.WithLabelValues("success").Inc() // 成功状态
    // opsProcessed.WithLabelValues("fail").Inc() // 失败状态

    // 下单的业务逻辑
}
```
例如，通过 `rate()` 函数获取订单的增长率：
```
rate(order_service_processed_orders_total[5m])
```
2. 暴露 Prometheus 指标：
通过 `promhttp.Handler()` 把监控埋点数据暴露到 HTTP 服务上。
``` go
package main

import (
	"net/http"

	"github.com/prometheus/client_golang/prometheus/promhttp"
)

func main() {
        // 业务代码

        // 把 Prometheus 指标暴露在 HTTP 服务上
        http.Handle("/metrics", promhttp.Handler())

        // 业务代码
}

```

3. 采集数据：
完成相关业务自定义监控埋点之后，应用发布，即可通过 Prometheus 来抓取监控指标数据。采集完成后，等待数分钟，您即可在 Prometheus 监控服务集成的 Grafana 中查看业务指标监控数据。
![img](https://main.qcloudimg.com/raw/fc6bf3f5cfbab1bbd931d418b9dddef2.png)

