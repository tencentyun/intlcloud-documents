## Overview

Similar to the scenario of data reporting by Flink jobs, you need to write data directly to Prometheus through APIs, as the lifecycle of these jobs may be very short, and it would be too late to wait for Prometheus to pull the data. To write data, you can directly use the [remote write](https://prometheus.io/docs/practices/remote_write/) protocol or [Pushgateway](https://prometheus.io/docs/practices/pushing/).

## Remote Write

```
POST /api/v1/prom/write
```

Remote write is a standard protocol of Prometheus. For more information, please see [REMOTE WRITE TUNING](https://prometheus.io/docs/practices/remote_write/). With remote write, you can write other Prometheus data in the VPC to TMP, which helps improve the data stability and make migration easier.


## Pushgateway

Although the pull method is recommended in Prometheus, you may still need to use the push method in some scenarios. For more information, please see [WHEN TO USE THE PUSHGATEWAY](https://prometheus.io/docs/practices/pushing/).

TMP is natively integrated with the Pushgateway module, which can directly push data to it. Below is a simple example of pushing data in Go. You need to change the variables of `$IP`, `$PORT`, `$APPID`, and `$TOKEN` to the authentication information of your own instance, which can be queried in the console.

>?We strongly recommend you replace `$INSTANCE` with an identifier of the current machine, such as `IP/Hostname`. If this `groupingKey` is not set, when multiple machines report data together, the data entries will overwrite each other.

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

> !You can customize the HTTP Client through the `Client` method for the object generated by `push.New`. We recommend you set an appropriate timeout period. In addition, if data is pushed, we recommend you use an async method for calls so as to avoid blocking the primary business process.

For other reporting scenarios, please see Custom Monitoring. 
