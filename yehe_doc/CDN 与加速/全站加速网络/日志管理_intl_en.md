You can download the detailed logs of user access to your connected domain names for the last 40 days for analysis, which are recorded hourly.
>? If your application has been migrated to the CDN console, you can go to the console for operation by referring to [Content Delivery Network](https://intl.cloud.tencent.com/document/product/228).

## Downloading Logs
Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and select **Log Management** on th left sidebar. Select the domain for which you want to check logs and the time period. Then, click **OK** to get the log download link.
![](https://main.qcloudimg.com/raw/3b735673ecd023a7d905d22b334d8a51.png)
No access logs will be generated for the queried time period in which there is no request received, and you will see **No Data** on the page.
>!
> + By default, the ECDN logs requests on an hourly basis, that is, there can be 24 log files generated per day. No logs will be generated for the hour in which there is no request received.  
> + ECDN logs can be delayed by approximately 30 minutes.

## Log Field Description
Decompress the downloaded log data packages and view the log files in text format. The fields are separated by space. Below is an example:
![](https://mc.qcloudimg.com/static/img/a3ef1ea051dc277872ec10a7135872df/logs.png)
The corresponding fields (from left to right) and their descriptions in a log are as shown below:

| Order | Log Content                                        |
| ---- | ----------------------------------------------- |
| 1    | Request time                                        |
| 2    | IP of the client accessing the domain name                             |
| 3    | Accessed domain name                                    |
| 4    | File request path                                    |
| 5    | Number of bytes of this access request                              |
| 6    | District (for the district codes, please see **District mappings** below)       |
| 7    | ISP (for the district codes, please see **ISP mappings** below) |
| 8    | HTTP status code                                     |
| 9    | Referer information                                    |
| 10   | Response time in milliseconds                                |
| 11   | User-Agent information                                 |
| 12   | Range parameter                                      |
| 13   | HTTP Method                                     |
| 14   | HTTP protocol identifier                                    |
| 15   | Cache hit/miss (all resources are not cached in dynamic acceleration by default)         |

### Region mappings
1: North China; 2: Northwest China; 3: Northeast China; 4: East China; 5: Central China; 6: Southwest China; 7: South China; 8: outside Mainland China.

### District mappings
22: Beijing; 86: Inner Mongolia; 146: Shanxi; 1069: Hebei; 1177: Tianjin; 119: Ningxia; 152: Shaanxi; 1208: Gansu; 1467: Qinghai; 1468: Xinjiang; 145: Heilongjiang; 1445: Jilin; 1464: Liaoning; 2: Fujian; 120: Jiangsu; 121: Anhui; 122: Shandong; 1050: Shanghai; 1442: Zhejiang; 182: Henan; 1135: Hubei; 1465: Jiangxi; 1466: Hunan; 118: Guizhou; 153: Yunnan; 1051: Chongqing; 1068: Sichuan; 1155: Tibet; 4: Guangdong; 173: Guangxi; 1441: Hainan; 0: Other; 1: Hong Kong, Macao, and Taiwan; -1: outside Mainland China.

### ISP mappings
2: China Telecom; 26: China Unicom; 38: CERNET; 43: Great Wall Broadband Network; 1046: China Mobile; 3947: China Mobile Tietong; -1: ISP outside Mainland China; 0: Other ISPs.

## Precautions
The bandwidth or traffic data recorded in logs is the returned data at the application layer (HTTP protocol), which is smaller than that calculated at the TCP layer due to such factors as TCP protocol packet loss, three-way handshake, and retransmission.

## Downloading ECDN Logs Outside China
At present, ECDN outside Mainland China is in beta test. If you have enabled it, you can submit a ticket to apply for the log service.
