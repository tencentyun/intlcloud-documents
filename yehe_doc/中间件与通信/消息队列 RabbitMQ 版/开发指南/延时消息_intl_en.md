This document describes the feature, use cases, and usage of delayed message in TDMQ for RabbitMQ.

## Glossary

**Delayed message**: After a message is sent to the server, the business may want the consumer to receive it after a period of time rather than immediately. This type of message is called "delayed message".

## Use Cases

- Use case 1: Scenarios with requirements for message consumption time. For example, if a user fails to pay within 30 minutes after placing an order in an ecommerce system, the order will be automatically canceled.
- Use case 2: Scenarios where delayed tasks need to be triggered by messages. For example, if a user hasn't placed an order after viewing an item for over 20 minutes after logging in to an app, an item review message will be automatically pushed, and a coupon for the item will be issued.

## Usage

The delayed message feature in TDMQ for RabbitMQ can be used in the same way as the delayed message plugin of RabbitMQ, so you don't need to modify your business when migrating it.

1. Declare an exchange and specify its route type.
```java
Map<String, Object> args = new HashMap<String, Object>();
args.put("x-delayed-type", "direct");
channel.exchangeDeclare("ExchangeName", "x-delayed-message", true, false, args);
```
The parameters are described as follows:
<table>
<thead>
<tr>
<th>Parameter</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td>x-delayed-type</td>
<td>Exchange type, which specifies the routing rule. Valid values: <ul><li>direct</li><li>fanout</li><li>topic</li></ul>For more information, see <a href="https://intl.cloud.tencent.com/document/product/1112/43066">Exchange</a>.</td>
</tr>
<tr>
<td>ExchangeName</td>
<td>Exchange name, which can be obtained from the exchange list in the console.</td>
</tr>
<tr>
<td>x-delayed-message</td>
<td>Specified exchange type for delayed message delivery.</td>
</tr>
</tbody></table>


2. Send a delayed message. Add a key-value pair (key: x-delay; value: number of milliseconds) to the `Header` attribute of the message and specify the target exchange as the one declared in the previous step.
```java
byte[] messageBodyBytes = "delayed payload".getBytes("UTF-8");
Map<String, Object> headers = new HashMap<String, Object>();
headers.put("x-delay", 4000);
AMQP.BasicProperties.Builder props = new AMQP.BasicProperties.Builder().headers(headers);
channel.basicPublish("ExchangeName", "", props.build(), messageBodyBytes);
```
After the message arrives at the exchange, it will be delivered to the corresponding queue in 4,000 milliseconds.

