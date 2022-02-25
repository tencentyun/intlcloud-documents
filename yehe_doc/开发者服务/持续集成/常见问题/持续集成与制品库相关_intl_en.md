[](#dockerhub-limited)
### Why does the system return the error `reached your pull rate limit`?

When pulling images using CI, you may be prompted with the error `reached your pull rate limit`, as shown below:
![](https://main.qcloudimg.com/raw/a7ce5421447af6ee35cc5b2bd9574af9.png)

This occurs when users with the trial version of Docker Hub reach their image pull limit, due to the CODING egress IP address reaching the Docker Hub pull limit. Use one of the two methods below to solve this problem:
-   Host images in the CODING Docker artifact repository. For details, see [Docker Artifact Repository](https://intl.cloud.tencent.com/document/product/1136/44806).
-   Use your personal Docker Hub account.

If you don't have a Docker Hub account, you can [sign up](https://hub.docker.com).

After signing up for an account, modify the build plan configuration by adding this line and entering the account before executing commands in Docker.

```bash
    docker login -u <dockerhub username> -p <dockerhub password>
    username=$(docker info | sed '/Username:/!d;s/.* //'); 
    echo $username
```
During execution, you can view the current Docker Hub account in the log. An account that has not reached its pull limit will not have this problem.
![](https://qcloudimg.tencent-cloud.cn/raw/402bc3037a3d0a411956b2410301e45b.png)
