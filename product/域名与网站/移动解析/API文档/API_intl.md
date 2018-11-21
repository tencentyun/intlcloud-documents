## Querying by Domain Name and User IP
Both the data request and response use the HTTP protocol.
The request format is:
```
http://119.29.29.29/d?dn=www.dnspod.cn.&ip=1.1.1.1
```
Here, `dn` indicates the domain name to be queried;
`ip` indicates the user IP. If `ip` is a private or invalid IP, the source IP of the HTTP message will be used as the user IP by default. At this time, HttpDNS will resolve based on the default route set by the user.
### Domain Name Exists
If HttpDNS can query the IP to which the domain name points, it will return the IP directly.
Take the following request as an example:
```
http://119.29.29.29/d?dn=www.dnspod.cn.&ip=1.1.1.1
```
Return
```
183.60.57.155
```
![Return value 1](//mccdn.qcloud.com/static/img/ad7dbfd17112fba557f96deec30677df/image.png)

### Domain Name Doesn't Exist
If the domain name doesn't exist, HttpDNS will not be able to query the corresponding IP, so it returns null.
Take the following request as an example:
```
http://119.29.29.29/d?dn=www.dnspod2.cn.&ip=1.1.1.1
```
An empty string is returned as shown below:
![Return value 2](//mccdn.qcloud.com/static/img/15b5daaeeedd2f2c68c00465554dbae2/image.png)


## Querying the Result with TTL by Domain Name and User IP
Both the data request and response use the HTTP protocol.
The request format is:
```
http://119.29.29.29/d?dn=www.dnspod.cn.&ip=1.1.1.1&ttl=1
```
`ttl=1` indicates that the returned result is required to bring the TTL value of the resolution result.
The returned TTL and domain name resolution result are separated by commas.

Take the following request as an example: it indicates that the result is required to bring the TTL:
```
http://119.29.29.29/d?dn=www.dnspod.cn.&ip=1.1.1.1&ttl=1
```
The return value is as follows, indicating that the TTL of the recursive server cache is 60 seconds:
```
183.60.57.155,60
```:
![Return value 3](//mccdn.qcloud.com/static/img/0e845c5b777dbcd81ebb800437c786ee/image.png)
