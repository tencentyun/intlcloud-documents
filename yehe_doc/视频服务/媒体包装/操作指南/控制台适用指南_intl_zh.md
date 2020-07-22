MediaPackage控制台基于Channel维度进行管理，整体可分为Channel、Input、Endpoint三个模块。

## 一、	Channel
Channel是MediaPackage输入流及输出流的基础配置，用户基于创建完成Channel可以输入既定协议的直播流，也可以创建相应的回源节点（Endpoint，详见第三节）供直播流输出分发。
创建Channel的基本步骤有：
>1.点击“Create Channel”按钮创建频道
>2.输入Channel Name，选择Channel输入协议（支持HLS/DASH）
>3.保存参数，创建完毕

创建完毕后即跳转至Channel的详情页，详情页会显示Channel的Name、ID（由后台自动生成）以及指定的输入协议。同时会基于指定的协议自动生成两个输入点（详见第二节）。
在Channel列表页，用户可对创建完成的所有Channel进行管理，可以查看Channel的详情，可以重新编辑、删除Channel。当Channel已有endpoint节点时不支持删除，若需要删除channel需先删除包含的所有endpoint节点。

## 二、	Input
Input是Channel输入的基本单位，后台会基于创建完成的Channel自动生成两个Input节点以及对应的输入URL，用户可将直播流推到节点的URL中。

![](https://main.qcloudimg.com/raw/ca34978793d405f87e5329aadc0c7a3d.png)

Input模块支持Authentication操作，用户可对每个输入点独立做Authentication配置。当用户打开Authentication配置后，后台会对该输入节点自动生成一对Username和Password，通过http认证模式进行鉴权。同时用户可点击下方按钮来rotate credentials。
注意：一旦用户rotate credentials, the existing channel credential will become invalid.

![](https://main.qcloudimg.com/raw/af9879f64b667cb86a0abf8c7f3ca24e.png)

## 三、	Endpoint

用户可对每个Channel创建回源拉流endpoint节点，创建的基本步骤有：

![](https://main.qcloudimg.com/raw/ef20b721c63718a2ecbece5799f9b686.png)

>1.点击“Create Endpoints”按钮创建频道
>2.输入Endpoint Name，Endpoint type默认与Channel的输入协议相同
>3.用户可根据需要选择是否开启IP黑白名单、Authkey等功能
>4.保存设置，创建完毕

Endpoint输出支持输出配置IP 黑白名单：指定固定合法ip段进行推流，或者拒绝异常IP端推流。支持配置Authkey，支持http-header通过 X-TENCENT-PACKAGE进行鉴权。

创建完毕后即跳转至Endpoint的列表页，创建完毕的endpoint支持编辑及删除操作。用户可基于生成的endpoint URL进行回源拉流操作，从而对直播流进行distribution。

