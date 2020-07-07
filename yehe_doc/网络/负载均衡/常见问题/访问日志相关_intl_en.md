### How do I change the access log storage location from COS to CLS?
Please [configure access log storage in CLS](https://intl.cloud.tencent.com/document/product/214/35063) first and then disable [access log storage in COS](https://intl.cloud.tencent.com/document/product/214/10329), as the feature of storing access logs in COS will be officially deactivated after 00:00:00, June 30, 2020, and access logs cannot be directly written to COS after then.

### What is the difference between storing access logs in CLS and COS?
Compared to storing access logs in COS, storing access logs in CLS can provide:
- Real-time logging at a minute-level granularity and diversified online search based on full-text, key-value, and fuzzy keywords.
- Multi-region coverage and other capabilities, making it more suitable for large-scale use in production environments.

For detailed comparison, please see [Access Log Overview](https://intl.cloud.tencent.com/document/product/214/34893).

### Is it possible to store access logs in both COS and CLS?
It is possible to store access logs in both COS and CLS:
- Before the feature of storing access logs in COS is officially deactivated (i.e., before 23:59:59, May 31, 2020), existing access logs stored in COS will not be affected, and access logs will be written to CLS and COS at the same time.
- After the feature of storing access logs in COS is officially deactivated at 00:00:00, June 30, 2020, new access logs cannot be directly written to COS, and existing access logs in COS remain.

After storing access logs in CLS, certain CLS features can be used to store logs in COS. For example, latest logs (generated in the last 3 days) can be stored in CLS for easy query, while historical logs (generated more than 3 days ago) can be transferred to COS from CLS. For more information, please see [CLS - Shipping Overview](https://intl.cloud.tencent.com/document/product/614/32940).

### Will more fees be incurred by using CLS?
The access log service for CLB is free of charge. You only need to pay [CLS](https://intl.cloud.tencent.com/document/product/614) or [COS](https://intl.cloud.tencent.com/document/product/436) fees.
