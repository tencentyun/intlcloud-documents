## Issue Description

[Sarama](https://github.com/Shopify/sarama) is a Kafka client written in Go with a high message throughput.

After you actively increase the number of CKafka partitions due to a performance bottleneck, Sarama may be unable to perceive the partition rebalance, causing a failure to produce/consume messages in the new partitions.

## Common Causes

After CKafka rebalances partitions for various reasons, it will take about 10 minutes for Sarama to perceive the partition changes and then pull the metadata of the current topic to parse the latest partition data. As the pull is time-consuming, it may be regarded as a failure sometimes.

In addition, the CKafka team has found occasional failures of Sarama to pull the latest partition information, causing message retention and random exception reporting.

This problem has been repeatedly reported and fixed in the Sarama community. It occurs less frequently on the latest version but still exists.

## Solutions

If you are sensitive to rebalance and use the Go technology stack, we recommend you migrate to [Confluent-Kafka-Go](https://github.com/confluentinc/confluent-kafka-go), a client maintained by Confluent&trade;.

## Comparison of Common Go Clients
<table>
    <thead>
    <tr>
        <th>Go Client</th>
        <th>Strengths</th>
				<th>Limitations</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Sarama</td>
        <td><ul style = "margin-bottom: 0px;"><li>It is very active in the community and widely used. Questions raised in the community are answered and solved quickly.</li>
				<li>It performs well. As it is written in native Go, it supports async and high-concurrency operations.</li></ul></td>
				<td>It is moderately stable. It may experience unknown errors after the number of partitions is increased and all partitions are rebalanced.</td>
    </tr>
    <tr>
        <td>Confluent-Kafka-go (recommended)</td>
        <td><ul style = "margin-bottom: 0px;"><li>It is very stable. As it actually provides a layer of encapsulation for <a href = "https://github.com/edenhill/librdkafka">librdkafka</a>, and librdkafka
  has been running for many years in multiple languages, it can be reliable enough.</li>
				<li>It performs well. As it is implemented in C++ at the underlying layer, it requires fewer resources and computes faster.</li></ul></td>
				<td><ul style = "margin-bottom: 0px;"><li>As it imports a C++ library, the Go compiler needs additional compilation configurations, which add compilation dependencies and make compilation more complex.</li>
				<li>In addition, as the logic for C++ library implementation varies by compilation environment, importing the `librdkafka` library may affect the cross-compilation of Go projects.</li></ul></td>
    </tr>
		<tr>
        <td>kafka-go</td>
        <td><ul style = "margin-bottom: 0px;"><li>It provides top-level APIs and exposes underlying APIs, which can be called more flexibly to configure the Kafka client.</li>
				<li>It is easy to use since it requires less code to produce and consume messages and has many default configuration items.</li></ul></td>
				<td>It underperforms the above two clients and may be unable to sustain a high concurrency.</td>
    </tr>
    </tbody>
</table>


  





