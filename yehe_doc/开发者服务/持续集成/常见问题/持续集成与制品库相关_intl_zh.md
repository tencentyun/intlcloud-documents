[](#dockerhub-limited)
### 为什么会提示 `reached your pull rate limit` 错误？

使用 CI 拉取镜像时提示 `reached your pull rate limit` 报错，如下图所示：
![](https://main.qcloudimg.com/raw/a7ce5421447af6ee35cc5b2bd9574af9.png)

这是因为 dockerhub 的免费账户存在镜像拉取次数限制，CODING 的出口 IP 达到了 dockerhub 的拉取次数限制而出现的错误，您可以参考下文中的两个办法解决此问题：
-   将镜像托管至 CODING Docker 制品仓库，详情请参见 [Docker 制品库](https://intl.cloud.tencent.com/document/product/1136/44806)。
-   使用个人 Dockerhub 账号。

若您没有 dockerhub 账号，请 [注册账号](https://hub.docker.com)。

注册完成后修改构建计划配置，在 docker 执行命令前添加此行，填入已注册的账号：

```bash
    docker login -u <dockerhub username> -p <dockerhub password>
    username=$(docker info | sed '/Username:/!d;s/.* //'); 
    echo $username
```
执行时可以在日志查看到正在使用的 dockerhub 账号，若账号符合拉取次数限制条件即可解决此问题。
![](https://qcloudimg.tencent-cloud.cn/raw/402bc3037a3d0a411956b2410301e45b.png)
