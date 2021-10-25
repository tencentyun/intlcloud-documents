
CLS provides a low-cost offline log storage solution to search and store massive infrequently accessed logs. The solution applies to scenarios where users do not have real-time log search requirements and logs need to be stored for a long time. It provides the minute-level offline log retrieval capability, meeting users' requirements for backtracking and archiving historical logs. Offline log storage does not support real-time log processing features such as monitoring alarms, streaming consumption, and real-time shipping.

>!
> - Currently, the offline log storage solution is in beta testing, and supports only the Beijing, Guangzhou, and Chongqing regions. If the solution is not supported in the region of your log topic, contact [smart customer service](https://intl.cloud.tencent.com/contact-sales) for application.
> - For offline storage in the beta phase, the fees for log write traffic and storage of log topics are exempted.
> 

## Advantages

- **Lost cost:** charges only log write traffic and storage fees, resulting in a total cost 80% lower than that of CLS real-time storage
- **Ease of use:** compatible with the search syntax of Lucene, eliminating the cost for extra learning; allows users to search for data without configuring indexes
- **Stability and reliability:** provides a brand-new proprietary log system with separated computing and storage, supporting scale-out, high availability, and flexibility of use

## Directions

1. Create a log topic and set **Storage Class** to **Offline**. For more information, please see [Managing Log Topic](https://intl.cloud.tencent.com/document/product/614/34239).

2. Collect logs to the target topic. For more information, please see [Collection Methods](https://intl.cloud.tencent.com/document/product/614/12502).
3. Go to the target log topic search page, and enter a search statement, for example, `status: 200`, to create a search task.
>? The search syntax of offline storage is basically consistent with that of real-time storage. For their differences, please see [Collection Methods](https://intl.cloud.tencent.com/document/product/614/12502).
>
4. After the search task is created, click **Offline Tasks** to view the task details.

After the task execution is completed, you can click **View** to view data.



## Use Limits

| Item              | Description                                       |
| -------------------- | -------------------------------- |
| Maximum number of offline search tasks     | 50 tasks per logset               |
| Retention time of offline search results | 24 hours                              |
| Maximum number of results supported by an offline search task | 500                          |
| Context search limits       | Time range: 1 hour earlier and 1 hour later of the specified point in time; maximum number of search results: 100 |


## FAQs

#### How is offline storage charged after beta?

Only log write traffic and storage fees are charged. The log storage volume charged is the original volume of uncompressed logs, and the price is 0.0033 CNY/GB/day.

For example, based on the pricing for the Guangzhou region, if 2 TB raw log data is written per day and data is stored for 30 days, the corresponding fees are as follows:

| Billable Item     | Real-time Storage | Offline Storage        |  Remarks                                        |
| ---------- | -------- | --------------- | ---------------------------------------- |
| Write traffic     | 3,600 CNY     | 3,600 CNY            | Prices for both the storage types: 0.18 CNY/GB/day                     |
| Index traffic   | 21,000 CNY    | 0 CNY               | Real-time storage: 0.35 CNY/GB/day<br />Offline storage: 0 CNY/GB/day  |
| Log storage   | 8,400 CNY    | 6,000 CNY               | Real-time storage: 0.014 CNY/GB/day<br />Offline storage: 0.0033 CNY/GB/day  |
| Index storage   | 25,200 CNY    | 0 CNY               | Real-time storage: 0.014 CNY/GB/day<br />Offline storage: 0 CNY/GB/day  |
| Other fees   | Little     | Little            | Other fees include partition fees and fees for the number of API calls             |
| Total price (month) | 58,280 CNY    | 9,600 CNY (83% lower than that of real-time storage) | -                                        |


#### What are the differences between the search syntax of offline storage and that of real-time storage?

In principle, the search syntax of offline storage is consistent with the Lucene syntax of real-time storage. For more information, please see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439). Offline storage does not support the following syntax:

| Syntax Not Supported by Offline Storage                                         | Example                                                   |
| --------------------------------------------------- | ------------------------------------------------------ |
| Full-text keyword search and key-value search are used simultaneously, and AND and OR operators exist simultaneously | (a OR key1:value1) AND b<br />(a AND key1:value1) OR b |
| `?` for matching a single character                                  | a?                                                     |
| `~` for approximate query                                           | from~                                                  |
| Range query                                            | date:[20020101 TO 20030101]                            |

   





