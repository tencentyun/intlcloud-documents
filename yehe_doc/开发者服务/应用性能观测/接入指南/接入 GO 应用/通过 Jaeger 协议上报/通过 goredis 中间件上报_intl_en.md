This document describes how to report the data of a Go application with the go-redis middleware.

## Directions

### Step 1. Get the endpoint and token

Log in to the [APM console](https://console.cloud.tencent.com/apm), enter the **Application monitoring** > **Application list** page, click **Access application**, and select the Go language and the go-redis data collection method.
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
Select the reporting type to report the data of a Go application through the go-redis middleware:
#### Client

1. Import the instrumentation dependency `opentracing-contrib/goredis`.
 - Dependency path: `github.com/opentracing-contrib/goredis`
 - Version requirement: ≥ `v0.0.0-20190807091203-90a2649c5f87`

2. Configure Jaeger, create a trace object, and set GlobalTracer. Below is a sample:
<dx-codeblock>
:::  Go
cfg := &jaegerConfig.Configuration{
    ServiceName: clientServerName, // Call trace of the target service. Enter the service name.
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
3. Initialize the Redis connection. Below is a sample:
<dx-codeblock>
:::  Go
func InitRedisConnector() error {
	redisClient = redis.NewUniversalClient(&redis.UniversalOptions{
		Addrs:    []string{redisAddress},
		Password: redisPassword,
		DB:       0,
	})
	if err := redisClient.Ping().Err(); err != nil {
		log.Println("redisClient.Ping() error:", err.Error())
		return err
	}
	return nil
}
:::
</dx-codeblock>
4. Get the Redis connection. Below is a sample:
<dx-codeblock>
:::  Go
func GetRedisDBConnector(ctx context.Context) redis.UniversalClient {
	client := apmgoredis.Wrap(redisClient).WithContext(ctx)
	return client
}
:::
</dx-codeblock>
The complete code is as follows:
<dx-codeblock>
:::  Go
package main

import (
	"context"
	"fmt"
	"github.com/go-redis/redis"
	apmgoredis "github.com/opentracing-contrib/goredis"
	"github.com/opentracing/opentracing-go"
	"github.com/uber/jaeger-client-go"
	jaegerConfig "github.com/uber/jaeger-client-go/config"
	"log"
	"time"
)

const (
	redisAddress     = "127.0.0.1:6379"
	redisPassword    = ""
	clientServerName = "redis-client-demo"
	testKey          = "redis-demo-key"
	endPoint         = "xxxxx:6831" // HTTP reporting address
	token            = "abc"
)

func main() {
	cfg := &jaegerConfig.Configuration{
		ServiceName: clientServerName, // Call trace of the target service. Enter the service name.
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
	opentracing.SetGlobalTracer(tracer)
	defer closer.Close()
	if err != nil {
		panic(fmt.Sprintf("ERROR: fail init Jaeger: %v\n", err))
	}
	InitRedisConnector()
	redisClient := GetRedisDBConnector(context.Background())
	redisClient.Set(testKey, "redis-client-demo", time.Duration(1000)*time.Second)
	redisClient.Get(testKey)
}

var (
	redisClient redis.UniversalClient
)

func GetRedisDBConnector(ctx context.Context) redis.UniversalClient {
	client := apmgoredis.Wrap(redisClient).WithContext(ctx)
	return client
}
func InitRedisConnector() error {
	redisClient = redis.NewUniversalClient(&redis.UniversalOptions{
		Addrs:    []string{redisAddress},
		Password: redisPassword,
		DB:       0,
	})
	if err := redisClient.Ping().Err(); err != nil {
		log.Println("redisClient.Ping() error:", err.Error())
		return err
	}
	return nil
}
:::
</dx-codeblock>
