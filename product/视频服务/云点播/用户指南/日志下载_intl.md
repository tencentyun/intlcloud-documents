
Tencent Cloud VOD enables you to download the most recent 30-day CDN access log files, which contains detailed information about every request that your Tencent Cloud VOD received.
## Downloading a CDN Access Log
Log in to the [VOD Console](https://console.cloud.tencent.com/video/cdnlog) and select **Download Log** > [CDN Logs] in the left navigation pane. Select the desired time range and domain name, and click **OK** to get the log download link.
![](https://main.qcloudimg.com/raw/dfd43c068bfc861fb0df3ae4719b2f4c.png)
>!
- No access logs will be generated for the day on which there is no request received, and you will see "No data".
- By default, the CDN logs the requests on an hourly basis. That is, there are up to 24 log files logged per day. No logs will be generated for the hour in which there is no request received.
- Timing of log files delivery: Tencent Cloud VOD delivers the log file for that time period within around half an hour of the events that appear in the log.

## Log Field Description
Decompress the downloaded log data packages and view the log files as text files. You can see that the fields are separated by spaces. Below is an example:
![](https://main.qcloudimg.com/raw/4ad0e7f934c666a52ed80791d9e4a3e5.png)

| Order | Log content |
| --- |------------------------------------------ |
| 1    | Request time                                    |
| 2 | IP of the client accessing the domain name |
| 3    | Accessed domain name                                |
| 4    | File request path                                |
| 5    | Number of bytes of this access request                          |
| 6    | Province; for more information, see the [province mappings](#province) below      |
| 7    | ISP; for more information, see the [ISP mappings](#carrier) below |
| 8    | HTTP status code                                 |
| 9    | Referer information                                |
| 10   | Response time in milliseconds                            |
| 11   | User-Agent information                             |
| 12   | Range parameter                                  |
| 13   | HTTP method                                 |
| 14   | HTTP protocol identifier                                |
| 15   | Cache hits/misses                               |


<span id="province"></span>
- **Province Mappings**
  22: Beijing; 86: Inner Mongolia; 146: Shanxi; 1069: Hebei; 1177: Tianjin; 119: Ningxia; 152: Shaanxi; 1208: Gansu; 1467: Qinghai; 1468: Xinjiang; 145: Heilongjiang; 1445: Jilin; 1464: Liaoning; 2: Fujian; 120: Jiangsu; 121: Anhui; 122: Shandong; 1050: Shanghai; 1442: Zhejiang; 182: Henan; 1135: Hubei; 1465: Jiangxi; 1466: Hunan; 118: Guizhou; 153: Yunnan; 1051: Chongqing; 1068: Sichuan; 1155: Tibet; 4: Guangdong; 173: Guangxi; 1441: Hainan; 0: Other; 1: Hong Kong, Macao, and Taiwan; -1: Overseas.
<span id="carrier"></span>
- **ISP Mapping**
  2: China Telecom; 26: China Unicom; 38: CERNET; 43: Great Wall Broadband Network; 1046: China Mobile; 3947: China Mobile Tietong; -1: Overseas ISP; 0: Other ISPs.

## Precautions

Due to less bandwidth/traffic consumed by such as TCP packet loss, three-way handshake, and retransmission on application layer than that on the transport layer, bandwidth/traffic data recorded in the logs is the data of the packets return on the application layer (HTTP protocol).
