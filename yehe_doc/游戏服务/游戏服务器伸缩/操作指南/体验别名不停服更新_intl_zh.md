## 操作场景
本文档指导您如何在别名的应用进行不停服更新操作。




## 准备工作 
- 已集成 [ServerSDK 的代码包](https://intl.cloud.tencent.com/document/product/1055/36674)，您也可以 [使用示范包](https://intl.cloud.tencent.com/document/product/1055/36678)。
- 完成创建服务器舰队1。
- 完成创建服务器舰队2。
![](https://main.qcloudimg.com/raw/b174c992b0988f64e432f4066987ed5e.png)

## 操作步骤
### 创建别名 
1. 登录 [游戏服务器引擎控制台](https://console.cloud.tencent.com/gse/asset)，单击左侧菜单【别名】。
2. 选择左上侧服务区域，单击【新建】。
3. 进入新建别名页面，填写名字、别名类型、描述等信息，单击【确定】。
 - 名称：请输入别名名称。
 - 类型：请选择别名的类型。
    - 常规别名：指向 fleet，系统会自动查找 fleet 下的服务器，并分配给客户端。
    - 终止别名：常规别名表示别名已停止使用，不能使用的原因可以在终止信息中进行描述，将会发送给客户端。
 - 关联服务器舰队：选择“服务器舰队1”。
 - 描述：请输入描述。
4. 信息填写完成后，单击【确定】，即可完成创建别名。
![别名](https://main.qcloudimg.com/raw/e2c7e31268702861f6a53efafee291cb.png)

### 创建游戏服务器会话
除了在代码里集成 SDK 并调用云 API，您还可以通过 [云 API 调试](https://console.cloud.tencent.com/api/explorer?Product=gse) 快捷创建。
![](https://main.qcloudimg.com/raw/676fc6ade84a0e5284f474af2cd92d3d.png)

通过云 API 调试创建成功一个游戏服务器会话，即可看到服务器舰队1产生一个游戏服务器会话。
![](https://main.qcloudimg.com/raw/5e0f14322ec92296e63947dfa88482de.png)

### 修改别名的配置
1. 进入别名列表页面，选择刚新建的别名，单击右上角【编辑】。
2. 进入别名编辑页面，修改别名的配置，将关联服务器舰队修改为“服务器舰队2”。
![](https://main.qcloudimg.com/raw/dd5a258098c49aaa00cb7d7048507bd1.png)

### 再次创建游戏服务器会话
>请使用相同的别名再次创建游戏服务器会话。

通过云 API 调试再次创建一个游戏服务器会话，即可看到服务器舰队1仍仅有一个游戏服务器会话。
![](https://main.qcloudimg.com/raw/ad5d8b727c25930ce6d32437be72cb18.png)

服务器舰队2产生了一个游戏服务器会话，可见新的游戏服务器会话被分配到了服务器舰队2上了。
![](https://main.qcloudimg.com/raw/14a5feb8995eb22c4d1f3c26b6c2fcf3.png)

### 不停服更新说明
当需要版本更新时，新建一个 fleet，并将别名指向新的 fleet。
- 原来的 fleet 随着游戏服务器会话的减少将自动缩容。
- 新的 fleet 会随着游戏服务器会话的增多自动扩缩容。而不需停服。






