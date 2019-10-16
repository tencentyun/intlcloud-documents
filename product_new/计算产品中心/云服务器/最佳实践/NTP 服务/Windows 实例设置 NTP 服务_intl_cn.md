## 操作场景

本文介绍 Windows Server 如何开启 NTP 服务和修改时钟源服务器地址。

Windows 时间服务（Windows Time service， W32Time）用于本地系统与时钟源服务器之前的时间同步。其使用网络时间协议（NTP）来同步网络上的计算机时钟。 下面以 Windows Server 2016 为例，说明如何用客户端和命令行的方式开启 NTP 服务和修改时钟源服务器地址。

## 操作步骤

1. [远程登录 Windows 实例](https://intl.cloud.tencent.com/document/product/213/5435)。
2. 单击 “管理工具 > 服务 > Windows Time”。
![Windows Time](https://main.qcloudimg.com/raw/c5e41df2fc832b0f25f798408163664c.png)
3. 启动类型设置为 “自动”，如果服务未启动，则单击 “启动”。
![w32time](https://main.qcloudimg.com/raw/9201ddaca176a1523d5d12d02b6c8ec5.png)
4. 任务栏的通知区域，单击时间，单击 “更改日期和时间设置”。
![时间设置](https://main.qcloudimg.com/raw/28ba1cf5968466e114e93d222b957f99.png)	
5. 切换到 “Internet时间” 标签，单击更改设置。
![Internet时间](https://main.qcloudimg.com/raw/acc52fce975638cef4e39f9f821d66bc.png)
6. 在 Internet 时间设置弹窗中，输入目标时钟源服务器域名或者 IP 地址，单击 “确定”。
![Internet时间设置](https://main.qcloudimg.com/raw/205ef59f3e8583af965a9381df0a9ef9.png)
7. 设置完成后，重新打开 “日期与时间” 即可看到时钟源服务器已经更换。
![确认](https://main.qcloudimg.com/raw/767eee448b33ed38ea7bc2fbdadf780d.png)


