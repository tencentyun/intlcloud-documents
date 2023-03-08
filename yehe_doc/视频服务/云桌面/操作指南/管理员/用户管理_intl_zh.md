## 功能概述
用于构建云桌面终端用户账号体系。用户管理功能由 [腾讯云CAM](https://console.tencentcloud.com/cam) 提供，为您提供快速账户认证管理、安全登录设置等服务。
![](https://qcloudimg.tencent-cloud.cn/raw/80bf33f1ab284f469f13dc2cbec45ac7.png)

## 创建终端用户

1. 进入 [腾讯云CAM控制台](https://console.tencentcloud.com/cam)。
2. 创建子用户，详细步骤请参考 [新建子用户](https://www.tencentcloud.com/document/product/598/13674)。
3. 新建子用户时需要授予子用户 QcloudVPCFullAccess 或 QcloudVPCReadOnlyAccess 策略。
4. 子用户使用云桌面，需要授予子用户 QcloudCVDFullAccess 或 QcloudCVDReadOnlyAccess 策略。