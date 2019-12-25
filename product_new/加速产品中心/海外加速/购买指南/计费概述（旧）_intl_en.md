> Starting January 1, 2020, 00:00, the Global Content Delivery(GCD) billing method will be upgraded from monthly pay-as-you-go to daily pay-as-you-go with fees billed by traffic by default. This document describes the old billing method which is scheduled to cease to have effect as from the end of December, 2019.

Global Content Delivery (GCD) offers two **pay-as-you-go** billing plans when in beta: **bill-by-bandwidth** and **bill-by-traffic**. Both are based on **[monthly tiered usage](https://intl.cloud.tencent.com/document/product/1014/33472#shili)**, and the current calendar month total usage will be billed on the 1st day of the following month at 12 pm.

## Billing Regions
GCD has eight billing regions: Asia Pacific Region 1, Asia Pacific Region 2, Asia Pacific Region 3, Middle East Region, Europe Region, North America Region, South America Region, and Africa Region.
- Asia Pacific Region 1: Hong Kong (China), Macao (China), Singapore, Vietnam, Thailand
- Asia Pacific Region 2: Taiwan, China, Japan, Malaysia, Indonesia, South Korea
- Asia Pacific Region 3: The Philippines, India, Australia, and other Asia Pacific countries and regions

>
- Billing region is determined by the location of Tencent Cloud CDN node server.
- Each region's CDN fee is calculated separately according to applicable unit price and usage.

## Billing Plans
### Bill-by-bandwidth
Bill-by-bandwidth uses the **monthly 95th percentile** billing method, so you are billed by the monthly 95th percentile bandwidth and on a tiered basis.
- **Monthly 95th Percentile bandwidth**
In the monthly 95th percentile bandwidth billing method, there are 288 CDN bandwidth statistical points per day. Starting from the 1st day of the current month, all statistical points of valid days (when bandwidth is actually consumed) are sorted in order. The first 5% points are removed, and the remaining highest value is the billable bandwidth. The fee is then calculated based on the listing price and settlement method.

Example:
1. Suppose a customer's billing officially started on February 1, 2018, and the monthly bill-by-bandwidth unit price is USDP/Mbps/month.
2. A valid day refers to a day when more than 1 Kbps of bandwidth is consumed.
3. Assuming there are 14 days in February with over 1 Kbps bandwidth, the billable bandwidth for all 14 days has 14 \* 288 statistical points, and the highest 5% points are removed, the highest remaining point is the Max95, which is the billable bandwidth. So the February fee is: Max95 \* P \* 14/28 (P is subject to the actual tier, billable bandwidth in different tiers are billed according to the corresponding unit price).
- **Tiered price**
The pricing is as shown in the table below. **All the monthly unit prices is based on 30 days (daily unit price \* 30)**.

| Bandwidth tier <br/>(USD/Mbps/day) | North America - NA | Europe - EU | Asia Pacific Region 1 - AP1 | Asia Pacific Region 2 - AP2 | Asia Pacific Region 3 - AP3 | Middle East - ME | Africa - AA | South America - SA |
|----------------------------------|-----------|------------|-------------------|---------------------|--------------|-------------|--|--|
|0 Mbps - 500 Mbps (inclusive)|0.2941|0.2941|0.4412|0.5882|0.6471|0.8529|0.6471|0.6471|
|500 Mbps - 5 Gbps (inclusive)|0.2471|0.2471|0.3882|0.5294|0.5941|0.7824|0.5941|0.5941|
|5 Gbps - 50 Gbps (inclusive)|0.1824|0.1824|0.3412|0.4706|0.5471|0.7059|0.5471|0.5471|
|Over 50 Gbps |0.1294|0.1294|0.2941|0.4118|0.5|0.6176|0.5|0.5|

### Bill-by-traffic
For the **monthly bill-by-traffic** billing plan, you are billed by the monthly traffic on a tiered basis.
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
If you have already spent or expect to spend over USD 20,000 per month on Tencent Cloud, you may be eligible for favorable pricing and flexible billing methods. For more information, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=83&level2_id=85&level1_name=%E5%AD%98%E5%82%A8%E4%B8%8ECDN&level2_name=%E5%86%85%E5%AE%B9%E5%88%86%E5%8F%91%E7%BD%91%E7%BB%9C%20%20CDN).

## Choosing a Billing Plan
- CDN offers two billing plans: **bill-by-bandwidth** and **bill-by-traffic**, and you can choose a plan based on your business needs or bandwidth utilization.
+ If your bandwidth utilization is over 50%, your business is relatively stable. We recommend bill-by-bandwidth.
 + Otherwise, the bill-by-traffic plan is more suitable.

- Below is an example of bandwidth utilization calculation:
- Suppose the traffic consumed by your business between 00:00 and 24:00 yesterday was 200 GB. The graph below shows the traffic curve, and the consumed traffic is the area occupied by the curve.
 ![](https://mc.qcloudimg.com/static/img/3ecfe86a031782ebeaf0b1f7595cc69f/image.png)
- Suppose that your bandwidth peak between 00:00 and 24:00 yesterday was 40 Mbps, as there are 86,400 seconds per day, the traffic for one day is 40 \* 1000 \* 1000 \* 86400 bit (equivalent to 432 GB), which can be seen as the area occupied by the rectangle in the graph:
 ![](https://mc.qcloudimg.com/static/img/b80d043b6e7f461d62fd2d87abf67005/image.png)
- Therefore, the bandwidth utilization is: 200 GB / 432 GB \* 100% = 46%.

 <span id='shili'></span>
## Billing Example
Bill-by-traffic and bill-by-bandwidth are both billed on a monthly tiered basis. Take bill-by-traffic as an example.
Suppose there are 14 days in February with over 1 Kbps bandwidth, the billable bandwidth for all 14 days has 14 \* 288 statistical points, and the highest 5% points are removed, The highest remaining point is the Max95, which is the billable bandwidth. 

Therefore, the February fee is: Max95 \* P \* 14/28 (P is subject to the actual tier, billable bandwidth in different tiers are billed according to the corresponding unit price).
