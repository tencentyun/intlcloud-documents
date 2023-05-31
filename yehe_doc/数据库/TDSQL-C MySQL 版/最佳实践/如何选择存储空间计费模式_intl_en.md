
Storage space refers to the space used by data files, index files, log files (redo logs, undo logs, slow logs, and error logs), and temporary files. Fees are charged for the used storage space.

This document describes how to select a billing mode for the storage space.

## Pay-as-You-Go
### Billing rules
The storage space of TDSQL-C for MySQL is billed per GB per hour. You don't need to select the storage space capacity when purchasing an instance, as the storage space will be automatically expanded as the data volume grows. You only pay for the storage space you use. You can view the database storage usage details and the storage space cap under the current compute node specification in the configuration information on the cluster details page in the [console](https://console.cloud.tencent.com/cynosdb).
![](https://qcloudimg.tencent-cloud.cn/raw/0521531ad584039a5005df1b09aa7a08.png)

### Pricing
- Guangzhou, Shanghai, Beijing, and Nanjing: 0.00072 USD/GB/hour.
- Hong Kong (China), Taipei (China), Singapore, Silicon Valley, Frankfurt, Tokyo, and Virginia: 0.000792 USD/GB/hour.

### Use cases
It is suitable for instantaneously fluctuating businesses. In this mode, instances can be released immediately after the use to save costs.

## Monthly Subscription
### Billing rules
The monthly subscribed storage space can be selected only when the billing mode of TDSQL-C for MySQL compute nodes is monthly subscription. Compared with the pay-as-you-go billing, the (prepaid) monthly subscription billing mode offers discounts when your required storage space is large.

### Pricing
- Guangzhou, Shanghai, Beijing, and Nanjing: 0.20541177 USD/GB/month for below 3000 GB; 0.18829412 USD/GB/month for 3000 GB or above.
- Hong Kong (China), Taipei (China), Singapore, Silicon Valley, Frankfurt, Tokyo, and Virginia: 0.22447059 USD/GB/month for below 3000 GB; 0.20576471 USD/GB/month for 3000 GB or above.

### Use cases
It is more cost-effective in the long term for businesses with stable needs than pay-as-you-go billing. It supports tiered pricing with a higher cost performance.

## Storage Space Price Comparison
>?The actual daily usage cannot be predicted in pay-as-you-go mode, which makes comparison difficult. Therefore, the following pay-as-you-go storage space usage is based on the amount of stored data imported at one time within a month.

<table>
<thead><tr>
<th rowspan=2 >Storage Space (GB)</th>
<th colspan=2>Chinese Mainland</th><th colspan=2>Hong Kong (China), Taipei (China), and other countries and regions</th></tr>
<tr>
<th>Pay-as-You-Go (USD/Month)</th><th>Monthly Subscription (USD/Month)<br>Equivalent to 36% to 40% of Pay-as-You-Go Prices</th>
<th>Pay-as-You-Go (USD/Month)</th><th>Monthly Subscription (USD/Month)<br>Equivalent to 36% to 39% of Pay-as-You-Go Prices</th>
</tr></thead>
<tbody><tr>
<td>50</td><td>25.92</td><td>10.2705885 (60% off)</td><td>28.512</td><td>11.2235295 (61% off)</td></tr>
<tr>
<td>100</td><td>51.84</td><td>20.541177 (60% off)</td><td>57.024</td><td>22.447059 (61% off)</td></tr>
<td>200</td><td>103.68</td><td>41.082354 (60% off)</td><td>114.048</td><td>44.894118 (61% off)</td></tr>
<td>300</td><td>155.52</td><td>61.623531 (60% off)</td><td>171.072</td><td>67.341177 (61% off)</td></tr>
<td>500</td><td>259.2</td><td>102.705885 (60% off)</td><td>285.12</td><td>112.235295 (61% off)</td></tr>
<td>1000</td><td>518.4</td><td>205.41177 (60% off)</td><td>570.24</td><td>224.47059 (61% off)</td></tr>
<td>2000</td><td>1036.8</td><td>410.82354 (60% off)</td><td>1140.48</td><td>448.94118 (60% off)</td></tr>
<td>3000</td><td>1555.2</td><td>564.88236 (64% off)</td><td>1710.72</td><td>617.29413 (64% off)</td></tr>
<td>5000</td><td>2592</td><td>941.4706 (64% off)</td><td>2851.2</td><td>1028.82355 (64% off)</td></tr>
<td>10000</td><td>5184</td><td>1882.9412 (64% off)</td><td>5702.4</td><td>2057.6471 (64% off)</td></tr>
<td>400000</td><td>207360</td><td>75317.648 (64% off)</td><td>228096</td><td>82305.884 (64% off)</td></tr>
</tbody></table>
