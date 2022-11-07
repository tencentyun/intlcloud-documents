## Overview

This document describes how to use open-source SDK to send and receive messages by using the SDK for Go as an example and helps you better understand the message sending and receiving processes.

## Prerequisites

- You have created the required resources. For more information, see [Resource Creation and Preparation](https://intl.cloud.tencent.com/document/product/1110/42915).
- You have installed Go. Download one at [here](https://golang.org/dl/)
- You have downloaded the demo at [here](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-go-sdk-demo.zip)

## Directions

1. Import the `pulsar-client-go` library in the client environment.

   1. Run the following command in the client environment to download the dependency package of the Pulsar client.
      <dx-codeblock>
      :::  shell
      go get -u "github.com/apache/pulsar-client-go/pulsar"
      :::
      </dx-codeblock>
   2. After the installation is completed, use the following code to import the client into your Go project file.
      <dx-codeblock>
      :::  go
      import "github.com/apache/pulsar-client-go/pulsar"
      :::
      </dx-codeblock>

2. Create a Pulsar client.
   <dx-codeblock>
   :::  go
   // Create a Pulsar client
   client, err := pulsar.NewClient(pulsar.ClientOptions{
       // Service access address
       URL: serviceUrl,
       // Role token
       Authentication:    pulsar.NewAuthenticationToken(authentication),
       OperationTimeout:  30 * time.Second,
       ConnectionTimeout: 30 * time.Second,
   })

   if err != nil{
       log.Fatalf("Could not instantiate Pulsar client: %v", err)
   }

   defer client.Close()
   :::
   </dx-codeblock>

<table>
    <thead>
    <tr>
        <th style='text-align:left;'>Parameter</th>
        <th style='text-align:left;'>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td style='text-align:left;'>serviceUrl</td>
        <td style='text-align:left;'>Cluster access address, which can be viewed and copied on the <a
                href='https://console.cloud.tencent.com/tdmq/cluster'><strong>Cluster</strong></a> page in the console.<br><img
                src="https://qcloudimg.tencent-cloud.cn/raw/8612bb79a799375eb97d5e871e239372.png"
                referrerpolicy="no-referrer" alt="img"></td>
    </tr>
    <tr>
        <td style='text-align:left;'>Authentication</td>
        <td style='text-align:left;'>Role token, which can be copied in the <strong>Token</strong> column on the <strong><a
                href='https://console.cloud.tencent.com/tdmq/role'>Role Management</a></strong> page.<img
                src="https://qcloudimg.tencent-cloud.cn/raw/65a283caa4b28d9fab366114ea8636b1.png" referrerpolicy="no-referrer"
                alt="img"></td>
    </tr>
    </tbody>
</table>

3. Create a producer.
   <dx-codeblock>
   :::  go
   // Create a producer with the client
   producer, err := client.CreateProducer(pulsar.ProducerOptions{
       // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`
       Topic: "persistent://pulsar-mmqwr5xx9n7g/sdk_go/topic1",
   })

   if err != nil{
       log.Fatal(err)
   }
   defer producer.Close()
   :::
   </dx-codeblock>
   <dx-alert infotype="explain" title="">
   You need to enter the complete path of the topic name, i.e., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
   </dx-alert>

4. Send the message.
   <dx-codeblock>
   :::  go
   // Send the message
   _, err = producer.Send(context.Background(), &pulsar.ProducerMessage{
       // Message content
       Payload: []byte("hello go client, this is a message."),
       // Business key
       Key: "yourKey",
       // Business parameter
       Properties: map[string]string{"key": "value"},
   })
   :::
   </dx-codeblock>

5. Create a consumer.
   <dx-codeblock>
   :::  go
   // Create a consumer with the client
   consumer, err := client.Subscribe(pulsar.ConsumerOptions{
       // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`
       Topic:            "persistent://pulsar-mmqwr5xx9n7g/sdk_go/topic1",
       // Subscription name
       SubscriptionName: "topic1_sub",
       // Subscription mode
       Type:             pulsar.Shared,
   })
   if err != nil{
       log.Fatal(err)
   }
   defer consumer.Close()
   :::
   </dx-codeblock>

> ?
>
> - You need to enter the complete path of the topic name, that is., `persistent://clusterid/namespace/Topic`, where the `clusterid/namespace/topic` part can be copied directly from the **[Topic](https://console.cloud.tencent.com/tdmq/topic)** page in the console.
>   ![img](https://qcloudimg.tencent-cloud.cn/raw/4bb986f5e871cb9d72d9066ecf7eea66.png)
> - You need to enter the subscription name in the `subscriptionName` parameter, which can be viewed on the **Consumption Management** page.

6. Consume the message.
   <dx-codeblock>
   :::  go
   // Obtain the message
   msg, err := consumer.Receive(context.Background())
   if err != nil{
       log.Fatal(err)
   }
   // Simulate business processing
   fmt.Printf("Received message msgId: %#v -- content: '%s'\n",
              msg.ID(), string(msg.Payload()))

   // If the consumption is successful, return `ack`; otherwise, return `nack` or `ReconsumeLater` according to your business needs
   consumer.Ack(msg)
   :::
   </dx-codeblock>

7. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq), click **Topic** > **Topic Name** to enter the consumption management page, and click the triangle below a subscription name to view the production and consumption records.
 ![img](https://qcloudimg.tencent-cloud.cn/raw/206f52b4a67a3a5eba82309e0d5bc001.png)

>? The above is a brief introduction to the way of publishing and subscribing to messages. For more operations, see [Demo](https://tdmq-document-1306598660.cos.ap-nanjing.myqcloud.com/%E5%85%AC%E6%9C%89%E4%BA%91demo/pulsar/tcp/tdmq-pulsar-go-sdk-demo.zip) or [Pulsar Go client](https://pulsar.apache.org/docs/en/client-libraries-go/).


## Customizing Log File Output

### Use cases

As many users don’t customize the logging library when using the Pulsar SDK for Go, logs are output to `os.Stderr` by default, as shown below:

<dx-codeblock>
:::  go

// It's recommended to make this a global instance called `log`.
func New() *Logger {
	return &Logger{
		Out:          os.Stderr, // Default output address
		Formatter:    new(TextFormatter),
		Hooks:        make(LevelHooks),
		Level:        InfoLevel,
		ExitFunc:     os.Exit,
		ReportCaller: false,
	}
}

:::
</dx-codeblock>

Generally, log information is output to `os.Stderr`. If you don’t specify a custom logging library, the SDK for Go logs and business logs will be mixed, making it difficult for troubleshooting.


### Solution

With the `logger` API exposed on the client by the SDK for Go, you can customize the log output format and location and use logging libraries such as `logrus` and `zap`. Related parameters are as follows:

1. Implement the `log.Logger` API provided by the Pulsar SDK for Go by customizing `log lib`.
<dx-codeblock>
:::  go

// ClientOptions is used to construct a Pulsar Client instance.
type ClientOptions struct {
	// Configure the logger used by the client.
	// By default, a wrapped logrus.StandardLogger will be used, namely,
	// log.NewLoggerWithLogrus(logrus.StandardLogger())
	// FIXME: use `logger` as internal field name instead of `log` as it's more idiomatic
	Logger log.Logger
}

:::
</dx-codeblock>
When using the SDK for Go, you can customize the `logger` API to customize `log lib` so that you can redirect logs to a specified location. Taking `logrus` as an example, the demo below shows you how to customize `log lib` to output the SDK for Go logs to a specified file.
<dx-codeblock>
:::  go

package main

import (
	"fmt"
	"io"
	"os"

	"github.com/apache/pulsar-client-go/pulsar/log"
	"github.com/sirupsen/logrus"

)

// logrusWrapper implements Logger interface
// based on underlying logrus.FieldLogger
type logrusWrapper struct {
	l logrus.FieldLogger
}

// NewLoggerWithLogrus creates a new logger which wraps
// the given logrus.Logger
func NewLoggerWithLogrus(logger *logrus.Logger, outputPath string) log.Logger {
	writer1 := os.Stdout
	writer2, err := os.OpenFile(outputPath, os.O_WRONLY|os.O_CREATE, 0755)
	if err != nil{
		logrus.Error("create file log.txt failed: %v", err)
	}
	logger.SetOutput(io.MultiWriter(writer1, writer2))
	return &logrusWrapper{
		l: logger,
	}
}

func (l *logrusWrapper) SubLogger(fs log.Fields) log.Logger {
	return &logrusWrapper{
		l: l.l.WithFields(logrus.Fields(fs)),
	}
}

func (l *logrusWrapper) WithFields(fs log.Fields) log.Entry {
	return logrusEntry{
		e: l.l.WithFields(logrus.Fields(fs)),
	}
}

func (l *logrusWrapper) WithField(name string, value interface{}) log.Entry {
	return logrusEntry{
		e: l.l.WithField(name, value),
	}
}

func (l *logrusWrapper) WithError(err error) log.Entry {
	return logrusEntry{
		e: l.l.WithError(err),
	}
}

func (l *logrusWrapper) Debug(args ...interface{}) {
	l.l.Debug(args...)
}

func (l *logrusWrapper) Info(args ...interface{}) {
	l.l.Info(args...)
}

func (l *logrusWrapper) Warn(args ...interface{}) {
	l.l.Warn(args...)
}

func (l *logrusWrapper) Error(args ...interface{}) {
	l.l.Error(args...)
}

func (l *logrusWrapper) Debugf(format string, args ...interface{}) {
	l.l.Debugf(format, args...)
}

func (l *logrusWrapper) Infof(format string, args ...interface{}) {
	l.l.Infof(format, args...)
}

func (l *logrusWrapper) Warnf(format string, args ...interface{}) {
	l.l.Warnf(format, args...)
}

func (l *logrusWrapper) Errorf(format string, args ...interface{}) {
	l.l.Errorf(format, args...)
}

type logrusEntry struct {
	e logrus.FieldLogger
}

func (l logrusEntry) WithFields(fs log.Fields) log.Entry {
	return logrusEntry{
		e: l.e.WithFields(logrus.Fields(fs)),
	}
}

func (l logrusEntry) WithField(name string, value interface{}) log.Entry {
	return logrusEntry{
		e: l.e.WithField(name, value),
	}
}

func (l logrusEntry) Debug(args ...interface{}) {
	l.e.Debug(args...)
}

func (l logrusEntry) Info(args ...interface{}) {
	l.e.Info(args...)
}

func (l logrusEntry) Warn(args ...interface{}) {
	l.e.Warn(args...)
}

func (l logrusEntry) Error(args ...interface{}) {
	l.e.Error(args...)
}

func (l logrusEntry) Debugf(format string, args ...interface{}) {
	l.e.Debugf(format, args...)
}

func (l logrusEntry) Infof(format string, args ...interface{}) {
	l.e.Infof(format, args...)
}

func (l logrusEntry) Warnf(format string, args ...interface{}) {
	l.e.Warnf(format, args...)
}

func (l logrusEntry) Errorf(format string, args ...interface{}) {
	l.e.Errorf(format, args...)
}

:::
</dx-codeblock>
2. Specify a custom `log lib` when creating the client.
	<dx-codeblock>
	:::  go

	client, err := pulsar.NewClient(pulsar.ClientOptions{
		URL:    "pulsar://localhost:6650",
		Logger: NewLoggerWithLogrus(log.StandardLogger(), "test.log"),
	})


:::
</dx-codeblock>
The above demo shows you how to redirect the log file of the Pulsar SDK for Go to the `test.log` file in the current path. You can redirect the log file to a specified location as needed.

