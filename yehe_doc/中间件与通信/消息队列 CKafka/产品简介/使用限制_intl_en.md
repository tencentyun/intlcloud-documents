This document lists the limits of certain metrics and performance in CKafka. Be careful not to exceed the corresponding limits during use to avoid exceptions.
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
        <td>The number of topics varies with product specification. For more information, see <a href='https://intl.cloud.tencent.com/document/product/597/11745'>Billing Overview</a>.</td>
    </tr>
    <tr>
        <td>Number of partitions</td>
        <td>
            <li>One topic can support up to 2,500 partitions.</li>
            <li>The number of instance-level partitions is the partition limit per topic * the number of topics (generally 2 or 3).</li>
            <li>The number of partitions cannot be reduced.</li>
        </td>
    </tr>
		    <tr>
        <td>Partition throughput</td>
        <td>
            <li>In the case of `ack = 1`, the throughput of a single CKafka partition is between 30 and 60 MB/s due to factors such as CKafka's partition architecture, business data size, and request frequency.</li>
            <li>In the case of `ack = -1` (for strong consistency), due to factors such as CKafka's partition architecture, business data size, and request frequency, in order to ensure the stability of the request time, <b>we recommend that the throughput of a single CKafka partition be between 10 and 20 MB/s</b>.
            </li>
        </td>
    </tr>
    <tr>
        <td>Number of consumer groups</td>
        <td>The instance-level number of consumer groups should be below 200. For Pro Edition instances, you can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> to increase the limit to 500.
        </td>
    </tr>
    <tr>
        <td>Instance</td>
        <td>
            <li>The region attribute of instances cannot be changed.</li>
            <li>The maximum number of client connections to an instance is 5,000. When the number of instance connections has reached the limit, the client cannot create more connections. If this maximum value is unreasonable in your actual business, you can <a href='https://console.cloud.tencent.com/workorder/category'>submit a ticket</a> to increase it.
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
        <td>Multiple routing</td>
        <td>An instance can create up to 5 routes, with only one of them being a public network route.</td>
    </tr>
    <tr>
        <td>Public network bandwidth</td>
        <td>CKafka provides a public network bandwidth of 3 Mbps for free by default. Pro Edition instances can upgrade public network bandwidth to 198 Mbps additionally.</td>
    </tr>
    <tr>
        <td>Opening ZooKeeper</td>
        <td>It is not supported.</td>
    </tr>
    <tr>
        <td>Opening underlying resource</td>
        <td>It is not supported so as to avoid risks caused by user's operation.</td>
    </tr>
    <tr>
        <td>Message size</td>
        <td>It cannot exceed 12 MB; otherwise, messages will fail to be sent.</td>
    </tr>
    <tr>
        <td>Tag</td>
        <td>One Tencent Cloud resource can have up to 50 tags.</td>
    </tr>
    </tbody>
</table>
