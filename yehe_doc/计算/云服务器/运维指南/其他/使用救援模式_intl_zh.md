## 操作场景
在使用云服务器操作系统的过程中，若引发机器 grub 引导文件丢失、系统关键文件缺失、lib 动态库文件损坏/缺失等问题时，可能会导致操作系统无法进入单用户模式并完成修复，此时需使用云服务器救援模式来进行系统修复。本文介绍如何通过云服务器控制台，使用救援模式。


## 操作步骤

### 进入救援模式

<dx-alert infotype="notice" title="">
进入救援模式前，强烈建议您对实例进行备份，以防止由于出现误操作等造成的影响。云硬盘可通过 [创建快照](https://intl.cloud.tencent.com/document/product/362/5755) 备份，本地系统盘可通过 [创建自定义镜像](https://intl.cloud.tencent.com/document/product/213/4942) 镜像备份。
</dx-alert>

1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/instance/index?rid=1)。
2. 在实例管理页面中，根据实际使用的视图模式进行操作：
<dx-tabs>
::: 列表模式
选择实例所在行右侧的**更多** > **运维与检测** > **进入救援模式**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/1c550dfc43f5b136401f877a1621a84e.png)
:::
::: 页签模式
选择实例所在页签，并选择右上方的**更多操作** > **运维与检测** > **进入救援模式**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/633e92a792afa8d19e735db38c7e5598.png)
:::
</dx-tabs>
3. [](id:step3)在弹出的“进入救援模式”窗口中，设置救援模式期间登录实例的密码。如下图所示：
<dx-alert infotype="notice" title="">
- 目前救援模式仅支持 Linux 实例，不支持 Windows 实例。如您操作 Windows 实例进入救援模式，则会默认进入 Linux 救援模式（CentOS 7.5 64位）下。
- 救援模式下实例用户名默认为 `root`。
- 实例仅在关机状态下可进入救援模式，强制关机可能会导致数据丢失或文件系统损坏，建议现将实例关机后再进行操作。实例关机操作请参见 [关机实例](https://intl.cloud.tencent.com/document/product/213/4929)。
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/0c4462f0c86de84a23cac475e0541c84.png"/>
4. 单击**进入救援模式**。
此时可在查看实例正在进入救援模式，当查看实例状态如下图所示，则说明已成功进入救援模式，请参考下一步尽快修复实例。
![](https://qcloudimg.tencent-cloud.cn/raw/46661eec9cabb65ab9ba358015373492.png)



### 使用救援模式进行系统修复
1. 使用 `root` 帐户及 [步骤3](#step3) 中设置的密码，通过以下方式登录实例。
 - 若实例有公网 IP，则请参考 [使用 SSH 登录 Linux 实例](https://intl.cloud.tencent.com/document/product/213/32501)。
 - 若实例无公网 IP，则请参考 [使用 VNC 登录 Linux 实例](https://intl.cloud.tencent.com/document/product/213/32494)。
2. 登录成功后，依次执行以下命令挂载系统盘根分区。
救援模式下实例系统盘设备名为 `vda`，根分区为 `vda1`，默认未挂载。
```
mkdir -p /mnt/vm1
```
```
mount /dev/vda1 /mnt/vm1
```
挂载成功后，您即可操作根分区中的数据。您也可使用 `mount -o bind` 命令，挂载原文件系统的一部分子目录，并通过 `chroot` 命令用来在指定的根目录下运行指令，具体操作命令如下：
```
mount -o bind /dev /mnt/vm1/dev
mount -o bind /dev/pts /mnt/vm1/dev/pts
mount -o bind /proc /mnt/vm1/proc
mount -o bind /run /mnt/vm1/run
mount -o bind /sys /mnt/vm1/sys
chroot /mnt/vm1 /bin/bash
```


### 退出救援模式
1. 实例修复完成后，根据实际使用的视图模式通过以下步骤退出救援模式：
<dx-tabs>
::: 列表模式
选择实例所在行右侧的**更多** > **运维与检测** > **退出救援模式**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/42b6657af00132b39a4b3242748a449c.png)
:::
::: 页签模式
选择实例所在页签，并选择右上方的**更多操作** > **运维与检测** > **退出救援模式**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/24df2366e42e1bdc22c171d871073c68.png)
:::
</dx-tabs>
2. 实例退出救援模式后，将处于关机状态，参考 [开机实例](https://intl.cloud.tencent.com/document/product/213/38168) 开机后即可恢复使用。

