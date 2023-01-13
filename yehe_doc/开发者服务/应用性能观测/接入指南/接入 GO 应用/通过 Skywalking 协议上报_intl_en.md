GO2Sky is a package provided by Go for developers to implement SkyWalking agent's probe, which can be used to report data to the SkyWalking collector. This document describes how to report the data of a Go application over the SkyWalking protocol.


## Directions
<span id="step1"></span>

### Step 1. Get the endpoint and token

Log in to the [APM console](https://console.cloud.tencent.com/apm), enter the **Application monitoring** > **Application list** page, click **Access application**, and select the Go language and the SkyWalking data collection method.
Then, get the endpoint and token in the step of access method selection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5rBD100_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A120230112-120043%402x.png)

### Step 2. Report application data
Report the data of a Go application over the SkyWalking protocol:
1. Instrument the application.
Instrument the cross-service calls in Go as instructed in the [GO2Sky documentation](https://github.com/SkyAPM/go2sky). You need to modify a small amount of the business code of your Go application to instrument it before you can use SkyWalking to report its data.
2. Modify the reporting configuration.
Change the `serverAddr` and `auth` of the reporter to the endpoint and token of APM respectively.
3. Restart the service to start reporting data.
4. Verify the access.

Send a request to the application, and after receiving the response, view the call data in the APM console. You can find call details in **Tracing** > **[Call query](https://console.cloud.tencent.com/apm/monitor/span)** within one minute. The monitoring curve and statistics will start to be displayed normally after one minute.

## GO2Sky modification example

The following is a GO2Sky-based demo modification example. You can modify it as needed.

1. Set the reporting address and authentication under NewGRPCReporter (refer to [step 1](#step1) for how to get the reporting address and token).
<dx-codeblock>
:::  Go
report, err = reporter.NewGRPCReporter(
"ap-guangzhou.tencentservicewatcher.com:11800",
reporter.WithAuthentication("tsw_site@xxxxxxxxxx"))
:::
</dx-codeblock>
<dx-alert infotype="notice" title="">
Change the parameters to the private network endpoint and token displayed in the console.
</dx-alert>
2. Configure the server. Below is a demo:
<dx-codeblock>
:::  Go
import (
   "flag"
   "github.com/SkyAPM/go2sky"
   v3 "github.com/SkyAPM/go2sky-plugins/gin/v3"
   "github.com/SkyAPM/go2sky/reporter"
   "github.com/gin-gonic/gin"
   "log"
   "net/http"
)
var (
   grpc        bool
   oapServer   string
   listenAddr  string
   serviceName string
   client *http.Client
)
func init() {
   flag.BoolVar(&grpc, "grpc", false, "use grpc reporter")
   // `9.223.77.222:11800` should be replaced with the private network endpoint of APM.
   flag.StringVar(&oapServer, "oap-server", "9.223.77.222:11800", "oap server address")
   flag.StringVar(&listenAddr, "listen-addr", "0.0.0.0:8809", "listen address")
   flag.StringVar(&serviceName, "service-name", "go2sky-server", "service name")
}
func main() {
   flag.Parse()
   log.Println("reporter.NewGRPCReporter start")
   var report go2sky.Reporter
   var err error
   /*
      Parameter description:
      @oapServer: SkyWalking backend collector address
   */
   report, err = reporter.NewGRPCReporter(
   oapServer,
   reporter.WithAuthentication("c944279f910baee6d2e102817270696f"))
   // `c944279f910baee6d2e102817270696f` should be replaced with your token.
   //report, err = reporter.NewLogReporter()
   if err != nil {
     log.Fatalf("crate grpc reporter error: %v \n", err)
   }
   /*
      Parameter description:
      @service: Service name, which ends with @ and represents the DMP tenant where the service resides.
      @opts: A reporter instance in the fixed format
   */
   log.Println("go2sky.NewTracer")
   tracer, err := go2sky.NewTracer(serviceName, go2sky.WithReporter(report))
   if err != nil {
     log.Fatalf("crate tracer error: %v \n", err)
   }
   gin.SetMode(gin.ReleaseMode)
   r := gin.New()
    /*
       GO2Sky's middleware implements path tracing.
       `v3` is short for `github.com/SkyAPM/go2sky-plugins/gin/v3`.
    */
   r.Use(v3.Middleware(r, tracer))
   r.GET("/ping", func(c *gin.Context) {
       c.JSON(200, gin.H{
           "message": "hi gin",
       })
   })
   log.Println("0.0.0.0:8809")
   r.Run(listenAddr)
}

:::
</dx-codeblock>
