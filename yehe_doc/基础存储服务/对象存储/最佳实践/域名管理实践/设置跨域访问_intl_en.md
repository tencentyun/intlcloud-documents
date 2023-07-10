## One-Origin Policy

The one-origin policy is a key security mechanism for isolating potentially malicious files. It restricts the way files/scripts loaded from one origin interacts with resources from another origin. Resources with the same protocol, domain name (or IP), and port are considered to belong to the same origin. Scripts on one origin only have permissions to read/write resources on the origin but cannot access resources on other origins. 

#### Definition of one-origin resources

Webpages from a single origin should have the same protocol, domain name, and port (if specified). The following table shows how to test whether a webpage belongs to the same origin as `http://www.example.com/dir/page.html`:

| **URL** | **Result** | **Reason** |
|:---------:|:---------:|:---------:|
| `http://www.example.com/dir2/other.html` | Yes | Same protocol, domain name, and port |
| `http://www.example.com/dir/inner/another.html` |	Yes | Same protocol, domain name, and port |
| `https://www.example.com/secure.html` |	No	| Different protocols (HTTPS) |
| `http://www.example.com:81/dir/etc.html` |	No |	Different ports (81) |
|`http://news.example.com/dir/other.html` |	No |	Different domain names |

#### CORS

Cross-Origin Resource Sharing (CORS) is also known as cross-origin access. It allows web application servers to perform cross-origin access control to ensure secure cross-origin data transfer. Both the browser and server need to support this feature before you can use it. The feature is compatible with all browsers (for IE, IE 10 or later is required).

The CORS communication process is automatically completed by the browser without any manual intervention required. For developers, CORS communication and one-origin AJAX communication work in the same way and use the same code. Once the browser identifies an AJAX request for cross-origin access, it automatically adds additional header information. In some cases, an additional request is made, but you will not perceive it.

Therefore, the key to CORS communication lies in the server. As long as the server implements CORS APIs, cross-origin communication can be implemented.

## CORS Use Cases

CORS is used when you are using a browser. This is because access permissions are controlled by the browser but not the server. Therefore, if you use other clients, you don't need to care about cross-origin access.

With CORS, you can use AJAX in a browser to directly access, upload, and download COS data without using your app server for data transfer. If your website adopts both COS and AJAX technologies, we recommend you use CORS for direct communication with COS.

## COS Support for CORS

COS supports configuring CORS rules to allow or deny cross-origin requests as needed. CORS rules are configured at the bucket level.

COS authentication and whether a CORS request is allowed are independent of each other. In other words, CORS rules of COS are only used to decide whether to add CORS-related headers. It is up to the browser whether to block the request.

All object and multipart APIs of COS support CORS authentication.

>?When two webpages (`www.a.com` and `www.b.com`) running in the same browser request the same cross-origin resource at the same time, if the request from `www.a.com` arrives at the server first, the server will return the resource to the user of `www.a.com` with the `Access-Control-Allow-Origin` header. If `www.b.com` sends a request later, the browser will return the cached response of the last request to the user. In this case, the header content does not match the CORS-required content, so the `www.b.com` request will fail.

## CORS Configuration Example

The following example shows how to configure CORS to get data from COS by using AJAX. The bucket permission used in the example is set to public. For a bucket with private access permission, a signature needs to be added in the request, while other configurations are the same.
The bucket used in the following example is named `corstest`, with the access permission of public read/private write.

