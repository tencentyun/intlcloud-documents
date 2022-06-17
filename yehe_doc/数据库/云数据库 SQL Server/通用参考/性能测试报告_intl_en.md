## Test Tool
The performance test in this document is conducted with the TPC-C benchmark load built in HammerDB. TPC-C is a typical OLTP workload that simulates a scenario where a wholesaler with multiple warehouses ships goods to a large number of customers. The adjustment of the number of warehouses can reflect the data size that the database can sustain in the test.
- [HammerDB download address](https://www.hammerdb.com/download.html)
- [HammerDB user guide](https://www.hammerdb.com/document.html)
- [Introduction to OLTP Testing (TPROC-C derived from TPC-C)](https://www.hammerdb.com/docs/ch03.html)

## Test Environment and Parameters
### Test instance editions
The test instances are of 2008 R2 Enterprise Edition, 2012 Enterprise Edition, 2014 Enterprise Edition, 2016 Enterprise Edition, 2017 Enterprise Edition, and 2019 Enterprise Edition.

### Test instance specifications
#### High-availability edition
The test instances of high availability edition cover all purchasable specifications, including 1-core 2 GB MEM, 1-core 4 GB MEM, 1-core 8 GB MEM, 2-core 16 GB MEM, 4-core 32 GB MEM, 8-core 64 GB MEM, 12-core 96 GB MEM, 16-core 128 GB MEM, 24-core 192 GB MEM, 32-core 256 GB MEM, 48-core 384 GB MEM, 64-core 512 GB MEM, and 90-core 720 GB MEM.

#### Basic edition
The test instances of basic edition cover all purchasable specifications, including 1-core 2 GB MEM, 1-core 4 GB MEM, 2-core 4 GB MEM, 2-core 8 GB MEM, 4-core 8 GB MEM, 4-core 16 GB MEM, 8-core 16 GB MEM, 8-core 32 GB MEM, 16-core 32 GB MEM, 16-core 64 GB MEM, 24-core 48 GB MEM, and 24-core 96 GB MEM.

### Load generation environment
The machines on which HammerDB is installed are of the same models as the SQL Server instances, ensuring that the performance of the instances can be fully measured in the stress test.

### TPC-C benchmark parameters
- Number of Warehouses = 100: Sets the number of warehouses to 100.
- Minutes of Rampup Time = 2: Sets the rampup time before the test to 2 minutes.
- Minutes Test Duration = 5: Sets the test duration to 5 minutes.

### Number of virtual users
The number of virtual users is the number of concurrent connections. In this document, different numbers of concurrent connections are tested on instances of different editions with different specifications.

#### High-availability edition
| Concurrent Connections | 2        | 4        | 8        | 16       | 32       | 64       | 128      | 256      | 512      | 1024     |
| ---------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| 1-core 2 GB MEM     | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -   | -    |
| 1-core 4 GB MEM     | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -   | -    |
| 1-core 8 GB MEM     | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -   | -    |
| 2-core 16 GB MEM   | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -        |
| 4-core 32 GB MEM   | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -        |
| 8-core 64 GB MEM   | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -        |
| 12-core 96 GB MEM   | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |
| 16-core 128 GB MEM  | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |
| 24-core 192 GB MEM  | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |
| 32-core 256 GB MEM  | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |
| 48-core 384 GB MEM  | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |
| 64-core 512 GB MEM  | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |
| 90-core 720 GB MEM | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |

#### Basic edition
| Concurrent Connections | 2        | 4        | 8        | 16       | 32       | 64       | 128      | 256      | 512      | 1024 |
| ---------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- | ---- |
| 1-core 2 GB MEM     | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -        | -    |
| 1-core 4 GB MEM     | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -        | -    |
| 2-core 4 GB MEM     | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -    |
| 2-core 8 GB MEM     | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -    |
| 4-core 8 GB MEM     | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -    |
| 4-core 16 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -    |
| 8-core 16 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -    |
| 8-core 32 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | -    |
| 16-core 32 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003;   |
| 16-core 64 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003;   |
| 24-core 48 GB MEM    | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003;   |
| 24-core 96 GB MEM  | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003; | &#10003;  |

## Test Method
1. Prepare the TPC-C workload.
 - Number of Warehouses: The number of warehouses, which will affect the size of the test database generated.
 - Virtual Users to Build Schema: The number of concurrent connections when generating the load data, which cannot be larger than the number of warehouses. This value affects the efficiency of load data generation, so we recommend you make it the same as the number of CPU cores of the load generating device.
![](https://main.qcloudimg.com/raw/976f094fdf0e32dcfb5537bc6cf2cf0b.png)
2. Set the test script.
 - Total Transactions per User: The total number of transactions per user. We recommend you set this parameter to a higher value so as to ensure that the user will not exit due to the completion of transactions during the stress test.
 - Minutes of Rampup Time: Rampup time for the stress test.
 - Minutes for Test Duration: Duration of the stress test.
![](https://main.qcloudimg.com/raw/c0225b4272891c94f58ffb6645ca0da1.png)
3. Set the automated test script.
 - Minutes per Test in Virtual User Sequence: The interval between two automated test sessions during which the program completes various tasks such as creating virtual users, ramping up, running the test, and stopping the test. This value should be greater than the sum of "Minutes of Rampup Time" and "Minutes for Test Duration".
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

### High availability edition (local SSD)
#### Performance comparison of different high availability editions (local SSD)
![](https://qcloudimg.tencent-cloud.cn/raw/2811a30c30849a8eb6d0a0d3e39e4e5b.png)

#### TPM comparison of different high availability editions (local SSD)
| High Availability Edition Instance Specification | Concurrent Connections | 2008 R2 Enterprise Edition | 2012 Enterprise Edition | 2014 Enterprise Edition | 2016 Enterprise Edition | 2017 Enterprise Edition | 2019 Enterprise Edition |
| ------------------ | ---------- | --------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1-core 2 GB MEM       | 256        | 279798          | 229854        | 261396        | 219142        | 201851        | 181198        |
| 1-core 4 GB MEM       | 256        | 284680          | 234401        | 288282        | 222796        | 202510        | 268330        |
| 1-core 8 GB MEM       | 256        | 269039          | 236773        | 303002        | 219676        | 208685        | 300385        |
| 2-core 16 GB MEM     | 256        | 368366          | 333797        | 446344        | 336843        | 331650        | 390546        |
| 4-core 32 GB MEM     | 256        | 657641          | 608801        | 621186        | 665065        | 625370        | 670666        |
| 8-core 64 GB MEM     | 256        | 1164062         | 1020500       | 924915        | 1070826       | 1102296       | 1007612       |
| 12-core 96 GB MEM   | 1024       | 1348121         | 1266868       | 1153585       | 1337473       | 1325010       | 1367211       |
| 16-core 128 GB MEM  | 1024       | 1357678         | 1385158       | 1260322       | 1705660       | 1716818       | 1629583       |
| 24-core 192 GB MEM  | 1024       | 1226621         | 1500900       | 1406203       | 2261815       | 1950871       | 2198697       |
| 32-core 256 GB MEM  | 1024       | 1401600         | 1526762       | 1462100       | 2280252       | 2520856       | 2771797       |
| 48-core 384 GB MEM    | 1024       | 2127159         | 1486582       | 1637912       | 2806496       | 2683302       | 3358182       |
| 64-core 512 GB MEM    | 1024       | 2136500         | 1512763       | 1789105       | 2630581       | 2814599       | 3635133       |
| 90-core 720 GB MEM    | 1024       | 2205323         | 1602736       | 1813094       | 2948427       | 3391680       | 4579980       |

### Basic edition (premium cloud disk)
#### Performance comparison of different basic editions (premium cloud disk)
![](https://qcloudimg.tencent-cloud.cn/raw/dab7533cd878b8bc2f976e96cf04d0b8.png)

#### TPM comparison of different basic editions (premium cloud disk)
| Basic Edition Instance Specification | Concurrent Connections | 2008 R2 Enterprise Edition | 2012 Enterprise Edition | 2014 Enterprise Edition | 2016 Enterprise Edition | 2017 Enterprise Edition | 2019 Enterprise Edition |
| ---------------- | ---------- | --------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1-core 2 GB MEM     | 256        | 271822          | 201348        | 239864        | 155318        | 180204        | 181062        |
| 1-core 4 GB MEM     | 256        | 271311          | 224851        | 263445        | 206871        | 218065        | 226523        |
| 2-core 4 GB MEM     | 256        | 300573          | 286984        | 349251        | 301520        | 282145        | 280967        |
| 2-core 8 GB MEM     | 256        | 343630          | 312184        | 379705        | 315539        | 304840        | 331574        |
| 4-core 8 GB MEM     | 256        | 569589          | 557047        | 567886        | 464900        | 457702        | 507047        |
| 4-core 16 GB MEM   | 256        | 578367          | 560981        | 602897        | 504379        | 537819        | 592712        |
| 8-core 16 GB MEM   | 256        | 968175          | 977350        | 866079        | 705806        | 812833        | 871512        |
| 8-core 32 GB MEM   | 256        | 974293          | 945406        | 890642        | 734445        | 842877        | 895221        |
| 16-core 32 GB MEM  | 1024        | 965995          | 1033233        | 1008835        | 993027        | 1007447        | 1056011        |
|16-core 64 GB MEM   | 1024        | 1017271          | 1122514        | 1064300        | 1075603        | 1100160        | 1147242        |
| 24-core 48 GB MEM   | 1024        | 912623          | 1055985        | 1045071        | 1129963        | 1139872        | 1203012        |
| 24-core 96 GB MEM   | 1024        | 954747          | 1061295        | 1044175        | 1184654        | 1147836        | 1315849        |

### Basic editions (SSD cloud disk)
#### Performance comparison of different basic editions (SSD cloud disk)
![](https://qcloudimg.tencent-cloud.cn/raw/13c3d04e4a22937bdd7046fe6425368c.png)

#### TPM comparison of different basic editions (SSD cloud disk)
| Basic Edition Instance Specification | Concurrent Connections | 2008 R2 Enterprise Edition | 2012 Enterprise Edition | 2014 Enterprise Edition | 2016 Enterprise Edition | 2017 Enterprise Edition | 2019 Enterprise Edition |
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
