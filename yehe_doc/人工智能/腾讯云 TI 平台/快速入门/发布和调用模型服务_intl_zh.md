## 发布和调用模型服务  

### 案例1：将平台训练出的模型部署为在线服务   
本案例基于用户在任务式建模模块，使用 mnist 数据集与 PyTorch 框架训练出的手写数字识别模型为例，讲解如何将平台训练出的模型部署为在线服务，并进行调用验证。

#### 准备内容   
1、模型文件  
登录 TI-ONE 控制台，在左侧导航栏中选择 **训练工坊>任务式建模** ，确认手写数字识别模型已完成训练。     
![](https://qcloudimg.tencent-cloud.cn/raw/93f53ab727012c8dc8d6629b8fdd7b35.png)     

2、推理脚本与配置文件  
已为您准备了手写数字识别模型的推理脚本与配置文件，下载地址为 [mnist-pytorch-infer](https://tencent-cloud-product-release-1258877907.cos.ap-guangzhou.myqcloud.com/TI-ONE-release/TIONE%E5%85%AC%E6%9C%89%E4%BA%91%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8-%E5%8B%BF%E5%88%A0/mnist-pytorch-infer.zip)。

3、测试数据    
已为您准备了如下测试数据，可以在服务发布后直接用于调用测试。  
（1）图片2 https://qcloudimg.tencent-cloud.cn/raw/81ebbd130357ec4b1bbbecf73d1330f5.jpeg  
（2）图片5 https://qcloudimg.tencent-cloud.cn/raw/43b8f14ba3515c34b5c572f0c6bc225e.jpeg  
（3）图片9 https://qcloudimg.tencent-cloud.cn/raw/3768c5d8a47b5da666c82a286e00759b.jpeg    


#### 步骤1：导入模型仓库   
（1）进入 TI-ONE 控制台，在左侧导航栏中选择 **模型管理>模型仓库** ，进入模型列表页面。  
（2）点击 **导入模型** ，在模型导入页面参考如下参数填写。  
- 导入方式：选择 **导入新模型**
- 模型名称：自定义模型名称，例如命名为 mnist_train
- 标签：按需添加，可不配置
- 模型来源：选择 **从任务导入**
- 选择任务：选择任务 **mnist_train**
- 模型指标：按需填写，例如 accuracy
- 运行环境来源：建议使用内置的GPU运行环境，例如 py1.9.0-py36-cu111
- 模型移动方式：按需选择，例如 **复制**  

![](https://qcloudimg.tencent-cloud.cn/raw/0a26e3aec884e159a7a62f7835ea9f8d.png)  

（3）点 击**确定** ，完成模型文件的导入。  
（4）上传推理脚本与配置文件   
找到已上传的模型版本，点击 **上传文件** 操作，在弹出的 COS 对话框中，点击左下方【上传文件】，将 mnist-pytorch-infer 包解压后的3个文件依次上传，完成后点击**确定**。  

![](https://qcloudimg.tencent-cloud.cn/raw/61de66cc52fd883dcad302ec39263e18.png)   

![](https://qcloudimg.tencent-cloud.cn/raw/211cf4a3b3a9d2ba27d245717b48351d.png)    

#### 步骤2：启动在线服务   
（1）进入 TI-ONE 控制台，在左侧导航栏中选择 **模型服务>在线服务** ，进入服务列表页面。  
（2）点击 **新建服务** ，在启动服务页面参考如下参数，填写服务基础信息
- 服务名称：自定义服务名称，例如命名为 mnist-pytorch-infer  
- 服务描述：按需填写服务描述信息，可不配置  
- 计费模式：若您尚未使用过资源组管理模块，建议选择 **后付费** 模式    

![](https://qcloudimg.tencent-cloud.cn/raw/465371d082eb694f9f675ef742d8426b.png)  

（3）实例容器信息，可参考如下参数填写
- 是否使用模型文件：选择 **使用模型文件**
- 选择模型：选择上一步骤中导入的模型文件 mnist_train
- 选择版本：选择 v1
- 算力规格：按需选择，例如 32C128G T4*1  

![](https://qcloudimg.tencent-cloud.cn/raw/c2cf50b3b1dee181620468d5c1518577.png)  

（4）参考如下信息完成服务高级配置  
- CLS 日志投递：按需开启，可使用默认值关闭
- 实例调节：按需选择，可使用默认值 **手动调节**
- 实例数量：按需配置，可使用默认值1
- 是否生成鉴权：按需开启，可使用默认值关闭
- 标签：按需添加，可不配置 

![](https://qcloudimg.tencent-cloud.cn/raw/ee67206a559e63402e59b9fb2253b84a.png)  

（5）点击启动服务，若选择后付费模式，会出现费用冻结确认。  
后付费模式需要预先冻结两小时费用，若您账户内余额充足，点击 **确定** 即可完成服务创建。  
此时在服务列表中，新创建的服务会处于 **创建中** 状态，服务部署过程中将为您创建网关并调度计算资源，需要等待一段时间，待服务成功完成部署时，服务状态将变为**运行中**。  

#### 步骤3：服务调用测试   
（1）确认上一步中发布的服务已完成部署，处于 **运行中** 的状态。  
（2）点击 **调用** 操作，进入服务调用页面。    
![](https://qcloudimg.tencent-cloud.cn/raw/221696fec909f39faa838419711d31fa.png)  
（3）查看接口信息，点击接口列表的 **在线测试** 操作，打开服务调用测试页面。  
![](https://qcloudimg.tencent-cloud.cn/raw/afb5d85daea00853e069fceba489eeed.png)  
（4）在请求体模块录入JSON格式的请求信息，并点击 **发送请求** 后，可在请求响应模块查看预测结果。  

- 示例1：在请求体中录入图片2的路径`{"images":["https://qcloudimg.tencent-cloud.cn/raw/81ebbd130357ec4b1bbbecf73d1330f5.jpeg"]}`，此时的预测结果为2。  

![](https://qcloudimg.tencent-cloud.cn/raw/c788b2ca978755aeebb0b5c33a2677f0.png)  
- 示例2：在请求体中录入图片5的路径`{"images":["https://qcloudimg.tencent-cloud.cn/raw/43b8f14ba3515c34b5c572f0c6bc225e.jpeg"]}`，此时的预测结果为5。  

![](https://qcloudimg.tencent-cloud.cn/raw/c0d39239ede2f4d5261bfa88e275c188.png)   
- 示例3：在请求体中录入图片9的路径`{"images":["https://qcloudimg.tencent-cloud.cn/raw/3768c5d8a47b5da666c82a286e00759b.jpeg"]}`，此时的预测结果为9。  
  

![](https://qcloudimg.tencent-cloud.cn/raw/1ab553bab36c9d51f105734048d9cfd4.png)    

  

### 案例2：将第三方模型导入平台，并部署为在线服务   
本案例以平台预置模型包中 PyTorch 图像分类模型为例，讲解如何将第三方模型部署为在线服务，部署完成后，用户可通过在线测试功能调用服务，识别输入图片的图像种类。   

#### 准备内容   
1、模型包  
（1）登录 TI-ONE 控制台，在左侧导航栏中选择**模型管理>模型仓库**，进入模型列表页面；  
（2）点击页面右上角的**下载推理代码模板**，获取平台提供的预置模型包；  
（3）将模型包解压后，找到其中的**pytorch>classify文件夹**用于后续步骤使用。
![](https://qcloudimg.tencent-cloud.cn/raw/384d8e3036530d8727c7d533a4eca5ea.png)  

2、测试数据  
已为您准备了如下测试数据，可以在服务发布后直接用于调用测试。  
（1）猫图片
https://qcloudimg.tencent-cloud.cn/raw/bcbdae25439713ecb4dbb154d43a9ef8.jpeg   
（2）蝴蝶图片
https://qcloudimg.tencent-cloud.cn/raw/40a99b15e76d6957644f160b9149522a.jpeg  
（3）狗图片
https://qcloudimg.tencent-cloud.cn/raw/aab789b6e047fa804bbf803de16f49a0.jpeg   

#### 步骤1：导入模型仓库   
（1）进入 TI-ONE 控制台，在左侧导航栏中选择 **模型管理>模型仓库** ，进入模型列表页面。  
（2）点击 **导入模型** ，在模型导入页面参考如下参数填写。  
- 导入方式：选择 **导入新模型**
- 模型名称：自定义模型名称，例如命名为 classify
- 标签：按需添加，可不配置
- 模型来源：选择 **从COS导入**
- 算法框架：选择 **PyTorch**
- 模型指标：按需填写，例如 accuracy
- 运行环境来源：建议使用内置的 GPU 运行环境，例如 py1.9.0-py36-cu111
- 模型文件：点击【选择文件】，在弹出的 COS 对话框中，选择需要使用的存储桶，点击左下方【上传文件夹】，将模型包中的 **pytorch>classify文件夹** 上传，上传完成后选中文件夹路径  

![](https://qcloudimg.tencent-cloud.cn/raw/6a81ba8eb6057d7df8552f4b6d6b8604.png)    

![](https://qcloudimg.tencent-cloud.cn/raw/9b7ee973750b5540504490382c1be7b8.png) 

（3）点击 **确定** ，完成模型文件的导入。  

#### 步骤2：启动在线服务   
（1）进入 TI-ONE 控制台，在左侧导航栏中选择 **模型服务>在线服务** ，进入服务列表页面。  
（2）点击 **新建服务** ，在启动服务页面参考如下参数，填写服务基础信息
- 服务名称：自定义服务名称，例如命名为 classify  
- 服务描述：按需填写服务描述信息，可不配置  
- 计费模式：若您尚未使用过资源组管理模块，建议选择 **后付费** 模式    

![](https://qcloudimg.tencent-cloud.cn/raw/b7ae7f48eccee13f5a8e9c96609a20af.png)  

（3）实例容器信息，可参考如下参数填写
- 是否使用模型文件：选择 **使用模型文件**
- 选择模型：选择上一步骤中导入的模型文件 classify
- 选择版本：选择 v1
- 算力规格：按需选择，例如 32C128G T4*1   

![](https://qcloudimg.tencent-cloud.cn/raw/1c880b1b5320caca26fbf24f1b44c657.png)  

（4）参考如下信息完成服务高级配置  
- CLS 日志投递：按需开启，可使用默认值关闭
- 实例调节：按需选择，可使用默认值 **手动调节**
- 实例数量：按需配置，可使用默认值1
- 是否生成鉴权：按需开启，可使用默认值关闭
- 标签：按需添加，可不配置

![](https://qcloudimg.tencent-cloud.cn/raw/39754b396bd146d3ceb1e6e2a9be3af8.png)  

（5）点击启动服务，若选择后付费模式，会出现费用冻结确认。  
后付费模式需要预先冻结两小时费用，若您账户内余额充足，点击**确定**即可完成服务创建。  
此时在服务列表中，新创建的服务会处于**创建中**状态，服务部署过程中将为您创建网关并调度计算资源，需要等待一段时间，待服务成功完成部署时，服务状态将变为**运行中**。  

#### 步骤3：服务调用测试   
（1）确认上一步中发布的服务已完成部署，处于 **运行中** 的状态。  
（2）点击 **调用** 操作，进入服务调用页面。    
![](https://qcloudimg.tencent-cloud.cn/raw/f5ae2e1abf0a03706fc9e51b6ae04d94.png)     
（3）查看接口信息，点击接口列表的 **在线测试** 操作，打开服务调用测试页面。  
![](https://qcloudimg.tencent-cloud.cn/raw/324356d1c8fa9cd9907ae47021fabecf.png)   
（4）在请求体模块录入 JSON 格式的请求信息，并点击 **发送请求** 后，可在请求响应模块查看预测结果。
- 示例1：在请求体中录入猫图片路径`{"image": "https://qcloudimg.tencent-cloud.cn/raw/bcbdae25439713ecb4dbb154d43a9ef8.jpeg"}`，此时在返回结果中，图像归类为猫的置信度最高。  

![](https://qcloudimg.tencent-cloud.cn/raw/7c45893e92568a1363294aa9929e900a.png)   
- 示例2：在请求体中录入蝴蝶图片路径`{"image": "https://qcloudimg.tencent-cloud.cn/raw/40a99b15e76d6957644f160b9149522a.jpeg"}`，此时在返回结果中，图像归类为蝴蝶的置信度最高。  

![](https://qcloudimg.tencent-cloud.cn/raw/bd27ed7d6115a6ee6f644cc30f7e1ed0.png)    
- 示例3：在请求体中录入狗图片路径`{"image": "https://qcloudimg.tencent-cloud.cn/raw/aab789b6e047fa804bbf803de16f49a0.jpeg"}`，此时在返回结果中，图像归类为狗的置信度最高。  

![](https://qcloudimg.tencent-cloud.cn/raw/b3fca3e59878a059b81e68a20fb98aa0.png)   
