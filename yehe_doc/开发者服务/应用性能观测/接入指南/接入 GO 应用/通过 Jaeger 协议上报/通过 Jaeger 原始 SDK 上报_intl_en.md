This document describes how to report the data of a Go application with the native Jaeger SDK.

## Directions
### Step 1. Get the endpoint and token

Log in to the [APM console](https://console.cloud.tencent.com/apm), enter the **Application monitoring** > **Application list** page, click **Access application**, and select the Go language and the native Jaeger SDK data collection method.
Then, get the endpoint and token in the step of access method selection.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5rBD100_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A120230112-120043%402x.png)

### Step 2. Install the Jaeger agent

1. Download the [Jaeger agent](https://github.com/jaegertracing/jaeger/releases/tag/v1.22.0).
2. Run the following command to start the agent:
<dx-codeblock>
:::  Shell
nohup ./jaeger-agent --reporter.grpc.host-port={{endpoint}} --agent.tags=token={{token}}
:::
</dx-codeblock>

>?For Jaeger agent v1.15.0 and earlier, replace `--agent.tags` in the startup command with `--jaeger.tags`.

### Step 3. Report data
Report data through the native Jaeger SDK:
1. Due to the need to simulate HTTP requests on the client, import the `opentracing-contrib/go-stdlib/nethttp` dependency.
 - Dependency path: `github.com/opentracing-contrib/go-stdlib/nethttp`
 - Version requirement: ≥ `dv1.0.0`
2. Configure Jaeger and create a trace object. Below is a sample:
<dx-codeblock>
:::  Go
cfg := &jaegerConfig.Configuration{
    ServiceName: ginClientName, // Call trace of the target service. Enter the service name.
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
3. Construct a span and put it in the context. Below is a sample:
<dx-codeblock>
:::  Go
span := tracer.StartSpan("CallDemoServer") // Construct a span
ctx := opentracing.ContextWithSpan(context.Background(), span) // Put the span reference in the context
:::
</dx-codeblock>
4. Construct a request with the tracer. Below is a sample:
<dx-codeblock>
:::  Go
// Construct an HTTP request
req, err := http.NewRequest(
		http.MethodGet,
		fmt.Sprintf("http://localhost%s/ping", ginPort),
		nil,
	)
req = req.WithContext(ctx)
// Construct a request with the tracer
req, ht := nethttp.TraceRequest(tracer, req)
:::
</dx-codeblock>
5. Send an HTTP request and get the returned result.
<dx-codeblock>
:::  Go
httpClient := &http.Client{Transport: &nethttp.Transport{}} // Initialize the HTTP client
res, err := httpClient.Do(req)
// ... Error judgment is omitted.
body, err := ioutil.ReadAll(res.Body)
// ... Error judgment is omitted.
log.Printf(" %s recevice: %s\n", clientServerName, string(body))
:::
</dx-codeblock>
The complete code is as follows:
<dx-codeblock>
:::  Go
// Copyright © 2019-2020 Tencent Co., Ltd.

// This file is part of tencent project.
// Do not copy, cite, or distribute without the express
// permission from Cloud Monitor group.

package gindemo

import (
	"context"
	"fmt"
	"github.com/opentracing-contrib/go-stdlib/nethttp"
	"github.com/opentracing/opentracing-go"
	"github.com/opentracing/opentracing-go/ext"
	opentracingLog "github.com/opentracing/opentracing-go/log"
	"github.com/uber/jaeger-client-go"
	jaegerConfig "github.com/uber/jaeger-client-go/config"
	"io/ioutil"
	"log"
	"net/http"
)

const (
	// Service name, which is the unique identifier of the service and the basis for service metric aggregation and filtering.
	ginClientName = "demo-gin-client"
	ginPort       = ":8080"
	endPoint      = "xxxxx:6831" // Local agent address
	token         = "abc"
)

// The Gin client under StartClient is also a standard HTTP client.
func StartClient() {
	cfg := &jaegerConfig.Configuration{
		ServiceName: ginClientName, // Call trace of the target service. Enter the service name.
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
	// Construct a span and put it in the context
	span := tracer.StartSpan("CallDemoServer")
	ctx := opentracing.ContextWithSpan(context.Background(), span)
	defer span.Finish()
	
	// Construct an HTTP request
	req, err := http.NewRequest(
		http.MethodGet,
		fmt.Sprintf("http://localhost%s/ping", ginPort),
		nil,
	)
	if err != nil {
		HandlerError(span, err)
		return
	}
	// Construct a request with a tracer
	req = req.WithContext(ctx)
	req, ht := nethttp.TraceRequest(tracer, req)
	defer ht.Finish()
	
	// Initialize the HTTP client
	httpClient := &http.Client{Transport: &nethttp.Transport{}}
	// Send the request
	res, err := httpClient.Do(req)
	if err != nil {
		HandlerError(span, err)
		return
	}
	defer res.Body.Close()
	body, err := ioutil.ReadAll(res.Body)
	if err != nil {
		HandlerError(span, err)
		return
	}
	log.Printf(" %s recevice: %s\n", ginClientName, string(body))
}

// HandlerError handle error to span.
func HandlerError(span opentracing.Span, err error) {
	span.SetTag(string(ext.Error), true)
	span.LogKV(opentracingLog.Error(err))
}
:::
</dx-codeblock>
