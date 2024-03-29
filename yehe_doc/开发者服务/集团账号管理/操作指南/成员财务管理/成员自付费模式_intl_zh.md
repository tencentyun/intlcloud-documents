成员自付模式包含如下功能：

| 财务权限         | 说明                                   |
| ---------------- | -------------------------------------- |
| 查看成员账户信息 | 管理账号查看成员账号的账户余额信息。   |
| 查看成员账单     | 管理账户查看成员账号的账单消耗信息。   |
| 为成员账号开票   | 管理账号给成员账号开具发票。           |
| 合并出账         | 管理账号将多个成员账号的费用合并下载。 |
| 优惠继承         | 成员账号继承管理账号的合同价优惠。     |



### **查看成员账户余额信息**

介绍管理账号如何查看成员账号的账户余额信息。

#### **操作步骤**

1. 管理账号登录费用中心控制台，选择左侧导航栏中的 [账户信息](https://console.tencentcloud.com/expense)。

2. 通过右上方的下拉列表，选择对应的成员账号，查看成员账号的账户余额信息。

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/2Mf9943_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230324150920.png)



### **查看成员账号的账单**

介绍管理账号如何查看成员账号的账单消费信息。

#### **操作步骤**

1. 管理账号登录费用中心控制台，选择左侧导航栏中的[费用账单](https://console.tencentcloud.com/expense/bill/overview)。

2. 通过右上方的下拉列表，选择对应的成员账号，查看成员账号的账单概览。

3. 通过右上方的下拉列表，选择对应的成员账号，查看成员账号的账单详情。在账单详情页面，也可以通过“账单确认”按钮，为成员账号确认对应月份的账单。

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/DtV2725_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230324150658.png)  

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/AAwx873_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230324150742.png)

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/AAWP795_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230324150814.png)


### **选择成员账号合并账单**

介绍管理账号如何将多个成员账号的账单进行合并。

#### **操作步骤**

1. 管理账号登录费用中心控制台，选择左侧导航栏中的 [账单详情](https://console.tencentcloud.com/expense/bill)。

2. 选择“合并账单”页签，勾选需合并出账的成员账号，单击**下载合并账单**即可。如下图所示： 您也可在 [下载记录](https://console.tencentcloud.com/expense/download) 页面中，单击合并账单所在行右侧的**下载**，下载合并账单。 

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/hu72019_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230324150851.png)


### **为成员账号开票**

介绍管理账号如何为成员账号开具发票。

#### **操作步骤**

1. 管理账号登录费用中心控制台，选择左侧导航栏中的[发票](https://console.tencentcloud.com/expense/invoicing)。

2. 通过右上方的下拉列表，选择对应的成员账号，为对应的成员账号开票。开具的发票归属于成员账号。

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/FkNv495_image%20%281%29.png)


### **优惠继承**

介绍成员账号如何继承管理账号的合同价优惠。

#### **优惠继承范围**

可继承商务给客户申请的合同价优惠，但不包含官网折扣和运营活动折扣。

合同价优惠的类型包含**计费级优惠**、**财务级优惠**及**满返**。不同场景下可继承关系如下表所示：

| 合同价优惠的类型             | 计费级优惠                                            | 账务级优惠                                                   | 满返                                                         |
| ---------------------------- | ----------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 优惠形式                     | 基于单个预付费订单/单条后付费推量的优惠模式，实时生效 | 基于单个账号 ID 或多个账号 ID 合并整月消耗规模来设置的优惠，次月1日执行 | 参考本月已出账单金额，按比例返送代金券/赠送金的优惠模式， 次月3日执行 |
| 折扣                         | ✔                                                     | ×                                                            | ×                                                            |
| 合同价（线性、阶梯、一口价） | ✔                                                     | ×                                                            | ×                                                            |
| 保底（按月固定、按月浮动）   | ×                                                     | ×                                                            | ×                                                            |

<dx-alert infotype="explain" title="">
✔ 代表可继承，× 代表不可继承。
</dx-alert>

<dx-alert infotype="notice" title="">
1、请务必确保管理员账号已申请的优惠包含了所有成员账号要享受的优惠。优惠继承后，成员账号将完全采用管理员账号的优惠，成员账号单独申请的优惠将不再生效。
2、优惠继承的产品范围不包含全量黑名单、指定产品黑名单。
3、成员账号UIN使用产品的计量方式（如日结/月结）需与主UIN一致才能继承，例如直播、点播、文本短信产品等，可通过CPQ报价器调整成员账号UIN的计量模式。
4、满返和账务级优惠不支持继承。
</dx-alert>

您可以通过集团账号管理为**同主体的账号**设置优惠继承，**不同主体的账号**可以联系商务进行申请。无论哪一种方式，在优惠继承建立后您都可以看到成员账号的优惠继承情况。

集团资金划拨模式（自付费）下，管理员删除集团组织、移除组织成员和成员主动退出集团组织时，已有的优惠继承不会自动取消，如需取消请联系您的商务经理进行处理。


#### **操作步骤**

设置优惠继承

1. 您可在添加成员时，设置成员账号优惠继承，步骤如下：

2. 登录集团账号管理控制台，选择左侧导航栏中的 [成员账号管理](https://console.tencentcloud.com/organization/member)。

3. 在“成员账号管理”页面中，单击添加成员。

4. 在“添加成员”页面中，根据添加成员方式，设置优惠继承：

新建成员：新建成员时，成员账号默认和管理员账号使用同一个企业实名认证名称，在“付费模式”中勾选“自付费”后，可以再次勾选“优惠继承”，创建成员即可。如下图所示：

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/KwxJ366_image%20%282%29.png)

邀请成员：

若成员账号和管理员账号使用同一个企业认证主体，在“付费模式”中勾选“自付费”后，可以再次勾选“优惠继承”，邀请成员即可。如下图所示：

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/Y9aR987_image%20%283%29.png)

若成员账号和管理者帐号企业认证主体不同时，在“付费模式”中勾选“自付费”后，如需设置“优惠继承”，请联系商务经理进行处理。


#### **取消优惠继承**

如需取消成员账号的优惠继承，请联系您的商务经理进行处理。