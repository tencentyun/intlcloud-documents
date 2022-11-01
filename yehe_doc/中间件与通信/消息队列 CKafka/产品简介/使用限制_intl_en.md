This document lists the limits of certain metrics and performance in CKafka. Be careful not to exceed the limits during use to avoid exceptions.

<table>
    <thead>
    <tr>
        <th>Item</th>
        <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>Number of topics</td>
        <td>The topic limit depends on product specifications. For details, see <a href='https://intl.cloud.tencent.com/document/product/597/11745'>Billing Overview</a>.</td>
    </tr>
    <tr>
        <td>Number of partitions</td>
        <td>
            <li>One topic can support up to 3,000 partitions.</li>
            <li>The number of instance-level partitions is the partition limit per topic * the number of topics (generally 2 or 3).</li>
            <li>The number of partitions cannot be reduced.</li>
        </td>
    </tr>
    <tr>
        <td>Partition throughput</td>
        <td>
            <li>In the case of `ack = 1`, the throughput of a single CKafka partition is between 30 and 60 MB/sec due to factors such as CKafka's partition architecture, business data size, and request frequency.</li>
            <li>In the case of `ack = -1` (for strong consistency), <b>we recommend that the throughput of a single CKafka partition be between 10 and 20 MB/sec</b>, so that the stability of the request duration is not affected by factors such as CKafka's partition architecture, business data size, and request frequency.
            </li>
        </td>
    </tr>
    <tr>
        <td>Duration</td>
        <td>
            Featuring high-traffic and high-throughput message queues, Kafka cannot guarantee that each request has low latency. The recommended timeout period settings are as follows:
            <li>For the producer, when ACK = 1, the timeout period defaults to <b>30s</b>;</li>
            <li>For the producer, when ACK = -1, the timeout period defaults to <b>60s</b>;</li>
            <li>The timeout period for the consumer is set to <b>60s</b>.</li>
        </td>
    </tr>
    <tr>
    <tr>
        <td>Number of consumer groups</td>
        <td>
          <li>For Standard Edition, the recommended number of instance-level consumer groups is up to 50.</li>
          <li>For Pro Edition, the recommended number of instance-level consumer groups is up to 200. You can <a href='https://intl.cloud.tencent.com/contact-sales'>submit a ticket </a>
            to apply for more.</li>
        </td>
    </tr>
    <tr>
        <td>Instance</td>
        <td>
            <li>The region attribute of instances cannot be changed.</li>
            <li>The maximum number of client connections to a Standard Edition instance is 5,000, and to a Pro Edition instance, 10,000. When the limit is reached, the client cannot create more connections. If this maximum value is unreasonable for your actual business, you can <a
                    href='https://intl.cloud.tencent.com/contact-sales'>submit a ticket</a> to increase it.
            </li>
        </td>
    </tr>
    <tr>
        <td>Version</td>
        <td>
            <li>Standard Edition: It is compatible with open-source versions 0.9, 0.10, and 1.1. v1.1 is installed by default. Customized versions are not supported.</li>
            <li>Pro Edition: It is compatible with open-source versions 0.9, 0.10, 1.1, 2.4, and 2.8.</li>
        </td>
    </tr>
    <tr>
        <td>Routes</td>
        <td>An instance can create up to five routes, with only one of them being a public network route.</td>
    </tr>
    <tr>
        <td>Public network bandwidth</td>
        <td>CKafka provides a public network bandwidth of 3 Mbps for free by default. Pro Edition instances can upgrade public network bandwidth to 198 Mbps additionally.</td>
    </tr>
    <tr>
        <td>Exposing ZooKeeper</td>
        <td>It is not supported.</td>
    </tr>
    <tr>
        <td>Exposing underlying resources</td>
        <td>It is not supported so as to avoid risks caused by user's operation.</td>
    </tr>
    <tr>
        <td>Message size</td>
        <td>It cannot exceed 12 MB; otherwise, messages will fail to be sent.</td>
    </tr>
    <tr>
        <td>Tag</td>
        <td>Each Tencent Cloud resource can have up to 50 tags.</td>
    </tr>
    <tr>
        <td>Concurrent operations in the console</td>
        <td>Some management and control operations may cause the instance metadata to be modified, leading to data inconsistency when the concurrency is high, and underlying data distribution will be affected. Therefore, some API operations will be locked to limit the request concurrency. <br>To improve the stability and success rate of console operations, up to <b>20</b> concurrent console requests (including those directly initiated via SDK) can be initiated for <b>a single instance</b>.</td>
    </tr>
    </tbody>
</table>



<dx-alert infotype="explain" title="">
Due to CKafka's partition architecture, business data size, request frequency, and the stability of the physical layer, CKafka cannot guarantee that each request has low latency.

- We will try our best to guarantee that:
  1. The percentage of an instance’s monthly low production duration is the same as [the instance’s stability SLA](https://intl.cloud.tencent.com/document/product/597/41815).
  2. The percentage of an instance’s monthly low consumption duration is the same as [the instance’s stability SLA](https://intl.cloud.tencent.com/document/product/597/41815).
- The calculation formula is as follows:
  The percentage of low production duration in a month = (the number of minutes when the production duration 99.9th percentile per minute is less than or equal to 30s that month / the monthly service duration in minutes) * 100%
  The percentage of low consumption duration in a month = (the number of minutes when the consumption duration 99.9th percentile per minute is less than or equal to 60s that month / the monthly service duration in minutes) * 100%
  </dx-alert>
