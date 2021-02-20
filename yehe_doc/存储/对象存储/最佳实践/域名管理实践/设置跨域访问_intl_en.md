## One-Origin Policy
The one-origin policy is a key security mechanism for isolating potentially malicious files. The policy restricts the way files/scripts loaded from one origin interacts with the resources from another origin. Resources with the same protocol, domain name (or IP), and port are considered to belong to the same origin. The scripts in one origin only have permissions to read/write resources in its origin, and cannot access resources from other origins. 

#### Definition of one-origin resources
Webpages from a single origin should have the same protocol, domain name, and port (if specified). The following table shows how to test whether a webpage belongs to the same origin as `http://www.example.com/dir/page.html`:

| **URL** | **Result** | **Reason** |
|:---------:|:---------:|:---------:|
| `http://www.example.com/dir2/other.html` | Successful | Same protocol, domain name, and port |
| `http://www.example.com/dir/inner/another.html` |	Successful | Same protocol, domain name, and port |
| `https://www.example.com/secure.html` |	Failed	| Different protocols (HTTPS) |
| `http://www.example.com:81/dir/etc.html` |	Failed |	Different ports (81) |
|`http://news.example.com/dir/other.html` |	Failed |	Different domain names |

#### CORS

Cross-Origin Resource Sharing (CORS) is also known as cross-origin access. It allows Web application servers to perform cross-origin access control to ensure secure cross-origin data transfer. Both browser and server need to support this feature before you can use it. The feature is compatible with all browsers (for IE browser, IE10 or above is required).

The CORS communication process is automatically completed by the browser without any manual intervention. For developers, CORS communication and one-origin AJAX communication work in the same way and use the same code. Once the browser identifies an AJAX request for cross-origin access, it automatically adds some header information. In some cases, an additional request is made, but the user will not perceive it.

Therefore, the key to CORS communication lies in the server. As long as the server implements the CORS APIs, cross-origin communication can be implemented.

## CORS Use Cases

CORS is used when you're using a browser. This is because access permissions are controlled by the browser but not the server. Therefore, if you use other clients, you don't need to concern about cross-origin.

With CORS, you can use AJAX on browsers to directly access, upload, and download COS data without using your app server for data transfer. If your websites use both COS and AJAX, you are advised to use CORS for direct communication with COS.

## COS Support for CORS

COS supports configuring CORS rules to allow or deny cross-origin requests as needed. CORS rules are configured at bucket level.

COS authentication and whether a CORS request is allowed are independent. In other words, CORS rules of COS are only used to decide whether to add CORS-related headers. It's up to the browser whether to block the request.

All object-related APIs of COS and Multipart APIs support CORS authentication.

>?When two webpages (`www.a.com` and `www.b.com`) running on the same browser request the same cross-origin resource at the same time, if the request from `www.a.com` arrives at the server first, the server will return the resource to the user of `www.a.com` with the `Access-Control-Allow-Origin` header. If `www.b.com` sends a request later, the browser will return the cached response of the last request to the user. In this case, the header content does not match the CORS-required content, leading to the `www.b.com` request failure.

## CORS Configuration Example

The following example shows how to configure CORS to get data from COS using AJAX. The bucket permission used in the example is set to public. For a bucket with private access permission, a signature needs to be added in the request, and other configurations are the same.
The bucket used in the following example is named `corstest`, with the access permission of public read/private write.

