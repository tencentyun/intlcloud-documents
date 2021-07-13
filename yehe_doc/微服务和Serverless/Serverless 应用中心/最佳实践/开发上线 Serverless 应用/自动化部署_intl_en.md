## Overview
During serverless application development, you need to run the deployment command manually to deploy the developed project into the cloud. You can introduce certain CI capabilities to automatically deploy a serverless application.

## Automated Deployment Based on GitHub

### Prerequisites

- You have created a serverless application. You can create a serverless project and the required environments and branches as instructed in [Developing Project](https://intl.cloud.tencent.com/document/product/1040/38253).
- You have hosted your serverless project onto GitHub.

### Directions

During development and testing, to facilitate development, testing, and debugging, you can implement automated deployment of the code after it is submitted in the following steps:
1. Select the target branch for automated deployment (in this example, the `dev` branch is selected).
2. Create your action under this branch as instructed in [Configuring a workflow](https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions).  
![](https://main.qcloudimg.com/raw/6863deb3acfb9a8de75d8a0447ec4d20.png)
>!GitHub stipulates that if an event occurs on a certain repository branch, the workflow file must exist in the repository of the branch.
3. Configure the Tencent Cloud key as instructed in [Using variables and secrets in a workflow](https://docs.github.com/en/actions/reference/encrypted-secrets).
![](https://main.qcloudimg.com/raw/e67ecc4fd932124db5d6bfa54b3ebb73.png)
4. Configure the action for deployment.

```
# When the code is pushed to the `dev` branch, the current workflow will be executed
# For more information on configuration, please visit https://docs.github.com/cn/actions/getting-started-with-github-actions.

name: deploy serverless

on: # Configuration of the event and branch listened on
  push:
    branches:
      - dev 
  
jobs:
  test: # Configure unit test
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
        env: # Environment variable
          STAGE: dev # Your deployment environment
          SERVERLESS_PLATFORM_VENDOR: tencent # The serverless platform is `aws` by default outside Mainland China. Here, it is set to `tencent`
          TENCENT_SECRET_ID: ${{ secrets.TENCENT_SECRET_ID }} # `secret ID` of your Tencent Cloud account
          TENCENT_SECRET_KEY: ${{ secrets.TENCENT_SECRET_KEY }}# `secret key` of your Tencent Cloud account
          
```

After the above configuration is completed, every time the code is submitted to the `dev` branch, it will be automatically deployed.
