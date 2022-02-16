TencentDB data centers are hosted in multiple locations worldwide. These locations are known as regions. Each region is an independent geographical area.
Region name can most directly embody the coverage of a data center. The following naming convention is used for your convenience:
A region name is composed of **region + city**. The `region` indicates the geographic area that the data center covers, while the `city` represents the city in or near which the data center is located.


>?TcaplusDB does not divide instances by AZ.

## How to Select Region
Tencent Cloud regions are completely isolated. This guarantees the maximum cross-region stability and fault tolerance. When purchasing Tencent Cloud services, you are recommended to select the region closest to your end users to minimize access latency and improve download speed. Operations such as launching or viewing instances are performed at the region level.
Notes on private network communication:
- Tencent Cloud resources in the same region (under the same account and in the same VPC) can communicate with each other over private network. They can also be accessed via [private IPs](https://intl.cloud.tencent.com/document/product/213/5225).
- The networks of different regions are fully isolated from each other, and Tencent Cloud services in different regions cannot communicate with each other over the private network by default.
- Tencent Cloud services in different regions can communicate with each other by accessing the internet through [public IPs](https://intl.cloud.tencent.com/document/product/213/5224). Tencent Cloud services in different VPCs can communicate with each other through [CCN](https://intl.cloud.tencent.com/document/product/1003), which is faster and more stable.


## Region List
TcaplusDB divides instances only by region and is available in the following regions:

### China
| Region | Identifier | 
|---------|---------|
| East China (Shanghai) | ap-shanghai | 
| Hong Kong/Macao/Taiwan (Hong Kong, China) | ap-hongkong |

### Other countries/regions
| Region | Identifier | 
|---------|---------|
| Southeast Asia Pacific (Singapore) | ap-singapore | 
| Northeast Asia Pacific (Seoul) | ap-seoul |
| Northeast Asia Pacific (Tokyo) | ap-tokyo |
| West US (Silicon Valley) | na-siliconvalley |
| East US (Virginia) | na-ashburn |
| Europe (Frankfurt) | eu-frankfurt |


