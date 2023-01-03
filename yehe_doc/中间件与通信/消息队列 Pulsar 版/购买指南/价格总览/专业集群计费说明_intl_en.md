
This document describes the billing mode of TDMQ for Pulsar pro cluster.

## Billable Items

TDMQ for Pulsar pro cluster is monthly subscribed (postpaid) with the following billable items:

- Cluster specification
- Storage specification

## Billable Specification

### Cluster specification limits
- **Messaging TPS upper limit:** Indicates the upper limit on the messaging (production and consumption) TPS of a TDMQ for Pulsar pro cluster.
>?The TPS upper limit varies by cluster specification. For more information, see [Pro Cluster Specification](https://www.tencentcloud.com/document/product/1110/52236).
- **Peak bandwidth upper limit:** If it is 45 MB/s, both the outbound and inbound bandwidth of the TDMQ for Pulsar pro cluster can reach up to 45 MB/s, including the traffic of three copies.
- **Other resource limits:** Besides TPS and bandwidth, cluster specifications also vary in terms of certain controlled resources and configuration limits. For more information, see [Pro Cluster Specification](https://www.tencentcloud.com/document/product/1110/52236).



### Exceeded specification limits

Currently, no throttling measures are taken by the system if your actual usage exceeds the upper limit of the purchased cluster specification. However, we recommend you subscribe to the alarms for core cluster metrics, keep an eye on the processing performance in case of metric changes, and upgrade the cluster specification promptly to guarantee stable business operations. We may provide elasticity in this regard in the future to ease your worries.

### Cluster TPS specification

1. Messaging TPS refers to the sum of messages sent and subscribed per second.
2. The message size is measured in 4 KB. For example, if the numbers of messages sent and received per second are both 5,000, and the average message body size is 8 KB, then the messaging TPS is (8 / 4) * (5,000 + 5,000) = 20,000 messages/sec.
3. For advanced messages, i.e., sequential, scheduled/delayed, and transactional messages, the number of calls for message sending needs to be five times that of general messages. For example, if 1,000 delayed messages are sent per second, the TPS for message sending is 1,000 * 5 = 5,000 messages/sec.


## Billing Description

### Cluster specification billing
<style>
table th:first-of-type {
    width: 20%;
}
table th:nth-of-type(2) {
    width: 30%;
}
</style>

TDMQ for Pulsar pro cluster provides different computing specifications determined by the messaging TPS and peak bandwidth.

| Item      | Description                                                         |
| :--------------- | :----------------------------------------------------------- |
| Billable item | Fees are charged based on the purchased cluster specification. |
| Billing mode | Billing cycle: It is subject to the actual validity period of the cluster. |
| Billing formula | Monthly subscription: Cluster specification fees = validity period (month) * unit price (USD/month) |
| Unit price | It is subject to the price on the purchase page. |


### Storage specification billing

TDMQ for Pulsar pro cluster provides SSD cloud disks to store cluster data with three copies by default. You can purchase the storage space as needed.

| Item      | Description                                                         |
| :--------------- | :----------------------------------------------------------- |
| Billable item | Fees are charged based on the storage specification configured during cluster purchase. |
| Billing mode | Billing cycle: It is subject to the actual validity period of the cluster. |
| Billing formula | Monthly subscription: Storage specification fees = selected specification (GB) * 3 * validity period (month) * unit price (USD/GB/month) |
| Unit price | See the table below. |

#### Storage unit price

In USD/GB/month
<table>
	<tbody>
   <tr>
	   <th style="width: 20%;" rowspan="2">Region</th>
		 <th colspan="1">Cloud Disk Type</th>     
		 </tr>
 <tr>        
	<th style="width: 13%;">SSD cloud disk</th>
	</tr>
      <tr>
            <td>South China (Guangzhou)</td>
			<td>0.1550</td>
       </tr>
       <tr>
            <td>East China (Shanghai)</td>
			<td>0.1550</td>
      </tr>
			<tr>
            <td>East China (Nanjing)</td>
			<td>0.1550</td>
      </tr>
			<tr>
            <td>North China (Beijing)</td>
			<td>0.1550</td>
      </tr>
			<tr>
            <td>Southwest China (Chengdu)</td>
			<td>0.1550</td>
      </tr>
			<tr>
            <td>Southwest China (Chongqing)</td>
			<td>0.1550</td>
      </tr>
			<tr>
            <td>East China (Shanghai Finance Zone)</td>
			<td>0.2728</td>
      </tr>
			<tr>
            <td>South China (Shenzhen Finance Zone)</td>
			<td>0.2728</td>
      </tr>
			<tr>
            <td>North China (Beijing Finance Zone)</td>
			<td>0.2728</td>
      </tr>
			<tr>
            <td>Hong Kong/Macao/Taiwan (China Region) (Hong Kong, China)</td>
						<td>0.1705</td>
      </tr>
			<tr>
            <td>North America (Toronto)</td>
			<td>0.1705</td>
      </tr>
			<tr>
            <td>Southeast Asia (Singapore)</td>
            <td>0.1938</td>
      </tr>
			<tr>
            <td>Southeast Asia (Jakarta)</td>
            <td>0.1938</td>
      </tr>
			<tr>
            <td>West US (Silicon Valley)</td>
            <td>0.1783</td>
      </tr>
			<tr>
            <td>Europe (Frankfurt)</td>
            <td>0.1938</td>
      </tr>
			<tr>
            <td>Northeast Asia (Seoul)</td>
            <td>0.2015</td>
      </tr>
			<tr>
            <td>East US (Virginia)</td>
            <td>0.1938</td>
      </tr>
			<tr>
            <td>Southeast Asia (Bangkok)</td>
            <td>0.1938</td>
      </tr>
		    <tr>
            <td>Eastern Europe (Moscow)</td>
            <td>0.2015</td>
        </tr>
        <tr>
            <td>Northeast Asia (Tokyo)</td>
            <td>0.2325</td>
        </tr>
		    <tr>
            <td>South America (São Paulo)</td>
            <td>0.1938</td>
        </tr>
    </tbody></table>

