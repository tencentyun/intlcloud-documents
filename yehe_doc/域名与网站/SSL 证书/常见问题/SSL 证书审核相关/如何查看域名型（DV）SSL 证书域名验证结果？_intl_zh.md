### 如何查看 DV 型证书域名验证结果？

在您提交证书申请后，CA 机构中心将对您的域名及所提交的信息进行审核。域名验证成功后，CA 机构中心才会对证书进行颁发，若您的证书一直未颁发，建议您根据以下内容检验域名验证结果。

>?
> 
> 腾讯云 SSL 证书服务提供的主机记录是全域名的，如果您的域名管理系统不支持全域名的主机记录，请去掉根域名的后缀部分。
> 

**DNS 验证类型**

1. 请登录您的域名服务器，执行 dig 命令查询域名 DNS 解析。

2. 执行 `dig + 记录类型 + @119.29.29.29` 命令指定使用 DNSPod 的 DNS 进行验证。
例如 `dig txt cloud.tencent.com @119.29.29.29`![](https://staticintl.cloudcachetci.com/yehe/backend-news/zrr7795_111111111111111111111111.png)

  - 如果返回结果中存在类似图示中的 TXT 记录，且记录值与证书控制台中证书详情页面中的记录值一致，表示您的 DNS 配置正确且已生效。

  - 如果返回结果中不存在 TXT 记录，可能是 DNS 解析配置有误或者配置未生效。
若 DNS 解析配置错误，请登录 [证书管理控制台](https://console.cloud.tencent.com/certoverview)，单击**待验证**页签，进入该证书的详情页面。将证书详情中的记录值复制，并在您的 DNS 域名解析服务商更新解析。如果配置长时间未生效，请联系您的域名托管商。
    

  >?
  > 具体操作请您参考 [DNS 验证](https://intl.cloud.tencent.com/document/product/1007/45895)。



**文件验证类型**

1. 请登录 [证书管理控制台](https://console.cloud.tencent.com/certoverview) ，单击**待验证**页签，进入该证书的详情页面。

2. 单击访问验证 URL 地址，若访问页面中显示的内容和证书详情页面中的验证文件内容一致，说明可正常访问，若不一致，请从以下几个方面着重进行检查：

  - 检查该验证 URL 地址是否已存在 HTTPS 可访问的地址。若存在，请在浏览器中使用 HTTPS 地址重新访问，如果浏览器提示 “证书不可信” 或者显示的内容不正确，请您暂时关闭该域名的 HTTPS 服务。

  - 确保验证 URL 地址在任何一个地方都能正确访问。由于每个品牌证书的检测服务器区域不同，请确认您的站点是否有国外镜像，或者是否使用了智能 DNS 服务等。

  - 文件验证需要直接响应200状态码和文件内容，不支持任何形式的跳转。检查该验证 URL 地址是否存在301或302跳转。如存在此类重定向跳转，请取消相关设置关闭跳转。
    

      >?
      > 
      > 您可执行 `wget -S URL 地址` 命令检测该验证 URL 地址是否存在跳转。
      > 
