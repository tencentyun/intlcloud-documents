# Github Actions 在 TEM 中的使用

### GitHub Actions

集成世界级 CI/CD 的工具，方便用户的使用 Github 的 workflow。可参考[官方文档](https://docs.github.com/en/actions)自行学习。

> GitHub Actions makes it easy to automate all your software workflows, now with world-class CI/CD.

### TEM 支持的应用发布类型

TEM 平台以 Cloud Native 为基础设施，所有应用在 runtime 时都以 Container 形式存在。TEM 对于 java 应用特别支持了 JAR、WAR 包的发布，平台负责 Image 的构建和管理。除此以外的其他语言，均需自己构建 Image，并推送至腾讯云的镜像仓库中。

### 使用方式

以 .Net 为例，展示一下基本 GitHub Actions 的使用方式

```yaml
name: .NET

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup .NET
        uses: actions/setup-dotnet@v1
        with:
          dotnet-version: 5.0.x
      - name: Declare some variables
        id: vars
        shell: bash
        run: |
          echo "::set-output name=sha_short::$(git rev-parse --short HEAD)"
      - name: Build Code
        run: dotnet publish -o ./target
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v1
      - name: Login to Registry
        uses: docker/login-action@v1 
        with:
          registry: ${{ secrets.REGISTRY_URL }}
          username: ${{ secrets.REGISTRY_USERNAME }}
          password: ${{ secrets.REGISTRY_TOKEN }}
      - name: Build and push
        uses: docker/build-push-action@v2
        with:
          context: .
          push: true
          platforms: linux/amd64,linux/arm64
          tags: ccr.ccs.tencentyun.com/han_test/my-web-app:${{ steps.vars.outputs.sha_short }}
```

1. 客户需代码仓库内包含 dockerfile 文件，供构建的 action 使用

   ```yaml
   FROM mcr.microsoft.com/dotnet/aspnet:5.0
   COPY ./target /app 
   WORKDIR /app
   ENTRYPOINT ["dotnet", "myWebApp.dll"]
   ```

2. 此处以 commitId 作为镜像的 tag，方便确认 runtime 的应用代码版本。如无此需求，可直接使用 latest 镜像版本

   ```bash
   git rev-parse --short HEAD
   ```

3. 腾讯云的[个人版镜像仓库](https://console.cloud.tencent.com/tke2/registry/user/self?rid=1)需要用户的登录信息。首次打开个人版页面时账户信息会自动弹窗。企业版类似，可自行查找云上相关文档

   ```yaml
         - name: Login to Registry
           uses: docker/login-action@v1 
           with:
             registry: ${{ secrets.REGISTRY_URL }}
             username: ${{ secrets.REGISTRY_USERNAME }}
             password: ${{ secrets.REGISTRY_TOKEN }}
   ```

4. 相关的秘钥可使用 仓库设置页面的 Secrets 管理
   ![](https://main.qcloudimg.com/raw/de0b2cc6f187ce140f7d132d638d8849.png)



