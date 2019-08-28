## 网络环境介绍
腾讯云的网络环境可以分为 [私有网络](https://intl.cloud.tencent.com/product/vpc?idx=2)（Virtual Private Cloud，VPC）和基础网络两种，推荐您使用私有网络。
腾讯云私有网络（Virtual Private Cloud，VPC）是一块您在腾讯云上自定义的逻辑隔离网络空间，与您在数据中心运行的传统网络相似，托管在腾讯云私有网络内的是您在腾讯云上的服务资源，包括 [云服务器](http://intl.cloud.tencent.com/document/product/213/495)、[负载均衡](http://intl.cloud.tencent.com/document/product/214/524)、[云数据库](https://intl.cloud.tencent.com/doc/product/236) 等。
具体基础网络和私有网络的区别请参考[私有网络产品概述](http://intl.cloud.tencent.com/document/product/215/535) 。

## 为云数据库 Redis 配置网络
### 新购 Redis 配置网络
1. 登录 [腾讯云控制台](https://console.cloud.tencent.com/)，选择【云产品】>【数据库】>【云数据库Redis】，进入TencentDB for Redis控制台，单击【新建实例】开始新建数据库；或打开 [腾讯云官网](https://cloud.tencent.com/)，选择【产品】>【基础】>【数据库】>【云数据库Redis】，单击【立即选购】，在 [云数据库Redis选购页面](https://buy.cloud.tencent.com/buy/redis?regionId=4#/)开始新建数据库。

![](https://main.qcloudimg.com/raw/f391b05ba2abb90f54d68eee3c075fa5.png)
2. 在 [云数据库Redis选购页面](https://buy.cloud.tencent.com/buy/redis?regionId=4#/)，在【网络类型】中，可选【基础网络】和【私有网络】，推荐您选择私有网络，选择现有的【私有网络】和【子网】；如果目前【可用区】没有私有网络，请您先 [新建私有网络](https://console.cloud.tencent.com/vpc/vpc?rid=4) 后，在选购页面【网络类型】刷新一下，再选择私有网络。

![](https://main.qcloudimg.com/raw/8be0e67db61e588d2b8ec4bc43ef2c1f.png)
### 现有 Redis 更换网络
1. 登录 [腾讯云控制台](https://console.cloud.tencent.com/)，选择【云产品】>【数据库】>【云数据库Redis】，进入TencentDB for Redis控制台。
2. 在TencentDB for Redis控制台中，单击【实例列表】，单击【ID/实例名】，进入【实例详情】。

![](https://main.qcloudimg.com/raw/8a2383161e87e03ca1c53c33b935274f.png)
![](https://main.qcloudimg.com/raw/882d495354b725a4fa0b4d9b6b513d29.png)
3. 在【实例详情】的【网络信息】模块中，即可看到当前Redis实例的所属网络和内网地址等网络信息，单击【更换网络】，可以将Redis实例所属网络，从【基础网络】转换为【VPC网络】或从当前实例所属的【VPC网络】更换到另一个【VPC网络】，【新IP地址】可以自动分配也可指定地址，【旧IP地址】可以选择立即释放也可以数日后释放，以保证业务在更换网络时不中断，单击确认即可更换网络。
>!旧IP地址可以选择立即释放也可以数日后释放，更换网络时为保持服务可用性和业务不中断，请根据业务需要及时更新IP地址，谨慎释放旧IP地址。
>
![](https://main.qcloudimg.com/raw/1befc1f612813a27792cd811b7c2f8c1.png)

## 网络的基本操作
您在使用私有网络和云数据库Redis时，可能碰到诸如创建私有网络、创建弹性网卡、绑定和解绑 HAVIP 等问题。本文将介绍使用私有网络以及与其相关产品的常用操作，供您参考。

### 私有网络和子网
[私有网络和子网](http://intl.cloud.tencent.com/document/product/215/4927) 的关系如下：子网是 VPC 内的 IP 地址块，私有网络中的所有云资源都必须部署在子网内。子网具有可用区属性，创建 VPC后，您可以在私有网络所属地域的每个可用区中添加子网。下面将介绍使用私有网络和子网及与其相关产品的常用操作，供您参考。
- [创建私有网络](https://intl.cloud.tencent.com/document/product/215/8113)
- [新增子网](https://intl.cloud.tencent.com/document/product/215/8114)

## 云数据库Redis的网络连接
云数据库Redis在满足业务在缓存、存储、计算等不同场景中的需求时，可能面临云服务器和云数据库的网络连接问题。云服务器与云数据库部署在同一区域上，云服务器与云数据库部署在不同区域上：基础网络和 VPC 网络互通、VPC 网络之间互通，网络连接相关问题请参见 [云数据库Redis连接登录问题](http://intl.cloud.tencent.com/document/product/239/18664)。

