# TEMでのGithub Actionsの使用

### GitHub Actions

ワールドクラスのCI/CDツールを統合することで、ユーザーがGithubのworkflowを簡単に使用できるようにします。[公式ドキュメント](https://docs.github.com/en/actions)を参照すれば、ご自分で学べます。

> GitHub Actions makes it easy to automate all your software workflows, now with world-class CI/CD.

### TEMでサポートされているアプリケーションのパブリッシュタイプ

TEMプラットフォームはCloud Nativeをインフラストラクチャとし、すべてのアプリケーションはruntimeのときにContainer形式で存在します。TEMはjavaアプリケーション用として、JAR、WARパッケージのパブリッシュをサポートしており、プラットフォームはImageのビルドと管理を担当します。これ以外のその他言語では、独自のImageをビルドして、Tencent Cloudのイメージレジストリにプッシュする必要があります。

### 利用方法

.Netを例として、基本的なGitHub Actionsの利用方法を示します

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

1. 顧客は、コードレジストリ内にdockerfileファイルを含めて、ビルドされたactionに使用する必要があります

   ```yaml
   FROM mcr.microsoft.com/dotnet/aspnet:5.0
   COPY ./target /app 
   WORKDIR /app
   ENTRYPOINT ["dotnet", "myWebApp.dll"]
   ```

2. ここではcommitIdがミラーリングされたtagとなるため、runtimeアプリケーションコードのバージョンを確認するのに便利です。必要がない場合は、latestイメージのバージョンをそのまま使用できます

   ```bash
   git rev-parse --short HEAD
   ```

3. Tencent Cloudの[パーソナル版イメージレジストリ](https://console.cloud.tencent.com/tke2/registry/user/self?rid=1)には、ユーザーのログイン情報が必要です。パーソナル版ページを初めて開くと、アカウント情報が自動的にポップアップ表示されます。エンタープライズ版と同様に、クラウド上で関連ドキュメントをご自分で探すことができます

   ```yaml
         - name: Login to Registry
           uses: docker/login-action@v1 
           with:
             registry: ${{ secrets.REGISTRY_URL }}
             username: ${{ secrets.REGISTRY_USERNAME }}
             password: ${{ secrets.REGISTRY_TOKEN }}
   ```

4. 関連する秘密鍵は、レジストリ設定ページのSecretsを使用して管理できます
   ![](https://main.qcloudimg.com/raw/de0b2cc6f187ce140f7d132d638d8849.png)



