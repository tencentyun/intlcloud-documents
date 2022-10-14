## Overview
CSS routes global push and playback traffic based on DNS resolution by default. This is a common and simple method. However, DNS resolution errors and cross-network traffic occurrences are common due to the complexity of global network environments. We recommend you use Tencent Cloud’s HTTPDNS to optimize traffic routing for live streaming.

An ISP's local DNS egress performs NAT based on an authoritative DNS destination IP address or forwards the resolving request to other DNS servers. This makes it difficult for the authoritative DNS server to correctly identify the IP address of the ISP's local DNS, resulting in resolution errors and cross-network traffic. Tencent Cloud’s HTTPDNS service is powered by leading DNS cluster technologies and supports multi-ISP routing and custom routes.

>? This document shows you how to use HTTPDNS to optimize traffic routing for live streaming across the world. For details about the HTTPDNS API used, see [Querying with HTTP Request Methods](https://intl.cloud.tencent.com/document/product/1130/44468).

## Preparations
1. Activate HTTPDNS. For detailed directions, see [Activating HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461).
2. Go to the [Development Configuration](https://console.cloud.tencent.com/httpdns/configure) page to view the authorization ID and DES key.
![](https://qcloudimg.tencent-cloud.cn/raw/ad5bf89eb5cfe81d4d9b7d19176c622a.png)

## Routing Push Traffic Using HTTPDNS

### Requesting a push IP address

Use an HTTP GET request in the format of `http://119.29.29.98/d?dn={$push_domain DES-encrypted string}&ip={$ip DES-encrypted string}&id=$id` to request a push IP address from HTTPDNS.

- `push_domain` indicates the push domain, which must be encrypted using the DES algorithm. You can view the key on the [HTTPDNS Development Configuration](https://console.cloud.tencent.com/httpdns/configure) page. For details, see [AES/DES Encryption/Decryption](https://intl.cloud.tencent.com/document/product/1130/44470).
- `ip` indicates the public egress IP address of the requester. This field determines the region and ISP of the IP address to which traffic is routed. It also needs to be encrypted using the DES algorithm.
- `id` indicates the authorization ID, which uniquely identifies a user.

### Decrypting the IP address

The data obtained from HTTPDNS is DES-encrypted. Decrypt it to get the IP address (`server_ip`). For details, see [AES/DES Encryption/Decryption](https://intl.cloud.tencent.com/document/product/1130/44470).

### Splicing the push URL

The format of a push URL is `rtmp://server_ip/live/streamname?txTime=xxx&txSecret=xxx&txHost=domain`. `server_ip` is the **push IP address obtained in the previous step**. `txHost` (important) is the domain you use for push.

## Routing Playback Traffic Using HTTPDNS

### Requesting the playback IP address

Use an HTTP GET request in the format of `http://119.29.29.98/d?dn={$domain DES-encrypted string}&ip={$ip DES-encrypted string}&id=$id` to request the playback IP address from HTTPDNS.

| Field | Description |
|---------|---------|
| push_domain | The playback domain. The value of this field must be encrypted using the DES algorithm. You can view the key on the [HTTPDNS Development Configuration](https://console.cloud.tencent.com/httpdns/configure) page. For details, see [AES/DES Encryption/Decryption](https://intl.cloud.tencent.com/document/product/1130/44470). |
| ip | The public egress IP address of the requester. This field determines the region and ISP of the IP address to which traffic is routed. It also needs to be encrypted using the DES algorithm. |
| id | The authorization ID, which uniquely identifies a user. |

### Decrypting the IP address

The data obtained from HTTPDNS is DES-encrypted. Decrypt it to get the IP address (`server_ip`). For details, see [AES/DES Encryption/Decryption](https://intl.cloud.tencent.com/document/product/1130/44470).

### Splicing the playback URL
- **HTTP**: The formats of HTTP playback URLs for FLV and HLS are as follows (`server_ip` is the **playback IP address obtained in the previous step** and `play_domain` is the playback domain):
```
http://server_ip/play_domain/live/streamname.flv?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname.m3u8?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname -123.ts?xxxxxxxxxx
```
- **HTTPS**: The splicing rules of HTTPS playback URLs for FLV and HLS depend on the player. **The destination IP address of the TCP connection must be the `server_ip` assigned by HTTPDNS**, and the URLs should be regular playback requests. The formats are as follows:
```
https://server_ip/play_domain/live/ streamname.flv?xxxxxxxxxx
https://server_ip/play_domain/live/ streamname.m3u8?xxxxxxxxxx
https://server_ip/play_domain/live/ streamname -123.ts?xxxxxxxxxx
```
- **RTMP**: The format of an RTMP playback URL is as follows (`server_ip` is the **playback IP address obtained in the previous step** and `play_domain` is the playback domain):
```
rtmp://server_ip/play_domain/live/ streamname?xxxxxxxxxx
```

>? There is a small likelihood of HTTPDNS request errors. If your request times out or the result returned is not an IP address or is empty, please perform resolution at the local DNS server.
