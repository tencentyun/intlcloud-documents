This document describes how to report the data of a Go application with Jaeger HTTP.

## Directions

### Step 1. Get the endpoint and token
Enter the **Application monitoring** > **Application list** page, click **Access application**, and select the Go language and the Jaeger HTTP data collection method.
Then, get the endpoint and token in the step of access method selection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5rBD100_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A120230112-120043%402x.png)



### Step 2. Modify the endpoint information
> ? We use the gRPC Go interceptor to report data, and the endpoint needs to be changed to [ap-guangzhou.apm.tencentcs.com](http://ap-guangzhou.apm.tencentcs.com/):14268/api/traces. Data can be directly reported to the collector, with no agent required.

### Step 3. Import dependencies
You should import the SDK instrumentation dependencies of OpenTelemetry.
- Dependency path: "[go.opentelemetry.io/otel/sdk/trace](http://go.opentelemetry.io/otel/sdk/trace)"

### Step 4. Initialize the trace
```
// Configure OpenTelemetry under `Init`
func Init() *sdktrace.TracerProvider {
    if ctx == nil {
        ctx = context.Background()
    }
    // Create an exporter and set the basic endpoint
    opts := []otlptracegrpc.Option{
        otlptracegrpc.WithEndpoint("<endpoint>"),
        otlptracegrpc.WithInsecure(),
    }
    exporter, err := otlptracegrpc.New(ctx, opts...)
    if err != nil {
        log.Fatal(err)
    }

    // Set the token or configure the environment variable `OTEL_RESOURCE_ATTRIBUTES=token=xxxxxxxxx`
    r, err := resource.New(ctx, []resource.Option{
        // Set the token value
        resource.WithAttributes(attribute.KeyValue{
            Key: "token", Value: attribute.StringValue("<Token>"),
        }),
        // Set the service name
        resource.WithAttributes(attribute.KeyValue{
            Key: "service.name", Value: attribute.StringValue("audotanggrpcdemo"),
        }),
    }...)
    if err != nil {
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

### Step 5. Select the reporting type to report application data
#### Server
1. Initialize TracerProvider.
```
    // Initialize the trace
    tp := trace.Init()
    defer func() {
        if err := tp.Shutdown(context.Background()); err != nil {
            log.Printf("Error shutting down tracer provider: %v", err)
        }
    }()
    // Specify the host
    host := os.Getenv("grpc1")

    lis, err := net.Listen("tcp", host+":7778")
    if err != nil {
        log.Fatalf("failed to listen: %v", err)
    }
```
2. Configure the interceptor.
```
    s := grpc.NewServer(
        grpc.UnaryInterceptor(otelgrpc.UnaryServerInterceptor()),
        grpc.StreamInterceptor(otelgrpc.StreamServerInterceptor()),
    )
```
3. Start the server service.
```
    // Register our service with the gRPC server
    api.RegisterHelloServiceServer(s, &server{})
    reflection.Register(s)
    if err := s.Serve(lis); err != nil {
        log.Fatalf("failed to serve: %v", err)
    }
```

#### Client configuration
1. Initialize TracerProvider.
```
    // Initialize the trace
    tp := trace.Init()
    defer func() {
        if err := tp.Shutdown(context.Background()); err != nil {
            log.Printf("Error shutting down tracer provider: %v", err)
        }
    }()
```
2. Establish a connection to configure the interceptor.
```
    // Establish a connection to the server to configure the interceptor
    conn, err := grpc.DialContext(context.Background(), "localhost:7778", grpc.WithTransportCredentials(insecure.NewCredentials()), grpc.WithBlock())
```
3. Make a gRPC call.
```
    c := api.NewHelloServiceClient(conn)
    for {
        callSayHelloClientStream(c)
        time.Sleep(100 * time.Millisecond)
    }
```

