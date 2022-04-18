TDSQL-C for MySQL offers the following three billing modes:

| Billing Mode | Supported Engine | Payment Mode | Use Case |
| -------------------------------- | ----------------- | -------------------------------- | --------------------------------------------- |
| Monthly subscription                                                     | MySQL | [Prepaid](https://intl.cloud.tencent.com/document/product/555/42701). You need to pay the fees when creating an instance. | It is more cost-effective in the long term for businesses with stable needs than pay-as-you-go billing. Moreover, the longer a service is purchased, the less it costs. |
| Pay-as-you-go                                                     | MySQL | [Postpaid](https://intl.cloud.tencent.com/document/product/555/30328). You can apply for resources for on-demand use and will be charged based on the actual usage of resources upon settlement. | It is suitable for businesses that may fluctuate greatly and instantaneously. In this mode, instances can be released immediately after use to save costs. |
| [Serverless](https://intl.cloud.tencent.com/document/product/1098/40618) | MySQL             | [Postpaid](https://intl.cloud.tencent.com/document/product/555/30328). You can set the maximum and minimum computing power values as needed first, but you will be charged based on the actual usage of computing and storage resources upon settlement. | It is suitable for business scenarios with low frequency and uncertain load such as development and testing. <dx-alert infotype="explain" title="Description">A serverless instance will start with the minimum CPU specification during initialization and will be downgraded if there are no requests in ten minutes after startup. Therefore, even if you don't use the instance after purchasing it, compute node fees will be charged for ten minutes.</dx-alert> |

## Billing
**Total monthly subscription/pay-as-you-go fees = compute node fees + storage space fees = compute node price * number of compute nodes + storage space price * storage space**

**Total serverless fees = compute node fees + storage space fees = serverless computing power price * number of CCUs + storage space price * storage space**

TDSQL-C for MySQL adopts a computing-storage separation architecture. It is sold by cluster, and the compute nodes and storage space of each cluster are billed separately:

- Compute node fees are charged in the corresponding billing mode (monthly subscription or pay-as-you-go) based on the specification you purchase.
- Storage space fees are charged in your selected billing mode: monthly subscription (prepaid storage space) or pay-as-you-go (postpaid by hourly storage space usage).
>?Only TDSQL-C for MySQL supports **the purchase of monthly-subscribed storage space** under the premise that you select the **monthly subscription** billing mode.
>


## [Product Specifications](id:cpgg)

<table>
<thead><tr>
<th rowspan=2 >Compute Node Specification<br>(CPU and Memory)</th>
<th colspan = "2" style="text-align:center" width="50%">Supported Max Storage Space (GB)</th>
<th rowspan=2 >Max IOPS</th>
<th rowspan=2 >I/O Bandwidth</th></tr>
<tr>
<th>MySQL 5.7 kernel minor version &lt; 2.0.15<br>MySQL 8.0 kernel minor version &lt; 3.1.2</th><th>MySQL 5.7 kernel minor version ≥ 2.0.15<br>MySQL 8.0 kernel minor version ≥ 3.1.2</th></tr>
</thead><tbody>
<tr>
<td>1-core 1 GB MEM</td>
<td>1,000</td><td>3,000</td><td>8,000</td><td>1 Gbps</td></tr>
<tr>
<td>1-core 2 GB MEM</td>
<td>1,000</td><td>3,000</td><td>8,000</td><td>1 Gbps</td></tr>
<tr>
<td>2-core 4 GB MEM</td>
<td>5,000</td><td>10,000</td><td>48,000</td><td>6 Gbps</td></tr>
<tr>
<td>2-core 8 GB MEM</td>
<td>5,000</td><td>10,000</td><td>48,000</td><td>6 Gbps</td></tr>
<tr>
<td>2-core 16 GB MEM</td>
<td>5,000</td><td>10,000</td><td>48,000</td><td>6 Gbps</td></tr>
<tr>
<td>4-core 8 GB MEM</td>
<td>10,000</td><td>30,000</td><td>96,000</td><td>12 Gbps</td></tr>
<tr>
<td>4-core 16 GB MEM</td>
<td>10,000</td><td>30,000</td><td>96,000</td><td>12 Gbps</td></tr>
<tr>
<td>4-core 24 GB MEM</td>
<td>10,000</td><td>30,000</td><td>96,000</td><td>12 Gbps</td></tr>
<tr>
<td>4-core 32 GB MEM</td>
<td>10,000</td><td>30,000</td><td>96,000</td><td>12 Gbps</td></tr>
<tr>
<td>8-core 16 GB MEM</td>
<td>10,000</td><td>50,000</td><td>216,000</td><td>27 Gbps</td></tr>
<tr>
<td>8-core 32 GB MEM</td>
<td>10,000</td><td>50,000</td><td>216,000</td><td>27 Gbps</td></tr>
<tr>
<td>8-core 48 GB MEM</td>
<td>10,000</td><td>50,000</td><td>216,000</td><td>27 Gbps</td></tr>
<tr>
<td>8-core 64 GB MEM</td>
<td>10,000</td><td>50,000</td><td>216,000</td><td>27 Gbps</td></tr>
<tr>
<td>12-core 48 GB MEM</td>
<td>10,000</td><td>80,000</td><td>288,000</td><td>36 Gbps</td></tr>
<tr>
<td>12-core 72 GB MEM</td>
<td>10,000</td><td>80,000</td><td>288,000</td><td>36 Gbps</td></tr>
<tr>
<td>12-core 96 GB MEM</td>
<td>10,000</td><td>80,000</td><td>288,000</td><td>36 Gbps</td></tr>
<tr>
<td>16-core 64 GB MEM</td>
<td>20,000</td><td>100,000</td><td>384,000</td><td>48 Gbps</td></tr>
<tr>
<td>16-core 96 GB MEM</td>
<td>20,000</td><td>100,000</td><td>384,000</td><td>48 Gbps</td></tr>
<tr>
<td>16-core 128 GB MEM</td>
<td>20,000</td><td>100,000</td><td>384,000</td><td>48 Gbps</td></tr>
<tr>
<td>24-core 96 GB MEM</td>
<td>20,000</td><td>150,000</td><td>480,000</td><td>60 Gbps</td></tr>
<tr>
<td>24-core 144 GB MEM</td>
<td>20,000</td><td>150,000</td><td>480,000</td><td>60 Gbps</td></tr>
<tr>
<td>24-core 192 GB MEM</td>
<td>20,000</td><td>150,000</td><td>480,000</td><td>60 Gbps</td></tr>
<tr>
<td>32-core 128 GB MEM</td>
<td>50,000</td><td>200,000</td><td>576,000</td><td>72 Gbps</td></tr>
<tr>
<td>32-core 192 GB MEM</td>
<td>50,000</td><td>200,000</td><td>576,000</td><td>72 Gbps</td></tr>
<tr>
<td>32-core 256 GB MEM</td>
<td>50,000</td><td>200,000</td><td>576,000</td><td>72 Gbps</td></tr>
<tr>
<td>48-core 192 GB MEM</td>
<td>50,000</td><td>300,000</td><td>648,000</td><td>81 Gbps</td></tr>
<tr>
<td>48-core 288 GB MEM</td>
<td>50,000</td><td>300,000</td><td>648,000</td><td>81 Gbps</td></tr>
<tr>
<td>48-core 384 GB MEM</td>
<td>50,000</td><td>300,000</td><td>648,000</td><td>81 Gbps</td></tr>
<tr>
<td>48-core 488 GB MEM</td>
<td>50,000</td><td>300,000</td><td>648,000</td><td>81 Gbps</td></tr>
<tr>
<td>64-core 256 GB MEM</td>
<td>50,000</td><td>400,000</td><td>720,000</td><td>90 Gbps</td></tr>
<tr>
<td>64-core 384 GB MEM</td>
<td>50,000</td><td>400,000</td><td>720,000</td><td>90 Gbps</td></tr>
<tr>
<td>64-core 512 GB MEM</td>
<td>50,000</td><td>400,000</td><td>720,000</td><td>90 Gbps</td></tr>
<tr>
<td>88-core 710 GB MEM</td>
<td>50,000</td><td>400,000</td><td>780,000</td><td>98 Gbps</td></tr>
</tbody></table>		

## Compute Node Pricing
<table>
<thead><tr>
<th rowspan=2 >Compute Node Specification</th>
<th colspan=2>Guangzhou, Shanghai, Beijing, and Nanjing</th><th colspan=2>Hong Kong (China)</th><th colspan=2>Silicon Valley and Frankfurt</th><th colspan=2>Singapore</th><th colspan=2>Tokyo</th></tr>
<tr>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
</tr></thead>
<tbody><tr>
<td>1-core 1 GB MEM</td>
<td>0.04</td><td>8.82</td><td>0.07</td><td>31.32</td><td>0.07</td><td>32.74</td><td>-</td><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td>1-core 2 GB MEM</td>
<td>0.05</td><td>13.24</td><td>0.08</td><td>40.15</td><td>0.09</td><td>42</td><td>-</td><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td>2-core 4 GB MEM</td>
<td>0.1</td><td>48</td><td>0.17</td><td>80.29</td><td>0.17</td><td>84</td><td>0.17</td><td>83.21</td><td>0.13</td><td>62.4</td></tr>
<tr>
<td>2-core 8 GB MEM</td>
<td>0.14</td><td>69.18</td><td>0.24</td><td>115.59</td><td>0.25</td><td>121.06</td><td>0.25</td><td>120.26</td><td>0.19</td><td>89.93</td></tr>
<tr>
<td>2-core 16 GB MEM</td>
<td>0.23</td><td>111.53</td><td>0.39</td><td>186.18</td><td>0.41</td><td>195.18</td><td>0.4</td><td>194.38</td><td>0.3</td><td>144.99</td></tr>
<tr>
<td>4-core 8 GB MEM</td>
<td>0.2</td><td>96</td><td>0.33</td><td>160.59</td><td>0.35</td><td>168</td><td>0.35</td><td>166.41</td><td>0.26</td><td>124.8</td></tr>
<tr>
<td>4-core 16 GB MEM</td>
<td>0.29</td><td>138.35</td><td>0.48</td><td>231.18</td><td>0.5</td><td>242.12</td><td>0.5</td><td>240.53</td><td>0.37</td><td>179.86</td></tr>
<tr>
<td>4-core 24 GB MEM</td>
<td>0.38</td><td>180.71</td><td>0.63</td><td>301.76</td><td>0.66</td><td>316.24</td><td>0.66</td><td>314.65</td><td>0.49</td><td>234.92</td></tr>
<tr>
<td>4-core 32 GB MEM</td>
<td>0.46</td><td>223.06</td><td>0.78</td><td>372.35</td><td>0.81</td><td>390.35</td><td>0.81</td><td>388.76</td><td>0.6</td><td>289.98</td></tr>
<tr>
<td>8-core 16 GB MEM</td>
<td>0.4</td><td>192</td><td>0.67</td><td>321.18</td><td>0.7</td><td>336</td><td>0.69</td><td>332.82</td><td>0.52</td><td>249.6</td></tr>
<tr>
<td>8-core 32 GB MEM</td>
<td>0.58</td><td>276.71</td><td>0.96</td><td>462.35</td><td>1.01</td><td>484.24</td><td>1</td><td>481.06</td><td>0.75</td><td>359.72</td></tr>
<tr>
<td>8-core 48 GB MEM</td>
<td>0.75</td><td>361.41</td><td>1.26</td><td>603.53</td><td>1.32</td><td>632.47</td><td>1.31</td><td>629.29</td><td>0.98</td><td>469.84</td></tr>
<tr>
<td>8-core 64 GB MEM</td>
<td>0.93</td><td>446.12</td><td>1.55</td><td>744.71</td><td>1.63</td><td>780.71</td><td>1.62</td><td>777.53</td><td>1.21</td><td>579.95</td></tr>
<tr>
<td>12-core 48 GB MEM</td>
<td>0.86</td><td>415.06</td><td>1.45</td><td>693.53</td><td>1.51</td><td>726.35</td><td>1.5</td><td>721.59</td><td>1.12</td><td>539.58</td></tr>
<tr>
<td>12-core 72 GB MEM</td>
<td>1.13</td><td>542.12</td><td>1.89</td><td>905.29</td><td>1.98</td><td>948.71</td><td>1.97</td><td>943.94</td><td>1.47</td><td>704.75</td></tr>
<tr>
<td>12-core 96 GB MEM</td>
<td>1.39</td><td>669.18</td><td>2.33</td><td>1117.06</td><td>2.44</td><td>1171.06</td><td>2.43</td><td>1166.29</td><td>1.81</td><td>869.93</td></tr>
<tr>
<td>16-core 64 GB MEM</td>
<td>1.15</td><td>553.41</td><td>1.93</td><td>924.71</td><td>2.02</td><td>968.47</td><td>2</td><td>962.12</td><td>1.5</td><td>719.44</td></tr>
<tr>
<td>16-core 96 GB MEM</td>
<td>1.5</td><td>722.82</td><td>2.52</td><td>1207.06</td><td>2.63</td><td>1264.94</td><td>2.62</td><td>1258.59</td><td>1.96</td><td>939.67</td></tr>
<tr>
<td>16-core 128 GB MEM</td>
<td>1.86</td><td>892.24</td><td>3.1</td><td>1489.41</td><td>3.25</td><td>1561.41</td><td>3.24</td><td>1555.06</td><td>2.42</td><td>1159.91</td></tr>
<tr>
<td>24-core 96 GB MEM</td>
<td>1.73</td><td>830.12</td><td>2.89</td><td>1387.06</td><td>3.03</td><td>1452.71</td><td>3.01</td><td>1443.18</td><td>2.25</td><td>1079.15</td></tr>
<tr>
<td>24-core 144 GB MEM</td>
<td>2.26</td><td>1084.24</td><td>3.77</td><td>1810.59</td><td>3.95</td><td>1897.41</td><td>3.93</td><td>1887.88</td><td>2.94</td><td>1409.51</td></tr>
<tr>
<td>24-core 192 GB MEM</td>
<td>2.79</td><td>1338.35</td><td>4.66</td><td>2234.12</td><td>4.88</td><td>2342.12</td><td>4.86</td><td>2332.59</td><td>3.62</td><td>1739.86</td></tr>
<tr>
<td>32-core 128 GB MEM</td>
<td>2.3</td><td>1106.82</td><td>3.85</td><td>1849.41</td><td>4.03</td><td>1936.94</td><td>4.01</td><td>1924.24</td><td>3</td><td>1438.87</td></tr>
<tr>
<td>32-core 192 GB MEM</td>
<td>3.01</td><td>1445.65</td><td>5.03</td><td>2414.12</td><td>5.27</td><td>2529.88</td><td>5.24</td><td>2517.18</td><td>3.91</td><td>1879.34</td></tr>
<tr>
<td>32-core 256 GB MEM</td>
<td>3.71</td><td>1784.47</td><td>6.21</td><td>2978.82</td><td>-</td><td>-</td><td>6.48</td><td>3110.12</td><td>4.83</td><td>2319.81</td></tr>
<tr>
<td>48-core 192 GB MEM</td>
<td>3.46</td><td>1660.24</td><td>5.78</td><td>2774.12</td><td>6.05</td><td>2905.41</td><td>6.01</td><td>2886.35</td><td>4.49</td><td>2158.31</td></tr>
<tr>
<td>48-core 288 GB MEM</td>
<td>4.51</td><td>2168.47</td><td>7.55</td><td>3621.18</td><td>-</td><td>21235.20</td><td>7.86</td><td>3775.76</td><td>5.87</td><td>2819.01</td></tr>
<tr>
<td>48-core 384 GB MEM</td>
<td>5.57</td><td>2676.71</td><td>9.31</td><td>4468.24</td><td>-</td><td>-</td><td>9.72</td><td>4665.18</td><td>7.25</td><td>3479.72</td></tr>
<tr>
<td>48-core 488 GB MEM</td>
<td>6.72</td><td>3227.29</td><td>11.23</td><td>5385.88</td><td>-</td><td>-</td><td>11.72</td><td>5628.71</td><td>8.74</td><td>4195.48</td></tr>
<tr>
<td>64-core 256 GB MEM</td>
<td>4.61</td><td>2213.65</td><td>7.71</td><td>3698.82</td><td>-</td><td>-</td><td>8.02</td><td>3848.47</td><td>5.99</td><td>2877.74</td></tr>
<tr>
<td>64-core 384 GB MEM</td>
<td>6.02</td><td>2891.29</td><td>10.06</td><td>4828.24</td><td>-</td><td>-</td><td>10.49</td><td>5034.35</td><td>7.83</td><td>3758.68</td></tr>
<tr>
<td>88-core 710 GB MEM</td>
<td>10.28</td><td>4939.06</td><td>-</td><td>-</td><td>-</td><td>-</td><td>17.93</td><td>8608.41</td><td>-</td><td>-</td></tr>
</tbody></table>

## Serverless Computing Power Pricing
<table>
<thead><tr>
<th rowspan=2 >Billable Unit</th>
<th >Guangzhou, Shanghai, Beijing, and Nanjing</th>
<tr>
<th>CCU Price (USD/Unit/Second)</th></tr></thead>
<tbody><tr>
<td>Serverless instance</td>
<td>0.00001397</td></tr>
</tbody></table>

>?
>- CynosDB Compute Unit (CCU) is the computing and billing unit for the Serverless Edition. A CCU is approximately equal to 1 CPU core and 2 GB memory. The number of CCUs used in each billing cycle is the greater value between the number of CPU cores used by the database and 1/2 of the memory size.
>- You can refer to [product specifications](#cpgg) to select the corresponding maximum and minimum CCU values. The storage space upper limit is the same as the maximum storage space corresponding to the [common compute node specifications](#cpgg).

## Storage Space Pricing
<table>
<thead><tr>
<th colspan=2>Guangzhou, Shanghai, Beijing, and Nanjing</th><th colspan=2>Hong Kong (China), Taipei (China), Singapore, Silicon Valley, Frankfurt, Tokyo, and Virginia</th></tr>
<tr>
<th>Pay-as-You-Go Price (USD/GB/Hour)</th><th>Monthly Subscription Price (USD/GB/Month)</th>
<th>Pay-as-You-Go Price (USD/GB/Hour)</th><th>Monthly Subscription Price (USD/GB/Month)</th>
</tr></thead>
<tbody><tr>
<td>0.00072</td><td><li>Below 3,000 GB: 0.20541177<br><li>3,000 GB or above: 0.18829412</td>
<td>0.000792</td><td><li>Below 3,000 GB: 0.22447059<br><li>3,000 GB or above: 0.20576471</td></tr>
</tbody></table>

## Fees Calculation Examples
>?Node and storage prices in the examples are for reference only. The specific prices of the configurations on the actual purchase page shall prevail.
#### Monthly subscription
You purchased a 1-core 2 GB MEM TDSQL-C for MySQL cluster that contained one instance in Beijing Zone 3 for one month, and used 10 GB of storage space every day.

Monthly compute node fees = 13.24 USD 
Monthly storage space fees = 0.20541177 USD/GB/month * 10 GB = 2.0541177 USD
Total monthly fees = compute node fees + storage space fees = 13.24 USD + 2.0541177 USD = 15.2947117 USD

#### Pay-as-You-Go
You purchased a 1-core 2 GB MEM TDSQL-C for MySQL cluster that contained one instance in Beijing Zone 3, and used 10 GB of storage space every day.

Daily compute node fees = 0.05 USD/hour * 24 hours = 1.2 USD
Daily storage space fees = 0.00072 USD/GB/hour * 10 GB * 24 hours = 0.1728 USD
Total daily fees = compute node fees + storage space fees = 1.2 USD + 0.1728 USD = 1.3728 USD

#### Serverless billing
You purchased a serverless database with a minimum computing specification of 0.25 CCU/s and a maximum computing specification of 2 CCU/s in Beijing Zone 3, and used 10 GB of storage space all day and an average of 1.5 CCU/s in one hour every day.

Daily compute node fees = 1.5 * 3600 seconds * 0.00001397 USD/unit/second = 0.075438 USD
Daily storage space fees = 0.00072 USD/GB/hour * 10 GB * 24 hours = 0.1728 USD
Total daily fees = compute node fees + storage space fees = 0.075438 USD + 0.1728 USD = 0.248238 USD

