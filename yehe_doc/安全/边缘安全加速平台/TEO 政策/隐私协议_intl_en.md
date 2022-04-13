## 1. INTRODUCTION
This Module applies if you use TencentCloud EdgeOne (“Feature”). This Module is incorporated into the privacy policy located at [Privacy Policy](https://intl.cloud.tencent.com/document/product/301/17345) . Terms used but not defined in this Module shall have the meaning given to them in the Privacy Policy. In the event of any conflict between the Privacy Policy and this Module, this Module shall apply to the extent of the inconsistency.
## 2. CONTROLLERSHIP
The controller of the personal information described in this Module is as specified in the Privacy Policy.
## 3. AVAILABILITY
This Feature is available to users globally.
## 4. HOW WE USE PERSONAL INFORMATION
We will use the information in the following ways and in accordance with the following legal basis:

| **Personal Information**                                     | **Use**                                                      | **Legal Basis**                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Edge Node Access Log Data:** Access timestamp, client IP address, node server public IP address, host, port, URL, accessed HTTP headers (HTTP requests of the end-user, such as user-agent, referer, cookie), POST data body (the first 10KB), whether there are malicious attacks, triggered security rules | We use this information for the purpose of providing the Feature to you, including:<li>for user queries on the business traffic and top access status of different dimensions (such as URL, UA);<li>analyzing traffic risks and identifying malicious characteristics; and<li>troubleshooting.<br/>Please note that this data is integrated with our ClickHouse feature for storage and pre-aggregation purposes, and is also stored in our Cloud Virtual Machine (CVM), Cloud Object Storage (COS) and ClickHouse features. | We process this information as it is necessary for us to perform our contract with you to provide the Feature. |
| **Traffic Data:** Access traffic data of each host on a single server IP (incoming traffic, outgoing traffic, number of requests) | We use this information for the purpose of calculating the number of user visits, for billing purposes. <br/>Please note that this data is integrated with our ClickHouse feature for storage and pre-aggregation purposes, and is also stored and backed up in our TencentDB for MySQL feature. | We process this information as it is necessary for us to perform our contract with you to provide the Feature. |
| **System Configuration Data:** Node configuration data (IP, ISP, address), server cluster configuration data, API configuration data, DB addresses and keys | We use this information for the purpose of providing the Feature to you, including ensuring the proper functioning of the content delivery network (CDN). <br/>Please note that this data is stored and backed up in our TencentDB for MySQL feature. | We process this information as it is necessary for us to perform our contract with you to provide the Feature. |
| **API Access Log Data:** Access timestamp, client IP address, API server intranet IP address, URL, request body (including your configuration data), response body (including your configuration data) | We use this information for the purpose of troubleshooting. <br/>Please note that this data is integrated with our Cloud Audit feature to provide CAM authentication and audit logs, and is stored in our Cloud Log Service feature. | We process this information as it is necessary for us to perform our contract with you to provide the Feature. |

## 5. HOW WE SHARE AND STORE PERSONAL INFORMATION
As specified in the Privacy Policy. 
Additionally, APPID and UIN is stored in our TencentDB for MySQL feature.
## 6. DATA RETENTION
We will retain personal information in accordance with the following:

| **Personal Information**          | **Retention Policy** |
| -------------------------           | -------------------- |
| Edge Node Access Log Data        | Stored for 30 days.  |
| Traffic Data        | Stored for 30 days, after which such data is anonymized. |
| System Configuration Data            | We retain such data for as long as you use the Feature. When your use of the Feature is terminated, we will delete this data after 30 days. |
| API Access Log Data         | Stored for 180 days. |