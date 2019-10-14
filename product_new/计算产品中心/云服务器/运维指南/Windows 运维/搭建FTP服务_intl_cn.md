## 操作场景
本文档以 FileZilla 为例介绍在 Windows 云服务器上搭建 FTP 服务的操作。您也可以通过获取服务市场镜像，免除了您安装配置的各种工作，具体详情请参见 [云市场](https://market.cloud.tencent.com/list?cid=64)。

## 软件下载
 FileZilla 是一个快速可靠的、跨平台的 FTP 、 FTPS 和 SFTP 软件。具有图形用户界面（GUI） 和很多特性。易于使用，支持多种协议。
 FileZilla 中文版官方下载地址：[点此获取](https://www.filezilla.cn/download)

## 操作步骤

1. 登录云服务器。
2. 下载并运行 FileZilla Server 安装程序。
3. 阅读许可协议，单击【我接受】。
4. 选择安装的类型（保持默认即可），单击【下一步】。如下图所示：
![](https://main.qcloudimg.com/raw/96537179989adaae28ed43987910763d.png)
5. 选择安装位置，单击【下一步】。
6. <span id="step2">选择 FileZilla Server 的启动模式，设置 FileZilla Server的端口，单击【下一步】。如下图所示：</span>
一般情况下，选择默认的启动模式，管理端口选择未被占用的端口即可。
 ![](https://main.qcloudimg.com/raw/9336caf9f56b4cd84be68b0bf108bb9b.png)
7. 单击【安装】，启动 FileZilla Server。
8. 在打开的 “连接到服务器” 窗口中，填写以下信息，单击【确定】，连接 FileZilla 服务器。如下图所示：
![](https://main.qcloudimg.com/raw/70e43cd78e7b52b2a3f7db51341fc011.png)
 - 服务器地址：输入127.0.0.1
 - 端口：填写 [步骤6](#step2) 设置的管理端口。例如 14147。
9. 在 FileZilla Server 窗口中，单击 <img src="https://main.qcloudimg.com/raw/6eaffea83cd46f08300a27dcdf1c62a1.png" style="margin: 0;">，打开用户窗口。
10. 在打开的 “用户” 窗口中，单击【添加】，弹出 “添加用户账户” 对话框。如下图所示：
![](https://main.qcloudimg.com/raw/192ce19ec011d7b4848146a3a4b6a1e6.png)
11.  在弹出的 “添加用户账户” 对话框中，输入用户名，单击【确定】。
例如，输入 tencent-qcloud 用户名。
12.  在 “用户” 窗口中，勾选【密码】，为新增的用户设置密码，并单击【确定】。如下图所示：
![](https://main.qcloudimg.com/raw/b456b2cddb1a44806d0a2c1fc5377c6a.png)
13.  在弹出的提示框中，单击【确定】。
14.  在 “Shared folders” 设置界面，单击【添加】，新增用户目录。如下图所示：
![](https://main.qcloudimg.com/raw/567e7c0bec0d9d69749835767cc6697d.png)
15.  选择 FTP 的资源目录，单击【确定】。如下图所示：
例如，选择 Tencent-Qcloud 目录作为 FTP 的资源目录，并在该目录下放置`欢迎使用腾讯云服务器.txt`文件，便于 [检验 FTP 服务](#checkFTPService)。
![](https://main.qcloudimg.com/raw/1df0c3ea3d63a1dcb671137b0b475f41.png)
16.  在 “共享文件夹” 栏中，设置用户对 FTP 的资源目录的操作权限。如下图所示：
![](https://main.qcloudimg.com/raw/43fae3ae7e4e0f7d63259d1068351cd2.png)
17.  单击【确定】，完成 FileZilla FTP 服务的搭建。

<sapn id="checkFTPService"></span>
## 检验 FTP 服务

1. 在本地 PC 中，安装并打开 FileZilla 客户端。
2. 在打开的 FileZilla 客户端中，输入云服务器公网 IP 、FTP 用户、密码，并单击【快速连接】，即可看到 FileZilla 服务器分享给该用户的目录，还可以看到之前放在该目录里面的文件“欢迎使用腾讯云服务器.txt ”。如下图所示：
![](https://main.qcloudimg.com/raw/875b51c3d89cc358e492a240caac1ce2.png)
3. 切换至 FileZilla 服务器，即可监控到 FileZilla 客户端的连接。如下图所示：
![](https://main.qcloudimg.com/raw/c2b9042feeded36ac872db7f9aee8062.png)



