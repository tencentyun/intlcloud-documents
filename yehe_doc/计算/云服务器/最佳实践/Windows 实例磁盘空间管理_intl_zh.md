## 操作场景
本文以操作系统为 Windows Server 2012 R2 的腾讯云云服务器为例，介绍如何在 Windows 实例磁盘空间不足的情况下进行空间释放操作，及如何进行磁盘的日常维护。

## 操作步骤

### 释放磁盘空间
您可通过 [删除容量较大文件](#deleteLargerFiles) 或 [删除不需要文件](#deleteObsoleteFiles) ，来解决磁盘空间不足的问题。若清理文件无法满足您的实际需求，则请选择扩容磁盘来扩展磁盘空间，详情请参见 [扩容场景介绍](https://intl.cloud.tencent.com/document/product/362/31600)。
<span id="deleteLargerFiles"></span>
#### 删除容量较大文件
1. [使用 RDP 文件登录 Windows 实例（推荐）](https://intl.cloud.tencent.com/document/product/213/5435)。您也可以根据实际操作习惯，[使用远程桌面连接登录 Windows 实例](https://intl.cloud.tencent.com/document/product/213/32498)。
2. 选择底部工具栏中的<img src="https://main.qcloudimg.com/raw/dcdf8e1ebc35bd6db1edaceff6784db2.png" style="margin:-5px 0px">，打开“这台电脑”。
3. 在“这台电脑”中，选择需要清理的磁盘，按 **Crtl + F** 打开搜索工具。
4. 选择【搜索】>【大小】，根据系统定义的大小在菜单中按需筛选文件。如下图所示：
![](https://main.qcloudimg.com/raw/48a1033c6b978dfe6de1b2dc6d8bcdd3.png)
>?您还可以在“这台电脑”右上角的搜索框中，自定义文件大小进行检索。例如：
>- 输入“大小：>500M”，则会检索该磁盘中大于500M的文件。
> - 输入“大小：> 100M < 500M”，则会检索该磁盘中大于100M但小于500M的文件。
>

<span id="deleteObsoleteFiles"></span>
#### 删除不需要文件
1. 选择<img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin:-5px 0px">，打开服务器管理器。
2. 单击【添加角色和功能】，弹出 “添加角色和功能向导” 窗口。
3. 在 “添加角色和功能向导” 窗口中，单击【下一步】。
4. 在 “选择安装类型” 界面，选择【基于角色或基于功能的安装】，并连续单击3次【下一步】。如下图所示：
![](https://main.qcloudimg.com/raw/d25dc913281f8cb5c688dd9cc62b8d73.png)
5. 在“选择功能”界面勾选“墨迹手写服务”和“桌面体验”，并在弹出的提示框中单击【确认】。如下图所示：
![](https://main.qcloudimg.com/raw/f1bf18c4598597ef86428bd4bbd77c15.png)
6. 选择【下一步】，并单击【安装】。安装完成后，参考界面上的提示重启服务器。
7. 选择<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-5px 0px">，单击右上角的<img src="https://main.qcloudimg.com/raw/4851c97390178d2d8ae2e6385756eb3b.png" style="margin:-5px 0px">。在搜索中输入“磁盘管理”，并进行搜索。
8. 在弹出的“磁盘清理”窗口中选择对应磁盘开始清理。如下图所示：
![](https://main.qcloudimg.com/raw/69e2c653c6304a450463cdf07bf5a3ef.png)

### 磁盘日常维护
#### 定期清理应用程序
您可选择“控制面板”中的“卸载程序”，定期清理不再使用的应用程序。如下图所示：
![](https://main.qcloudimg.com/raw/b9294f1e79429dbdb8a7800cfdb6d6b4.png)


#### 通过控制台查看磁盘使用情况
腾讯云默认在创建云服务器时开通云监控服务，因此可通过控制台查看云服务器磁盘使用情况。步骤如下：
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/instance/index)，进入“实例”列表页面。
2. 选择需查看的实例 ID，进入实例详情页面。
3. 在实例详情页面，选择【监控】页签，即可查看该实例下磁盘使用情况。如下图所示：
![](https://main.qcloudimg.com/raw/19f00a883ed73ba1c636830f06d3f00d.png)
