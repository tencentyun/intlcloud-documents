
You can download a CDN access log for the last 30 days, which contains the details of every request made to VOD. Logs are recorded hourly.
## Downloading Logs
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and click **Download Log** > **CDN Log** on the left sidebar.
2. Select a time range and domain name to get the download link.
![](https://qcloudimg.tencent-cloud.cn/raw/33fa2bf6cb303e6f5146757e5bef98ff.png)

>?
>- If a domain receives no requests in a day, no logs will be generated, and no data will be displayed.
>- By default, CDN access is logged on an hourly basis. That means 24 log files will be generated at most for a day. No log file will be generated for an hour during which there are no requests.
>- CDN logs may have a delay of about 30 minutes.

## Log Fields
Decompress the package downloaded and open the log files with Notepad. Different fields are separated by space. Below is part of a log file.
![](https://main.qcloudimg.com/raw/db73fc1837d5e6522d137993cfaff50b.png)

| Sequence | Field Meaning |
| --- |------------------------------------------ |
| 1    | Request time                                    |
| 2 | IP address of the client accessing the domain |
| 3    | Accessed domain name                                |
| 4    | File request path                                |
| 5    | Number of bytes of this access request                          |
| 6    | Province. For more information, see [province mapping](#province) below.      |
| 7    | ISP. For more information, see [ISP mapping](#carrier) below. |
| 8    | HTTP status code                                 |
| 9    | Referer information                                |
| 10   | Response time in milliseconds                            |
| 11   | User-Agent information                             |
| 12   | Range parameter                                  |
| 13   | HTTP method                                 |
| 14   | Protocol identifier                                |
| 15   | Cache hit/miss                               |
| 16   | The port via which connection is established between the client and CDN node. If there isn’t such a port, the value of this field is -.                             |


[](id:province)
- **Province mapping**
  22: Beijing; 86: Inner Mongolia; 146: Shanxi; 1069: Hebei; 1177: Tianjin; 119: Ningxia; 152: Shaanxi; 1208: Gansu; 1467: Qinghai; 1468: Xinjiang; 145: Heilongjiang; 1445: Jilin; 1464: Liaoning; 2: Fujian; 120: Jiangsu; 121: Anhui; 122: Shandong; 1050: Shanghai; 1442: Zhejiang; 182: Henan; 1135: Hubei; 1465: Jiangxi; 1466: Hunan; 118: Guizhou; 153: Yunnan; 1051: Chongqing; 1068: Sichuan; 1155: Tibet; 4: Guangdong; 173: Guangxi; 1441: Hainan; 0: Other; 1: Hong Kong, Macao, and Taiwan; -1: outside China
[](id:carrier)
- **ISP mapping**
  2: China Telecom; 26: China Unicom; 38: CERNET; 43: Great Wall Broadband Network; 1046: China Mobile; 3947: China Mobile Tietong; -1: ISPs outside the Chinese mainland; 0: Other ISPs


>! Bandwidth or traffic consumption in logs is based on data returned at the application layer (HTTP protocol) and may be lower than that calculated at the TCP layer due to factors including TCP packet loss, three-way handshake, and retransmission.


