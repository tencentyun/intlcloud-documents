## 1. API Description
API request domain name: cws.tencentcloudapi.com.

This API (DescribeVuls) is used to query the details of one or more vulnerabilities.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/692/16736).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeVuls |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-12 |
| Region | No | String | Common parameter; not passed in for this API |
| SiteId | No | Integer | Website ID |
| MonitorId | No | Integer | Monitoring task ID |
| Filters.N | No | Array of [Filter](/document/api/692/16759#Filter) | Filters |
| Offset | No | Integer | Offset; 0 by default |
| Limit | No | Integer | Number of returns; 10 by default, up to 100 |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of vulnerabilities. |
| Vuls | Array of [Vul](/document/api/692/16759#Vul) | List of vulnerability information items. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1 Viewing Vulnerability List

#### Input

```
https://cws.tencentcloudapi.com/?Action=DescribeVuls
&Filters.0.Name=Name
&Filters.0.Values.0=SQL
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "RequestId": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a",
    "TotalCount": 10,
    "Vuls": [
      {
        "CreatedAt": "2018-03-24T15:38:31+08:00",
        "Describe": "SQL injection vulnerability is a security threat that can be used by attackers to modify backend SQL queries through carefully constructed request data. It occurs when the web application executes the user-entered data directly as SQL statements without performing any processing such as dangerous character filtering or statement filtering. <br/><br/>Currently, SQL injection vulnerability is the most common vulnerability in the Internet with wide impact. In the second half of 2007, many websites were tampered with. The attackers exploited SQL injection vulnerability to modify the text in the database used to generate dynamic webpages, thus injecting malicious HTML script tags. Such attacks began to accelerate in the first quarter of 2008 and continued to affect vulnerable web applications." ,
        "From": "OWASP: <a target=_blank href=\"https://www.owasp.org/index.php/SQL_Injection\">SQL Injection</a>    WASC: <a target=_blank href=http://projects.webappsec.org/SQL-Injection>SQL Injection</a>    CVE: Not applicable   CWE: <a target=_blank href=http://cwe.mitre.org/data/definitions/89.html>89</a>",
        "Harm": "Data leakage - SQL injection vulnerability can lead to the following consequences: <br/>1. Confidential data is stolen <br/>2. Core business data is tampered with <br/>3. Webpage is tampered with <br/>4. The server where the database resides is attacked and turned into a zombie, and even the enterprise network is invaded." ,
        "Html": "<a target=_blank href=\"http://demo.aisec.cn:80/demo/aisec/ajax_link.php?t=0.2553907226758148&id=1-0\">http://demo.aisec.cn:80/demo/aisec/ajax_link.php?t=0.2553907226758148&id=1-0</a>\n<br><br>[Database Version:MYSQL]: <a target=_blank href=\"http://demo.aisec.cn:80/demo/aisec/ajax_link.php?t=0.2553907226758148&id=1-ROW_COUNT%28%29-%28-ROW_COUNT%28%29%29\">http://demo.aisec.cn:80/demo/aisec/ajax_link.php?t=0.2553907226758148&id=1-ROW_COUNT%28%29-%28-ROW_COUNT%28%29%29</a>\n<br><br>[Inject SELECT Statement:Success]: <a target=_blank href=\"http://demo.aisec.cn:80/demo/aisec/ajax_link.php?t=0.2553907226758148&id=1-%28%09select%090%09%29\">http://demo.aisec.cn:80/demo/aisec/ajax_link.php?t=0.2553907226758148&id=1-%28%09select%090%09%29</a>",
        "Id": 13,
        "Level": "high",
        "Name": "SQL Injection",
        "Nickname": "Data leakage - SQL injection vulnerability",
        "Parameter": "id",
        "SiteId": 1,
        "Solution": "The following methods can prevent injection attacks: <br/>1. Strictly filter the data entered by the user in the webpage code. <br/>2. Use the preprocessor to execute the SQL statements and bind the variables in all incoming SQL statements. <br/>3. Deploy a web application firewall <br/>4. Monitor database operations<br/>",
        "TaskId": 949057,
        "UpdatedAt": "2018-03-24T15:38:31+08:00",
        "Url": "http://demo.aisec.cn:80/demo/aisec/ajax_link.php?t=0.2553907226758148&id=1-0"
      }
    ]
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/692/16738#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter.Malformed | Incorrect data format. |
| InvalidParameter.NotFound | The requested data does not exist. |
| UnauthorizedOperation | Unauthorized operation. |

