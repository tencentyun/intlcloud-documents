## Billing overview
**Intra-region** peering connections are **free of charge**, and you will be charged for **cross-region** peering connections in the following pay-as-you-go modes:
- Billing by daily peak bandwidth: settlement is performed based on the peak inbound or outbound bandwidth on a day.
- Billing by monthly 95th percentile: settlement is performed based on the top 5 peak inbound and outbound bandwidth values in a month. (This billing mode is not yet open to all users. To use this mode, please [submit a ticket](https://cloud.tencent.com/apply/p/clg22aj1t6n).)
>! The cost of a cross-region or cross-account peering connection is paid by the initiator of the peering connection (not the actual communication requester).

## Billing modes

### Billing by daily peak bandwidth
Settlement is performed based on the daily peak inbound/outbound bandwidth.
- **Calculation formula**: Daily cost = Peak bandwidth of the current day \* Tiered unit price of the bandwidth.
   - Peak bandwidth of the current day: maximum inbound or outbound bandwidth of the current day, which is acquired every 5 minutes.
   - Tiered unit price: the unit price at the tiered interval into which the peak bandwidth of the current day falls.
   
- Tiered prices for billing by daily peak bandwidth

<table align=“center”>
 <tr>
 <th><center>计费项</center> </th>
 <th><center>计费区间（Mbps）</center> </th>
 <th><center>中国大陆（不含港澳台地区）地域间互通价格（USD/Mbps/天）</center> </th>
 </tr>
 <tr>
 <td rowspan=5><center>跨地域对等连接</center> </td>
 <td><center>(0,20] </td>
 <td><center>20 </center></td>
 </tr>
 <tr>
 <td><center>(20,100]</center> </td>
 <td><center>12</center> </td>
 </tr>
 <tr>
 <td><center>(100,500]</center> </td>
 <td><center>9 </center></td>
 </tr>
 <tr>
 <td><center>(500,2000]</center> </td>
 <td><center>7</center> </td>
 </tr>
 <tr>
 <td><center>> 2000 </center></td>
 <td><center>5</center> </td>
 </tr>
 </table>


>
- For prices of connections between regions outside Mainland China, consult your business manager.
 

- **Example of billing by daily peak bandwidth**
Assume that the initiator of a peering connection is in Shanghai, the acceptor is in Guangzhou, the peak outbound bandwidth on the current day is 20 Mbps, and peak inbound bandwidth on the current day is 30 Mbps. In this case, 30 Mbps is considered as the peak bandwidth on the current day. If the tiered unit price of the bandwidth is 1.98 USD/Mbps per day, the daily cost is: 30 × 1.98 = 59.4 USD, which is paid by the initiator.

 <span id=yjf> </span>

### Billing by monthly 95th percentile
Settlement is performed based on the top 5 peak inbound and outbound bandwidth values of the current month. (This billing mode is not yet open to all users. To use this mode, please [submit a ticket](https://cloud.tencent.com/apply/p/clg22aj1t6n).)

- **Calculation formula**: Monthly cost = Monthly 95th percentile of peak bandwidth for cross-region peering connections \* Ratio of valid days \* Tiered unit price.
   - Monthly 95th percentile of peak bandwidth: acquired every 5 minutes. The average bandwidth for a cross-region peering connection within 5 minutes is taken as a sample point. All sample points of the current month are sorted in descending order, the top 5% of the sample points are removed, and the highest value of the remaining sample points is used as the monthly 95th percentile of peak bandwidth.
**Example**: a customer used a peering connection in June, and the customer used the cross-region connection between regions A and B for 14 valid days. Because one sample point is generated every 5 minutes, 288 (60 min × 24/5 min) sample points are generated every day, and 4032 (14 days × 288 sample points/day) sample points are generated in 14 days. The bandwidth values of the 4032 sample points are sorted in descending order, the top 5% of the sample points (4032 sample points × 0.05 = 201.6 statistical points) are removed, and the bandwidth value of the 202nd sample point is taken as the monthly 95th percentile of peak bandwidth.
   - Ratio of valid days: valid days in which the bandwidth value of at least one sample point is higher than 10 Kbps.
Ratio of valid days = Valid days of the current month/Days of the current calendar month.
   - Tiered unit price: the unit price at the tiered interval into which the monthly 95th percentile of peak bandwidth falls.

- Tiered prices for billing by monthly 95th percentile

<table align=“center”>
 <tr>
 <th><center>计费项 </center></th>
 <th><center>计费区间（Mbps） </center></th>
 <th><center>中国大陆（不含港澳台地区）地域间互通（USD/Mbps/月） </center></th>
 </tr>
 <tr>
 <td rowspan=9><center>跨地域带宽 </center></td>
 <td><center>(0,10] </center></td>
 <td><center>550</center> </td>
 </tr>
 <tr>
 <td><center>(10,20]</center> </td>
 <td><center>410</center> </td>
 </tr>
 <tr>
 <td><center>(20,50]</center> </td>
 <td><center>290</center> </td>
 </tr>
 <tr>
 <td><center>(50,100]</center> </td>
 <td><center>220</center> </td>
 </tr>
 <tr>
 <td><center>(100,200] </center></td>
 <td><center>165</center> </td>
 </tr>
 <tr>
 <td><center>(200,500] </center></td>
 <td><center>115</center> </td>
 </tr>
 <tr>
 <td><center>(500,1000]</center> </td>
 <td><center>88</center> </td>
 </tr>
 <tr>
 <td><center>(1000,2000] </center></td>
 <td><center>69</center> </td>
 </tr>
 <tr>
 <td><center>> 2000</center> </td>
 <td><center>65</center> </td>
 </tr>
 </table>

>! For prices of connections between regions outside Mainland China, consult your business manager.

- **Example of billing by monthly 95th percentile**
A customer used a cross-region peering connection in June and consumed bandwidth that exceeded 10 Kbps for 14 valid days. In this case, 
   - Ratio of valid days: 14/30.
   - Tiered unit price: 24 USD/Mbps per month, which is the unit price at the tiered interval into which 120 Mbps falls.
  

Cost of June = Max95 \* Ratio of valid days \* Tiered unit price = 60 \* (14/30) \* 24 = 672 USD.
