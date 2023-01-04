本文档为您介绍容器模块功能，以及如何查看容器、镜像和主机等资产详情。
![](https://qcloudimg.tencent-cloud.cn/raw/fc1c92336f912f2e561e5be0bac01309.png)

## 查看容器模块
容器展示模块中提供容器资产总数，以及正在运行、暂停运行和停止运行容器的数量。
### 筛选容器列表
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**资产管理**，进入资产管理页面。
2. 在资产管理页面，单击“容器总数”，进入到容器列表页面，可查看全部容器资产列表。
![](https://qcloudimg.tencent-cloud.cn/raw/35434bace3aea3077242fbcdc17fc441.png)
3. 在容器列表页面，可按运行状态对容器资产进行筛选，或搜索框通过“容器名称、容器ID、镜像名称、主机IP”等关键字对容器进行查找。
 - 单击左上角的状态下拉框，按运行状态对容器资产进行筛选。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/039b82d88e66b63a8da93a29d37146e1.png" style="zoom:80%;" />
 - 单击搜索框，通过“容器名称、容器ID、镜像名称、主机IP”等关键字对容器进行查找。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/4f353d726656b5cee7d5bf26c4fee351.png" style="zoom:80%;" />

### 查看容器列表
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**资产管理**，进入资产管理页面。
2. 在资产管理页面，单击“容器总数”，进入到容器列表页面，可查看全部容器资产列表。
<img src="https://qcloudimg.tencent-cloud.cn/raw/e4c69b63a584601969c6b0ca273a7083.png" style="zoom:80%;" />
3. 在容器列表页面，单击“容器名称”，右侧弹出抽屉展示该容器详情，页面可切换查看容器基本信息、进程和端口等信息。
![](https://qcloudimg.tencent-cloud.cn/raw/cf8bb0e835c41ff857d9edb203d2892f.png)
![](https://qcloudimg.tencent-cloud.cn/raw/418576b0a585e60754dd34a456020d5c.png)
4. 在资产管理页面，单击“主机 IP”，右侧弹出抽屉展示主机详情，包括主机基本信息、Docker 信息、相关镜像数和相关容器数。
>?在抽屉中，单击“数字”查看主机相关镜像数和相关容器数详情。
><img src="https://qcloudimg.tencent-cloud.cn/raw/519c19224986ac12f7c489345aa9beea.png" style="zoom: 67%;" />

 ![](https://qcloudimg.tencent-cloud.cn/raw/8138493ec02e7e7500ab18fb567cd111.png)

### 自定义列表管理
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**资产管理**，进入资产管理页面。
2. 在资产管理页面，单击“容器总数”，进入到容器列表页面，可查看全部容器资产列表。
<img src="https://qcloudimg.tencent-cloud.cn/raw/2901f75ddc60d38092fdd6173e52c260.png" style="zoom:80%;" />
3. 在容器列表页面，单击![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png)图标，弹出自定义列表管理弹窗，在弹窗中可以自定义设定列表管理。
3. 在自定义列表管理弹窗，选择所需的类型后，单击**确定**，即可完成设置自定义列表管理。
<img src="https://qcloudimg.tencent-cloud.cn/raw/cd74bdaea9642a37ab2add6a9c4a4321.png" style="zoom:80%;" />

#### 列表重点字段说明
1. 运行状态：包括正常运行、暂停运行和停止运行三种状态。
2. 镜像：关联镜像名称。
3. 所属 POD：容器所属 POD。
4. CPU|占用率：CPU 使用率。
5. 内存|占用：内存占用大小。

## 查看本地镜像模块
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**资产管理**，进入资产管理页面。
2. 在资产管理页面，镜像模块展示了模块中镜像资产总数。单击“镜像总数”，可跳转**镜像安全**>**本地镜像**页面查看镜像详情。
>? 更多详细内容，请参见 [本地镜像](https://www.tencentcloud.com/document/product/1163/50891)。

<img src="https://qcloudimg.tencent-cloud.cn/raw/953a6225bb4b7b5d8066f413c4bdf72a.png" style="zoom:80%;" />

## 查看镜像仓库模块
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**资产管理**，进入资产管理页面。
2. 在资产管理页面，镜像仓库模块展示了镜像仓库资产总数。单击“镜像仓库总数”，可跳转**镜像安全**>**镜像仓库**页面查看镜像仓库详情。
>? 更多详细内容，请参见 [镜像仓库](https://www.tencentcloud.com/document/product/1163/50892)。

<img src="https://qcloudimg.tencent-cloud.cn/raw/15c55d5eb0aaf126e5dfbaab952ccd38.png" style="zoom:80%;" />

## 查看主机模块
主机展示模块中提供主机资产总数，以及正在运行和已离线主机的数量。
### 筛选主机列表
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**资产管理**，进入资产管理页面。
2. 在资产管理页面，单击“主机总数”，可查看全部主机资产列表。
<img src="https://qcloudimg.tencent-cloud.cn/raw/163265ba97903e592511c9d568d6bcf9.png" style="zoom:80%;" />
3. 在主机列表页面，可按主机状态对主机资产进行筛选，或搜索框通过“主机名、业务组、docker 版本、主机 IP”等关键字对主机进行查找。
 -  单击左上角的状态下拉框，按主机状态对主机资产进行筛选。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/6ddfbcd4abdde2829585dac2e7d74507.png" style="zoom:67%;" />
 - 单击搜索框，通过“主机名、业务组、Docker 版本	、主机 IP”等关键字对主机进行查找。
 <img src="https://qcloudimg.tencent-cloud.cn/raw/88038c9a34722c3ca47e27fe63490f43.png" style="zoom:67%;" />

### 查看容器列表
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**资产管理**，进入资产管理页面。
2. 在资产管理页面，单击“主机总数”，可查看全部主机资产列表。
<img src="https://qcloudimg.tencent-cloud.cn/raw/dece04e5e03c2ae6b9532228e549e816.png" style="zoom:80%;" />
3. 在主机列表页面，单击“主机 IP”，右侧弹出抽屉展示主机详情，包括主机基本信息、Docker 信息、相关镜像数和相关容器数。
>? 在抽屉中，可单击“数字”查看主机相关镜像数和相关容器数详情。
><img src="https://qcloudimg.tencent-cloud.cn/raw/ae1a64866593098c7be0495c9b50effe.png" style="zoom: 67%;" />

![](https://qcloudimg.tencent-cloud.cn/raw/7a16e7d58dce8b19464e26ae8578b55c.png)
4. 在主机列表页面，单击“镜像数”，可查看关联镜像详情。
![](https://qcloudimg.tencent-cloud.cn/raw/9c0faed8d6da42e60c5fca5980b25c50.png)
5. 在主机列表页面，单击“容器数”，可查看关联容器详情。
![](https://qcloudimg.tencent-cloud.cn/raw/45b2e82d9c3cd4bc23ab6eabd867326d.png)

### 自定义列表管理
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**资产管理**，进入资产管理页面。
2. 在资产管理页面，单击“主机总数”，可查看全部主机资产列表。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0822d61df17196ecdb629b1fce2b246.png" style="zoom:80%;" />
3. 在主机列表页面，单击![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png)图标，弹出自定义列表管理弹窗，在弹窗中可以自定义设定列表管理。
4. 在自定义列表管理弹窗，选择所需的类型后，单击**确定**，即可完成设置自定义列表管理。
<img src="https://qcloudimg.tencent-cloud.cn/raw/abe1abeea2988ac787bbf5660aeb5656.png" style="zoom:67%;" />

#### 列表字段说明
1. 主机名称：主机名称。
2. 主机 IP：单击“主机 IP”，右侧弹出抽屉展示主机详情，包括主机基本信息、Docker 信息、相关镜像数和相关容器数。
3. 业务组：主机所属业务组名称。
4. Docker 版本：展示 Docker 版本号，如未安装，则显示“未安装”。
5. Docker 文件系统类型：Docker 文件系统类型。
6. 镜像数：主机关联镜像数。单击“数字”可查看关联镜像详情。
7. 容器数：主机关联容器数。单击“数字”可查看关联容器详情。
