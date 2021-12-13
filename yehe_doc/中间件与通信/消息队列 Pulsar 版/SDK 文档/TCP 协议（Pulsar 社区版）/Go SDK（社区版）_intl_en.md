## Overview

TDMQ for Pulsar already supports Apache Pulsar SDK for Go. This document describes how to access the SDK.

## Prerequisites[](id:Prerequisites)
- Get the route ID and access point address
Copy the access address on the **[Cluster Management](https://console.cloud.tencent.com/tdmq/cluster)** page in the TDMQ for Pulsar console (for v2.6.1 and below, you need to copy the route ID and access point address on the access point list page).

- Get the token
Configure the role and permission as instructed in [Role and Authentication](https://intl.cloud.tencent.com/document/product/1110/42936) and get the token of the role.

## Directions

1. Install the Go client in your client environment as instructed in [Pulsar Go client](http://pulsar.apache.org/docs/en/client-libraries-go/).
```sh
$ go get -u "github.com/apache/pulsar-client-go/pulsar"
```

2. After the installation is completed, use the following code to import the client into your Go project file.
```go
import "github.com/apache/pulsar-client-go/pulsar"
```

3. In the code for creating the Go client, configure the prepared [route ID and token](#Prerequisites) (you don't need to copy the route ID for clusters on v2.7.1 or above).
>?You can click the following tabs to view the access samples for different cluster versions.
<dx-tabs>
::: Access sample for cluster on v2.7.1 or above
<dx-codeblock>
:::  go
client, err := pulsar.NewClient(pulsar.ClientOptions{
	 URL:               "http://***", // Replace with the access point address (copied from the **Cluster Management** page in the console)
	 Authentication:    pulsar.NewAuthenticationToken("eyJh****"), // Replace with the token
	 OperationTimeout:  30 * time.Second,
	 ConnectionTimeout: 30 * time.Second,
})
if err != nil {
	 log.Fatalf("Could not instantiate Pulsar client: %v", err)
}
:::
</dx-codeblock>

:::
::: Access sample for cluster on v2.6.1
<dx-codeblock>
:::  go
client, err := pulsar.NewClient(pulsar.ClientOptions{
	 URL:               "pulsar://*.*.*.*:6000/", // Replace with the access point address
	 ListenerName:      "custom:1300*****0/vpc-******/subnet-********", // Replace with the route ID
	 Authentication:    pulsar.NewAuthenticationToken("eyJh****"), // Replace with the token
	 OperationTimeout:  30 * time.Second,
	 ConnectionTimeout: 30 * time.Second,
})
if err != nil {
	 log.Fatalf("Could not instantiate Pulsar client: %v", err)
}
:::
</dx-codeblock>
:::
</dx-tabs>

**Note on using `Reader` in Apache Pulsar SDK for Go:**
If you use `Reader` to subscribe to topics, you need to specify the topic partition level (for the default partition, add `-partition-0` after the topic). Below is the sample code:
<dx-codeblock>
:::  go
reader, err := client.CreateReader(pulsar.ReaderOptions{
		Topic:          "persistent://test-tenant/test-ns/test-topic-partition-0",
		StartMessageID: pulsar.EarliestMessageID(),
	})
:::  
 </dx-codeblock> 

For how to use various features of the Apache Pulsar SDK for Go, see [Pulsar Go client](http://pulsar.apache.org/docs/en/client-libraries-go/).

