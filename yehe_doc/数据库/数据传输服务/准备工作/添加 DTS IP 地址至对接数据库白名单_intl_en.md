## Overview
When creating a data migration, sync, or subscription task, you need to add the DTS IP address to the allowlists of the source and target databases so that they can communicate with each other.

If you don’t add the DTS IP address to the database allowlists, the connectivity test may fail, and you will be prompted to do so if the test fails.

![](https://qcloudimg.tencent-cloud.cn/raw/631f9a6a9910f954516bdf69bda71736.png)

## Directions

Get the IP address for the database region from [DTS IP Addresses](#1), and add it to the source or target database allowlist.

- For a self-built database, allow the DTS IP address to access the database when you set the firewall.
  - Windows: Open “Control Panel”, find “Windows Defender Firewall”, and view the firewall policies.
  - Linux: Run the `iptables -L` command to view the server’s firewall policies.

- For a TencentDB database or a self-built database on CVM, follow the directions below to add the DTS IP address to the security group.
  1. Log in to the source database and click an instance ID in the instance list to enter the instance management page.
  2. On the instance management page, select the **Security Group** or **Data Security** tab and add the DTS IP address to the security group.
     ![](https://qcloudimg.tencent-cloud.cn/raw/276d6b7c7f112d3630d040496d9dbc07.png)
  
- For a third-party cloud database, add the DTS IP address to the security group of that database.

## [DTS IP Addresses](id:1)

#### Public network

| Region     | DTS IP Address                                           |
| -------- | ------------------------------------------------------------ |
| Guangzhou     | 111.230.198.143,118.89.34.161,123.207.84.254,139.199.74.159  |
| Shanghai     | 111.231.139.59,111.231.142.94,115.159.71.186,182.254.153.245 |
| Beijing     | 123.207.145.84,211.159.157.165,211.159.160.104,58.87.92.66   |
| Chengdu     | 111.231.225.99,118.24.42.158                                 |
| Chongqing     | 139.186.122.1/24,129.28.12.1/24,129.28.14.1/24,139.186.77.242,139.186.109.1/24,<br>139.186.131.1/23,94.191.102.144,94.191.98.210 |
| Hangzhou-ec   | 111.231.139.59,111.231.142.94,115.159.71.186,182.254.153.245 |
| Nanjing     | 129.211.166.117,129.211.167.130                              |
| Tianjin     | 154.8.246.150,154.8.246.48                                   |
| Shenzhen     | 118.126.124.6,118.126.124.83                                 |
| Hong Kong (China)     | 119.29.180.130,119.29.208.220,124.156.168.151,150.109.72.54  |
| Beijing Finance | 62.234.240.36,62.234.241.241                                 |
| Shenzhen Finance | 118.89.251.206,139.199.90.75                                 |
| Shanghai Finance | 115.159.237.246,211.159.242.74                               |
| Singapore   | 119.28.103.40,119.28.104.184,119.28.116.123,150.109.11.113   |
| Jakarta   | 43.129.33.41,43.129.35.144                                   |
| Bangkok     | 150.109.164.203,150.109.164.82                               |
| Mumbai     | 119.28.246.130,119.28.246.18                                 |
| Seoul     | 119.28.150.71,119.28.157.173                                 |
| Tokyo     | 150.109.195.201,150.109.196.137                              |
| Silicon Valley     | 49.51.38.216,49.51.39.189                                    |
| Virginia | 170.106.2.63,49.51.85.120                                    |
| Toronto   | 45.113.70.156,45.113.70.6,49.51.10.104,49.51.9.221           |
| Frankfurt | 49.51.132.38,49.51.133.85                                    |
| Moscow   | 162.62.16.46,162.62.21.243                                   |

#### VPN access /Direct Connect/CCN/Self-built on CVM/VPC/Database

| Region     | DTS IP Address                                           |
| ------ | ------------------------------------------------------------ |
| All regions | 10.0.1.1/16,10.1.1.1/16,172.19.1.1/16,169.254.1.1/16,10.200.1.1/16,172.20.1.1/16,<br>10.159.1.1/16,10.45.1.1/16,192.168.1.1/16,172.16.1.1/16,172.30.1.1/16,172.31.1.1/16,<br/>10.26.1.1/16,10.162.1.1/16,10.203.1.1/16,10.206.1.1/16,9.145.1.1/16,9.146.1.1/16,<br/>10.209.1.1/16,10.6.1.1/16,11.163.1.1/16 |

