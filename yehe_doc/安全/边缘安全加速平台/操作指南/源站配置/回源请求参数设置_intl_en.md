## Overview
You can specify which part of the query string and Cookie to be included in the request when it’s forwarded to the origin. Note that this configuration does not affect node caching.

## Use Cases
1. Allow the origin to serve resources based on the query string or Cookie.
2. Ensure a successful origin-pull by ignoring the authentication parameter in the request.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the page that displays, select the target site and create rules for origin-pull request parameters as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).
Description of configuration items:
<table>
<thead>
<tr>
<th>Configuration Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Query string</td>
<td>Modify the query string in the URL. By default, all query parameters included in the request.</td>
</tr>
<tr>
<td>Cookie</td>
<td>Modify the Cookie. By default, all cookie parameters are included in the request.</td>
</tr>
</tbody></table>

## Configuration Samples
- If the request contains the authentication parameter in the query string, ignore the authentication parameter before origin-pull as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/f3176b055ee1f1dffbe1eb8ee3601708.png)
Client request URL: `http://www.example.com/path/demo.jpg?abc=18867530-chgdksbvhjsbvdjhsbvfj12` (`abc` is the authentication parameter.)
Origin-pull request URL: `http://www.example.com/path/demo.jpg`

- To include the `key1` and `key2` query parameters in the request, ignore the rest part of the query string before origin-pull as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/a192dc8c135c6aaf2212f0064df2a53a.png)
Client request URL: `http://www.example.com/path/demo.jpg?key1=a&key2=b&key3=c&key4=d` and `http://www.example.com/path/demo.jpg?key1=a&key2=b&key3=c&key4=d&key5=e`
Origin-pull request URL: `http://www.example.com/path/demo.jpg?key1=a&key2=b`

- To exclude the `key3` query parameter in the request, ignore it before origin-pull as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/7a1812e1369755ac482c982087662ad4.png)
Client request URL: `http://www.example.com/path/demo.jpg?key1=a&key2=b&key3=c&key4=d`
Origin-pull request URL: `http://www.example.com/path/demo.jpg?key1=a&key2=b&key4=d`
