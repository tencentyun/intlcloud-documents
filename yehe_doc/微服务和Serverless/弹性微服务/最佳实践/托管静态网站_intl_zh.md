## 操作场景

TEM 通过 **应用实例+CFS** 的方式提供静态网站资源托管的能力，本文以业界流行的静态网站服务 [Hugo](https://gohugo.io/) 为例，为您提供静态资源托管的最佳实践。下述将通过 Hugo 生成个人静态博客，然后通过 TEM 部署反向代理应用，配合 CFS 管理静态资源，最后通过 TEM 提供的访问配置，在公网上提供对个人静态博客的访问。

整体流程如下：
<dx-steps>
- [本地通过 Hugo 生成静态博客](#step1)
- [上传静态博客内容到 CFS](#step2)
- [在 TEM 上部署 nginx 应用并关联 CFS](#step3)
- [在 TEM 上配置 nginx 的网络访问](#step4)
- [(可选) 配置域名](#step5)
- [(可选) 配置防火墙](#step6)
- [(可选) 配置 CDN](#step7)
</dx-steps>


## 操作步骤

### 步骤1：本地通过 Hugo 生成静态博客[](id:step1)

1. 安装 Hugo（参考 [Install Hugo](https://gohugo.io/getting-started/installing/)）。
   以 MacOS 系统为例，通过如下命令安装：
   ```
   brew install hugo
   ```

2. 执行如下命令创建静态站点。
   ```
   hugo new site quickstart
   ```

3. 执行如下命令添加主题。
   ```
   cd quickstart
   git init
   git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
   echo theme = \"ananke\" >> config.toml
   ```

4. 执行如下命令添加博客。
   ```
   hugo new posts/my-first-post.md
   ```

5. 执行如下命令构建静态页面。
   ```
   hugo -D
   ```

6. 生成的静态内容存放在 quickstart 项目的 `public/` 目录下。
      ![](https://main.qcloudimg.com/raw/1719df20926f87db5edd93d32dbde0fd.png)


### 步骤2：上传静态博客内容到 CFS[](id:step2)

1. 参考 [CFS：创建文件系统及挂载点](https://intl.cloud.tencent.com/document/product/582/9132) 购买 CFS 文件系统。
>!购买的 CFS 文件系统的**区域**、**VPC 网络** 应与在 TEM 上部署应用的区域保持一致。

2. 参考 [CFS：在 Linux 客户端上使用 CFS 文件系统](https://intl.cloud.tencent.com/document/product/582/11523) 或 [CFS：在 Windows 客户端上使用 CFS 文件系统](https://intl.cloud.tencent.com/document/product/582/11524) 将 hugo 生成的 `public/` 目录中的文件上传到 CFS 文件系统根目录或子目录中。

### 步骤3：在 TEM 上部署 nginx 应用并关联 CFS[](id:step3)

1. 登录 [弹性微服务控制台](https://console.cloud.tencent.com/tem)，在应用部署所在的环境中关联上述购买的 CFS 实例。
![](https://main.qcloudimg.com/raw/065bea19e71061eb3e314c294254d9f6.png)

2. 在【[应用管理](https://console.intl.cloud.tencent.com/tem/env)】页面创建一个名为 hugo 的应用。
![](https://main.qcloudimg.com/raw/db37dc37340615e024871c65832972e4.png)

3. 部署应用，在【持久化存储】模块选择已关联的 CFS 存储资源。
![](https://main.qcloudimg.com/raw/d5abd09485e8f23a3934f5580651e7b3.png)


### 步骤4：在 TEM 上配置 nginx 的网络访问[](id:step4)
<dx-tabs>
::: 方案一：配置转发规则（推荐）
1. 在【[应用管理](https://console.intl.cloud.tencent.com/tem/env)】页面，单击刚刚创建的应用的“ID”，进入应用基本信息页面。
2. 在应用基本信息页面，在【访问配置】模块单击【前往配置】，进入环境访问配置页面。
![](https://main.qcloudimg.com/raw/80b914a4a5419cf717d26c67c480fc76.png)


3. 在环境访问配置页面，单击【新建】，创建一条访问配置规则。
![](https://main.qcloudimg.com/raw/88ad1932a18ce466e90e68bf1b4fe69a.png)


4. 单击【完成】，可获取如下 IP 地址。
![](https://main.qcloudimg.com/raw/b305cc5523afb03ac157cabaef7702cc.png)

通过生成的地址对 hugo 服务进行访问：

![](https://main.qcloudimg.com/raw/9b76fee79a65e46760235629b05f244f.png)
:::
::: 方案二：配置公网 CLB
1. 在【[应用管理](https://console.intl.cloud.tencent.com/tem/env)】页面，单击刚刚创建的应用的“ID”，进入应用基本信息页面。
2. 在应用基本信息页面，在【访问配置】模块单击右上角的【编辑并更新】，添加公网 CLB。
![](https://main.qcloudimg.com/raw/5bf8823dccf189f8be4fb495a87ea0c8.png)

3. 选择公网访问方式，填写端口映射关系。
![](https://main.qcloudimg.com/raw/c542ccc1cda09e456d86a275ec9263f8.png)

4. 单击【提交】后，可获取如下公网访问IP。
![](https://main.qcloudimg.com/raw/2aba58753a1fe53cb4f42a3c3d46d75e.png)

通过生成的地址对 hugo 服务进行访问：

![](https://main.qcloudimg.com/raw/fceeebcacde7f9b68a726d7777b8ca90.png)
:::
</dx-tabs>


### 步骤5：(可选) 配置域名[](id:step5)

1. 注册域名。
2. 将域名与上述生成的 CLB 实例进行关联，关联后即可通过域名访问静态网站，参考 [配置 DNS 解析 DNSPod 将域名指向 CLB](https://intl.cloud.tencent.com/document/product/214/8975)。

### 步骤6：(可选) 配置防火墙[](id:step6)

若静态网站的访问是通过 **转发配置** 设置，则可与腾讯云的 [Web 应用防火墙](https://intl.cloud.tencent.com/product/waf) 结合，对静态网站进行安全保护。详细配置可参见 [配置 WAF 对负载均衡的监听域名进行 Web 安全防护](https://intl.cloud.tencent.com/document/product/214/38751) 。

### 步骤7：(可选) 配置 CDN[](id:step7)

静态网站为了给用户更好的体验，通常会与 CDN 结合提供访问加速，托管的静态网站可与腾讯云 CDN 结合，参见 [腾讯云 CDN 新手指引](https://intl.cloud.tencent.com/document/product/228/36383)。
