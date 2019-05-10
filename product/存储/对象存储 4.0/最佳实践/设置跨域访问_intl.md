## One-Origin Policy
One-origin policy is a key security mechanism for isolating potentially malicious files and restricts the way the files or scripts loaded from one origin interacts with the resources from another one. Resources with the same protocol, domain name (or IP), and port are considered to belong to one origin. The scripts in one origin only have the permissions to read or write the resources in the same origin, and cannot access the resources from other origins. 
### Definition of one-origin resources
Webpages from a single origin should have the same protocol, domain name, and port (if specified). The following table shows how to test whether a webpage belongs to the same origin as `http://www.example.com/dir/page.html`:

| **URL** | **Result** | **Reason** |
|:---------:|:---------:|:---------:|
| `http://www.example.com/dir2/other.html` | Successful | Same protocol, domain name, and port |
| `http://www.example.com/dir/inner/another.html` |	Successful | Same protocol, domain name, and port |
| `https://www.example.com/secure.html` |	Failed	| Different protocols (HTTPS) |
| `http://www.example.com:81/dir/etc.html` |	Failed |	Different ports (81) |
|`http://news.example.com/dir/other.html` |	Failed |	Different domain names |
### CORS
Cross-Origin Resource Sharing (CORS) is also known as cross-origin access. It allows Web application servers to perform cross-origin access control to ensure secure cross-origin data transfer. Both browser and server need to support this feature before you can use it. The feature is compatible with all browsers (for IE browser, IE10 or above is required).
The CORS communication process is automatically completed by the browser without any manual intervention. For developers, CORS communication and one-origin AJAX communication work the same way using the same code. Once the browser identifies an AJAX request for cross-origin access, it automatically adds some header information. In some cases, an additional request is made, but user will not be aware of it.
Therefore, the key to CORS communication is server. As long as the server implements the CORS APIs, it can implement a cross-origin communication.

## CORS Use Cases
CORS is used only when you're using a browser, because access permissions are controlled by a browser, instead of a server. You don't need to care about any cross-origin issues when using other clients.
CORS is mainly used in an upload or download scenario where the data in COS is accessed directly using AJAX on a browser without having to be transfered via the user's application server. For the websites using both COS and AJAX, it is recommended to use CORS for direct communication with COS.
## COS Support for CORS
COS supports configuring CORS rules to allow or deny cross-origin requests as needed. CORS rules are configured at bucket level.
Whether a CORS request is allowed is entirely independent of such factors as COS authentication. COS's CORS rules are only used to decide whether to add the CORS-related headers. It's up to the browser whether to block the request.
All object-related APIs of COS and Multipart APIs support CORS authentication.
> When two webpages from `www.a.com` and `www.b.com` respectively that run on the same browser request the same cross-origin resource at the same time, if the request from `www.a.com` arrives at the server first, the server appends the Header of Access-Control-Allow-Origin to the resource and returns it to the user at `www.a.com`. If a user then sends a request from `www.b.com`, the browser returns the cached response to the last request to the user. If the content of the Header does not match the content required by CORS, the `www.b.com` request fails.

