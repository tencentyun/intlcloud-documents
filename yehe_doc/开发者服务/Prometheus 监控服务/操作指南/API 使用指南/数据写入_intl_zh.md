## 操作场景

类似 flink job 上报数据的场景，我们需要通过 API 直接将数据写入 Prometheus，因为这些 job 的生命周期可能会很短，来不及等待 Prometheus 来拉取数据。写入数据可以直接使用 [Remote Write](https://prometheus.io/docs/practices/remote_write/) 协议或者 [Pushgateway](https://prometheus.io/docs/practices/pushing/) 的方式。

## Remote Write

```
POST /api/v1/prom/write
```

Remote Write 是 Prometheus 标准的协议，更多介绍可以参见 [Prometheus-remote write](https://prometheus.io/docs/practices/remote_write/)。使用 remote write 我们可以把 VPC 内其他 Prometheus 的数据写入到 Prometheus 监控服务中，对于数据的稳定性提升和迁移，都不失为一种不错的方案。


## Pushgateway

虽然 Prometheus 场景主张以拉为主，但是有些场景我们仍然需要使用推的方式，可以参见 [Prometheus -Pushgateway 说明](https://prometheus.io/docs/practices/pushing/)。

Prometheus 监控服务原生集成了 Pushgateway 模块，可以直接推送数据到服务中。下面是一个使用 Go 语言推送数据的简单的例子, 需要将 `$IP`、`$PORT`、`$APPID`、`$TOKEN` 这些变量改为自己实例的认证链接信息，这些链接信息可以从控制台进行查询。

>?强烈建议替换 `$INSTANCE` 为当前机器的标识，例如 `IP/Hostname`。如果没有设置这个 groupingKey，当多台机器一起上报时，数据会互相覆盖。

<dx-codeblock>
::: go 
package main

import (
	"fmt"
	"time"

	"github.com/prometheus/client_golang/prometheus"
	"github.com/prometheus/client_golang/prometheus/push"
	"github.com/prometheus/common/expfmt"
)

var completionTime = prometheus.NewGauge(prometheus.GaugeOpts{
	Name: "db_backup_last_completion_timestamp_seconds",
	Help: "The timestamp of the last successful completion of a DB backup.",
})

func do() {
	completionTime.SetToCurrentTime()
}

func ExamplePusher_Push() {
	if err := push.New("http://$IP:$PORT", "db_backup").
		BasicAuth("$APPID", "$TOKEN").
		Collector(completionTime).
		Grouping("instance", "$INSTANCE").
		Grouping("db", "customers").
		Format(expfmt.FmtText).
		Push(); err != nil {
		fmt.Println("Could not push completion time to Pushgateway:", err)
	}
}

func main() {
	do()
	ticker := time.NewTicker(2 * time.Second)
	done := make(chan bool)
	for {
		select {
		case <-done:
			return
		case <-ticker.C:
			ExamplePusher_Push()
		}
	}
}
:::
</dx-codeblock>

> !`push.New` 生成的对象可以通过 `Client` 方法自定义 HTTP Client，我们推荐设置一个合适的超时时间，同时 push 数据我们建议使用异步的方式调用，以免阻塞业务主流程。

其它上报场景请参见自定义监控说明。 
