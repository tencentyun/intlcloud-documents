在 HAVIP 控制台，可查看指定地域下的所有 HAVIP 详细信息。
>?目前 HAVIP 产品处于灰度优化中，如有需要，请提交 [工单申请](https://console.intl.cloud.tencent.com/workorder/category)。
>


## 操作步骤
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/)。
2. 在左侧导航栏中，选择 **IP 与网卡** > **高可用虚拟 IP**，进入高可用虚拟 IP 界面。
3. 选择**地域**，可查看该地域下所有已申请的 HAVIP 的详细信息。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/imK6454_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230330100432.png)
	字段含义如下：
	+ **ID/名称**：HAVIP 创建后，系统会自动生成一个 ID，单击 ID 可进入 HAVIP 的基本信息界面；名称为创建时用户自定义的名称。
	+ **状态**：表示该 HAVIP 是否已在云服务器的 HA 软件的配置文件中被指定为可漂移的 VIP，如已配置成功，则状态显示为**已绑定云服务器**，如未配置或配置失败，则状态显示为**未绑定云服务器**。
	+ **地址**：HAVIP 的地址。
	+ **后端网卡**：HAVIP 绑定的云服务器的弹性网卡 ID，如 HAVIP 未绑定云服务器，则此处显示为 **-** 。
	+ **所属主机**：HAVIP 绑定的云服务器 ID，如 HAVIP 未绑定云服务器，则此处显示为 **-** 。
	+ **弹性公网 IP**：HAVIP 绑定的 EIP，如 HAVIP 未绑定 EIP，则此处显示为 **-** 。
	+ **所属网络**：HAVIP 所在私有网络。
	+ **所属子网**：HAVIP 所在子网。
	+ **申请时间**：HAVIP 申请的时间。
	+ **操作**：HAVIP 可执行的操作，包括：绑定弹性 IP、解绑弹性 IP、释放。
	   +  **绑定弹性 IP**：用于绑定 EIP
	   +  **解绑弹性 IP**：用于解绑 EIP
	   +  **释放**：用于释放 HAVIP
3. 在右侧搜索框中，可输入 ID、名称或地址，进行快速搜索。
4. 单击右上角刷新图标，可刷新界面。
