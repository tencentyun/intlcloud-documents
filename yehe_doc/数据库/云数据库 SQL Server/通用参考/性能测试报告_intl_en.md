## Test Tool
The performance test in this document is conducted with the TPC-C benchmark load built in HammerDB. TPC-C is a typical OLTP workload that simulates a scenario where a wholesaler with multiple warehouses ships goods to a large number of customers. The adjustment of the number of warehouses can reflect the data size that the database can sustain in the test.
- [HammerDB download address](https://www.hammerdb.com/download.html)
- [HammerDB User Manual](https://www.hammerdb.com/document.html)
- [Overview of the TPC-C test load built in HammerDB](https://www.hammerdb.com/docs/ch03.html)

## Test Environment and Parameters
### Test instance editions
The test instances are of 2008 R2 Enterprise Edition, 2012 Enterprise Edition, 2014 Enterprise Edition, 2016 Enterprise Edition, 2017 Enterprise Edition, and 2019 Enterprise Edition.

### Test instance specifications
#### Two-node (formerly High Availability Edition)
The test two-node (formerly High Availability Edition) instances cover all purchasable specifications, including 1-core 2 GB MEM, 1-core 4 GB MEM, 1-core 8 GB MEM, 2-core 16 GB MEM, 4-core 32 GB MEM, 8-core 64 GB MEM, 12-core 96 GB MEM, 16-core 128 GB MEM, 24-core 192 GB MEM, 32-core 256 GB MEM, 48-core 384 GB MEM, 64-core 512 GB MEM, and 90-core 720 GB MEM.

#### Single-node (formerly Basic Edition)
The test single-node (formerly Basic Edition) instances cover all purchasable specifications, including 1-core 2 GB MEM, 1-core 4 GB MEM, 2-core 4 GB MEM, 2-core 8 GB MEM, 4-core 8 GB MEM, 4-core 16 GB MEM, 8-core 16 GB MEM, 8-core 32 GB MEM, 16-core 32 GB MEM, 16-core 64 GB MEM, 24-core 48 GB MEM, and 24-core 96 GB MEM.

### Load generation environment
The machines on which HammerDB is installed are of the same models as the database instances, ensuring that the performance of the SQL Server instances can be fully measured in the stress test.

### TPC-C benchmark parameters
- Number of Warehouses = 100: Sets the number of warehouses to 100.
- Minutes of Rampup Time = 2: Sets the warm-up time before the test to 2 minutes.
- Minutes Test Duration = 5: Sets the test duration to 5 minutes.

### Number of virtual users
The number of virtual users is the number of concurrent connections. In this document, different numbers of concurrent connections are tested on instances of different editions with different specifications.

#### Two-node (formerly High Availability Edition)
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

#### Single-node (formerly Basic Edition)
| Concurrent Connections | 2        | 4        | 8        | 16       | 32       | 64       | 128      | 256      | 512      | 1,024 |
| ---------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | ---- |
| 1-core 2 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        | -    |
| 1-core 4 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -        | -    |
| 2-core 4 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |
| 2-core 8 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |
| 4-core 8 GB     | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |
| 4-core 16 GB    | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | -    |
| 8-core 16 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -    |
| 8-core 32 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -    |
| 16-core 32 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003;   |
| 16-core 64 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003;   |
| 24-core 48 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003;   |
| 24-core 96 GB MEM  | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003;  |

## Test Method
1. Prepare the TPC-C workload.
 - Number of Warehouses: The number of warehouses, which will affect the size of the test database generated.
 - Virtual Users to Build Schema: The number of concurrent connections when generating the load data, which cannot be larger than the number of warehouses. This value affects the efficiency of load data generation, so it is recommended to be the same as the number of CPU cores of the load generating device.
![](https://main.qcloudimg.com/raw/976f094fdf0e32dcfb5537bc6cf2cf0b.png)
2. Set the test script.
 - Total Transactions per User: The total number of transactions per user. We recommend that you set this parameter to a higher value so as to ensure that the user will not exit due to the completion of transactions during the stress test.
 - Minutes of Rampup Time: Warm-up time for the stress test.
 - Minutes for Test Duration: Duration of the stress test.
![](https://main.qcloudimg.com/raw/c0225b4272891c94f58ffb6645ca0da1.png)
3. Set the automated test script.
 - Minutes per Test in Virtual User Sequence: The interval between two automated test sessions during which the program completes various tasks such as creating virtual users, warming up, running the test, and stopping the test. This value should be greater than the sum of "Minutes of Rampup Time" and "Minutes for Test Duration".
 - Active Virtual User Sequence (Space Separated): The number of virtual users generated by each iteration of the automated test. It can be understood as the number of concurrent connections.
![](https://main.qcloudimg.com/raw/c6657ad27fb862ab2d758d5e06c4dfb6.png)
4. Select **Autopilot** > **Autopilot** in the left pane to start the test.
![](https://main.qcloudimg.com/raw/786137e8672adac87b224a7bfc783f51.png)
5. The test result will be output in the hammerdb.log file.
![](https://main.qcloudimg.com/raw/89d6adf0bf52b416fda5a387ff48ea49.png)

## Test Results
>?
>- The TPM in HammerDB is obtained through the SQL Server performance counter "batch requests/sec", so the TPM actually refers to the batch requests per minute.
>- The size of test data set for a instance specification is larger than the memory size of the specification.

### Two-node (formerly High Availability Edition - local SSD)
#### Performance comparison of different editions
![](https://qcloudimg.tencent-cloud.cn/raw/2811a30c30849a8eb6d0a0d3e39e4e5b.png)

#### TPM comparison of different editions
| Two-Node (Formerly High Availability Edition) Instance Specification | Concurrent Connections | 2008 R2 Enterprise Edition | 2012 Enterprise Edition | 2014 Enterprise Edition | 2016 Enterprise Edition | 2017 Enterprise Edition | 2019 Enterprise Edition |
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

### Single-node (formerly Basic Edition - premium cloud disk)
#### Performance comparison of different editions
![](https://qcloudimg.tencent-cloud.cn/raw/dab7533cd878b8bc2f976e96cf04d0b8.png)

#### TPM comparison of different editions
| Single-Node (Formerly Basic Edition) Instance Specification | Concurrent Connections | 2008 R2 Enterprise Edition | 2012 Enterprise Edition | 2014 Enterprise Edition | 2016 Enterprise Edition | 2017 Enterprise Edition | 2019 Enterprise Edition |   
| ---------------- | ---------- | --------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1-core 2 GB     | 256        | 271,822          | 201,348        | 239,864        | 155,318        | 180,204        | 181,062        |  
| 1-core 4 GB     | 256        | 271,311          | 224,851        | 263,445        | 206,871        | 218,065        | 226,523        |     
| 2-core 4 GB     | 256        | 300,573          | 286,984        | 349,251        | 301,520        | 282,145        | 280,967        |      
| 2-core 8 GB     | 256        | 343,630          | 312,184        | 379,705        | 315,539        | 304,840        | 331,574        |      
| 4-core 8 GB     | 256        | 569,589          | 557,047        | 567,886        | 464,900        | 457,702        | 507,047        |      
| 4-core 16 GB   | 256        | 578,367          | 560,981        | 602,897        | 504,379        | 537,819        | 592,712        |     
| 8-core 16 GB MEM   | 256        | 968175          | 977350        | 866079        | 705806        | 812833        | 871512        |   
| 8-core 32 GB MEM   | 256        | 974293          | 945406        | 890642        | 734445        | 842877        | 895221        |   
| 16-core 32 GB MEM  | 1024        | 965995          | 1033233        | 1008835        | 993027        | 1007447        | 1056011        |   
|16-core 64 GB MEM   | 1024        | 1017271          | 1122514        | 1064300        | 1075603        | 1100160        | 1147242        |   
| 24-core 48 GB MEM   | 1024        | 912623          | 1055985        | 1045071        | 1129963        | 1139872        | 1203012        |   
| 24-core 96 GB MEM   | 1024        | 954747          | 1061295        | 1044175        | 1184654        | 1147836        | 1315849        |  

### Single-node (formerly Basic Edition - SSD cloud disk)
#### Performance comparison of different editions
![](https://qcloudimg.tencent-cloud.cn/raw/13c3d04e4a22937bdd7046fe6425368c.png)

#### TPM comparison of different editions
| Single-Node (Formerly Basic Edition) Instance Specification | Concurrent Connections | 2008 R2 Enterprise Edition | 2012 Enterprise Edition | 2014 Enterprise Edition | 2016 Enterprise Edition | 2017 Enterprise Edition | 2019 Enterprise Edition |   
| ---------------- | ---------- | --------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1-core 2 GB MEM     | 256        | 277486          | 212148        | 268084        | 209753        | 198943        | 188967        |  
| 1-core 4 GB MEM    | 256        | 287696          | 230418        | 261590        | 210630        | 207538        | 236449        |     
| 2-core 4 GB MEM    | 256        | 329331          | 307056        | 395540        | 312891        | 311241        | 301509        |      
| 2-core 8 GB MEM     | 256        | 351604          | 314275        | 434242        | 325675        | 324843        | 371492        |      
| 4-core 8 GB MEM    | 256        | 582886          | 574929        | 585404        | 550150        | 464908        | 551348        |      
| 4-core 16 GB MEM   | 256        | 600462          | 599149        | 596735        | 664131        | 505928        | 638924        |     
| 8-core 16 GB MEM   | 256        | 1053565          | 987506        | 889740        | 708025        | 824114        | 957938        |   
| 8-core 32 GB MEM   | 256        | 1104104          | 1009945        | 903942        | 767060        | 892721        | 995933        |   
| 16-core 32 GB MEM  | 1024        | 1224515          | 1193629        | 1118041        | 1009075        | 1123299        | 1088041        |   
|16-core 64 GB MEM  | 1024        | 1230516          | 1200651        | 1136268        | 1052159        | 1156376        | 1081471        |   
| 24-core 48 GB MEM   | 1024        | 1145090          | 1080964        | 1099758        | 1155533        | 1187867        | 1269441        |   
| 24-core 96 GB MEM   | 1024        | 1200990          | 1040499        | 1108077        | 1243883        | 1262611        | 1377183        | 
