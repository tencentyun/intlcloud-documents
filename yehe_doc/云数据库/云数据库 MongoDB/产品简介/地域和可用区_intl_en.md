## Region
TencentDB data centers are hosted in multiple locations world-wide, covering South China, East China, North China, Southwest China, Hong Kong (China), Macao (China), Taiwan (China), Southeast Asia Pacific, South Asia Pacific, Northeast Asia Pacific, West US, East US, North America, Europe, and other regions. Tencent Cloud will gradually deploy nodes in more regions for a wider coverage.
Current regions where instances can be created include:
Guangzhou, Shanghai, Nanjing, Beijing, Chengdu, Chongqing, Hong Kong (China), Singapore, Seoul, Tokyo, Mumbai, Bangkok, Silicon Valley, Toronto, Virginia, Frankfurt, Moscow.

>?
>- Tencent Cloud resources in the same VPC in the same region under the same account can communicate with each other using [private IPs](https://intl.cloud.tencent.com/document/product/213/5225) over the private network.
>- Networks in different regions are completely isolated. By default, Tencent Cloud resources in different regions cannot communicate with each other over the private network.
>- When purchasing Tencent Cloud services, we recommend selecting the region closest to your end users to minimize access latency .

## Availability Zone
Availability zones (AZs) refer to Tencent Cloud's physical data centers that are in the same region. Each AZ is independently powered and have its own network resources. They are designed to ensure that failures within one AZ can be isolated from other zones, thereby ensuring service availability and business stability, excepting the occurrences of large-scale disasters or major power failures. AZs in the same region can communicate with each other over the private network, and products in the same AZ can access each other with a lower latency.
