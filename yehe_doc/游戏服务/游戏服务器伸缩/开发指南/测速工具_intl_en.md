This document provides the addresses and examples for latency test in different regions. Both HTTPS and UDP addresses are supported.

### HTTPS and UDP addresses for latency test in regions 

|   Region   |                 HTTPS Address                 |   UDP Address   |
| :------: | :-------------------------------------------: | :-------------: |
|   Beijing   |    https://ap-beijing.speed.tencentgse.com    | ap-beijing.speed.tencentgse.com |
|   Shanghai   |   https://ap-shanghai.speed.tencentgse.com    | ap-shanghai.speed.tencentgse.com  |
|   Hong Kong (China)   |   https://ap-hongkong.speed.tencentgse.com    | ap-hongkong.speed.tencentgse.com  |
|   Guangzhou   |   https://ap-guangzhou.speed.tencentgse.com   |  ap-guangzhou.speed.tencentgse.com |
|   Chengdu   |   https://ap-chengdu.speed.tencentgse.com   |   ap-chengdu.speed.tencentgse.com | 
|  Singapore  |   https://ap-singapore.speed.tencentgse.com   |  ap-singapore.speed.tencentgse.com  |
|   Mumbai   |    https://ap-mumbai.speed.tencentgse.com     | ap-mumbai.speed.tencentgse.com  |
|   Silicon Valley   | https://na-siliconvalley.speed.tencentgse.com |  na-siliconvalley.speed.tencentgse.com   |
| Virginia |    https://na-ashburn.speed.tencentgse.com    |  na-ashburn.speed.tencentgse.com   |
| Frankfurt |   https://eu-frankfurt.speed.tencentgse.com   | eu-frankfurt.speed.tencentgse.com  |
|   Seoul   |     https://ap-seoul.speed.tencentgse.com     | ap-seoul.speed.tencentgse.com  |
|   Tokyo   |     https://ap-tokyo.speed.tencentgse.com     | ap-tokyo.speed.tencentgse.com  |



### Example  
Let’s take Guangzhou as an example.
- **HTTPS**
```plaintext
ping ap-guangzhou.speed.tencentgse.com
curl https://ap-guangzhou.speed.tencentgse.com/v1/ping
```
- **UDP**
```
Domain name + PORT (8888)
ap-guangzhou.speed.tencentgse.com + PORT (8888)
```
