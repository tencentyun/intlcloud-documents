## 操作场景

在创建多台实例过程中，如果您希望实例名称具有一定的规则性，我们提供批量创建实例后缀数字自动升序功能以及指定模式串功能，您可以通过购买页和云 API 两种方式实现。

- 当您需要购买 n 个实例并希望生成类似为 “CVM+序号” 的实例名称时（即实例名称为 CVM1、CVM2、CVM3 等实例），您可通过 [后缀数字自动升序](#AutoAscending) 实现。
- 当您需要创建 n 个实例且指定实例的序号从 x 开始递增时，您可通过 [指定单个模式串](#SpecifySingleString) 实现。
- 当您希望创建 n 个有多个前缀且每个前缀均指定序号的实例时，您可通过 [指定多个模式串](#SpecifyMultipleStrings) 实现。


## 操作步骤

<span id="AutoAscending"></span>
### 后缀数字自动升序

可将批量购买的实例设置为前缀相同，仅序号递增的实例名称。
>创建成功的实例默认序号从1开始递增，且不能指定开始的序号。
>
以下操作以您购买了3台实例，并希望生成的实例名称为 “CVM+序号”（即实例名称为 CVM1、CVM2 和 CVM3）为例。

#### 购买页操作

1. 参考 [创建实例](http://intl.cloud.tencent.com/document/product/213/4855) 购买3台实例，并在“2.设置主机”中以**“前缀+序号”**的命名规则填写实例名称，即将实例名称填写为 `CVM`。如下图所示：
![](https://main.qcloudimg.com/raw/820a52077080be5da4c1fb4715452e6b.png)
2. 根据页面提示逐步操作，并完成支付。
4. 返回 [云服务器控制台](https://console.cloud.tencent.com/cvm/index) 查看新创建实例，即可发现批量购买的实例前缀相同，序号递增。如下图所示：
![](https://main.qcloudimg.com/raw/27de624cd251910d47bea8e7732b284b.png)

#### API 操作

在云 API [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237) 中，将 InstanceName 字段指定为 `CVM`。

### 指定模式串

可将批量购买的实例设置为复杂且指定序号的实例名称。实例名称支持指定单个或者多个模式串，在设置实例名称时，请根据实际需求进行设置。

指定模式串的命名：**{R:x}**，x 表示生成实例名称的初始序号。

<span id="SpecifySingleString"></span>
#### 指定单个模式串

以下操作以您需要创建3台实例，且指定实例的序号从3开始递增为例。

##### 购买页操作

1. 参考 [创建实例](http://intl.cloud.tencent.com/document/product/213/4855) 购买实例，并在“2.设置主机”中以**“前缀+指定模式串{R:x}”**的命名规则填写实例名称，即将实例名称填写为 `CVM{R:3}`。如下图所示：
![](https://main.qcloudimg.com/raw/4e09732d612222f619cf7a1e8da1ee06.png)
2. 根据页面提示逐步操作，并完成支付。
3. 返回 [云服务器控制台](https://console.cloud.tencent.com/cvm/index) 查看新创建实例，即可发现批量购买的实例前缀相同，序号从3开始递增。如下图所示：
![](https://main.qcloudimg.com/raw/78dc40cf4baa707573ad95a77bed4e1d.png)

##### API 操作

在云 API [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237) 中，将 InstanceName 字段指定为 `CVM{R:3}`。

<span id="SpecifyMultipleStrings"></span>
#### 指定多个模式串

以下操作以您需要创建3台实例，并希望生成实例名称含有 cvm、 Big 和 test 前缀，且 cvm 和 Big 前缀后面带序号，序号分别从13和2开始递增（即实例名称为 cvm13-Big2-test、cvm14-Big3-test、cvm15-Big4-test）为例。

##### 购买页操作

1. 参考 [创建实例](http://intl.cloud.tencent.com/document/product/213/4855) 购买3台实例，并在“2.设置主机”中以**“前缀+指定模式串{R:x}-前缀+指定模式串{R:x}-前缀”**的命名规则填写实例名称，即将实例名称填写为 `cvm{R:13}-Big{R:2}-test` 。如下图所示：
![](https://main.qcloudimg.com/raw/1042e86262bc7ce3939f1842a8025c23.png)
2. 根据页面提示逐步操作，并完成支付。
3. 返回 [云服务器控制台](https://console.cloud.tencent.com/cvm/index) 查看新创建实例，即可发现批量购买的实例会根据每个前缀指定的序号递增。如下图所示：
![](https://main.qcloudimg.com/raw/a3c5e58daf07381ffde5abc019edad33.png)

##### API 操作

在云 API  [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237) 中，将 InstanceName 字段指定为 ` cvm{R:13}-Big{R:2}-test`。

