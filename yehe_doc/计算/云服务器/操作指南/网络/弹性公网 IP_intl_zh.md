## 操作场景
弹性公网 IP 地址（EIP），简称弹性 IP 地址或弹性 IP。它是专为动态云计算设计的静态 IP 地址，是某地域下一个固定不变的公网 IP 地址。借助弹性公网 IP 地址，您可以快速将地址重新映射到账户中的另一个实例或  NAT 网关实例，从而屏蔽实例故障。本文档介绍如何使用弹性 IP 地址。

## 前提条件

已登录 [云服务器控制台](https://console.cloud.tencent.com/cvm)。

## 操作步骤

### 申请弹性公网 IP 

1. 在左侧导航导航栏中，单击[**公网IP**](https://console.tencentcloud.com/cvm/ip)，进入公网 IP 管理页面。
2. 在公网 IP 管理页面，单击**申请**。
3. 在弹出的 “申请EIP” 窗口中，选择地域，设置 IP 地址类型、计费模式以及带宽上限，并填写数量。
4. 单击**确定**，完成弹性公网 IP 的申请。
5. 申请结束后即可在列表中看到您申请的弹性公网 IP，此时处于未绑定状态。

<span id = "jump2">  </span>
### 弹性公网 IP 绑定云产品

1. 在左侧导航导航栏中，单击[**公网IP**](https://console.tencentcloud.com/cvm/ip)，进入公网 IP 管理页面。
2. 在公网 IP 管理页面，选择需要绑定云产品的 EIP，单击**更多**>**绑定**。
<dx-alert infotype="notice" title="">
 若绑定时，EIP 已绑定实例，请先解绑。
</dx-alert>
3. 在弹出的 “绑定资源” 窗口中，选择弹性公网 IP 要绑定的资源，单击**确定**。
4. 在弹出的 “绑定弹性公网IP” 提示框中，单击**确定**，即可完成与云产品的绑定。


### 弹性公网 IP 解绑云产品

1. 在左侧导航导航栏中，单击[**公网IP**](https://console.tencentcloud.com/cvm/ip)，进入公网 IP 管理页面。
2. 在公网 IP 管理页面，选择需要解绑云产品的 EIP，单击**更多**>**解绑**。
3. 在弹出的 “解绑弹性公网IP” 窗口中，确认解绑信息，单击**确定**。
4. 在弹出的 “解绑弹性公网IP” 提示框中，单击**确定**，即可完成与云产品的解绑。
<dx-alert infotype="notice" title="">
 解绑后云产品实例可能会被分配新的公网 IP，被分配新的公网 IP 可能与绑定前公网 IP 不一致。
</dx-alert>

<span id = "jump">  </span>
### 释放弹性公网 IP

1. 在左侧导航导航栏中，单击[**公网IP**](https://console.tencentcloud.com/cvm/ip)，进入公网 IP 管理页面。
2. 在公网 IP 管理页面，选择需要释放云产品的 EIP，单击**更多**>**释放**。
3. 在弹出的 “确定释放所选弹性公网IP？” 窗口中，勾选**确定释放以上IP**，单击**释放**。

### 调整带宽
1. 在左侧导航导航栏中，单击[**公网IP**](https://console.tencentcloud.com/cvm/ip)，进入公网 IP 管理页面。
2. 在公网 IP 管理页面，选择需要调整带宽的 EIP，单击**调整网络**。
3. 在弹出的 “调整带宽” 窗口中，设置目标带宽值，单击**确定**，完成带宽调整。

### 公网 IP 转弹性 IP
随购买云服务器（Cloud Virtual Machine，CVM）实例时一起购买的公网 IP 为普通公网 IP，不具备弹性能力，即不能被挂载和卸载。 您可根据以下操作步骤，将普通公网 IP 转成 EIP。
1. 在左侧导航导航栏中，单击[**实例**](https://console.cloud.tencent.com/cvm/index)，进入实例管理页面。
2. 选择需转换为 EIP 的实例，单击 <img src="https://main.qcloudimg.com/raw/25e8c0e37b73c12da900301f03e57dbc.png" style="margin: 0;"></img>。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/dac8677bd2b48e99f6b99a5d351ec21e.png)
3. 在弹出的 “转换为弹性公网IP” 窗口，单击**确定转换**即可。
![](https://qcloudimg.tencent-cloud.cn/raw/4f6a6e6b93afa784983a7d67de80ff67.png)

## 异常排查
弹性 IP 地址可能出现网络不通的异常情况，一般有如下原因： 
- 弹性 IP 地址没有绑定云产品。具体绑定方法见 [弹性公网 IP 绑定云产品](#jump2)。
- 安全策略无效。查看是否有生效的安全策略（安全组或网络 ACL )。如果绑定的云产品实例有安全策略，例如禁止8080端口访问，那么弹性公网 IP 的8080端口也是无法访问的。
