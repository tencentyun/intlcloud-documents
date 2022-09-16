## 什么情况下需要进行域名归属校验？
1.域名首次接入时，例如：a.example.com；该域名接入后，同级域名及次级域名如b.example.com视为已有权限域名，默认可接入，无需校验。但上级域名如example.com接入仍需校验；
2.子域名已在其他账号下接入时，需进行域名归属校验验证当前域名归属权，如验证通过，可通过取回域名接入当前账号；
3.同级泛域名接入时，需校验，例如：a.example.com已接入，*.example.com接入时仍需校验，*.a.example.com属于次级泛域名，可免校验接入。

## 方法一：DNS解析验证（推荐）
1.在添加域名时，如果该域名需校验，在域名下方会提示需验证域名归属权，单击验证方法；
![](https://qcloudimg.tencent-cloud.cn/raw/1c6915b095d74f4358923be2ec7740dd.png)
2.验证方法中，默认为 DNS 解析验证。
使用 DNS 解析验证的方式，需要您前往该域名的解析服务商，在主域名下添加一个主机记录值为_cdnauth的 TXT 记录。
>!
无论您需要新增的域名为c.b.a.example.com、*.example.com或test.example.com，多级域名下主机记录值仍应添加在主域名下，例如：添加的域名是c.b.a.example.com，需要新增一条解析记录为_cdnauth.example.com即可。
![](https://qcloudimg.tencent-cloud.cn/raw/e1da0524ad0781544052fd65195d9798.png)
添加完解析记录后，等待 TXT 记录值生效，生效后，您可点击下方的验证按钮，即可完成域名归属校验；如果验证失败，请确认当前 TXT 记录值在域名解析服务商内是否已生效或是否填写了正确的 TXT 记录值。

## 方法二：文件验证
1.在添加域名时，如果该域名需校验，在域名下方会提示需验证域名归属权，单击验证方法；
![](https://qcloudimg.tencent-cloud.cn/raw/140a8b980bd0c30c0336dcd8f8e3607e.png)
2.在验证方法内，选择文件验证的方式，
![](https://qcloudimg.tencent-cloud.cn/raw/8883258277fef3bf2e42ceffb489324a.png)
3.单击下载文件 verification.html；
4.将该文件上传至您主域名的服务器（例如您的 CVM、COS、阿里 ECS、阿里 OSS 等）根目录下，例如：当前添加的域名为test.example.com，您需要将该文件上传至 example.com 的根目录下。
5.确保可通过http://example.com/verification.html 访问至到该文件后，即可单击验证按钮进行验证。如果文件内的记录值与我们提供的记录值是一致的，即可验证通过；如果验证失败，请确保上述文件链接可访问，并且您上传的文件为正确文件，可通过访问文件的链接与所下载的文件进行比对是否一致。

## 常见问题
### 如何手动检测域名归属校验的 TXT 记录值是否生效？
Windows 系统示例：
例如接入域名为test.example.com，可以在系统内打开 cmd 命令界面内，输入nslookup -qt=txt _cdnauth.example.com，根据当前的 TXT 结果，可以查看解析记录是否生效或是否正确。
![](https://qcloudimg.tencent-cloud.cn/raw/1728c7c311e4db18fc28287299ab2068.png)

Linux/Mac 系统示例：
例如接入域名为test.example.com，可以在命令界面内，输入dig _cdnauth.example.com txt，根据当前的 TXT 结果，可以查看解析记录是否生效或是否正确。
![](https://qcloudimg.tencent-cloud.cn/raw/d07ca2df386f12185af00abe813d4b60.png)

### 云点播域名提示无法直接接入？
您当前域名已在云点播的自定义分发加速域名中接入，因同一加速域名无法重复配置，如果您还需要在 CDN 控制台使用该加速域名，您需要先删除云点播内的加速域名（请注意先停用域名后再进行删除，仅停用仍然会有冲突），删除后，等待约1分钟左右即可在 CDN 控制台内接入，或者可以使用不同的其他子域名接入至 CDN 控制台内。

