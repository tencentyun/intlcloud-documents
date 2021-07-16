# TEMでのGithub Actionsの使用

### GitHub Actions

ワールドクラスのCI/CDツールを統合することで、ユーザーがGithubのworkflowを簡単に使用できるようにします。GitHub Actionsの詳細は[Github Actionsドキュメント](https://docs.github.com/en/actions)をご参照ください。

> GitHub Actions makes it easy to automate all your software workflows, now with world-class CI/CD.

### TEMでサポートされているアプリケーションのパブリッシュタイプ

TEMプラットフォームはCloud Nativeをインフラストラクチャとし、すべてのアプリケーションはruntimeのときにContainer形式で存在します。javaアプリケーションの場合、TEMはJAR、WARパッケージのパブリッシュをサポートしており、プラットフォームはImageのビルドと管理を担当します。これ以外のその他言語では、独自のImageをビルドして、Tencent Container Registryにプッシュする必要があります。

### 利用方法

下記は.Netの例で、基本的なGitHub Actionsの利用方法を示します

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

1. ビルドされたactionに使用するために、ソースコードレジストリ内にdockerfileファイルを用意する必要があります。

   ```yaml
   FROM mcr.microsoft.com/dotnet/aspnet:5.0
   COPY ./target /app 
   WORKDIR /app
   ENTRYPOINT ["dotnet", "myWebApp.dll"]
   ```

2. runtimeアプリケーションコードのバージョンを確認するために、ここではイメージのtagをcommitIdにとします。必要がない場合は、latestイメージのバージョンをそのまま使用できます

   ```bash
   git rev-parse --short HEAD
   ```

3. Tencent Container Registry[パーソナル版](https://console.cloud.tencent.com/tke2/registry/user/self?rid=1)には、ユーザーのログイン情報の設定が必要です。パーソナル版ページを開くと、アカウント情報が自動的にポップアップ表示されます。エンタープライズ版と同様に、関連ドキュメントをご確認ください。

   ```yaml
         - name: Login to Registry
           uses: docker/login-action@v1 
           with:
             registry: ${{ secrets.REGISTRY_URL }}
             username: ${{ secrets.REGISTRY_USERNAME }}
             password: ${{ secrets.REGISTRY_TOKEN }}
   ```

4. 秘密鍵には、レジストリ設定ページのSecretsをご利用ください。
   ![](https://main.qcloudimg.com/raw/de0b2cc6f187ce140f7d132d638d8849.png)



