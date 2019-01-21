[//]: # (chinagitpath:XXXXX)

### Product availability
1. We guarantee a 99.95% business availability for TcaplusDB, which means this service should be available for 30(day)×24(hr)×60(min)×99.95%=43,178.4 minutes, and thus be unavailable for 43,200-43,178.4=21.6 minutes at most each month.
2. The API layer of TcaplusDB uses cloud load balancer. When access server crashes, the servers at fault are automatically removed, and other servers continue to provide services. At the same time, sampling requests will be sent to the faulty server at regular intervals, and after it can respond normally, the requests will be gradually shared to the recovered server. The same strategy is used in the automatic expansion and reduction of the access layer. The game server will not be affected during the whole process.
3. TcaplusDB's data storage machine uses the Master-Slave hot backup mode, where every data change on Master is recorded as a binlog with a version number, and Slave requests binlog seq differences from Master, and writes the latest record to the local to ensure data consistency with Master.
4. The TcaplusDB console will monitor Master's quality of service including success rate, latency and survival status in real time. When Master is unavailable, failover is automatically triggered, so that the primary Slave will be switched to a new Master to provide services, and the original Master will be switched to a Slave and generate alarms.
5. TcaplusDB's data storage machine uses SSD to store data and memory to cache data, which enables high efficiency of data read and write, mostly within 10 ms.
6. Business availability formula: 100% - Σ (failure duration x module coefficient ratio x number of users affected) ÷ total duration for current month x 100%.

### Accuracy of product billing
The billing details for TcaplusDB are displayed on both the purchase and the order pages. You can select the services you need from a variety of service categories and make a purchase at the listed prices. Refer to the information published on Tencent Game Service website for actual prices, and the fee is charged based on the service specifications and the usage duration.

### Compensation
**Scope**
Compensation is applicable to circumstances where a user claims for compensation for incidents/failures caused by Tencent Game Service, such as the user's inability to use or access the purchased cloud products properly and the inability to access any games.

**Compensation standards**
Hundred-fold compensation for TcaplusDB failures: As the billing method is Postpaid, a cash coupon in an amount equal to the fee for 24 hours before the domain name in question fails ÷ 24 ÷ 60 × failure duration × 100 will be offered.
- Failure duration = the time when the failure is recovered - the start time of failure. The failure duration is calculated in minutes, and the duration less than 1 minute will be counted as 1 minute. For example, if the failure duration is 1 minute plus 1 second, it will be counted as 2 minutes.
- If the domain name has not been used for 24 hours, the charge per minute is calculated based on the actual usage duration.
- The compensation amount should not exceed the total amount the user has paid for the faulty domain name.

### Audit of data
In accordance with the applicable laws and regulations and on condition of compliance with relevant process and availability of all necessary documents, Tencent Game Service may provide information regarding game databases, including operation log of key components, operation records of OPS personnel and operation records of users, if required by regulatory authorities or if it is necessary to do so for other reasons such as collection of evidences during investigation into security incidents.

### Failure recovery capability
With a professional team that provides 7x24 maintenance service and technical support by means of tickets, telephone or other channels, Tencent Game Service boasts a series of excellent emergency response mechanisms covering efficient failure monitoring, alarm, positioning and recovery.

