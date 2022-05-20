This document describes the feature, use cases, and usage of message tag filtering in TDMQ for Pulsar.

## Overview

A message tag is used to categorize messages under a topic. When a producer in TDMQ for Pulsar sends messages with specified tags, the consumer needs to subscribe to those messages by tag.

If a consumer configures no tags when subscribing to a topic, all messages in the topic will be delivered to the consumer for consumption.

## Use Cases

Generally, messages with the same business attributes are stored in the same topic; for example, when an order transaction topic contains messages of order placement transactions, payment transactions, and delivery transactions, and if you want to consume only one type of transaction messages in your business, you can filter them on the client, but this will waste bandwidth resources.

To solve this problem, TDMQ for Pulsar supports filtering on the broker. You can set one or more tags during message production and subscribe to specified tags during consumption.

![img](https://main.qcloudimg.com/raw/32953b29d96dce605fa4a1598b3f5146.png)



## Limits





Tagged messages are passed in through `Properties` and can be obtained as follows:

<dx-tabs>
:::Java
<dx-codeblock>
:::  xml
<dependency>
    <groupId>org.apache.pulsar</groupId>
    <artifactId>pulsar-client</artifactId>
    <version>2.x.x</version> <!-- The specific version is to be added -->
</dependency>
:::
</dx-codeblock>


:::

:::Go

The latest master version of SDK for Go is required.

<dx-codeblock>
:::  go
go get -u github.com/apache/pulsar-client-go@master
:::
</dx-codeblock>

:::
</dx-tabs>


### Use limits of tagged message

- Tagged messages don't support batch operations. The batch operation feature is enabled by default. To use tagged messages, you need to disable it in the producer as follows:
<dx-codeblock>
:::  Java
  // Construct a producer
  Producer<byte[]> producer = pulsarClient.newProducer()
          // Disable batch operation
          .enableBatching(false)
          // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`
          .topic("persistent://pulsar-xxx/sdk_java/topic2").create();
:::
:::  Go
  producer, err := client.CreateProducer(pulsar.ProducerOptions{
  	DisableBatching: true, // Disable batch operation
  })
:::
</dx-codeblock>
- Tagged message filtering takes effect for only messages with tags. Messages without tags won't be filtered; that is, they will be pushed to all subscribers.
- To enable tagged message, when sending messages, set the `Properties` field in `ProducerMessage` and set the `SubscriptionProperties` field in `ConsumerOptions` when creating consumers.
- When you set the `Properties` field in `ProducerMessage`, the `key` is the tag name, and the `value` is fixed to `TAGS`.
- When you set the `SubscriptionProperties` field in `ConsumerOptions`, the `key` is the tag name to be subscribed to, and the `value` is the tag version (which is reserved for feature extension in the future and has no meaning currently). You can configure as follows:

<dx-accordion>
::: Specify one tag

<dx-codeblock>
:::  Java
     // Send the message
     MessageId msgId = producer.newMessage()
         .property("tag1", "TAGS")
         .value(value.getBytes(StandardCharsets.UTF_8))
		    .send();
	  
     // Subscription parameters, which can be used to set subscription tags
     HashMap<String, String> subProperties = new HashMap<>();
	  subProperties.put("tag1","1");
	  subProperties.put("tag2","1");
	  // Construct a consumer
	  Consumer<byte[]> consumer = pulsarClient.newConsumer()
	      // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from **Topic Management**
         .topic("persistent://pulsar-xxxx/sdk_java/topic2")
         // You need to create a subscription on the topic details page in the console and enter the subscription name here
         .subscriptionName("topic_sub1")
         // Declare the shared mode as the consumption mode
         .subscriptionType(SubscriptionType.Shared)
         // Subscription parameters for tag subscription
         .subscriptionProperties(subProperties)
	      // Configure consumption starting at the earliest offset; otherwise, historical messages may not be consumed
	      .subscriptionInitialPosition(SubscriptionInitialPosition.Earliest).subscribe();
:::
:::  Go
	   // Send the message
	   if msgId, err := producer.Send(ctx, &pulsar.ProducerMessage{
	              Payload: []byte(fmt.Sprintf("hello-%d", i)),
	     Properties: map[string]string{
	         "tag1": "TAGS",
	     },
	   	}); err != nil {
	              log.Fatal(err)
         }

    // Create a consumer
         consumer, err := client.Subscribe(pulsar.ConsumerOptions{
   	            Topic:            "topic-1",
   	            SubscriptionName: "my-sub",
               	SubscriptionProperties: map[string]string{"tag1": "1"},
	      })
:::
</dx-codeblock>


:::
::: Specify multiple tags
<dx-codeblock>
:::  Java
	  // Send the message
		MessageId msgId = producer.newMessage()
		    .property("tag1", "TAGS")
		    .property("tag2", "TAGS")
	      .value(value.getBytes(StandardCharsets.UTF_8))
		    .send();
     
     // Subscription parameters, which can be used to set subscription tags
     HashMap<String, String> subProperties = new HashMap<>();
     subProperties.put("tag1","1");
     subProperties.put("tag2","1");
     // Construct a consumer
     Consumer<byte[]> consumer = pulsarClient.newConsumer()
         // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from **Topic Management**
         .topic("persistent://pulsar-xxxx/sdk_java/topic2")
         // You need to create a subscription on the topic details page in the console and enter the subscription name here
         .subscriptionName("topic_sub1")
         // Declare the shared mode as the consumption mode
         .subscriptionType(SubscriptionType.Shared)
         // Subscription parameters for tag subscription
         .subscriptionProperties(subProperties)
         // Configure consumption starting at the earliest offset; otherwise, historical messages may not be consumed
         .subscriptionInitialPosition(SubscriptionInitialPosition.Earliest).subscribe();
:::
:::  Go
      // Create a producer
      if msgId, err := producer.Send(ctx, &pulsar.ProducerMessage{
                 Payload: []byte(fmt.Sprintf("hello-%d", i)),
           	    Properties: map[string]string{
     	                  "tag1": "TAGS",
     	                  "tag2": "TAGS",
                 },
         }); err != nil {
                 log.Fatal(err)
         }
   
    // Create a consumer
         consumer, err := client.Subscribe(pulsar.ConsumerOptions{
   	            Topic:            "topic-1",
   	            SubscriptionName: "my-sub",
   	            SubscriptionProperties: map[string]string{
   		                  "tag1": "1",
   		                  "tag2": "1",
   	            },
         })

:::
</dx-codeblock>

:::
::: Mix tags and properties
<dx-codeblock>
:::  Java
   	// Send the message
   	MessageId msgId = producer.newMessage()
   	    .property("tag1", "TAGS")
   	    .property("tag2", "TAGS")
   	    .property("xxx", "yyy")
         .value(value.getBytes(StandardCharsets.UTF_8))
   	    .send();
     
     // Subscription parameters, which can be used to set subscription tags
     HashMap<String, String> subProperties = new HashMap<>();
     subProperties.put("tag1","1");
     subProperties.put("tag2","1");
     // Construct a consumer
     Consumer<byte[]> consumer = pulsarClient.newConsumer()
         // Complete path of the topic in the format of `persistent://cluster (tenant) ID/namespace/topic name`, which can be copied from **Topic Management**
         .topic("persistent://pulsar-xxxx/sdk_java/topic2")
         // You need to create a subscription on the topic details page in the console and enter the subscription name here
         .subscriptionName("topic_sub1")
         // Declare the shared mode as the consumption mode
         .subscriptionType(SubscriptionType.Shared)
         // Subscription parameters for tag subscription
         .subscriptionProperties(subProperties)
         // Configure consumption starting at the earliest offset; otherwise, historical messages may not be consumed
         .subscriptionInitialPosition(SubscriptionInitialPosition.Earliest).subscribe();
:::
:::  Go
      // Create a producer
      if msgId, err := producer.Send(ctx, &pulsar.ProducerMessage{
                 Payload: []byte(fmt.Sprintf("hello-%d", i)),
                 Properties: map[string]string{
     	                  "tag1": "TAGS",
     	                  "tag2": "TAGS",
     	                  "xxx": "yyy",
                 },
         }); err != nil {
                 log.Fatal(err)
         }
   
    // Create a consumer
         consumer, err := client.Subscribe(pulsar.ConsumerOptions{
   	            Topic:            "topic-1",
   	            SubscriptionName: "my-sub",
   	            SubscriptionProperties: map[string]string{
   		                  "tag1": "1",
   		                  "tag2": "1",
   	            },
         })
:::
</dx-codeblock>

:::
</dx-accordion>


>! Once the `SubscriptionProperties` field is set in the consumer, the tags processed by the subscription cannot be modified. To modify tags, unsubscribe the current subscription first and create a new subscription.
