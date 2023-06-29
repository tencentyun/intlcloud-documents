
## Error Description

A CORS error is reported, which results in page error or exceptional page display. See the figure below:

![](https://main.qcloudimg.com/raw/af636dbb5bba454bb79234cd7b49dca2.png)

## Possible Reasons

CORS error are caused by the same-origin policy of the browser. For the webpage security, when the response for this request will be blocked by the browser, which will result in frontend error or exceptional page display. When the protocol, domain name or port of the request URL is different with that of the URL of requested page, the request is considered a cross-site request.

## Solutions

1. Check whether the issue is caused by cross-site request. See the figure below:
![](https://main.qcloudimg.com/raw/78d05383b9040d313c05add33a1737df.png)
2. Configure corresponding HTTP response header in CDN console and define domains allowed to access this resource.

## Troubleshooting Procedure

1. Log in to <a href="https://console.cloud.tencent.com/cdn/domains">CDN console</a>, go to **Domain Name Management** - **Advanced Configuration** - **HTTP Response Header**, complete the setting of **Access-Control-Allow-Origin** parameter as below to allow cross-site requests from all domains. For more information, see [Access-Control-Allow-Origin match mode description](#ac).

2. You can also configure to allow cross-region requests from a single or multiple specified domain names/IPs.
You can also configure header parameters such as Access-Control-Request-Method, Access-Control-Request-Headers, and Access-Control-Max-Age to specify the allowed request methods and headers and how long the results of a preflight request can be cached. For more information, see [List of Supported Parameters](#ap).


>! If you have configured cross-region access on the COS bucket, please configure cross-region rules in <a href="https://intl.cloud.tencent.com/document/product/228/35320">HTTP Response Header</a> in the CDN console.

[](id:ap)
### List of Supported Parameters

| Header Parameter                      | Description                                                         |
| :---------------------------- | :----------------------------------------------------------- |
| Access-Control-Allow-Origin   | Specifies which origins are allowed to access the resource. For requests from the allowed origins, the host is added to the request header. You can also configure it to `*` to allow requests from all origins. For more information, see [Access-Control-Allow-Origin match mode description]|(#ac). You can enter domain names, IPs and both of them. Note that `http://` or `https://` must be included (for example, `http://test.com`, `http://1.1.1.1`). Separate multiple entries with commas, and up to 1000 characters are allowed.|
| Access-Control-Allow-Methods  | Indicates the HTTP methods allowed for cross-origin requests. You can configure one or more methods, as shown below: Access-Control-Allow-Methods: `POST, GET, OPTIONS`. |
| Access-Control-Max-Age        | Specifies the validity period (in seconds) of a preflight request. For a non-simple cross-origin request, an HTTP query request, namely the preflight request, is needed before the official communication to check whether the cross-origin request is secure to be accepted. A cross-origin request is non-simple if it is: not a GET, HEAD, or POST request, or it is a POST request but its request data type is application/xml, text/xml or any other data type except application/x-www-form-urlencoded, multipart/form-data, and text/plain. For example, if a custom request header is Access-Control-Max-Age:`1728000`, there will not be another preflight request sent for this CORS within 1,728,000 seconds (20 days). |
| Access-Control-Expose-Headers | This specifies which headers can be exposed to clients as a part of responses. By default, these 6 headers can be exposed to clients: Cache-Control, Content-Language, Content-Type, Expires, Last-Modified, and Pragma. If you want to make other headers accessible to clients, you can separate multiple headers with a comma, e.g., Access-Control-Expose-Headers: Content-Length,X-My-Header. In this way, clients can access the two headers Content-Length and X-My-Header.|

[](id:ac)
### Access-Control-Allow-Origin Configuration

| **Mode**   | **Value/Example**                                                     | **Description**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Allow all         | `*`                                                            | When it is set to `*`, the header `Access-Control-Allow-Origin:*` will be added to the response, which means to allow requests from all origins. |
| Specified domain       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | When a request is initiated from `https://cloud.tencent.com`, which hits the rule, the header `Access-Control-Allow-Origin: https://cloud.tencent.com` is added to the response. However when there is a request from `https://www.qq.com`, which does not hit the rule, the response is not changed. |
| Specified second-level domain name | `https://*.tencent.com`                                       | When a request is initiated from `https://cloud.tencent.com`, which hits the rule, the header `Access-Control-Allow-Origin: https://cloud.tencent.com` is added to the response. However when there is a request from `https://cloud.qq.com`, which does not hit the rule, the response is not changed. |
| Specified port       | `https://cloud.tencent.com:8080`                             | When a request is initiated from `https://cloud.tencent.com:8080`, which hits the rule, the header `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` is added to the response. However when there is a request from `https://cloud.tencent.com`, which does not hit the rule, the response is not change. |

> ! If there are special ports, you need to enter the relevant information in the list. You must specify the port as arbitrary port match is not supported.
