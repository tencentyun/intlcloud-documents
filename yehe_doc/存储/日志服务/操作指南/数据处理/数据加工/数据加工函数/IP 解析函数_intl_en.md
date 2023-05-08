## Function geo_parse

### Function definition

This function is used to parse the geographical location.

### Syntax description

```sql
geo_parse(field value, keep=("country","province","city"), ip_sep=",")
```

### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data | IP value. Separate multiple IPs by separator. | string | Yes |-|-|
| keep | The field to be reserved | string | No | 	("country","province","city")	 |-|
| ip_sep | The number of the expression in the match result | string | No |-|-|

### Sample

- Example 1
Raw log:
```
{"ip":"101.132.57.150"}
```
Processing rule:
```
fields_set("result", geo_parse(v("ip")))
```
Processing result:
```
{"ip":"101.132.57.150","result":"{\"country\":\"China\",\"province\":\"Shanghai\",\"city\":\"Shanghai\"}"}
```
- Example 2
Raw log:
```
{"ip":"101.132.57.150,101.14.57.157"}
```
Processing rule:
```
fields_set("result", geo_parse(v("ip"),keep="province,city",ip_sep=","))
```
Processing result:
```
{"ip":"101.132.57.150,101.14.57.157", "result":"{\"101.14.57.157\":{\"province\":\"Taiwan\",\"city\":\"NULL\"},\"101.132.57.150\":{\"province\":\"Shanghai\",\"city\":\"Shanghai\"}}"}
```


## Function is_subnet_of
### Function definition
This function is used to check whether an IP is in the target IP range. Multiple IP ranges are supported.

### Syntax description

```
is_subnet_of(IP range list, IP)
```

### Parameter description
| Parameter  	 | Description  	   | Type	 | Required  	| Default Value 	| Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| IP range list |	IP range. Separate multiple IP ranges by comma. 	|String	| Yes |	-|	-|
|IP|	The IP to be checked |	String|	 Yes |	-|	-|


### Sample
- Example 1
Raw log:
```
{"ip": "192.168.1.127"}
```
Processing rule:
```
log_keep(is_subnet_of("192.168.1.64/26",v("ip")))
```
Processing result:
```
{"ip": "192.168.1.127"}
```
- Example 2
Raw log:
```
{"ip": "192.168.1.127"}
```
Processing rule:
```
fields_set("is_subnet",is_subnet_of("192.168.1.64/26",v("ip")))
```
Processing result:
```
{"ip": "192.168.1.127", "is_subnet":"true"}
```
- Example 3
Raw log:
```
{"ip": "192.168.1.127"}
```
Processing rule:
```
fields_set("is_subnet",is_subnet_of("172.16.0.0/16",v("ip")))
```
Processing result:
```
{"ip": "192.168.1.127", "is_subnet":"false"}
```
- Example 4
Raw log:
```
{"ip": "192.168.1.127"}
```
Processing rule:
```
fields_set("is_subnet",is_subnet_of("172.16.0.0/16,192.168.1.64/26",v("ip")))
```
Processing result:
```
{"ip": "192.168.1.127", "is_subnet":"true"}
```