### Preparations
1. **Verify whether the file can be accessed.**
Upload the `test.txt` file to `corstest`. The access address of this file is `http://corstest-125xxxxxxx.cos.ap-beijing.myqcloud.com/test.txt`.
Access the text file by using curl, with the following address replaced with your file address:
```
curl http://corstest-125xxxxxxx.cos.ap-beijing.myqcloud.com/test.txt
```
If "test" (the file content) is returned, the file can be accessed normally.
![](https://main.qcloudimg.com/raw/d9e4cee0e6ac49d9774bab3be46bed46.png)

2. **Access the file by using AJAX**
You can access the `text.txt` file directly by using AJAX.
 (1) Copy the following code to a local HTML file and then open it with a browser. As no custom header is set, no preflight request is required.
```
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
</head>
<body>
<a href="javascript:test()">Test CORS</a>
<script>
    function test() {
        var url = 'http://corstest-125xxxxxxx.cos.ap-beijing.myqcloud.com/test.txt';
        var xhr = new XMLHttpRequest();
        xhr.open('HEAD', url);
        xhr.onload = function () {
            var headers = xhr.getAllResponseHeaders().replace(/\r\n/g, '\n');
            alert('request success, CORS allow.\n' +
                'url: ' + url + '\n' +
                'status: ' + xhr.status + '\n' +
                'headers:\n' + headers);
        };
        xhr.onerror = function () {
            alert('request error, maybe CORS error.');
        };
        xhr.send();
    }
</script>
</body>
</html>
```
 (2) Open the HTML file in the browser and click **Test CORS** to send the request. The following error occurs with the message "Access denied. No Access-Control-Allow-Origin header is found". This is because CORS has not been configured on the server.
![](https://main.qcloudimg.com/raw/db84b59f4e48ec50b3b577fa116fe7ba.jpg)
 (3) When the access fails, go to the **Headers** page to find out the cause. You can see that the browser sent a request with **Origin** specified, meaning it is a cross-origin request.
![](https://main.qcloudimg.com/raw/0ba03fd90d9e6bb59785a6ba3b17d812.jpg)
>?The webpage is set up on the server with the address `http://127.0.0.1:8081`. Therefore, the **Origin** is `http://127.0.0.1:8081`.

### Configuring CORS
Now that you have identified the cause of the access failure, you can solve the problem by configuring CORS for the bucket. This example configures CORS in the COS console as follows, which is recommended for easy configurations:

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List**, and click the name of the target bucket. Then, select the **Security Management** tab and find **CORS (Cross-Origin-Resource Sharing)** in the drop-down list.
2. Click **Add a Rule** to add the first rule with the following least restricted configuration:
![](https://main.qcloudimg.com/raw/6a1f4bed7f42fba69449514822759c42.png)
>! The CORS configuration consists of multiple rules, which are matched individually from top to bottom. The first matched rule will be applied.

#### Verifying result
After the configuration is completed, try accessing the `test.txt` file again. If the result is as follows, the file can be accessed normally.
![](https://qcloudimg.tencent-cloud.cn/raw/b3725a24d973dd4799ec58ddb081dffd.jpg)

### Troubleshooting and suggestions
To avoid problems related to cross-origin access, you can set the least restricted CORS rule as described above to allow all cross-origin requests. If an error still occurs under this configuration, the root cause may lie in other factors rather than CORS.

In addition to configuring the least restricted rule, you can also configure a more refined rule. For example, in this example, you can use the following most restricted configuration to ensure a successful match:
![](https://main.qcloudimg.com/raw/6a1f4bed7f42fba69449514822759c42.png)
Therefore, for most scenarios, we recommend you use the most restricted configuration as needed to ensure security.


## CORS Configuration Items

CORS configuration items are as follows:

#### Origin
This refers to the origin allowing cross-origin requests.
- Multiple domain names can be specified, with one domain name per line.
- Asterisk (*) is supported, meaning that all domain names are allowed. This is not recommended.
- A single specific domain name such as `http://www.abc.com` is supported.
- Second-level wildcard domain names such as `http://*.abc.com` are supported. Note that each line can contain only one `*`.
- Do not omit the protocol name HTTP or HTTPS. If the port is not the default port 80, the port should also be specified.

#### Allow-Methods
Enumerate one or multiple allowed cross-origin request methods.
Examples: GET, PUT, POST, DELETE, and HEAD.

#### Allow-Headers
Allowed cross-origin request header.
- Multiple domain names can be specified, with one domain name per line.
- Headers may be easily omitted. Therefore, if there is no special requirement, we recommend you set this field to `*`, meaning that all headers are allowed.
- The values are case-insensitive.
- Each header specified in `Access-Control-Request-Headers` must correspond to a value in `Allow-Headers`.

#### Expose-Headers
This is a list of headers exposed to the browser, i.e., the response headers that you access from the application (for example, JavaScript's `XMLHttpRequest` object).
- The configuration should be specific to the requirements of the application. `ETag` is recommended by default.
- Wildcard is not allowed. The headers are case-insensitive, with one header per line.

#### Max-Age
This is the time (in seconds) the browser can cache the results of a preflight request (OPTIONS request) for specific resources. In general cases, you can set it to a bigger value, for example, 60 seconds. This configuration item is optional.

