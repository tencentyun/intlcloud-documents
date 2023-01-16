IP geographic functions can be used to determine whether an IP address belongs to a private or public network or analyze the country, province, or city to which an IP address belongs. This document introduces the basic syntax and examples of IP geographic functions.



## IP Address Function

>?
> - The `KEY` field in the following functions indicates the log field (for example, `ip`) and its value is an IP address. If the value is an internal IP address or an invalid field, the value cannot be parsed and is displayed as `NULL` or `Unknown`.
> - Currently, only IPv4 addresses are supported.
> - Due to the limitations of the IP address assignment mechanism, the IP address database cannot accurately cover all the geographic information of IP addresses. For a few IP addresses, the detailed geographic information may fail to be queried or the geographic information found may be incorrect.
> 

| Function                             | Description                                                         | Example                                                         |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------ |
| ip_to_domain(KEY) [](id:ip_to_domain)         | Determines whether an IP address belongs to a private or public network. Valid values are `intranet` (private network IP address), `internet` (public network IP address), and `invalid` (invalid IP address). | `* \| SELECT ip_to_domain(ip)`        |
| ip_to_country(KEY)[](id:ip_to_country)       | Analyzes the country or region to which an IP address belongs. The country's or region's name is returned. | `* \| SELECT ip_to_country(ip)`       |
| ip_to_country_code(KEY)[](id:ip_to_country_code)   | Analyzes the code of the country or region to which an IP address belongs. The country's or region's code is returned. | `* \| SELECT ip_to_country_code(ip)`  |
| ip_to_country_geo(KEY)[](id:ip_to_country_geo)   | Analyzes the latitude and longitude of the country or region to which an IP address belongs. The country's or region's latitude and longitude are returned. | `* \| SELECT ip_to_country_geo(ip`)   |
| ip_to_province(KEY) [](id:ip_to_province)   | Analyzes the province to which an IP address belongs. The province's name is returned.         | `* \| SELECT ip_to_province(ip)`      |
| ip_to_province_code(KEY)[](id:ip_to_province_code)  | Analyzes the code of the province to which an IP address belongs. The province's administrative zone code is returned. | `* \| SELECT ip_to_province_code(ip)` |
| ip_to_province_geo(KEY)[](id:ip_to_province_geo)  | Analyzes the latitude and longitude of the province to which an IP address belongs. The province's latitude and longitude are returned.   | `* \| SELECT ip_to_province_geo(ip)`  |
| ip_to_city [](id:ip_to_city)                | Analyzes the city to which an IP address belongs. The city's name is returned. | `* \| SELECT ip_to_city(ip)`          |
| ip_to_city_code [](id:ip_to_city_code)          | Analyzes the code of the city to which an IP address belongs. The city's administrative zone code is returned. Currently, cities in Taiwan (China) and outside China are not supported. | `* \| SELECT ip_to_city_code(ip)`     |
| ip_to_city_geo [](id:ip_to_city_geo)         | Analyzes the latitude and longitude of the city to which an IP address belongs. The city's latitude and longitude are returned. Currently, cities in Taiwan (China) and outside China are not supported. | `* \| SELECT ip_to_city_geo(ip)`      |
| ip_to_provider(KEY) [](id:ip_to_provider)       | Analyzes the ISP to which an IP address belongs. The ISP's name is returned. | `* \| SELECT ip_to_provider(ip)`      |

## IP Range Function

>?
> - The `KEY` field in the following functions indicates the log field (for example, `ip`) and its value is an IP address.
> - In the `ip_subnet_min`, `ip_subnet_max`, and `ip_subnet_range` functions, the value of the `KEY` field is an IP address with a subnet mask (for example, 192.168.1.0/24). If the value field is a general IP address, you need to use the `cancat` function to convert it to an IP address with a subnet mask.
> 

| Function                                  | Description                                                         | Example                                                         |
| -------------------------- | ------------------------------------------------------------ | -------------------------------------------- |
| ip_prefix(KEY,prefix_bits)[](id:ip_prefix) | Gets the prefix of an IP address. An IP address with a subnet mask is returned, for example, `192.168.1.0/24`. | `* \| SELECT ip_prefix(ip,24)`                 |
| ip_subnet_min(KEY)   [](id:ip_subnet_min)          | Gets the smallest IP address in an IP range. The return value is an IP address, for example, `192.168.1.0`. | `* \| SELECT ip_subnet_min(concat(ip,'/24'))`  |
| ip_subnet_max(KEY)  [](id:ip_subnet_max)          | Gets the largest IP address in an IP range. The return value is an IP address, for example, `192.168.1.255`. | `* \| SELECT ip_subnet_max(concat(ip,'/24'))`   |
| ip_subnet_range(KEY) [](id:ip_subnet_range)     | Gets the range of an IP range. The return value is an IP address of the Array type, for example, `[[192.168.1.0, 192.168.1.255]]`. | `* \| SELECT ip_subnet_range(concat(ip,'/24'))` |
|  is_subnet_of [](id:is_subnet_of)    | Determines whether an IP address is in a specified IP range. The return value is of the Boolean type. | `* \| SELECT is_subnet_of('192.168.0.1/24', ip)` |
|  is_prefix_subnet_of  [](id:is_prefix_subnet_of)     | Determines whether an IP range is a subnet of a specified IP range. The return value is of the Boolean type. | `* \| SELECT is_prefix_subnet_of('192.168.0.1/24',concat(ip, '/24'))` |



## Examples

The following are query and analysis statement examples of IP geographic functions. After performing such query and analysis operations, you can select appropriate statistics charts to display the query and analysis results.

>? In the following examples, the log field is `ip`.
>

- Count the total number of requests that are not from the private network:
```
* | SELECT count(*) AS PV where ip_to_domain(ip)!='intranet'
```

- Find the top 10 provinces with the largest total number of requests:
```
* | SELECT ip_to_province(ip) AS province, count(*) as PV GROUP BY province ORDER BY PV desc LIMIT 10
```

If the result includes requests from the private network and you want to exclude them, use the following query and analysis statement:

```
* | SELECT ip_to_province(ip) AS province, count(*) as PV where ip_to_domain(ip)!='intranet' GROUP BY province ORDER BY PV desc LIMIT 10
```
- Collect the longitude and latitude statistics of IP addresses to determine client distribution:
```
* | SELECT ip_to_geo(ip) AS geo, count(*) AS pv GROUP BY geo ORDER BY pv DESC
```