### Preparations
1. **Verify whether the file can be accessed**
Upload a `test.txt` file to `corstest`. The access address of `test.txt` is `http://corstest-125xxxxxxx.cos.ap-beijing.myqcloud.com/test.txt`.
Access the text file using curl, with the following address replaced with your file address:
```
curl http://corstest-125xxxxxxx.cos.ap-beijing.myqcloud.com/test.txt
```
If "test" (the file content) is returned, the file can be accessed normally.
![](https://main.qcloudimg.com/raw/d9e4cee0e6ac49d9774bab3be46bed46.png)

2. **Access the file using AJAX**
You can access the `text.txt` file directly using AJAX.
 (1) Copy the following code to a local file, save it as an HTML file, and then open it with a browser. Since no custom header is set, no preflight request is required.
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
 (2) Open the HTML file in the browser and click **Test CORS** to send the request. The following error occurs with the message "Access denied. No Access-Control-Allow-Origin Header found". This is because CORS has not been configured on the server.
![](https://main.qcloudimg.com/raw/db84b59f4e48ec50b3b577fa116fe7ba.jpg)
 (3) When the access fails, go to the **Headers** page to find out the cause. You can see that the browser sent a request with **Origin** specified, meaning it is a cross-origin request.
![](https://main.qcloudimg.com/raw/0ba03fd90d9e6bb59785a6ba3b17d812.jpg)
>?Our webpage is set up on the server whose address is `http://127.0.0.1:8081`. Therefore, the **Origin** is `http://127.0.0.1:8081`.

### Configuring CORS
Now that you have identified the cause of the access failure, you can solve the problem by configuring the bucket-related CORS. This example configures CORS in the COS console, which is recommended for uncomplicated configurations. You can configure as follows:

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5), click **Bucket List**, and click the name of the desired bucket. Then, choose the **Security Management** tab and select **CORS (Cross-Origin-Resource Sharing)** in the drop-down list.
2. Click **Add a Rule** to add the first rule with the following least restricted configuration:
![](https://main.qcloudimg.com/raw/e042f4e6b6513aa1309929c384c8b5d1.png)
>! The CORS configuration is made up of multiple rules, which are matched individually from top to bottom. The first matched rule will be applied.

#### Verifying the result
After the configuration is completed, try accessing the `test.txt` file again. If the result is as follows, the file can be accessed normally.
![](https://main.qcloudimg.com/raw/a887521f8561ea2a83a5416f11c00fb1.png)

### Troubleshooting and suggestions
To avoid problems related to cross-origin access, you can set the least restricted CORS rule as described above to allow all cross-origin requests. If an error occurs even under this configuration, the root cause may lie in other factors rather than CORS.

In addition to configuring the least restricted rule, you can configure a more refined rule. For example, in this example, you can use the following most restricted configuration to ensure a successful match:
![](https://main.qcloudimg.com/raw/6256632c56b643e3aadcc1fe94bb9eaa.png)
Therefore, for most scenarios, you are advised to use the most restricted configuration as needed to ensure security.


## CORS Configuration Items

CORS configuration items are as follows:

#### Origin
This refers to the origin allowing cross-origin requests.
- More than one domain name can be specified, with one domain name per line.
- Asterisk (*) is supported, meaning that all domain names are allowed. This is not recommended.
- A single specific domain name is supported, for example, `http://www.abc.com`.
- Second-level wildcard domain names, for example, `http://*.abc.com`, are supported. Note that each line can contain only one asterisk (*).
- Do not omit the protocol name HTTP or HTTPS. If the port is not the default 80, the port should also be specified.

#### Request methods
Enumerate one or multiple allowed cross-origin request methods.
Examples: GET, PUT, POST, DELETE, and HEAD

#### Allow-Header
Allowed cross-origin request header.
- More than one domain name can be specified, with one domain name per line.
- Header is easy to be omitted. Therefore, if there is no special requirement, you are advised to set this field to `*`, meaning that all headers are allowed.
- The values are case-insensitive.
- Each header specified in `Access-Control-Request-Headers` must correspond to a value in `Allowed-Header`.

#### Expose-Header
This is a list of headers exposed to the browser, that is, the response headers that the user accesses from the app (for example, Javascript's XMLHttpRequest object).
- The configuration should be specific to the requirements of the app. ETag is recommended by default.
- Wildcard is not allowed. The headers are case-insensitive, with one header per line.

#### Timeout Max-Age
This is the time (in seconds) the browser can cache the results of a preflight request (OPTIONS request) for specific resources. In general cases, you can set it to a bigger value, for example, 60 seconds. Note that this configuration item is optional.

