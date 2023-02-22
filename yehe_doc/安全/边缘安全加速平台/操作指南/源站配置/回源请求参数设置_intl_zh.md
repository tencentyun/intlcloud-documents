## 功能简介
自定义设置回源请求时，是否包含请求中原有的查询字符串和 Cookie。默认情况下，回源时会保留请求中原有的全部查询字符串和 Cookie。此配置不影响节点缓存行为。

## 适用场景
1. 业务源站会根据不同查询字符串或 Cookie 信息做精细化管理，返回不同的资源。
2. 原请求含节点鉴权相关查询字符串，为保障成功回源获取资源，回源时需忽略该鉴权参数。

## 操作步骤
1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧菜单栏中，单击**规则引擎**。
2. 在规则引擎页面，选择所需站点，可按需配置回源请求参数设置规则。如何使用规则引擎，请参见 [规则引擎](https://intl.cloud.tencent.com/document/product/1145/46151)。
配置项说明：
<table>
<thead>
<tr>
<th>配置项</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>查询字符串</td>
<td>调整 URL 中的查询字符串，默认保留原请求的全部查询参数。</td>
</tr>
<tr>
<td>Cookie</td>
<td>调整 Cookie 参数，默认保留原请求的全部 Cookie 参数。</td>
</tr>
</tbody></table>

## 配置示例
- 若原请求的查询字符串为节点鉴权相关参数，请求回源时需忽略该鉴权参数，则可配置如下：
![](https://qcloudimg.tencent-cloud.cn/raw/f3176b055ee1f1dffbe1eb8ee3601708.png)
客户端请求 URL：`http://www.example.com/path/demo.jpg?abc=18867530-chgdksbvhjsbvdjhsbvfj12`（`abc`为鉴权参数）。
回源请求 URL：`http://www.example.com/path/demo.jpg`。

- 若源站仅需要 `key1` 和 `key2` 查询参数，回源时可仅保留这两个参数，其余参数都忽略，可配置如下：
![](https://qcloudimg.tencent-cloud.cn/raw/a192dc8c135c6aaf2212f0064df2a53a.png)
客户端请求 URL：`http://www.example.com/path/demo.jpg?key1=a&key2=b&key3=c&key4=d` 和 `http://www.example.com/path/demo.jpg?key1=a&key2=b&key3=c&key4=d&key5=e`。
回源请求 URL：`http://www.example.com/path/demo.jpg?key1=a&key2=b`。

- 若源站不需要 `key3` 查询参数，回源时可忽略此参数，保留其余有用的参数，可配置如下：
![](https://qcloudimg.tencent-cloud.cn/raw/7a1812e1369755ac482c982087662ad4.png)
客户端请求 URL：`http://www.example.com/path/demo.jpg?key1=a&key2=b&key3=c&key4=d`。
回源请求 URL：`http://www.example.com/path/demo.jpg?key1=a&key2=b&key4=d`。
