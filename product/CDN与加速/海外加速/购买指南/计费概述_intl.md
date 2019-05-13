There are two types of **pay-as-you-go** billing methods of Global Content Delivery (GCD) during GCD's beta test: **bill-by-bandwidth** and **bill-by-traffic**. Both are based on **[monthly tiered usage](#shili)**, and the total current calendar month incurred usage will be billed on the 1st day of the following month at 12 pm.

## Billing Regions
GCD has eight billing regions: Asia Pacific Region 1, Asia Pacific Region 2, Asia Pacific Region 3, Middle East Region, Europe Region, North America Region, South America Region, and Africa Region.
- Asia Pacific Region 1: Hong Kong, Macao, Singapore, Vietnam, Thailand
- Asia Pacific Region 2: Taiwan, Japan, Malaysia, Indonesia, South Korea
- Asia Pacific Region 3: The Philippines, India, Australia, and other Asia Pacific countries and regions

>
- Billing region is determined by the location of Tencent Cloud CDN node server.
- Each region's CDN fee is calculated separately according to applicable unit price and usage.

## Billing Methods
### Bill-by-bandwidth
For **monthly 95th percentile** billing method, you are billed the by the monthly 95th percentile bandwidth on a tiered basis.
- **Monthly 95th Percentile bandwidth**
In the monthly 95th percentile bandwidth billing method, there are 288 CDN bandwidth statistical points per day. Starting from the 1st day of the current month, all statistical points of valid days (when bandwidth is actually consumed) are sorted in order. The first 5% points are removed, and the remaining highest value is the billable bandwidth. The fee is then calculated based on the listing price and settlement method.

Example:
1. Suppose a customer officially started on February 1, 2018, and the monthly bill-by-bandwidth unit price is USDP/Mbps/month.
2. Valid day refers to a day when more than 1 Kbps of bandwidth is consumed.
3. Assuming there are 14 days in February with over 1 Kbps bandwidth, the billable bandwidth for all 14 days has 14 \* 288 statistical points, and the highest 5% points are removed, The highest remaining point is the Max95, which is the billable bandwidth. So the February fee is: Max95 \* P \* 14/28 (P is subject to the actual tier, and the parts of the billable bandwidth falling into different tiers are billed based on the corresponding unit price).
- **Tiered price**
The pricing is as shown in the table below. **All the monthly unit prices is based on 30 days (daily unit price \* 30)**.

| Bandwidth tier <br/>(USD/Mbps/day) | North America - NA | Europe - EU | Asia Pacific Region 1 - AP1 | Asia Pacific Region 2 - AP2 | Asia Pacific Region 3 - AP3 | Middle East - ME | Africa - AA | South America - SA |
|----------------------------------|-----------|------------|-------------------|---------------------|--------------|-------------|--|--|
|0 Mbps - 500 Mbps (inclusive)|0.2941|0.2941|0.4412|0.5882|0.6471|0.8529|0.6471|0.6471|
|500 Mbps - 5 Gbps (inclusive)|0.2471|0.2471|0.3882|0.5294|0.5941|0.7824|0.5941|0.5941|
|5 Gbps - 50 Gbps (inclusive)|0.1824|0.1824|0.3412|0.4706|0.5471|0.7059|0.5471|0.5471|
|Over 50 Gbps |0.1294|0.1294|0.2941|0.4118|0.5|0.6176|0.5|0.5|

### Bill-by-traffic
For the **monthly bill-by-traffic** billing method, you are billed by the monthly traffic on a tiered basis.
- **Monthly traffic**
The monthly fee is calculated by the total traffic consumed in the current month based on the listed price and settlement method.
- **Tiered price**
The prices are as shown in the table below:

| Traffic tier <br/>(USD/GB) | North America - NA | Europe - EU | Asia Pacific Region 1 - AP1 | Asia Pacific Region 2 - AP2 | Asia Pacific Region 3 - AP3 | Middle East - ME | Africa - AA | South America - SA |
|---------------------------|---------------|------------|-----------|----------|-----------|-----------|-----------|-----------|
|0 TB - 2 TB (inclusive)|0.0547|0.0547|0.0812|0.1094|0.12|0.1588|0.12|0.12|
|2 TB - 10 TB (inclusive)|0.0459|0.0459|0.0724|0.1024|0.1129|0.1465|0.1129|0.1129|
|10 TB - 50 TB (inclusive)|0.0388|0.0388|0.0653|0.0935|0.1059|0.1359|0.1059|0.1059|
|50 TB - 100 TB (inclusive)|0.0318|0.0318|0.0582|0.0847|0.0988|0.1253|0.0988|0.0988|
|Over 100 TB|0.0247|0.0247| 0.0547        |0.0759|0.0918|0.1147|0.0918|0.0918|

### Quantity Discount
If you have already spent or expect to spend over USD20,000 per month in Tencent Cloud, you can apply for more favorable prices and more flexible billing methods through business negotiation. For more information, [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=83&level2_id=85&level1_name=%E5%AD%98%E5%82%A8%E4%B8%8ECDN&level2_name=%E5%86%85%E5%AE%B9%E5%88%86%E5%8F%91%E7%BD%91%E7%BB%9C%20%20CDN).

## Choice of Billing Method
- CDN provides two billing methods, i.e., **bill-by-bandwidth** and **bill-by-traffic**, and you can choose the appropriate one according to your business formats or bandwidth utilization:
+ If your bandwidth utilization is over 50%, your business is relatively stable, and the bill-by-bandwidth method is recommended.
 + Otherwise, the bill-by-traffic method is more suitable.

- Below is an example of bandwidth utilization calculation:
- Assuming that the traffic consumed by your business between 00:00 and 24:00 yesterday was 200 GB, the graph below shows your business curve, where the traffic usage can be seen as the area occupied by the curve in the graph:
 ![](https://mc.qcloudimg.com/static/img/3ecfe86a031782ebeaf0b1f7595cc69f/image.png)
- Assuming that your bandwidth peak between 00:00 and 24:00 yesterday was 40 Mbps, as there are 86,400 seconds per day, the traffic for one day is 40 \* 1000 \* 1000 \* 86400bit (equivalent to 432 GB), which can be seen as the area occupied by the rectangle in the graph:
 ![](https://mc.qcloudimg.com/static/img/b80d043b6e7f461d62fd2d87abf67005/image.png)
- The bandwidth utilization is: 200 GB / 432 GB \* 100% = 46%.

 <span id='shili'></span>
## Billing Example
Both bill-by-traffic and bill-by-bandwidth are on a monthly tiered basis. Bill-by-traffic is used as an example below:
If 20 TB of traffic is consumed in the North America in January,
Then:
The first 2 TB falls into the 0 TB - 2 TB billing tier, the next 8 TB falls into the 2 TB - 10 TB billing tier, and the last 10 TB falls into the 10 TB - 50 TB billing tier.
Then:
The actual fee for the North America Region in January is: 2 \* 1000 \* 0.0547 + 8 \* 1000 \* 0.0459 + 10 \* 1000 \* 0.0388.
When the billing starts on February 1, the tiering will be restarted from 0.
