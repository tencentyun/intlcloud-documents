## 简介
本文将为您介绍两种授权方式快速解决下述问题，详细操作步骤如下。如果您希望进行更多复杂权限配置策略，请参见 [访问管理 > 自定义策略](https://intl.cloud.tencent.com/document/product/1047/38088)。
- 子账号使用即时通信 IM 服务时，需要主账号授予 [访问控制台](https://console.cloud.tencent.com/im) 以及进行配置操作的权限，否则控制台应用列表将无法显示应用，如下图所示：
![](https://main.qcloudimg.com/raw/0a28018859d63fc6822457021fc1e023.png)
- 子账号有标签访问授权，但当前控制台应用标签和子账号标签权限不符时，子账号无法查看新建应用。


## 方案一、全局授权操作步骤
### 步骤1：进入授权
使用主账号，进入控制台 [**访问管理**](https://console.cloud.tencent.com/cam) >用户列表，单击子用户左侧的**授权**按钮，将弹出“关联策略”选择框。
![](https://main.qcloudimg.com/raw/9a87638c3298b3e50307e82186eb17ea.png) 

### 步骤2：选择策略
在策略筛选框，搜索“即时通信”，勾选需要授权的选项，单击**确定**即完成授权。
![](https://main.qcloudimg.com/raw/9a4b20af40d5800db94c058f6a492175.png)

>?
>- **读写访问权限**：既能访问控制台又可以修改配置。
>- **只读访问权限**：只能访问控制台，不可以做其他操作。
### 步骤3：完成授权
右上角提示“关联策略成功”即完成关联操作。
![](https://main.qcloudimg.com/raw/7c2812137b4afc10dcf3de7072a90761.png)


## 方案二、按标签授权操作步骤
本方案针对需要通过标签授权管理子账号的客户，子账号仅能访问及操作授权标签下的应用。
>!
>- 为子账号分配标签策略后，子账号无法访问及操作标签为空的应用。由于子账号在 [IM 控制台](https://console.cloud.tencent.com/im) 新建应用标签为空，因此需要主账号更改该应用标签为已授权标签，子账号方能使用。
>- 如需将已有应用按标签授权给子账号，请确保将要授权的应用已配置相应标签，否则将无法通过标签进行授权。
>- 如应用未配置标签请前往即时通信 IM 控制台中 [基本配置](https://console.cloud.tencent.com/im-detail) 页面进行配置， 详情请参见 [标签配置](https://intl.cloud.tencent.com/document/product/1047/34540)。 

>- 或进入 [标签列表](https://console.cloud.tencent.com/tag/taglist) 将应用批量绑定到标签下，详情请参照 [绑定资源](https://intl.cloud.tencent.com/document/product/651/41575)。

### 步骤1：进入授权
使用主账号，进入控制台 [**访问管理**](https://console.cloud.tencent.com/cam) >**策略**，单击顶部**新建自定义**，将弹出“选择创建策略方式”弹框。
![](https://main.qcloudimg.com/raw/289a2def35370b7511625b37f3e798b3.png)

### 步骤2：选择标签
选择“按标签授权”，进入“标签策略生成器”。
![](https://main.qcloudimg.com/raw/02098a1da180deae9c810b97cb0c453c.png)

### 步骤3：生成策略
在“标签策略生成器”填入需要授权的子账号、标签等信息，单击**下一步**进入检查页面。
![](https://main.qcloudimg.com/raw/e590a9843e852bf9eca22bfc95ffbc13.png)

>?如标签选择列表为空，则需要主账号先去 [标签控制台](https://console.cloud.tencent.com/tag/taglist) 新建标签。
>![](https://main.qcloudimg.com/raw/e6d0aeb3a04b9281627805f0cde3d052.png)

### 步骤4：完成授权
检查无误，单击**完成**，结束标签授权流程。
![](https://main.qcloudimg.com/raw/3c9e2624f334f9c9820402f579381ae6.png)