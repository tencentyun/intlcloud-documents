This document describes how to report the data of a Go application with the gRPC-Jaeger interceptor.

## Directions

### Step 1. Get the endpoint and token

Log in to the [APM console](https://console.cloud.tencent.com/apm), enter the **Application monitoring** > **Application list** page, click **Access application**, and select the Go language and the gRPC-Jaeger data collection method.
Then, get the endpoint and token in the step of access method selection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5rBD100_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A120230112-120043%402x.png)

### Step 2. Install the Jaeger agent

1. Download the [Jaeger agent](https://github.com/jaegertracing/jaeger/releases/tag/v1.22.0).
2. Run the following command to start the agent:
<dx-codeblock>
:::  Shell
nohup ./jaeger-agent --reporter.grpc.host-port={{collectorRPCHostPort}} --agent.tags=token={{token}}
:::
</dx-codeblock>

### Step 3. Select the reporting type to report application data
Select the reporting type to report the data of a Go application through the gRPC-Jaeger interceptor:
#### Server
1. Import the instrumentation dependency `opentracing-contrib/go-grpc` on the server.
 - Dependency path: `github.com/opentracing-contrib/go-grpc`
 - Version requirement: ≥ `v0.0.0-20210225150812-73cb765af46e`
2. Configure Jaeger and create a trace object. Below is a sample:
<dx-codeblock>
:::  Go
cfg := &jaegerConfig.Configuration{
    ServiceName: grpcServerName, // Call trace of the target service. Enter the service name.
    Sampler: &jaegerConfig.SamplerConfig{ // Sampling policy configuration. See section 4.1.1 for details.
    Type:  "const",
    Param: 1,
    },
    Reporter: &jaegerConfig.ReporterConfig{ // Configure how the client reports trace information. All fields are optional.
    LogSpans:          true,
    LocalAgentHostPort: endPoint,
    },
    // Token configuration
    Tags:        []opentracing.Tag{ // Set the tag, where information such as token can be stored.
    opentracing.Tag{Key: "token", Value: token}, // Set the token
    },
}
tracer, closer, err := cfg.NewTracer(jaegerConfig.Logger(jaeger.StdLogger)) // Get the tracer based on the configuration
:::
</dx-codeblock>
3. Configure the interceptor.
<dx-codeblock>
:::  Shell
s := grpc.NewServer(grpc.UnaryInterceptor(otgrpc.OpenTracingServerInterceptor(tracer)))
:::
</dx-codeblock>
4. Start the server service.
<dx-codeblock>
:::  Go
// Register our service with the gRPC server
pb.RegisterHelloTraceServer(s, &server{})
if err := s.Serve(lis); err != nil {
   log.Fatalf("failed to serve: %v", err)
}
:::
</dx-codeblock>
The complete code is as follows:
<dx-codeblock>
:::  Go
// Copyright © 2019-2020 Tencent Co., Ltd.

// This file is part of tencent project.
// Do not copy, cite, or distribute without the express
// permission from Cloud Monitor group.

package grpcdemo

import (
	"context"
	"fmt"
	"github.com/opentracing/opentracing-go"
	"github.com/uber/jaeger-client-go"
	jaegerConfig "github.com/uber/jaeger-client-go/config"
	"log"
	"net"

	"github.com/opentracing-contrib/go-grpc"
	"google.golang.org/grpc"
)

const (
	// Service name, which is the unique identifier of the service and the basis for service metric aggregation and filtering.
	grpcServerName = "demo-grpc-server"
	serverPort     = ":9090"
)

// server is used to implement proto.HelloTraceServer.
type server struct {
	UnimplementedHelloTraceServer
}

// SayHello implements proto.HelloTraceServer
func (s *server) SayHello(ctx context.Context, in *TraceRequest) (*TraceResponse, error) {
	log.Printf("Received: %v", in.GetName())
	return &TraceResponse{Message: "Hello " + in.GetName()}, nil
}

// StartServer
func StartServer() {
	cfg := &jaegerConfig.Configuration{
		ServiceName: grpcServerName, // Call trace of the target service. Enter the service name.
		Sampler: &jaegerConfig.SamplerConfig{ // Sampling policy configuration. See section 4.1.1 for details.
			Type:  "const",
			Param: 1,
		},
		Reporter: &jaegerConfig.ReporterConfig{ // Configure how the client reports trace information. All fields are optional.
			LogSpans:           true,
			LocalAgentHostPort: endPoint,
		},
		// Token configuration
		Tags: []opentracing.Tag{ // Set the tag, where information such as token can be stored.
			opentracing.Tag{Key: "token", Value: token}, // Set the token
		},
	}
	tracer, closer, err := cfg.NewTracer(jaegerConfig.Logger(jaeger.StdLogger)) // Get the tracer based on the configuration
	defer closer.Close()
	if err != nil {
		panic(fmt.Sprintf("ERROR: fail init Jaeger: %v\n", err))
	}
	lis, err := net.Listen("tcp", serverPort)
	if err != nil {
		log.Fatalf("failed to listen: %v", err)
	}
	s := grpc.NewServer(grpc.UnaryInterceptor(otgrpc.OpenTracingServerInterceptor(tracer)))

	// Register our service with the gRPC server
	RegisterHelloTraceServer(s, &server{})
	if err := s.Serve(lis); err != nil {
		log.Fatalf("failed to serve: %v", err)
	}
}

:::
</dx-codeblock>

#### Client

1. Due to the need to simulate HTTP requests on the client, import the `opentracing-contrib/go-stdlib/nethttp` dependency.
 - Dependency path: `github.com/opentracing-contrib/go-stdlib/nethttp`
 - Version requirement: ≥ `v1.0.0`
2. Configure Jaeger and create a trace object.
<dx-codeblock>
:::  Shell
cfg := &jaegerConfig.Configuration{
    ServiceName: grpcClientName, // Call trace of the target service. Enter the service name.
    Sampler: &jaegerConfig.SamplerConfig{ // Sampling policy configuration. See section 4.1.1 for details.
    Type:  "const",
    Param: 1,
    },
    Reporter: &jaegerConfig.ReporterConfig{ // Configure how the client reports trace information. All fields are optional.
    LogSpans:          true,
    LocalAgentHostPort: endPoint,
    },
    // Token configuration
    Tags:        []opentracing.Tag{ // Set the tag, where information such as token can be stored.
    opentracing.Tag{Key: "token", Value: token}, // Set the token
    },
}
tracer, closer, err := cfg.NewTracer(jaegerConfig.Logger(jaeger.StdLogger)) // Get the tracer based on the configuration
:::
</dx-codeblock>
3. Establish a connection to configure the interceptor.
<dx-codeblock>
:::  Go
// Establish a connection to the server to configure the interceptor
conn, err := grpc.Dial(serverAddress, grpc.WithInsecure(), grpc.WithBlock(),
		grpc.WithUnaryInterceptor(otgrpc.OpenTracingClientInterceptor(tracer)))
:::
</dx-codeblock>
4. Make a gRPC call to check whether the access is successful.
The complete code is as follows:
<dx-codeblock>
:::  Go
// Copyright © 2019-2020 Tencent Co., Ltd.

// This file is part of tencent project.
// Do not copy, cite, or distribute without the express
// permission from Cloud Monitor group.

package grpcdemo

import (
	"context"
	"fmt"
	"github.com/opentracing-contrib/go-grpc"
	"github.com/opentracing/opentracing-go"
	"github.com/uber/jaeger-client-go"
	jaegerConfig "github.com/uber/jaeger-client-go/config"
	"google.golang.org/grpc"
	"log"
	"time"
)

const (
	// Service name, which is the unique identifier of the service and the basis for service metric aggregation and filtering.
	grpcClientName = "demo-grpc-client"
	defaultName    = "TAW Tracing"
	serverAddress  = "localhost:9090"
	endPoint       = "xxxxx:6831" // Local agent address
	token          = "abc"
)

// StartClient
func StartClient() {
	cfg := &jaegerConfig.Configuration{
		ServiceName: grpcClientName, // Call trace of the target service. Enter the service name.
		Sampler: &jaegerConfig.SamplerConfig{ // Sampling policy configuration. See section 4.1.1 for details.
			Type:  "const",
			Param: 1,
		},
		Reporter: &jaegerConfig.ReporterConfig{ // Configure how the client reports trace information. All fields are optional.
			LogSpans:           true,
			LocalAgentHostPort: endPoint,
		},
		// Token configuration
		Tags: []opentracing.Tag{ // Set the tag, where information such as token can be stored.
			opentracing.Tag{Key: "token", Value: token}, // Set the token
		},
	}
	tracer, closer, err := cfg.NewTracer(jaegerConfig.Logger(jaeger.StdLogger)) // Get the tracer based on the configuration
	defer closer.Close()
	if err != nil {
		panic(fmt.Sprintf("ERROR: fail init Jaeger: %v\n", err))
	}
	// Establish a connection to the server to configure the interceptor
	conn, err := grpc.Dial(serverAddress, grpc.WithInsecure(), grpc.WithBlock(),
		grpc.WithUnaryInterceptor(otgrpc.OpenTracingClientInterceptor(tracer)))
	if err != nil {
		log.Fatalf("did not connect: %v", err)
	}
	defer conn.Close()

	//
	c := NewHelloTraceClient(conn)
	ctx, cancel := context.WithTimeout(context.Background(), time.Second)
	defer cancel()
	// Make an RPC call
	r, err := c.SayHello(ctx, &TraceRequest{Name: defaultName})
	if err != nil {
		log.Fatalf("could not greet: %v", err)
	}
	log.Printf("RPC Client receive: %s", r.GetMessage())
}

:::
</dx-codeblock>