## CORS Configuration Example
The following example shows the how to configure CORS to get data from COS using AJAX. The Bucket permission used in the example is set to Public. For a bucket with private access permission, all other configuration items are the same as those for a public bucket, except that a signature needs to be appended to the request.
The bucket used in the following example is named corstest, with an access permission of Public Read/Private Write.
### Before configuring CORS
1. **Verify whether the file can be accessed**
Upload a test.txt file to corstest. The access address of test.txt is `http://corstest-125xxxxxxx.cos.ap-beijing-1.myqcloud.com/test.txt`.
Access the text file using curl, with the following address replaced with your file address:
```
curl http://corstest-125xxxxxxx.cos.ap-beijing-1.myqcloud.com/test.txt
```
If "test" (the file content) is returned, the file can be accessed normally.
![图片0](//mc.qcloudimg.com/static/img/5e1740ac46efd2ddcb8258448af27815/image.png)
2. **Access the file using AJAX**
You can access the text.txt file directly using AJAX.
 (1) Write a simple HTML file by copying the following code to a local file and saving it as an HTML file, and then open it with a browser. Because no custom header is set, no preflight request is required.
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
        var url = 'http://corstest-125xxxxxxx.cos.ap-beijing-1.myqcloud.com/test.txt';
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
 (2) Open the HTML file in the browser and click the **Test CORS** button to send the request. The following error occurs with the message "Access denied. No Access-Control-Allow-Origin Header found". This is because CORS has not been configured on the server.
 ![错误提示](//mc.qcloudimg.com/static/img/b495296d08ddac2f5d8eacc0e9203c59/image.png)
 (3) When the access fails, enter the Header page to check the reason. You can find that the browser sent a Request with Origin, which means it is a cross-origin request.
![检查Header](//mc.qcloudimg.com/static/img/26976dee6cb15736e9aff86d353d5738/image.png)
> You can set up the webpage on the server with the address `http://127.0.0.1:8081`, so the Origin is `http://127.0.0.1:8081`.

### Configuring CORS
After identifying the reason for the failed access, you can solve the problem by configuring the bucket-related CORS. In this example, CORS is configured in the COS Console. For uncomplicated CORS settings, it is recommended to configure CORS using the console.
#### 1. Log in to the COS Console and go to the configuration page.
Log in to the [COS Console](), click **Bucket List**, select the bucket (such as corstest) to go to its details page, click **Basic Configuration** to find the CORS configuration items.
![图片4](//mc.qcloudimg.com/static/img/7a08a4ad4199580265a0359f2b39eafc/image.png)

#### 2. Enable and set CORS rules 
1. Click **Edit** to enable CORS, and click **+New Rule**. On the displayed page, add the first rule with the least restricted configuration, as shown below:
![](//mc.qcloudimg.com/static/img/198d6464fe3846451b6afc2b71cb0b78/image.png)
> **Notes:**
> The CORS configuration is composed of multiple rules, which are matched individually from top to bottom. The first matched rule will be used.

#### Verify the result
After the configuration is completed, try accessing the test.txt file again. If the result is as follows, you can request access normally.
![访问成功](//mc.qcloudimg.com/static/img/9d3f4370b337e73090efae2c2ef199f4/image.png)

### Troubleshooting and suggestions
To avoid problems related to cross-origin access, you can set the least restricted CORS rule as described above to allow all cross-origin requests. If an error occurs even under this configuration, the root cause may lie in other factors than CORS.

In addition to configuring the least restricted rule, you can configure more specific control mechanism for targeted control. For example, in this example, you can use the minimum allocation configuration as shown below to ensure successful match:
![](//mc.qcloudimg.com/static/img/c3cba398e89f643c58a742e720dbd955/image.png)
Therefore, for most scenarios, it is recommended to use the least configuration as needed to ensure security.
## CORS Configuration Items
CORS configuration items are as follows:
### Origin
This refers to the origin allowing cross-origin requests.
- Multiple origins can be specified (one domain name per line).
- A wildcard `*` can be used to indicate all domain names are allowed (not recommended).
- A specific domain name can be specified, such as `http://www.abc.com`.
- Second-level wildcard domain names, such as `http://*.abc.com`, are supported (only one `*` is allowed per line).
- Do not leave out protocol name HTTP or HTTPS. Specify the port if it is not 80 (default).
### Request Methods
Enumerate one or multiple allowed cross-origin request methods.
Such as GET, PUT, POST, DELETE, and HEAD.

### Allow-Header
Allowed cross-origin request headers;
- Multiple origins can be specified (one domain name per line).
- Header tends to be left out. In general cases, it is recommended to set this to "*" to allow all headers.
- The values are case insensitive.
- Each Header specified in Access-Control-Request-Headers must corresponds to a value in Allowed-Header.

### Expose-Header
This is a list of headers exposed to the browser, which are the response headers that the user accesses from the application (such as Javascript's XMLHttpRequest object).
- The configuration should be specific to the requirements of application. Etag is recommended by default.
- Wildcard is not allowed. The headers are case insensitive, with one header per line.

### Timeout Max-Age
This is the delay (in sec) from the moment when the browser issues a preflight request (OPTIONS request) for a specific resource until a result is returned. In general cases, you can set it to a bigger value, such as 60 seconds.
This configuration item is optional.

