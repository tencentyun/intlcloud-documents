OpenTelemetry is a set of tools, APIs, and SDKs used to monitor, generate, collect, and export telemetry data (metrics, logs, and traces) to help you analyze the performance and behaviors of your application. This document describes how to report the data of a Go application with OpenTelemetry.




### Step 1. Get the endpoint and token

Log in to the [APM console](https://console.cloud.tencent.com/apm), enter the **Application monitoring** > **Application list** page, click **Access application**, and select the Go language and the OpenTelemetry data collection method.
Then, get the endpoint and token in the step of access method selection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5rBD100_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A120230112-120043%402x.png)

<dx-alert infotype="explain" title="Reporting method description">
- Reporting over the private network: To use this reporting method, your service must run in a Tencent Cloud VPC. Direct connection through VPC can reduce the reporting traffic fees while avoiding the security risks in public network communication.
- Reporting over the public network: If your service is deployed locally or not in a Tencent Cloud VPC, you can report data in this method. However, it involves security risks in public network communication and incurs reporting traffic fees.
</dx-alert>


### Step 2. Report Go application data

1. Import the opentelemetry-sdk dependency for instrumenting and reporting from the SDK. First, construct the trace:
```
import (
	"context"
	"go.opentelemetry.io/otel"
	"go.opentelemetry.io/otel/attribute"
	"go.opentelemetry.io/otel/exporters/otlp/otlptrace/otlptracegrpc"
	"go.opentelemetry.io/otel/propagation"
	"go.opentelemetry.io/otel/sdk/resource"
	sdktrace "go.opentelemetry.io/otel/sdk/trace"
	"log"
	_ "os"
)
// Init configures an OpenTelemetry exporter and trace provider
func Init(ctx context.Context) *sdktrace.TracerProvider {
	//New otlp exporter
	opts := []otlptracegrpc.Option{
		// Configure the reporting address. If it has been configured in `config.yaml`, it can be ignored here.
		otlptracegrpc.WithEndpoint("{endpoint information}"), otlptracegrpc.WithInsecure(),
	}
	exporter, err := otlptracegrpc.New(ctx,opts...)
	if err != nil {
		log.Fatal(err)
	}
	// Set the reporting token in the resource, or directly configure the environment variable to set the token: OTEL_RESOURCE_ATTRIBUTES=token=xxxxxxxxx. If it has been configured in `config.yaml`, it can be ignored here.
	r,err := resource.New(ctx,[]resource.Option{
		resource.WithAttributes(attribute.KeyValue{Key: "token",Value: attribute.StringValue("{reporting token}"),}),
	}...)

	if err != nil{
		log.Fatal(err)
	}
	// Create a TracerProvider
	tp := sdktrace.NewTracerProvider(
		sdktrace.WithSampler(sdktrace.AlwaysSample()),
		sdktrace.WithBatcher(exporter),
		sdktrace.WithResource(r),
	)
	otel.SetTracerProvider(tp)
	otel.SetTextMapPropagator(propagation.NewCompositeTextMapPropagator(propagation.TraceContext{}, propagation.Baggage{}))
	return tp
}
```
2. Taking gRPC as an example, initialize the trace first in the server code, set the interceptor when creating the service, and then write the service code as needed.
```
func main() {

	tp := trace.Init() // Perform initialization. The `Init` method is the aforementioned constructor.
	defer func() {
		if err := tp.Shutdown(context.Background()); err != nil {
			log.Printf("Error shutting down tracer provider: %v", err)
		}
	}()

	host := os.Getenv("grpc1")

	lis, err := net.Listen("tcp", host+":7778")
	if err != nil {
		log.Fatalf("failed to listen: %v", err)
	}

	s := grpc.NewServer(
		grpc.UnaryInterceptor(otelgrpc.UnaryServerInterceptor()),     // Set the interceptor for instrumentation
		grpc.StreamInterceptor(otelgrpc.StreamServerInterceptor()),
	)

	api.RegisterHelloServiceServer(s, &server{})   // Register the service. You can modify the specific service code as needed.
	reflection.Register(s)
	if err := s.Serve(lis); err != nil {
		log.Fatalf("failed to serve: %v", err)
	}
}
```
3. Taking gRPC as an example, initialize the trace in the client code and establish a connection.
```
func main() {
	tp := trace.Init()    // Initialization
	fmt.Println("tp create success")
	defer func() {
		if err := tp.Shutdown(context.Background()); err != nil {
			log.Printf("Error shutting down tracer provider: %v", err)
		}
	}()
	fmt.Println("aaa")
	conn, err := grpc.DialContext(context.Background(), "localhost:7778", grpc.WithTransportCredentials(insecure.NewCredentials()), grpc.WithBlock()) // Connection establishment
	fmt.Println("pro")
	if err != nil {
		log.Fatalf("did not connect: %v", err)
	}
	defer conn.Close()
	fmt.Println("conn")

	c := api.NewHelloServiceClient(conn)  // Client code

	for {
		callSayHelloClientStream(c)
		time.Sleep(100 * time.Millisecond)
	}
```

>?To report server data, specify the `span.kind` field as `server`. 
><img src="https://qcloudimg.tencent-cloud.cn/raw/83246ec0c0c55a492c49401105e2bd58.png" width=55%"">

### Step 3. Start your application



### Viewing application data
Log in to the [APM console](https://console.cloud.tencent.com/apm) to view the performance data in the application list.

