## 添加规则
1. 登录 [云防火墙控制台](https://console.cloud.tencent.com/cfw/ac/secgroupnew)，在左侧导航中，选择**访问控制** > **企业安全组**。
2. 在企业安全组页面，单击**添加规则**，弹出添加规则窗口。
3. 在添加规则窗口中，配置相关参数，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/7885d50903093d454006bb15093daca2.png)
**参数说明**
 - 执行顺序：企业安全组规则的执行顺序，执行顺序较高的规则被优先匹配，命中后则不再匹配后序规则。当您修改某条规则的执行顺序时，原本该位置的规则的执行顺序+1，依次类推。当您删除某条规则时，后序所有规则的执行顺序-1。
 - 访问源：支持IP/CIDR、参数模板、资产实例、资产分组、资源标签、地域等类型。
 - 访问目的：跟访问源一样也支持 IP/CIDR、参数模板、资产实例、资产分组、资源标签、地域等类型。
>?当访问源选择其中的一种类型，访问目的也可以选择一种类型。但是，当访问源或访问目的选择的是地域时，访问目的或访问源不能选择地域，其他类型没有这个限制。

 - 目的端口：支持单端口号、基于'/'的端口段以及英文逗号分隔的离散端口值、最多填写15个离散端口，例如“80”、“80/80”、“-1/-1”、“1/65535”。
 - 协议：当前版本支持UDP、TCP 和 ICMP 协议。
 - 策略：
    - 放行：放通命中规则的流量，不记录企业安全组命中日志。
    - 阻断：拦截命中规则的流量，记录企业安全组命中日志
 - 描述：用于描述规则，最多支持50个字符，支持通过##的方式插入规则的特殊设置，当前版本支持的设定有#仅下发访问源#，#仅下发访问目的#。
>? 当访问目的地址填写为实例、子网、私有网络地址时，可通过自动双向下发，分配一条相同的入站规则。如果不想实现双向下发的效果，可通过在描述添加关键字： #仅下发访问源#（仅对访问源下发安全组规则），#仅下发访问目的#（仅对访问目的下发安全组规则）。

