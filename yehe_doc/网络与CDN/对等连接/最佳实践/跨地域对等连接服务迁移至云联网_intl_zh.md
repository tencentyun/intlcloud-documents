## 背景信息
云联网和对等连接均可以实现跨地域 VPC 间互通，相比对等连接，云联网具有链路全互联、路由自学习、配置简单、稳定可靠、更低成本和时延等优势。
为提供更优的业务体验，本文提供跨地域对等连接迁移至云联网的迁移方案和指导。

## 操作场景
+ **场景一**：南京 VPC1 和 VPC2 通过对等连接打通。
**迁移方案**：可将两个 VPC 关联至云联网来实现跨地域 VPC 间互通。
 + 迁移前：
![](https://qcloudimg.tencent-cloud.cn/raw/611e69a61efcf4a901109b8d23a441d1.png)
 + 迁移后：
![](https://qcloudimg.tencent-cloud.cn/raw/e74c2ad1a76e0bf6205e4538e266d6a7.png)
+ **场景二**：跨地域多个 VPC 间需要全互联，由于对等连接连通性不能传递，因此每两个 VPC 之间都通过对等连接互通。
 **迁移方案**：可将多个 VPC 加入一个云联网实例来实现全网互通。
 + 迁移前：
![](https://qcloudimg.tencent-cloud.cn/raw/ad9b5f6140c8f0db6820eecc46be0bad.png)
 + 迁移后：
![](https://qcloudimg.tencent-cloud.cn/raw/1c85740f9e423952797b3f3978a7d39d.png)
+ **场景三**：VPC1 通过对等连接分别与 VPC2、VPC3 打通，VPC2 和 VPC3 之间不互通。
  **迁移方案**：可使用云联网打通 VPC1 和 VPC2、VPC3，VPC2 和 VPC3 之间的不互通可通过子网关联网络 ACL 来实现访问控制，即 ACL 中仅放通需要通信的网段即可。
	迁移前：
	![](https://qcloudimg.tencent-cloud.cn/raw/6b8a072fb99dba9f432cf9cff91e3564.png)
	迁移后：
	![](https://qcloudimg.tencent-cloud.cn/raw/9303ef9f65fd712024287eb18bd67265.png)
+ **场景四**：VPC1 与 VPC2、VPC3 分别通过对等连接通信，VPC2 和 VPC3 不通，其中 VPC1 的子网11和 VPC2 的子网21、VPC3 的子网31通信；VPC1 的子网12与 VPC2 的子网22、VPC3 的子网32通信；VPC1 的子网13与 VPC2 的子网23、VPC3 的子网33通信。
>?子网间的访问控制通过各自的网络 ACL 来实现，例如 VPC2 的子网21的网络 ACL21，出入站仅放通需要通信的 VPC1 的子网11的网段，其余网段将均被拒绝，以此来达到子网间流量访问控制的目的。
>
**迁移方案**：可使用云联网打通 VPC1、VPC2、VPC3，由于云联网会使得 VPC1、VPC2、VPC 全互通，因此请提前确认好各个子网的 ACL 规则确保其只放通了需要通信的子网网段即可。
	 迁移前：
	 ![](https://qcloudimg.tencent-cloud.cn/raw/5a43d3bd93e71a43ee820f66f4d1f6bf.png)
	 迁移后：
	 ![](https://qcloudimg.tencent-cloud.cn/raw/b79d263535fa728032f342a083f88e51.png)

## 操作步骤
>?
>+ 以场景一为例，给出操作步骤。
>+ 场景二中相比场景一为多 VPC 间全互通，请将 VPC 逐一加入云联网，并及时确认云联网及 VPC 中的路由情况。当因网段重叠等原因导致路由产生冲突时，路由状态将为无效，请分别参考[ 云联网路由冲突处理原则](https://intl.cloud.tencent.com/document/product/1003/30052)、[VPC 路由冲突处理原则](https://intl.cloud.tencent.com/document/product/1003/30078) 处理即可。
>+ 场景三和场景四，请提前根据子网间的通信情况，为子网配置合适的 [ACL 策略](https://intl.cloud.tencent.com/document/product/215/31852)，再逐一关联 VPC 网络至云联网，并将路由迁移至云联网，期间可通过监控实时查看业务情况。
>
1. [创建1个云联网实例](https://intl.cloud.tencent.com/document/product/1003/30062)，并关联VPC1。
 ![]()
2. 单击云联网 ID，并进入路由表页签，可看到云联网路由表中，目的端为 VPC1 子网的路由策略。云联网路由添加逻辑，可参考[ 云联网路由概述](https://intl.cloud.tencent.com/document/product/1003/34259)。
![]()
3. 请参见 [关联网络实例](https://intl.cloud.tencent.com/document/product/1003/30064) 将 VPC2 关联至云联网。
4. 再次单击云联网 ID，进入路由表页签，可看到云联网路由表中，新增目的端为 VPC2 子网的路由策略。云联网侧路由如有状态异常，请参见[ 云联网路由冲突处理原则 ](https://intl.cloud.tencent.com/document/product/1003/30052)处理。
 ![]()
5. 分别查看 VPC1 和 VPC2 子网关联的路由表，可看到路由策略中均新增一条下一跳到云联网的路由策略，但根据路由冲突原则，目的端网段重叠时，后加入的路由不生效，因此此时 VPC1 和 VPC2 通信依然走的是对等连接。
VPC1 子网路由表：
 ![]()
VPC2 子网路由表：
![]()
6. <span id="step6">请参考 [启用路由策略](https://intl.cloud.tencent.com/document/product/215/40080) 在 VPC1 的路由表中，启用 VPC1 到 VPC2 指向云联网的路由策略，并禁用 VPC1 到 VPC2 指向对等连接的路由策略，此时 VPC1 到 VPC2 走的是云联网，VPC2 到 VPC1 仍然走的是对等连接，链路可正常通信。
	![]()
7. 查看监控或[ 登录 CVM](https://intl.cloud.tencent.com/document/product/213/5436) ping 网络查看流量是否正常，监控查看方式请参见[ 查看云联网监控数据](https://intl.cloud.tencent.com/document/product/1003/30071)、[查看跨地域对等连接监控数据](https://intl.cloud.tencent.com/document/product/553/18842)。如不正常请回退后 [提交工单](https://console.cloud.tencent.com/workorder/category)。
    ![](https://qcloudimg.tencent-cloud.cn/raw/0b107fad18337e7359249f53939ad706.png)
8. 请参考 <a href ="#step6">步骤6</a> 在 VPC2 的路由表中，启用 VPC2 到 VPC1 指向云联网的路由策略，并禁用 VPC2 到 VPC1 指向对等连接的路由策略。
9. 请查看监控或查看 ping 流量是否正常。
    + 如不正常请回退后 [提交工单](https://console.cloud.tencent.com/workorder/category)。
    + 如一周内业务流量均正常，且通过监控查看对等连接已确认无任何流量，则可以参考 [删除路由策略](https://intl.cloud.tencent.com/document/product/215/40080)、[删除对等连接](https://intl.cloud.tencent.com/document/product/553/18848) 删除 VPC1 和 VPC2 路由表中指向对等连接的路由策略以及对等连接服务，此时迁移完成。
    
