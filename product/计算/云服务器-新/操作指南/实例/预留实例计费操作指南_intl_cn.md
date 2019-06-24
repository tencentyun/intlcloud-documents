### 预留实例计费操作指南

目前预留实例计费仅提供api创建和使用

1. 查看您可以购买的预留实例计费，详情请参考API[列出可购买的预留实例计费](http://10.198.144.46/document/product/213/32751?!document=1&!preview)

2. 购买预留实例计费，详情请参考API[购买预留实例计费](http://10.198.144.46/document/product/213/32750?!document=1&!preview)

3. 查看您已经购买的预留实例计费，详情请参考API[列出已购买的预留实例计费](http://10.198.144.46/document/product/213/32752?!document=1&!preview)

4. 购买与预留实例计费属性完全匹配的按量计费实例，详情请参考API[创建实例](https://cloud.tencent.com/document/product/213/15730)或登录控制台操作

   > 注意，预留实例计费会与属性完全一致的按量计费实例进行匹配，包括您在预留实例计费生效之前购买的按量计费以及预留实例计费生效之后新建的按量计费实例

#### 操作步骤

示例：购买两台硅谷一区，S3.16XLARGE256，Linux预留实例计费

> 示例中展示的可用区，机型，操作系统等信息均为示例情况。您真实可购买的相关信息请使用API[列出可购买的预留实例计费](http://10.198.144.46/document/product/213/32751?!document=1&!preview)进行查询

#### 查看可购买预留实例计费DescribeReservedInstancesOfferings

> 如果已知预留实例计费配置ID请直接使用购买预留实例API进行购买

获取预留实例计费配置ID (ReservedInstancesOfferingId )

输入参数：

![1558619178147](C:\Users\aironpu\AppData\Local\Temp\1558619178147.png)

输出参数：![1558619236202](C:\Users\aironpu\AppData\Local\Temp\1558619236202.png)

#### 购买预留实例计费PurchaseReservedInstancesOffering

预留实例计费配置ID=149d1ebe-7c8c-XXXX-XXXX-XXXXXXXXXX，InstanceCount=2等作为购买预留实例计费API的输入参数

输入参数：

![1558618849117](C:\Users\aironpu\AppData\Local\Temp\1558618849117.png)

输出参数：

![1558618923611](C:\Users\aironpu\AppData\Local\Temp\1558618923611.png)

#### 查看已购买预留实例计费DescribeReservedInstances

输入可以定位您想要查看的预留实例计费的相关条件，例如硅谷地域，S3.16XLARGE256，Linux等信息可获得与上述条件相匹配的已购买的预留实例计费信息

输入参数：

![1558619333325](C:\Users\aironpu\AppData\Local\Temp\1558619333325.png)

输出参数：

![1558619386279](C:\Users\aironpu\AppData\Local\Temp\1558619386279.png)

#### 购买属性一致按量计费实例RunInstances

购买一台与预留实例计费属性相匹配的按量计费实例，即购买一台硅谷一区，S3.16XLARGE256，Linux按量计费实例。

输入参数：

![1558619924832](C:\Users\aironpu\AppData\Local\Temp\1558619924832.png)

输出参数：

![1558619966687](C:\Users\aironpu\AppData\Local\Temp\1558619966687.png)