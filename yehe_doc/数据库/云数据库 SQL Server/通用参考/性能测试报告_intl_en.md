

## Testing Tool
The performance test in this document is conducted with the TPC-C benchmark load built in HammerDB. TPC-C is a typical OLTP workload that simulates a scenario where a wholesaler with multiple warehouses ships goods to a large number of customers. The adjustment of the number of warehouses can reflect the data size that the database can sustain in the test.
- [HammerDB download address](https://www.hammerdb.com/download.html)
- [HammerDB User Manual](https://www.hammerdb.com/document.html)
- [Overview of the TPC-C test load built in HammerDB](https://www.hammerdb.com/docs/ch03.html)

## Test Environment and Parameters
### Test instance editions
The test instances are of 2008 R2 Enterprise Edition, 2012 Enterprise Edition, 2014 Enterprise Edition, 2016 Enterprise Edition, 2017 Enterprise Edition, and 2019 Enterprise Edition.

### Test instance specifications
##### High availability edition
The test instances of high availability edition cover all purchasable specifications, including 1-core 2 GB, 1-core 4 GB, 1-core 8 GB, 2-core 16 GB, 4-core 32 GB, 8-core 64 GB, 12-core 96 GB, 16-core 128 GB, 24-core 192 GB, 32-core 256 GB, 48-core 384 GB, 64-core 512 GB, and 90-core 720 GB.

#### Basic edition
The test instances of basic edition cover all purchasable specifications, including 1-core 2 GB, 1-core 4 GB, 2-core 4 GB, 2-core 8 GB, 4-core 8 GB, and 4-core 16 GB.

### Load generation environment
The machines on which HammerDB is installed are of the same models as the database instances, ensuring that the performance of the SQL Server instances can be fully measured in the stress test.

### TPC-C benchmark parameters
- Number of Warehouses = 100: sets the number of warehouses to 100.
- Minutes of Rampup Time = 2: sets the warm-up time before the test to 2 minutes.
- Minutes Test Duration = 5: sets the test duration to 5 minutes.

### Number of virtual users
The number of virtual users is the number of concurrent connections. In this document, different numbers of concurrent connections are tested on instances of different editions with different specifications.

#### High availability edition
| Concurrent Connections | 2        | 4        | 8        | 16       | 32       | 64       | 128      | 256      | 512      | 1,024     |
| ---------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| 1-core 2 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -   | -    |
| 1-core 4 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -   | -    |
| 1-core 8 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -   | -    |
| 2-core 16 GB   | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        |
| 4-core 32 GB   | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        |
| 8-core 64 GB   | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        |
| 12-core 96 GB   | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 16-core 128 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 24-core 192 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 32-core 256 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 48-core 384 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 64-core 512 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 90-core 720 GB  | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

#### Basic edition
| Concurrent Connections | 2        | 4        | 8        | 16       | 32       | 64       | 128      | 256      | 512      | 1,024 |
| ---------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | ---- |
| 1-core 2 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        | -    |
| 1-core 4 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        | -    |
| 2-core 4 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |
| 2-core 8 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |
| 4-core 8 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |
| 4-core 16 GB    | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |

## Test Method
 ## Test Method
1. Prepare the TPC-C workload.
 - Number of Warehouses: the number of warehouses, which will affect the size of the test database generated.
 - Virtual Users to Build Schema: the number of concurrent connections when generating the load data, which cannot be larger than the number of warehouses. This value affects the efficiency of load data generation, so it is recommended to be the same as the number of CPU cores of the load generating device.
![](https://main.qcloudimg.com/raw/976f094fdf0e32dcfb5537bc6cf2cf0b.png)
2. Set the test script.
 - Total Transactions per User: the total number of transactions per user. You are recommended to set this parameter to a higher value so as to ensure that the user will not exit due to the completion of transactions during the stress test.
 - Minutes of Rampup Time: warm-up time for the stress test.
 - Minutes for Test Duration: duration of the stress test.
![](https://main.qcloudimg.com/raw/c0225b4272891c94f58ffb6645ca0da1.png)
3. Set the automated test script.
 - Minutes per Test in Virtual User Sequence: the interval between two automated test sessions during which the program completes various tasks such as creating virtual users, warming up, running the test, and stopping the test. This value should be greater than the sum of "Minutes of Rampup Time" and "Minutes for Test Duration".
 - Active Virtual User Sequence (Space Separated): the number of virtual users generated by each iteration of the automated test. It can be understood as the number of concurrent connections.
![](https://main.qcloudimg.com/raw/c6657ad27fb862ab2d758d5e06c4dfb6.png)
4. Select **Autopilot** > **Autopilot** in the left pane to start the test.
![](https://main.qcloudimg.com/raw/786137e8672adac87b224a7bfc783f51.png)
5. The test result will be output in the hammerdb.log file.
![](https://main.qcloudimg.com/raw/89d6adf0bf52b416fda5a387ff48ea49.png)

## Test Results
>?
>- The TPM in HammerDB is obtained through the SQL Server performance counter "batch requests/sec", so the TPM actually refers to the batch requests per minute.
>- The size of test data set for a instance specification is larger than the memory size of the specification.

### High availability edition (local SSD)
#### Performance comparison of different high availability editions (local SSD)
![](https://qcloudimg.tencent-cloud.cn/raw/2811a30c30849a8eb6d0a0d3e39e4e5b.png)

#### TPM comparison of different high availability editions (local SSD)
| High Availability Edition Instance Specification | Concurrent Connections | 2008 R2 Enterprise Edition | 2012 Enterprise Edition | 2014 Enterprise Edition | 2016 Enterprise Edition | 2017 Enterprise Edition | 2019 Enterprise Edition |
| ------------------ | ---------- | --------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1-core 2 GB       | 256        | 279,798          | 229,854        | 261,396        | 219,142        | 201,851        | 181,198        |
| 1-core 4 GB       | 256        | 284,680          | 234,401        | 288,282        | 222,796        | 202,510        | 268,330        |
| 1-core 8 GB       | 256        | 269,039          | 236,773        | 303,002        | 219,676        | 208,685        | 300,385        |
| 2-core 16 GB     | 256        | 368,366          | 333,797        | 446,344        | 336,843        | 331,650        | 390,546        |
| 4-core 32 GB     | 256        | 657,641          | 608,801        | 621,186        | 665,065        | 625,370        | 670,666        |
| 8-core 64 GB     | 256        | 1,164,062         | 1,020,500       | 924,915        | 1,070,826       | 1,102,296       | 1,007,612       |
| 12-core 96 GB   | 1,024       | 1,348,121         | 1,266,868       | 1,153,585       | 1,337,473       | 1,325,010       | 1,367,211       |
| 16-core 128 GB  | 1,024       | 1,357,678         | 1,385,158       | 1,260,322       | 1,705,660       | 1,716,818       | 1,629,583       |
| 24-core 192 GB  | 1,024       | 1,226,621         | 1,500,900       | 1,406,203       | 2,261,815       | 1,950,871       | 2,198,697       |
| 32-core 256 GB  | 1,024       | 1,401,600         | 1,526,762       | 1,462,100       | 2,280,252       | 2,520,856       | 2,771,797       |
| 48-core 384 GB    | 1,024       | 2,127,159         | 1,486,582       | 1,637,912       | 2,806,496       | 2,683,302       | 3,358,182       |
| 64-core 512 GB    | 1,024       | 2,136,500         | 1,512,763       | 1,789,105       | 2,630,581       | 2,814,599       | 3,635,133       |
| 90-core 720 GB    | 1,024       | 2,205,323         | 1,602,736       | 1,813,094       | 2,948,427       | 3,391,680       | 4,579,980       |

### Basic edition (premium cloud disk)
#### Performance comparison of different basic editions (premium cloud disk)
![](https://qcloudimg.tencent-cloud.cn/raw/dab7533cd878b8bc2f976e96cf04d0b8.png)

#### TPM comparison of different basic editions (premium cloud disk)
| Basic Edition Instance Specification | Concurrent Connections | 2008 R2 Enterprise Edition | 2012 Enterprise Edition | 2014 Enterprise Edition | 2016 Enterprise Edition | 2017 Enterprise Edition | 2019 Enterprise Edition |
| ---------------- | ---------- | --------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1-core 2 GB     | 256        | 271,822          | 201,348        | 239,864        | 155,318        | 180,204        | 181,062        |
| 1-core 4 GB     | 256        | 271,311          | 224,851        | 263,445        | 206,871        | 218,065        | 226,523        |
| 2-core 4 GB     | 256        | 300,573          | 286,984        | 349,251        | 301,520        | 282,145        | 280,967        |
| 2-core 8 GB     | 256        | 343,630          | 312,184        | 379,705        | 315,539        | 304,840        | 331,574        |
| 4-core 8 GB     | 256        | 569,589          | 557,047        | 567,886        | 464,900        | 457,702        | 507,047        |
| 4-core 16 GB   | 256        | 578,367          | 560,981        | 602,897        | 504,379        | 537,819        | 592,712        |



