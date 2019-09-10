## Solution Background
The global push and playback scheduling of LVB is based on the DNS of the domain name by default, which is the most common and simplest access method. Due to the complexity of global network environments, domain name resolution errors or cross-network traffic occur frequently. LVB recommends that you use the HttpDNS solution to optimize global live broadcasting scheduling.

An ISP's LocalDNS egress performs NAT based on an authoritative DNS destination IP address or forwards the resolving request to other DNS servers, making it impossible for the authoritative DNS to correctly identify the ISP's LocalDNS IP and thus causing domain name resolution errors and cross-network traffic.
Empowered by world-leading DNS cluster technology, Tencent Cloud HttpDNS supports multiple ISPs and custom lines for optimal scheduling. 


>This document uses the free edition of HttpDNS as an example to describe how to use the HttpDNS scheduling solution for Tencent Cloud Global LVB.

## Scheduling Upstream Push Using HttpDNS

### 1. Requesting the Upstream Access Point IP
`http://119.29.29.29/d?dn=$push_domain.&ip=$ip`, which is an HTTP Get request. The meanings of the parameters are as follows:
- push_domain represents the push domain name.
- The IP field represents the external network egress IP of the requester, which indicates the region and ISP where the scheduled access point IP resides.


### 2. Splicing the Upstream Push URL
Here, server_ip is the IP obtained in **Requesting the Upstream Access Point IP**, and the spliced push URL is as follows:
`rtmp://server_ip/live/streamname?txTime=xxx&txSecret=xxx&txHost=domain`. The most important step is to add the txHost field representing the push domain name of the service to the original push parameters.

## Scheduling Downstream Playback Using HttpDNS

### 1. Requesting the Downstream Access Point IP
`http://119.29.29.29/d?dn=$domain.&ip=$ip`, which is an HTTP Get request. The meanings of the parameters are as follows:
- domain represents the playback domain name.
- The IP field represents the external network egress IP of the requester, which indicates the region and ISP where the scheduled access point IP resides.


### 2. Splicing the Downstream Playback URL
- HTTP: Including the playback protocols of FLV and HLS. Here, server_ip is the IP obtained in **Requesting the Downstream Access Point IP** and play_domain represents the playback domain name. The spliced HTTP playback URL is as follows:

```
http://server_ip/play_domain/live/streamname.flv?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname.m3u8?xxxxxxxxxx
http://server_ip/play_domain/live/ streamname -123.ts?xxxxxxxxxx
```

- HTTPS: Including the playback protocols of FLV and HLS. Here, server_ip is the IP obtained in **Requesting the Downstream Access Point IP** and play_domain represents the playback domain name. The HTTPS splicing rule depends on the player's logic. **The destination IP to which a connection is established based on TCP has to be the server_ip of the HttpDNS scheduling**, and the specific requested playback URL needs to be for a regular playback request:

```java
https://play_domain/live/ streamname.flv?xxxxxxxxxx
https://play_domain/live/ streamname.m3u8?xxxxxxxxxx
https://play_domain/live/ streamname -123.ts?xxxxxxxxxx
```

- RTMP: Here, server_ip is the IP obtained in **Requesting the Downstream Access Point IP** and play_domain represents the playback domain name. The spliced RTMP playback URL is as follows:

```
rtmp://server_ip/play_domain/live/ streamname?xxxxxxxxxx
```

>The schemes above are all based on the global scheduling platform of LVB and should not be used for scheduling in Mainland China without necessary modifications. If you want to use HttpDNS to optimize LVB scheduling in Mainland China, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
