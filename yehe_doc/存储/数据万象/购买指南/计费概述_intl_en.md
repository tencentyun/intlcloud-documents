## Billing Mode

CI is pay-as-you-go (postpaid).

Fees are charged by the **actual usage**. Amounts are deducted and the bill for the previous month is generated on the first day of each month. When you start using CI, you will be charged on a pay-as-you-go basis by default, so you do not need to purchase it.



## Pricing

For CI pricing details, see [Pricing | Cloud Infinite](https://buy.cloud.tencent.com/price/ci).

As CI uses the data storage service of COS, the storage fees will be listed on COS bills. For more information, see [Pricing | Cloud Object Storage](https://buy.cloud.tencent.com/price/cos).



## Amount Freezing Mechanism

After the bill for the current month is settled, 120% of its amount will be frozen for the next month. During settlement the next month, this frozen amount will be unfrozen first for deduction.



## Billable Items

CI billable items include image processing, media processing, file processing, and traffic.

**Billing cycle**

The billing cycles and sequence of CI billable items are as detailed below:

| Billable Item       |                      | Billing Cycle | Description                          | Billing Sequence                                                     |
| :----------- | :------------------- | :------- | :------------------------------------ | ------------------------------------------------- |
| Image processing | Basic image processing fees     | Monthly       | Amounts are deducted and the bill for the previous month is generated on the first day of each month. | Free tier > pay-as-you-go, or only pay-as-you-go in case of no free tier |
|              | Image advanced compression fees     |          |                                       |                                                              |
|              | Guetzli image compression fees |          |                                       |                                                              |
|              | Blind watermark fees           |          |                                       |                                                              |
| Media processing | Audio/Video transcoding fees       | Monthly       |                                       |                                                              |
|              | Top speed codec transcoding fees     |          |                                       |                                                              |
|              | Video montage fees         |          |                                       |                                                              |
|              | Video enhancement fees         |          |                                       |                                                              |
|              | Super resolution fees         |          |                                       |                                                              |
|              | SDR-to-HDR fees      |          |                                       |                                                              |
|              | Voice/Sound separation fees         |          |                                       |                                                              |
|              | Video tagging fees         |          |                                       |                                                              |
|              | Video metadata acquisition fees  |          |                                       |                                                              |
|              | Digital watermark fees         |          |                                       |                                                              |
|              | Video frame capturing fees         |          |                                       |                                                              |
|              | Intelligent thumbnail fees         |          |                                       |                                                              |
|              | Text-to-speech fees         |          |                                       |                                                              |
|              | Audio noise cancellation fees         |          |                                       |                                                              |
|              | Video quality scoring fees     |          |                                       |                                                   |
| File processing | File-to-image conversion fees       | Monthly       |                                       |                                                              |
|              | File-to-HTML conversion fees     |          |                                       |                                                              |
|              | Privacy protection fees     |          |                                       |                                                              |
| Traffic     | CDN origin-pull traffic fees         | Monthly       |                                       |                                                              |
|              | Public network outbound traffic fees           |          |                                       |                                                              |



## References

1. Currently, CI offers free tiers for various features such as image processing, media processing, and file processing. For more information, see [Free Tier](https://www.tencentcloud.com/document/product/1045/49594). For feature or discount details, [contact us](https://intl.cloud.tencent.com/contact-us).

2. For more information on the COS overdue payment policy (data retention and termination), see [Payment Overdue](https://www.tencentcloud.com/zh/document/product/436/10044).

   