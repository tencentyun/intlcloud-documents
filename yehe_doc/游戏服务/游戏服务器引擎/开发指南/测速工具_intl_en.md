This document describes the addresses and examples for latency test in different regions. Both HTTPS and UDP are supported.

### HTTPS and UDP addresses for latency test in regions 

|  Region   |                 HTTPS Address              |   UDP Address   |
| :------: | :-------------------------------------------: | :-------------: |
| Frankfurt |   https://eu-frankfurt.speed.tencentgse.com   | 162.62.115.241  |
| Beijing   |    https://ap-beijing.speed.tencentgse.com    | 109.244.169.222 |
| Tokyo   |     https://ap-tokyo.speed.tencentgse.com     | 124.156.236.22  |
| Seoul   |     https://ap-seoul.speed.tencentgse.com     | 150.109.249.54  |
| Singapore  |   https://ap-singapore.speed.tencentgse.com   |  129.226.2.138  |
| Mumbai   |    https://ap-mumbai.speed.tencentgse.com     | 129.226.26.136  |
|  Hong Kong (China)   |   https://ap-hongkong.speed.tencentgse.com    | 129.226.103.23  |
| Virginia |    https://na-ashburn.speed.tencentgse.com    |  49.51.78.239   |
| Silicon Valley  | https://na-siliconvalley.speed.tencentgse.com |  49.51.190.41   |
| Guangzhou   |   https://ap-guangzhou.speed.tencentgse.com   |  106.55.124.10  |
| Shanghai   |   https://ap-shanghai.speed.tencentgse.com    | 175.24.219.174  |

### Example  
This document uses Guangzhou as an example.
- **HTTPS**
```
ping ap-guangzhou.speed.tencentgse.com
curl https://ap-guangzhou.speed.tencentgse.com/v1/ping
```
- **UDP**
```
IP + PORT（8888）
```
