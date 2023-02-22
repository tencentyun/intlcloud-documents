
## 什么情况下需要验证站点归属权？
1. 站点首次接入并且选择了 CNAME 接入方式时，需要验证当前站点的归属权。
2. 该站点已在其他账号下接入时，需要验证当前站点的归属权，如验证通过，可通过取回站点接入当前账号。


## 方法一：DNS 验证
<dx-steps>
- 登录您的 DNS 服务商，新增一条 TXT 记录，按要求添加指定的主机记录和记录值。
- 耐心等待系统自动完成校验，如果添加完成长时间未生效，可手动刷新触发系统校验。
- 记录生效后，单击**验证**，验证通过即可。
</dx-steps>

![](https://qcloudimg.tencent-cloud.cn/raw/7fae841267887ab1f89577186e9665a0.png)

## 方法二：文件验证
### Windows 系统下的操作方法
<dx-steps>
- 前往服务器的根目录下创建验证目录 `.well-known/teo-verification`。
- 单击图中第二步文件链接获取验证文件，将其上传至验证目录。
- 复制图中第三步中 URL 链接到您的浏览器中，确保能够正常访问到该资源。
- 单击下方**验证**，验证通过即可。
</dx-steps>

<img src="https://qcloudimg.tencent-cloud.cn/raw/746be9b09061d0453987913720ce091f.png" width=700px>


### Linux 系统下的操作方法
<dx-steps>
- 通过命令行进入 Web 服务器根目录下。
- 复制图中第二步代码至命令行，并执行。
- 复制图中第三步中 URL 链接到您的浏览器中，确保能够正常访问到该资源。
- 单击下方**验证**，验证通过即可。
</dx-steps>

<img src="https://qcloudimg.tencent-cloud.cn/raw/6a6f7b0dfd7b795692358fa9b4b4aa79.png" width=700px>
