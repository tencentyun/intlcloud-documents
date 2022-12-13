## 功能介绍
EdgeOne 会在以下场景中要求您通过站点验证，来证明站点的所有权：
- 添加站点时，发现站点已被其他账户添加过。<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/jXa5485_1.png" width=700px>

- 加站点时，接入方式选择了 CNAME 接入，第四步会变成站点验证。<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/ENsI447_2.png" width=700px>

## 操作步骤
EdgeOne 提供 DNS 验证和文件验证两种方式来校验您站点的所有权，具体操作步骤如下：

### DNS 验证
<dx-steps>

- 登录您的 DNS 服务商，新增一条 TXT 记录，按要求添加指定的主机记录和记录值。
- 耐心等待系统自动完成校验，如果添加完成长时间未生效，可手动刷新触发系统校验。
- 记录生效后，单击**验证**，验证通过即可。
    </dx-steps>
    <img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Ah4y369_3.png" style="zoom:150%;" />

### 文件验证
#### Windows 系统下的操作方法
<dx-steps>
-前往服务器的根目录下创建验证目录 `.well-known/teo-verification`。
-单击图中第二步文件链接获取验证文件，将其上传至验证目录。
- 复制图中第三步中 URL 链接到您的浏览器中，确保能够正常访问到该资源。
-单击下方**验证**，验证通过即可。
</dx-steps>

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/GzPY329_6.png" width=700px>


#### Linux 系统下的操作方法
<dx-steps>
-通过命令行进入 Web 服务器根目录下。
- 复制图中第二步代码至命令行，并执行。
-  复制图中第三步中 URL 链接到您的浏览器中，确保能够正常访问到该资源。
-单击下方**验证**，验证通过即可。
</dx-steps>

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/6nrc408_7.png" width=700px>
