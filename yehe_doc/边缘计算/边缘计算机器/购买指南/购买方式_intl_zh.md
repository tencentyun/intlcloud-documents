边缘计算机器 ECM 提供了两种购买方式：控制台购买和 API 购买。本文将详细介绍两种购买方式。

## 控制台购买

腾讯云用户登录边缘计算机器控制台后，可以通过创建边缘模块并在边缘节点部署边缘实例的方式购买边缘计算机器服务。
其中，边缘计算机器的费用包括计算存储和网络带宽两部分，详情请参见 [计费概述](https://intl.cloud.tencent.com/document/product/1119/43404)。
如下介绍了如何在控制台上购买边缘计算机器的具体操作：
1. 登录 [边缘计算机器控制台](https://console.cloud.tencent.com/ecm/module/create1)。
2. 创建边缘模块，选择适合业务需求的实例配置、网络带宽等参数。
3. 在边缘模块下，设置密码、镜像及带宽，选择边缘节点，以及需要部署的边缘计算实例数量。
4. 确认边缘节点区域和实例数量无误后，提交创建边缘实例。
5. 订单支付成功后，系统将根据订单信息在相应的边缘节点区域部署边缘计算实例。

>!
> - 边缘计算实例创建完成后，会根据资源用量进行计费，请确保您的账户余额充足。账户余额不足可能导致欠费和实例被回收。详情请参阅 [欠费说明](https://intl.cloud.tencent.com/document/product/1119/43408)。
> - 关于边缘实例的各项配置，您可参阅 [计费概述](https://intl.cloud.tencent.com/document/product/1119/43404) 后结合实际需求进行选购。
>

## API 购买
欲通过 API 购买边缘计算机器 ECM 的用户，可参阅 API 文档创建实例。
