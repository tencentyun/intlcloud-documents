## 操作场景
在 Serverless 应用开发中，我们需要手动执行部署命令将开发项目部署到云端。通过引入一些 CI 能力进行 Serverless 应用的自动化部署。

##  基于 GitHub 的自动化部署

### 前提条件

- 已创建 Serverless 应用项目。参考 [开发项目](https://intl.cloud.tencent.com/document/product/1040/38253) 创建您的serverless项目并创建各个环境与分支。
- 已托管您的 Serverless 项目到 Github。

### 操作步骤

在开发测试阶段，为了方便开发、测试和调试，希望代码每次提交后进行自动化部署。操作如下：
1. 选取一个您需要执行自动化部署的分支（本示例选择 dev 分支）。
2. 在该分支下创建您的 action。（参考 GitHub 官网 [配置工作流程](https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions)）  
![](https://main.qcloudimg.com/raw/6863deb3acfb9a8de75d8a0447ec4d20.png)
>!GitHub 规定如果事件发生在特定仓库分支上，则工作流程文件必须存在于该分支的仓库中 。
3. 配置腾讯云密钥。参考 GitHub 官网 [使用变量和密码](https://docs.github.com/en/actions/reference/encrypted-secrets)。
![](https://main.qcloudimg.com/raw/e67ecc4fd932124db5d6bfa54b3ebb73.png)
4. 配置 action 部署步骤。

```
# 当代码推动到 dev 分支时，执行当前工作流程
# 更多配置信息: https://docs.github.com/cn/actions/getting-started-with-github-actions

name: deploy serverless

on: #监听的事件和分支配置
  push:
    branches:
      - dev 
  
jobs:
  test: #配置单元测试
    name: test
    runs-on: ubuntu-latest
    steps:
      - name: unit test
        run: '' 
  deploy:
    name: deploy serverless
    runs-on: ubuntu-latest
    needs: [test]
    steps:
      - name: clone local repository
        uses: actions/checkout@v2
      - name: install serverless
        run: npm install -g serverless
      - name: install dependency
        run: npm install
      - name: build
        run: npm build
      - name: deploy serverless
        run: sls deploy --debug
        env: # 环境变量
          STAGE: dev #您的部署环境
          SERVERLESS_PLATFORM_VENDOR: tencent #serverless 境外默认为 aws，配置为腾讯
          TENCENT_SECRET_ID: ${{ secrets.TENCENT_SECRET_ID }} #您的腾讯云账号 sercret ID
          TENCENT_SECRET_KEY: ${{ secrets.TENCENT_SECRET_KEY }}#您的腾讯云账号 sercret key
          
```

完成上述配置后，开发者每次提交代码到 dev 分支时，就会自动部署。
