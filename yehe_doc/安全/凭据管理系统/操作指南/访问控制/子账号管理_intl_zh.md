## 概述
本文详细介绍如何创建子账号，并授予子账号管理凭据管理系统的权限。
## 操作步骤
1. 创建子账号。用主账号登录腾讯云 [访问管理 CAM 控制台](https://console.cloud.tencent.com/cam/overview)，在左侧导航中，选择【用户】>【用户列表】，在【用户列表】页面下，单击【新建用户】，即可创建子账号。
![](https://main.qcloudimg.com/raw/6c2f5ac34a9cdf2ef3b7a3142d6d0b10.png)
2. 创建 API 密钥。单击子账号名称，进入子账号详情页，选择【API 密钥】>【新建密钥】，即可创建 SecretId 和 SecretKey，您通过该 API 密钥访问凭据管理系统。
>?如果您不需要通过 API 管理凭据管理系统，可直接操作授权子账号。

![](https://main.qcloudimg.com/raw/eea20b23c0b97942f4aefce64904f640.png)1
3. 授权子账号。对于新创建的子账号，通过授权凭据管理系统策略，即可允许该子账号访问凭据管理系统。在子账号详情页，选择【权限】>【关联策略】，进入添加策略页面。
![](https://main.qcloudimg.com/raw/5b06780aa1a27c8ac39069d259621196.png)
4. 添加策略。在添加策略页面，单击【从策略列表中选取策略关联】，选择合适的凭据管理系统策略，选择【下一步】>【确定】，即可授权子账号访问凭据管理系统权限。
![](https://main.qcloudimg.com/raw/3d6efb2e195a679c9e7146798624a182.png)
