### 操作场景

* 标签是用于从不同的维度对资源分类的管理、权限的管理
* 在 [**凭据管理系统**](https://console.cloud.tencent.com/ssm)  中，标签主要用于 **用户凭据**
* 在凭据中添加标签，是为了方便用户对凭据进行分类和跟踪管理，同时可以按照标签来汇总对应凭据的使用情况



### 使用限制

标签内容（标签键、标签值）的使用有相对应的限制条件，详情请查阅  [**标签使用限制**](https://intl.cloud.tencent.com/document/product/651/13354)

### 操作方法

#### 在密钥管理控制台设置标签

1. 已登录 [**凭据管理系统**](https://console.cloud.tencent.com/ssm) 控制台
2. 选择需要编辑凭据的所在区域
3. 找到需编辑标签的凭据，选择其右侧的 **编辑标签** 

![](https://main.qcloudimg.com/raw/adb1764eb082e54e282b0148cad120ff.png)

4. 在弹出的 “您已经选择1个资源” 窗口中设置，设置标签，如下图所示：

   例如，添加两组标签

   ![](https://main.qcloudimg.com/raw/64831a56619eb1a9fbc80ba2f040f826.png)

   5. 点击 **确定**，系统出现修改成功提示   

      

#### 通过标签筛选密钥

1. 已登录 [**凭据管理系统**](https://console.cloud.tencent.com/ssm) 控制台

2. 选择需要编辑凭据的所在区域

3. 在选择的区域凭据列表中，在右侧的搜索框选择以 **“标签”** 作为筛选条件，输入筛选内容即可，如下图所示

   例如：你希望筛选出ower为alex的密钥，可输入标签：owner:alex![](https://main.qcloudimg.com/raw/d2d91d47fad9dd2465094aece1aa4a2b.png)