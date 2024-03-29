## 功能简介

当源站响应指定错误状态码时，返回302状态码跳转到对应的自定义页面。
>?此功能为回源错误状态码的重定向，不支持 IP 黑白名单，Token 鉴权等访问控制产生的状态码重定向。

## 操作步骤
1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧菜单栏中，单击**规则引擎**。
2. 在规则引擎页面，选择所需站点，可按需配置自定义错误页面规则。如何使用规则引擎，请参见 [规则引擎](https://intl.cloud.tencent.com/document/product/1145/46151)。
参数说明：
<table>
<thead>
<tr>
<th>配置项</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>状态码</td>
<td>指定源站响应的错误状态码：<ul><li>4XX：400, 403, 404, 405, 414, 416, 451</li><li>5XX：500, 501, 502, 503, 504</li></td>
</tr>
<tr>
<td>页面地址</td>
<td>指定错误页面地址，例如：<code>http://www.example.com/custom-page.html</code></td>
</tr>
</tbody></table>

## 配置示例
当请求的源站响应为 404 Not Found 时，跳转到一个自定义错误页面，配置如下：
![](https://qcloudimg.tencent-cloud.cn/raw/ef5eb08e2ae402cd5cd9ab782817dc56.png)
