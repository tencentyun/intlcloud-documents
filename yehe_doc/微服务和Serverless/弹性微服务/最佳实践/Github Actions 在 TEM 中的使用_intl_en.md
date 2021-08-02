# Use of GitHub Actions in TEM

### GitHub Actions

TEM integrates world-class CI/CD tools to facilitate your use of GitHub workflows. You can learn more by referring to the [official documentation of GitHub Actions](https://docs.github.com/en/actions).

> GitHub Actions makes it easy to automate all your software workflows, now with world-class CI/CD.

### Application release types supported by TEM

The TEM platform uses cloud native as its infrastructure, where all applications exist in the form of containers at runtime. TEM especially supports the release of JAR and WAR packages for Java applications and takes care of the build and management of images. For other languages, you need to build images on your own and push them to Tencent Cloud Image Registry.

### How to use

The following takes .NET as an example to describe how to use GitHub Actions.

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

1. Your code repository should include the `dockerfile` file for use by the built action.

   ```yaml
   FROM mcr.microsoft.com/dotnet/aspnet:5.0
   COPY ./target /app 
   WORKDIR /app
   ENTRYPOINT ["dotnet", "myWebApp.dll"]
   ```

2. Here, `commitId` is used as the image tag, which makes it easier to confirm the runtime's application code version. If you don't need this, you can directly use the latest image tag.

   ```bash
   git rev-parse --short HEAD
   ```

3. Tencent Cloud [Image Registry Personal Edition](https://console.cloud.tencent.com/tke2/registry/user/self?rid=1) requires your login information. The account information will automatically pop up when you open the Personal Edition page for the first time. The Enterprise Edition works in a similar way. You can find relevant documents by yourself.

   ```yaml
         - name: Login to Registry
           uses: docker/login-action@v1 
           with:
             registry: ${{ secrets.REGISTRY_URL }}
             username: ${{ secrets.REGISTRY_USERNAME }}
             password: ${{ secrets.REGISTRY_TOKEN }}
   ```

4. Relevant keys can be managed by using the **Secrets** module on the **Repository Settings** page.
   ![](https://main.qcloudimg.com/raw/de0b2cc6f187ce140f7d132d638d8849.png)



