
Tencent Cloud VOD supports downloading detailed access requests to a domain name by providing CDN logs at the hour level. You can download the logs for the last 30 days.
## Downloading a CDN Log
Log in to the [VOD Console](https://console.cloud.tencent.com/video/cdnlog) and select **Download Log** > [CDN Logs] in the left navigation pane. Select the time range and domain name for which you want to obtain logs, and click **OK** to get the log download link.
![](https://main.qcloudimg.com/raw/dfd43c068bfc861fb0df3ae4719b2f4c.png)
>!
- If there is no request to the domain name on a day, no logs will be generated, and the page will display "No data".
- The CDN logs are divided by hour by default, that is, there are up to 24 log files per day. If there is no request to the domain name in an hour, no log data packages will be generated.
- In term of real-timeness, the CDN logs are delayed by about half an hour.

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

As the bandwidth or traffic consumed by mechanisms such as TCP packet loss, three-way handshake, and retransmission counted on the application layer is smaller than that counted on the transport layer, the bandwidth or traffic data recorded in the logs is the return packet data on the application layer (HTTP protocol).
