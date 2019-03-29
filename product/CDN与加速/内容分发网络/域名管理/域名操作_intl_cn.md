> 您可以在 CDN 控制台上，对接入 CDN 的加速域名进行加速服务启动、关闭、删除、修改所属项目等操作：
>
> 启动状态：正常提供加速服务
>
> 关闭状态：域名关闭后，若用户请求到达 CDN 节点，则会直接返回 404，无法正常服务。关闭状态的域名自定义配置在下一次开启时会继续保留
>
> 删除状态：从域名列表删除，仅关闭状态的域名可删除
>
> 项目：域名所属项目为涉及到 CDN 的子用户权限划分，请谨慎操作

## 启动加速
对处于 **已关闭** 状态的域名，您可以对其进行 **启动** 操作。启动加速服务大约需要5分钟，具体操作如下。
登录 [CDN控制台](https://console.cloud.tencent.com/cdn)，单击【域名管理】进入相应页面。启动加速服务有 2 种方式：
### 单域名启动

右键单击要启动加速服务的域名，选择【启动 CDN】：
![](https://main.qcloudimg.com/raw/6d40d5b457f67a93672bf740cb932332.png)

### 批量启动

勾选需要启动的域名，然后单击域名上方【启动 CDN】按钮：
![](https://main.qcloudimg.com/raw/df42098d7d31b608d09aaaa3a55fd25a.png)

## 关闭加速
对处于 **已启动** 状态的域名，您可以对其进行 **关闭** 操作。关闭后的域名配置会保留（下次开启时无需再次配置），但不会继续为您提供加速服务。关闭过程大约需要5分钟，具体操作如下。
登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，单击【域名管理】进入相应页面。关闭域名加速有 2 种方式：

### 单域名关闭

右键单击要关闭加速服务的域名，选择【关闭 CDN】。
![](https://main.qcloudimg.com/raw/472f15afc0483dcfa698c3a9cdde3066.png)

### 批量关闭

勾选需要关闭的域名，然后在【更多操作】下拉框中，选择【关闭 CDN】。
![](https://main.qcloudimg.com/raw/5e397998811cc1e7bfb22d21663b2ce2.png)

## 删除加速域名
对处于 **已关闭** 状态的域名，您可以对其进行 **删除** 操作，删除域名后，其配置将不会保留,具体操作如下。
登录 [CDN控制台](https://console.cloud.tencent.com/cdn)，单击【域名管理】进入相应页面。删除加速域名有 2 种方式：

### 单域名删除

右键单击要删除的域名，选择【删除】。
![](https://main.qcloudimg.com/raw/ce1e3fed32cf1d473c188bfd8e1e2d2d.png)

### 批量删除

勾选需要删除的域名，然后在【更多操作】下拉框中，选择【删除】。
![](https://main.qcloudimg.com/raw/3abcd4a868b4803690b6c4cb01e11c0c.png)

## 修改所属项目
登录 [CDN控制台](https://console.cloud.tencent.com/cdn)，单击【域名管理】进入相应页面。修改域名所属项目有 2 种方式：

### 单域名修改

右键单击要修改所属项目的域名，选择【修改所属项目】。
![](https://main.qcloudimg.com/raw/0b2c043c567f4f197b59b8f24ee73ad9.png)

### 批量修改

您也可以勾选多个需要调整项目的域名，然后在【更多操作】下拉框中，选择【修改所属项目】。![](https://main.qcloudimg.com/raw/32bd65f5cbd435bd4687ac09b3b1297d.png)

将所属项目修改为目标项目即可。
![](https://main.qcloudimg.com/raw/d0019607b105f2e1abc5c310d5def177.png)

## 复制域名

您可以单击【复制并创建】，复制一个已有域名的配置，并基于此添加一个新的加速域名。
![](https://main.qcloudimg.com/raw/cd446a17868a1bebb8800a3546a385ca.png)

添加新的加速域名，配置所属项目，回源host，及共享 CNAME 设置。新创建的域名的其他配置会与被复制的域名相同。若共享 CNAME 开启，新添加的域名会与被复制的域名共享相同的 CNAME。
![](https://main.qcloudimg.com/raw/a4bde16b3a02384de51b448edd532d11.png)