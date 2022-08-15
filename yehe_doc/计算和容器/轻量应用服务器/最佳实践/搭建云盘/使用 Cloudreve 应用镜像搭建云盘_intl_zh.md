## 操作场景
Cloudreve 是一款开源的网盘软件，支持服务器本机及腾讯云对象存储 COS 等多种存储方式，提供离线下载、拖拽上传、在线预览等功能，能够帮助您快速搭建个人使用或多人共享的云盘系统。该镜像基于 CentOS 8.2 64位操作系统，已预置 Nginx、Aria2、MariaDB 软件。

本文介绍如何使用 Cloudreve 应用镜像搭建 Cloudreve 云盘，实现文件上传、分享及离线下载功能。




## 操作步骤

### 使用 Cloudreve 镜像创建实例
1. 登录 [轻量应用服务器控制台](https://console.cloud.tencent.com/lighthouse)，在“服务器”页面单击【新建】。
2. 在轻量应用服务器购买页面，选择所需配置完成轻量应用服务器购买。
其中，“镜像”选择为【应用镜像】>【Cloudreve 3.3.1】，其他参数可参考 [购买方式](https://intl.cloud.tencent.com/document/product/1103/41404) 进行选择。
>?
>- 若实例所在地域为中国内地，则建议选择更适合搭建云盘的存储型套餐。详情请参见 [基础套餐](https://intl.cloud.tencent.com/document/product/1103/41403)。
>- 本文以使用应用镜像 Cloudreve 3.3.1 为例，镜像可能会进行版本升级与更新，请您以购买页实际版本为准。
>

### 使用 Cloudreve

#### 登录 Cloudreve 页面
1. 在实例详情页中，选择【应用管理】页签，进入应用管理详情页。您可以在此页面查看 Cloudreve 应用的各项配置信息。
2. [](id:Step2)在“应用内软件信息”栏中，单击 <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin:-3px 0px">，复制获取 Cloudreve 管理员密码的命令。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/578abda0cc68cd607ec3bd5e407836c7.png)
3. 在“应用内软件信息”栏中，单击【登录】。
4. 在弹出的登录窗口中，粘贴并执行 [步骤2](#Step2) 获取的命令，按 **Enter**。
5. [](id:Step5)记录返回结果中的 Cloudreve 管理员名与密码（即 “cloudreve_username” 和 “cloudreve_password” 值）。如下图所示：
![](https://main.qcloudimg.com/raw/34b600733c567907d203f2db974726fe.png)
6. 使用浏览器访问“应用内软件信息”中的“首页地址”，输入 [步骤5](#Step5) 获取的用户名与密码，并单击【登录】。

#### 上传文件至 Cloudreve
在 Cloudreve 页面中，您可直接将本地文件拖拽至指定区域，或单击右键选择上传文件/目录，进行文件上传。

#### 分享文件
 Cloudreve 支持将文件或文件夹的下载链接分享给您的好友，还可针对该下载链接设置密码保护或过期时间。步骤如下：
1. 在 Cloudreve 页面中，右键单击需分享的文件，并在弹出菜单中选择【创建分享链接】。
2. 在弹出的“创建分享链接”窗口中，按需进行设置，并单击【创建分享链接】。
3. 获取链接后，只需访问 `首页地址+分享链接` 即可下载该文件。
例如，首页地址为 `http://xxx.xxx.xxx`，分享链接为 `/s/jRfM`，则访问 `http://xxx.xxx.xxx/s/jRfM` 即可下载该文件。

#### 离线下载
Cloudreve 应用镜像中已预置 Aria2，无需重复下载安装。Cloudreve 支持 Aria2 驱动的离线下载功能。在使用该功能前，您需了解 Aria2 配置与 Cloudreve 接入设置。步骤如下：
1. 在 Cloudreve 页面中，选择右上角的用户头像，并在弹出菜单中单击【管理面板】。
2. 进入”Cloudreve 仪表盘“ 页面，选择左侧导航栏中的【参数设置】>【离线下载】。
您可参考 [离线下载](https://docs.cloudreve.org/use/aria2)，按需修改相关参数设置。



创建离线下载步骤如下：
1. 在 Cloudreve 页面中，选择左侧导航栏中的【离线下载】。
2. 进入“离线下载”页面，选择页面右下角的【+】。
3. 在弹出的“新建离线下载任务”窗口中，根据指引创建下载任务即可。如下图所示：

#### 后台管理
1. 在 Cloudreve 页面中，选择右上角的用户头像，并在弹出菜单中单击【管理面板】。
2. 进入”Cloudreve 仪表盘“页面，您可进行用户组权限、存储策略等参数设置。
 - 可根据用户所属的用户组类型设置其权限，例如容量上限、下载速度、创建分享、下载分享及 WebDAV 等。
 - 可更改默认存储策略，各类型存储策略对比请参见 [对比 - Cloudreve](https://docs.cloudreve.org/use/policy/compare)。

