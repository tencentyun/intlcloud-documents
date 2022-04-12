## Overview
When making a query with an HTTP request method, you can call the `http://119.29.29.98/d? + {request parameters}` API to use HTTPDNS.

>? 
>- After [activating HTTPDNS](https://intl.cloud.tencent.com/document/product/1130/44461), you need to first add a domain to be resolved in the HTTPDNS console as instructed in [Adding a Domain](https://intl.cloud.tencent.com/document/product/1130/44465).
>- The service addresses for the HTTP and HTTPS protocols are `119.29.29.98` and `119.29.29.99` respectively.
>- The new version of the APIs now can be accessed at `119.29.29.99/98`, and the original HTTPDNS service address `119.29.29.29` is for development and debugging purposes only without an SLA guarantee, so it is not recommended for business purposes. Migrate your business to `119.29.29.99/98` as soon as possible.

## Preparations
When using the request API `http://119.29.29.98/d? + {request parameters}`, you need to use the following configuration information, which can be obtained on the [**Development Configuration** page](https://console.cloud.tencent.com/httpdns/configure) in the HTTPDNS console:
![](https://main.qcloudimg.com/raw/ee9bab9e81c1afc51028f467cfc843a9.png)
- **Authorization ID**: It is the unique ID of a development configuration used in HTTPDNS, i.e., the authorization ID parameter passed in when you call the HTTP query API `http://119.29.29.28` of HTTPDNS.
- **DES encryption key**: The key used to encrypt the DNS request data when you call the HTTP DNS API `http://119.29.29.98` of HTTPDNS with DES encryption used.
- **AES encryption key**: The key used to encrypt the DNS request data when you call the HTTP DNS API `http://119.29.29.98` of HTTPDNS with AES encryption used.

## API Description
- API request address: `http://119.29.29.98/d? + {request parameters}`.
- Request method: POST or GET.

## Request Parameters
<table>
<thead>
  <tr>
    <th>Parameter</th>
    <th>Description</th>
    <th>Required</th>
    <th>Value</th>
    <th>Encryption</th>
    <th>Remarks</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>dn</td>
    <td>Queried domain</td>
    <td>Yes</td>
    <td>The length of a single domain before encryption is 253</td>
    <td>Yes</td>
    <td>It must be a domain added in the HTTPDNS console in the form of encrypted string for transfer.<ul style="margin:0"><li>For how to add a domain, see <a href="https://intl.cloud.tencent.com/document/product/1130/44465">Adding a Domain</a>.</li><li>For more information on encryption, see <a href="https://intl.cloud.tencent.com/document/product/1130/44470">Encryption and Decryption Algorithm Use Instructions</a>.</li></ul></td>
  </tr>
  <tr>
    <td>id</td>
    <td>User ID</td>
    <td>Yes</td>
    <td>1–10000</td>
    <td>No</td>
    <td>If you use AES or DES encryption, you must pass in the ID but don't need to encrypt it.</td>
  </tr>
  <tr>
    <td>alg</td>
    <td>Algorithm</td>
    <td>Yes</td>
    <td>[aes/des]</td>
    <td>No</td>
    <td>The DES algorithm is used by default. Different algorithms have different keys.</td>
  </tr>
  <tr>
    <td>ip</td>
    <td>ECS (EDNS-Client-Subnet) value of the DNS request</td>
    <td>No</td>
    <td>IPv4/IPv6 address value</td>
    <td>Yes</td>
    <td>By default, the HTTPDNS server will query the client's egress IP in order to query the IP for the DNS split zone. You can use the `ip=xxx` parameter to specify the split zone's IP address. You can pass in IPv4/IPv6 addresses, which will be automatically identified by the API. For more information on encryption, see <a href="https://intl.cloud.tencent.com/document/product/1130/44470">Encryption and Decryption Algorithm Use Instructions</a>.</td>
  </tr>
  <tr>
    <td>query</td>
    <td>Queried domain returned in the result</td>
    <td>No</td>
    <td>1</td>
    <td>No</td>
    <td>For single-domain queries, this parameter requires the returned result to carry the queried domain.</td>
  </tr>
  <tr>
    <td>timeout</td>
    <td>Timeout period</td>
    <td>No</td>
    <td>1000–5000 ms</td>
    <td>No</td>
    <td>It is the query timeout period, which is 5 seconds by default. Value range: [1000, 5000] ms</td>
  </tr>
  <tr>
    <td>ttl</td>
    <td>Specifies whether to return the TTL value in the query result</td>
    <td>No</td>
    <td>1</td>
    <td>No</td>
    <td>If this parameter is not carried, the TTL value will not be passed by default. Valid value: 1</td>
  </tr>
  <tr>
    <td>type</td>
    <td>Query type</td>
    <td>No</td>
    <td>[aaaa/AAAA/addrs/ADDRS]</td>
    <td>No</td>
    <td>Valid values: [aaaa,AAAA,addrs,ADDRS]. The A record will be queried by default. If AAAA/aaaa is set, the AAAA record will be queried; if addrs/ADDRS is set, both the A and AAAA records will be queried.</td>
  </tr>
  <tr>
    <td>clientip</td>
    <td>Client IP address returned in the query result</td>
    <td>No</td>
    <td>1</td>
    <td>No</td>
    <td>Valid value: 1. If this parameter is not carried, the clientip value will not be passed by default. If a value is assigned to this parameter, the address value will be after the | symbol in the returned result. If the ip parameter is carried, the value of the ip parameter will be returned; otherwise, the client IP address will be returned.</td>
  </tr>
</tbody>
</table>

>?The ECS (EDNS-Client-Subnet) protocol adds the IP address of the user requesting DNS in the DNS request packet, based on which the DNS server can return a server IP address for quicker access by the user.
>


## Request Description
The ID `xxx` is used as an example below.

>!
>- The following samples are for AES/DES encryption, where both the domain and IP parameter need to be encrypted. For example, the domain `cloud.tencent.com` needs to be encrypted, while the authorization ID doesn't.
>- If HTTPDNS does not find the DNS query result, it will return null.
>- HTTPDNS has been connected to BGP Anycast to implement multi-region cross-IDC disaster recovery. However, to guarantee a higher service quality, we recommend you use the [failover policy](https://intl.cloud.tencent.com/document/product/1130/44471) for connection. 

### Requesting A record
- **Sample input:**
```
curl "http://119.29.29.98/d?dn={encrypted string of cloud.tencent.com}&id=xxx"
```
- **Decrypted response format:**
```
2.3.3.4;2.3.3.5;2.3.3.6
```
- **Format description**: Multiple returned query results are separated by semicolon.


### TTL information carried in returned result
- **Sample input:**
```
curl "http://119.29.29.98/d?dn={encrypted string of cloud.tencent.com}&id=xxx&ttl=1"
```
- **Decrypted response format:**
```
2.3.3.4;2.3.3.5;2.3.3.6,120
```
- **Format description**: Multiple returned query results are separated by semicolon. The record values and TTL value are separated by comma.


### Carrying the IP address of query split zone in returned result
- **Sample input:**
```
curl "http://119.29.29.98/d?dn={encrypted string of cloud.tencent.com}&id=xxx&clientip=1&ip={encrypted string of the ECS value of the DNS request}&ttl=1"
```
- **Decrypted response format:**
```
12.3.3.4;2.3.3.5;2.3.3.6,120|1.2.3.4
```
- **Format description**: the returned result carries the split zone's IP address separated by '|'. If the "ip=xxx" parameter is not passed in, the egress IP address will be returned; otherwise, the address in the `ip` parameter will be returned.

### Requesting A and AAAA records at the same time
- **Sample input:**
```
curl "http://119.29.29.98/d?dn={encrypted string of cloud.tencent.com}&id=xxx&clientip=1&ip={encrypted string of the ECS value of the DNS request}&type=addrs&ttl=1"
```
- **Decrypted response format:**
```
2.3.3.4;2.3.3.5;2.3.3.6,120-2402:4e00:0123:4567:0::2345;2403:4e00:0123:4567:0::2346,120|1.2.3.4
```
- **Format description**: The A record is followed by a hyphen and then the AAAA record.


### Carrying queried domain in returned result
- **Sample input:**
```
curl "http://119.29.29.98/d?dn={encrypted string of cloud.tencent.com}&id=xxx&clientip=1&ip={encrypted string of the ECS value of the DNS request}&query=1&ttl=1"
```
- **Decrypted response format:**
```
cloud.tencent.com.:2.3.3.4;2.3.3.5;2.3.3.6,120|1.2.3.4
```
- **Format description**: The response is in the format of "domain.:result".

### Batch querying domains
- **Sample input:**
```
curl "http://119.29.29.98/d?dn={encrypted string of cloud.tencent.com, www.qq.com, and www.dnspod.cn}&id=xxx&clientip=1&ip={encrypted string of the ECS value of the DNS request}&ttl=1"
```
- **Decrypted response format:**
```
cloud.tencent.com.:2.3.3.4;2.3.3.5;2.3.3.6,120
www.qq.com.:3.3.3.4;3.3.3.5;3.3.3.6,180
www.dnspod.cn.:4.3.3.4;4.3.3.5;4.3.3.6,60|1.2.3.4
```
- **Format description:** The returned result of multiple domains are separated by line break, with the IP addresses appended at the end of all record values.

## Description of Request Error or No Record
>!
>- The following samples are for AES/DES encryption, where both the domain and IP parameter need to be encrypted. For example, the domain `cloud.tencent.com` needs to be encrypted, while the authorization ID doesn't.
>- If you use HTTPS, you must change the request address to `119.29.29.99` and pass in the token.
### Querying A record
- **Sample input:**
```
curl "http://119.29.29.98/d?dn={encrypted string of cloud.tencent.com}&id=xxx"
```
- **Decrypted response format:** Empty.
- **Format description:** If there are no records, an empty string will be returned.

### Carrying domain in returned result
- **Sample input:**
```
curl "http://119.29.29.98/d?dn={encrypted string of cloud.tencent.com}&id=xxx&type=addrs&query=1&ip={encrypted string of the ECS value of the DNS request}"
```
- **Decrypted response format:**
```
cloud.tencent.com|1.2.3.4
```
- **Format description:** 0 indicates no records.



### Returning A and AAAA records
- **Sample input:**
```
curl "http://119.29.29.98/d?dn={encrypted string of cloud.tencent.com}&id=xxx&type=addrs&query=1&ip={encrypted string of the ECS value of the DNS request}"
```
- **Decrypted response format:**
```
cloud.tencent.com.:0-0|1.2.3.4
```
- **Format description:** 0 indicates no records. If a record exists, it will be returned in the result. For example, `cloud.tencent.com.:2.3.4.5;3.3.3.3-0|1.2.3.4` indicates that no AAAA records can be found.


### Batch querying domains
- **Sample input:**
```
curl "http://119.29.29.98/d?dn={encrypted string of cloud.tencent.com, www.qq.com, and www.dnspod.cn}&id=xxx&clientip=1&ip={encrypted string of the ECS value of the DNS request}&ttl=1"
```
- **Decrypted response format**:
```
cloud.tencent.com.:0
www.qq.com.:3.3.3.4;3.3.3.5;3.3.3.6,180
www.dnspod.cn.:4.3.3.4;4.3.3.5;4.3.3.6,60|1.2.3.4
```
- **Format description:** For domains about which no data is found, 0 will be returned. If a record exists, it will be returned in the result.

## HTTP Status Codes
The following are the HTTP status codes related to the business logic of the APIs.

| Status Code | Description |
|---------|---------|
| 200 OK | If the API is called correctly, a 200 status code will be returned regardless of whether the query is successful. |
| 404 Not Found | The API does not exist, or the URL actually accesses a resource that does not exist. |
| 429 Too Many Requests | The access requests are too frequent and exceed the limit. |
| 501 Not Implemented | A request method other than "GET" or "POST" is used. |

