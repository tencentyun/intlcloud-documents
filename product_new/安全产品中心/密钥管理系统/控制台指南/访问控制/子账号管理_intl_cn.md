

## 概述
本文为您详细介绍如何创建子账号，并授权子账号管理 KMS 的权限。





## 操作步骤
#### 步骤1：创建子账号: 
1. 主账号登录腾讯云 [访问管理 CAM](https://console.cloud.tencent.com/cam) 控制台。
2. 在【用户列表】页面下，单击【新建用户】，即可创建子账号。

#### 步骤2：创建 API 密钥: 
1. 单击子账号名称，进入子账号详情页。
2. 选择【API 密钥】>【新建密钥】，即可创建 SecretId 和 SecretKey，通过该 API 密钥用来访问 KMS。
![](https://main.qcloudimg.com/raw/b86373cfc243c4a60c337ec767cbcb73.png)

#### 步骤3：授权子账号
对于新创建的子账号，通过授权 KMS 策略，即可允许该子账号访问 KMS。
1. 选择【权限】>【关联策略】>【从策略列表中选取策略关联】，选择合适的 KMS 策略。
<img src="https://main.qcloudimg.com/raw/b95ea21c77d4f45752e73443a8fc2739.png" width="80%">
2. 单击【下一步】>【确定】，即可授权子账号 KMS 权限。
