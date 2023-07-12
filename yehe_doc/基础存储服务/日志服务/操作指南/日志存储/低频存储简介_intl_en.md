CLS STANDARD_IA is a low-cost log storage solution to search for and store massive numbers of infrequently accessed logs. It applies to scenarios where users don't require statistical analysis and logs need to be stored for a long time. STANDARD_IA provides full-text search, context search, shipping to COS, shipping to CKafka, and log consumption capabilities, meeting user requirements for backtracking and archiving historical logs. STANDARD_IA doesn't support SQL analysis, monitoring alarm, and dashboard features.

>! Currently, STANDARD_IA log storage is available only in Beijing, Guangzhou, Shanghai, Hong Kong (China), Nanjing, Singapore, Silicon Valley, and Frankfurt regions. If it is not supported in the region of your log topic, contact [smart customer service](https://intl.cloud.tencent.com/contact-sales) for application.
>


## Advantages

- **Low cost:** Charges only log write traffic and storage fees, resulting in a total cost 73% lower than that of **CLS - STANDARD** storage.
- **Ease of use:** Compatible with the search syntax of Lucene, eliminating the cost for extra learning; allows users to search for data without configuring indexes.
- **Stability and reliability:** Provides a brand-new proprietary log system with separated computing and storage, supporting scale-out, high availability, and flexibility of use.


## Use cases

| Scenario         | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| Long-term storage | In audit/security log scenarios, long-term storage with STANDARD_IA can reduce fees by more than 80% compared with STANDARD. |
| Simple use | In scenarios that don't require frequent statistical analysis of data, such as Ops log analysis, the advanced features of dashboard and monitoring alarm are not needed. |



## Directions

1. Create a log topic and set **Storage Class** to **STANDARD_IA**. For more information, see [Managing Log Topic](https://intl.cloud.tencent.com/document/product/614/34239).

2. Collect logs to the target topic. For more information, see [Collection Overview](https://intl.cloud.tencent.com/document/product/614/31652).
3. Go to the target log topic search page and enter the full-text search statement, such as `a AND b NOT c`.
4. Click **Search and Analysis** to view the search result.




## STANDARD_IA and STANDARD feature comparison

| Feature       | STANDARD_IA            | STANDARD |
| ------------ | ------------------- | -------- |
| Index creation     | ✓ (supports only full-text indexes) | ✓        |
| Context search   | ✓                   | ✓        |
| Quick analysis     | ×                   | ✓        |
| Full-text search     | ✓ (responds in 2 seconds for searches in 100 million records)                   | ✓ (responds in 0.5 second for searches in 100 million records)        |
| Key-value search     | ×                   | ✓       |
| Log download     | ✓                   | ✓       |
| SQL analysis      | ×                   | ✓        |
| Dashboard       | ×                   | ✓       |
| Monitoring alarm     | ×                   | ✓        |
| Shipping to COS    | ✓                   | ✓        |
| Shipping to CKafka | ✓                   | ✓        |
| Shipping to ES     | ✓                   | ✓       |
| Shipping to SCF    | ✓                   | ✓        |
| Log consumption     | ✓                   | ✓        |
| Data processing     | ✓                   | ✓        |




