
You can download a CDN access log for the last 30 days, which contains details of every request made to VOD. Logs are recorded hourly.
## Downloading a CDN Log
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod) and click **Log Download** > **CDN Log** on the left sidebar.
2. Select the desired time range and domain name, and click **OK** to get the log download link.
![](https://main.qcloudimg.com/raw/4f651b5c1fafbb3a382f4ce9b09314c7.png)
>
>- No access logs will be generated for a day on which there is no request received, and you will see "No Data" on the page.
>- By default, the CDN logs requests on an hourly basis, that is, there can be up to 24 log files generated per day. No logs will be generated for the hour in which there is no request received.
>- CDN logs can be delayed by approximately 30 minutes.

## Descriptions of Log Fields
Decompress the downloaded log data packages and view the log files in text format. The fields are separated by space. Below is an example:
![](https://main.qcloudimg.com/raw/db73fc1837d5e6522d137993cfaff50b.png)

| Order | Log Content |
| --- |------------------------------------------ |
| 1    | Request time                                    |
| 2 | IP of the client accessing the domain name |
| 3    | Accessed domain name                                |
| 4    | File request path                                |
| 5    | Number of bytes of this access request                          |
| 6    | District; for more information, please see [district mappings](#province) below      |
| 7    | ISP; for more information, please see [ISP mappings](#carrier) below |
| 8    | HTTP status code                                 |
| 9    | Referer information                                |
| 10   | Response time in milliseconds                            |
| 11   | User-Agent information                             |
| 12   | Range parameter                                  |
| 13   | HTTP method                                 |
| 14   | HTTP protocol identifier                                |
| 15   | Cache hits/misses                               |


<span id="province"></span>
- **District mappings**
  22: Beijing; 86: Inner Mongolia; 146: Shanxi; 1069: Hebei; 1177: Tianjin; 119: Ningxia; 152: Shaanxi; 1208: Gansu; 1467: Qinghai; 1468: Xinjiang; 145: Heilongjiang; 1445: Jilin; 1464: Liaoning; 2: Fujian; 120: Jiangsu; 121: Anhui; 122: Shandong; 1050: Shanghai; 1442: Zhejiang; 182: Henan; 1135: Hubei; 1465: Jiangxi; 1466: Hunan; 118: Guizhou; 153: Yunnan; 1051: Chongqing; 1068: Sichuan; 1155: Tibet; 4: Guangdong; 173: Guangxi; 1441: Hainan; 0: Other; 1: Hong Kong, Macao, and Taiwan; -1: Overseas.
<span id="carrier"></span>
- **ISP mappings**
  2: China Telecom; 26: China Unicom; 38: CERNET; 43: Great Wall Broadband Network; 1046: China Mobile; 3947: China Mobile Tietong; -1: Overseas ISP; 0: Other ISPs.


>The bandwidth or traffic data recorded in logs is the returned data at the application layer (HTTP protocol), which is smaller than that calculated at the TCP layer due to such factors as TCP protocol packet loss, three-way handshake, and retransmission.
