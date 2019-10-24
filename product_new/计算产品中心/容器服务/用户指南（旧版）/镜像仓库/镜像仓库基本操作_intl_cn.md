## 镜像仓库概述
镜像仓库用于存放 Docker 镜像，Docker 镜像用于部署容器服务，每个镜像有特定的唯一标识（镜像的 Registry 地址+镜像名称+镜像 Tag）。

## 镜像类型
目前镜像支持 Docker Hub 官方镜像和用户私有镜像。

## 开通镜像仓库
![Alt text](https://main.qcloudimg.com/raw/19b5216380d339b0b6b2d7742f847cbf.png)
首次使用镜像仓库的用户，需要先开通镜像仓库。

- **命名空间**：命名空间是您创建的私人镜像地址的前缀。
- **用户名**：默认是当前用户的账号，是您登录到腾讯云 docker 镜像仓库的身份。
- **密码**：是您登录到腾讯云 docker 镜像仓库的凭证。

## 创建镜像
1. 单击镜像列表页【新建】按钮。
![Alt text](https://main.qcloudimg.com/raw/2c704951542f736e21ce0d5cec1c178c.png)
2. 输入镜像名称和描述，然后【提交】。
![Alt text](https://main.qcloudimg.com/raw/c10278379a87f962c24c42abb83746ca.png)

## 推送镜像到镜像仓库
### 登录到腾讯云 registry
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
username：腾讯云账号，开通时已注册。输入密码后即登录完成。
### 上传镜像
```
$ sudo docker tag [ImageId] ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[镜像版本号]
$ sudo docker push ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[镜像版本号]
```
- ImageId 和镜像版本号根据镜像信息补充
- namespace 是开通镜像仓库时填写的命名空间
- ImageName 是在控制台创建的镜像名称


## 下载镜像
登录到镜像仓库，需输入密码。
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
下载镜像。
```
$ sudo docker pull ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[镜像版本号]
```

## 删除镜像
选择镜像，单击【删除】并【确定】。删除镜像会删除该镜像的所有版本。
![Alt text](https://main.qcloudimg.com/raw/cb73a61a4aa649373b2bcaa41af38143.png)