4. 规则添加完成后，将展示在规则列表里面。
 ![](https://qcloudimg.tencent-cloud.cn/raw/dcf3266787e1fe2511594d066a2d2eb7.png)
5. 规则添加完并下发成功之后，在云防火墙的安全组可视化页面或者是进入私有网络控制台的 [安全组页面](https://console.cloud.tencent.com/vpc/securitygroup?rid=1&rid=1) 可以查看到相应的安全组，并且自动关联了实例。

## 查看安全组可视化
1. 登录 [云防火墙控制台](https://console.cloud.tencent.com/cfw/ac/secgroupnew)，在左侧导航中，选择**访问控制** > **企业安全组**。
2. 在企业安全组页面，单击**安全组可视化**，进入安全组可视化页面。
![](https://qcloudimg.tencent-cloud.cn/raw/7bd36e721d5b6127853f63a6a5b0167f.png)
3. 在安全组可视化页面，可查看实例所在的地域和各种配额信息，安全组配额可以根据实际情况去扩容。
![](https://qcloudimg.tencent-cloud.cn/raw/ebcc2c8d01525a436e24b256ff0e9e14.png)
4. 在安全组可视化页面下方，可查看关联实例、安全组列表、安全组规则。
 - 关联实例：展示当前某个地域所有的实例，包括实例名称、实例类型、所属网络、IP 地址等信息。单击安全组或安全组规则列的“数字”，可以跳转到单个实例所对应的安全组列表或安全组规则详情页面。单击**查看详情**可以跳转到实例的详情页面。
![](https://qcloudimg.tencent-cloud.cn/raw/97bdaaa2f3f3eb9983baa1a92e7aa494.png)
 - 安全组列表：展示了当前地域的所有安全组列表、每个安全组关联的实例、安全组规则条目数、创建时间等。单击关联实例或安全组规则列的“数字”，可以跳转到单个实例所对应的安全组列表或安全组规则详情页面。单击**查看详情**，可跳转到私有网络控制台安全组详情页面。
 ![](https://qcloudimg.tencent-cloud.cn/raw/f8155a2a69773014b75c93a896eae3a8.png)
 - 安全组规则：展示当前地域所有安全组的入站规则和出站规则，单击![](https://qcloudimg.tencent-cloud.cn/raw/41eb4aef52d06599b05022e5dfabd945.png)可查看规则详情，也可验证企业安全组是否下发成功。
 ![](https://qcloudimg.tencent-cloud.cn/raw/44ee82266f0f84473e6017c5ea742d11.png)
5. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/securitygroup)，在左侧导航中，选择**安全** > **安全组**，并选择所需地域和项目。
![](https://qcloudimg.tencent-cloud.cn/raw/1e0ba16be9d24517273cb81710f0b0ee.png)
6. 单击任意一条安全组“ID/名称”，即可查看该安全组所对应的入站规则、出站规则以及关联的实例。
![](https://qcloudimg.tencent-cloud.cn/raw/e89f2358136eaa3ebdade9e59dd180aa.png)

## 管理规则
企业安全组规则完成设置后，在企业安全组页面可以对规则条目执行编辑、插入、删除操作、快速排序等操作。
#### 编辑规则
在 [企业安全组页面](https://console.cloud.tencent.com/cfw/ac/secgroupnew)，选择所需规则，单击**编辑**，修改相关参数后，单击**确定**即可。
![](https://qcloudimg.tencent-cloud.cn/raw/e17eb728c752eb7075d99bff9d7465ad.png)

#### 停用规则
在 [企业安全组页面](https://console.cloud.tencent.com/cfw/ac/secgroupnew)，可以控制规则是否生效。若关闭开关，即停用规则，此规则不再参与规则匹配。
![](https://qcloudimg.tencent-cloud.cn/raw/a15d37e54e5f91816f4dd221fcff43a4.png)

#### 插入规则
在 [企业安全组页面](https://console.cloud.tencent.com/cfw/ac/secgroupnew)，选择所需规则，单击**插入**，输入相关参数后，单击**完成**，可在当前规则的前方新增一条规则，优先级高于当前规则。
![](https://qcloudimg.tencent-cloud.cn/raw/f08aabccb11838d2e07176484882da44.png)

#### 删除规则
在 [企业安全组页面](https://console.cloud.tencent.com/cfw/ac/secgroupnew)，选择所需规则，单击**删除**，二次确认后，可以删除目标规则。
![](https://qcloudimg.tencent-cloud.cn/raw/779c691335105427fa6d07bc3cd48007.png)

#### 快速排序
规则在列表中的顺序，决定了执行的优先级。
1. 在 [企业安全组页面](https://console.cloud.tencent.com/cfw/ac/secgroupnew)，单击**快速排序**，选择所需规则，点击鼠标左键拖拽至合适的位置。
![](https://qcloudimg.tencent-cloud.cn/raw/b69063f6c2e5fb77bfa351125d58be6c.png)
2. 调整完成后，单击**保存**，调整后的优先级即可生效，企业安全组会自动将新的规则优先级下发到实例。

#### 导出规则
1. 在 [企业安全组页面](https://console.cloud.tencent.com/cfw/ac/secgroupnew)，单击规则列表右上方的![](https://qcloudimg.tencent-cloud.cn/raw/8006bef9330b3f1da99531210014319c.png)，弹出自定义列表导出窗口。
![](https://qcloudimg.tencent-cloud.cn/raw/9ae905aae0ebbd420ca70d79273d4daa.png)
2. 在自定义列表导出窗口中，选择忽略检索条件全量导出或基于检索条件导出，单击**导出**，即可导出规则。
![](https://qcloudimg.tencent-cloud.cn/raw/7339532c069aab4bf88232242878f774.png)
