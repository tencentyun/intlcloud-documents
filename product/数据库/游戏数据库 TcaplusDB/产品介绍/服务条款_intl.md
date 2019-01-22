[//]: # (chinagitpath:XXXXX)

### Product Availability
1. We guarantee a 99.95% business availability for TcaplusDB, which means this service should be available for 30(day)×24(hr)×60(min)×99.95%=43,178.4 minutes, and thus be unavailable for 43,200-43,178.4=21.6 minutes at most each month.
2. The API layer of TcaplusDB uses cloud load balancer. When access server crashes, the servers at fault are automatically removed, and other servers continue to provide services. At the same time, sampling requests will be sent to the faulty server at regular intervals, and after it can respond normally, the requests will be gradually shared to the recovered server. The same strategy is used in the automatic expansion and reduction of the access layer. The game server will not be affected during the whole process.
3. TcaplusDB's data storage machine uses the Master-Slave hot backup mode, where every data change on the Master device is recorded as a binlog with a version number. The Slave device will request the binlog seq differences from the Master device and write the latest record to the local device to ensure data consistency with the Master device.
4. The TcaplusDB console will monitor the Master device's quality of service including success rate, latency and survival status in real time. When the Master device is unavailable, failover is automatically triggered, so that the primary Slave device will take over as a new Master device to provide services, and the original Master device will become a Slave device and generate alarms.
5. TcaplusDB's data storage machine uses SSD to store data and memory to cache data, which enables high efficiency of data read and write, mostly within 10 ms.
6. Business availability formula: 100% - Σ (failure duration x module coefficient ratio x number of affected users) ÷ total duration for current month x 100%.

### Pricing Details
The pricing information for TcaplusDB are displayed on both the purchase and the order pages. The user can select the specific service type and purchase it at list price. Prices are based on the prices published on Tencent Game Service’s website. Prices are also dependent on the selected cloud service specifications and usage duration. 

### Compensation
**Applicable Circumstances**
Compensation is applicable in circumstances such as when the user is unable to use or access their purchased cloud products, or if the game is inaccessible due to failure on Tencent Game Service’s end. In such situations, the user can claim for compensation accordingly. 

**Compensation Standards**
Hundred-fold compensation for TcaplusDB failures: As the billing method is Postpaid, the compensation will be in the form of cash credit. Credited amount will be equal to the fees incurred in the 24 hours before the domain name in question failed ÷ 24 ÷ 60 × failure duration × 100.
- Failure duration = system recovery time - failure start time. The failure duration is calculated in minutes, and any duration less than 1 minute will be counted as 1 minute. For example, if the failure duration is 1 minute and 1 second, it will be counted as 2 minutes.
- If the domain name has not been used for 24 hours, the charge per minute is calculated based on the actual usage duration.
- The compensation amount should not exceed the total amount the user has paid for the faulty domain name. 

### Data Audit
In accordance with the applicable laws and regulations and if in of compliance with relevant process and availability of all necessary documents, Tencent Game Service may provide information regarding game databases, including operation log of key components, operation records of OPS personnel and operation records of users, if required by regulatory authorities or if it is necessary to do so for other reasons such as collection of evidences during investigation into security incidents.

### Failure Recovery Capability
With a professional team that provides 7x24 maintenance service and technical support by means of tickets, telephone or other channels, Tencent Game Service boasts a series of excellent emergency response mechanisms covering efficient failure monitoring, alarm, positioning and recovery.

