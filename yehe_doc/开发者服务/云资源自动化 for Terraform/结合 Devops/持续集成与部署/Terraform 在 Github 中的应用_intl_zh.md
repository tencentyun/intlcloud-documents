本文介绍如何将 Terraform 结合 Github action 实现自动化部署。

### 前置条件
1. 注册 [Github](https://github.com/join) 账号。

2. 注册 [腾讯云账号](https://www.tencentcloud.com/zh/document/product/378/17985)。

3. 获取凭证，在 [API密钥管理](https://console.cloud.tencent.com/cam/capi) 页面中创建并复制 SecretId 和 SecretKey。


## 创建项目

在 GitHub 中新建代码仓库，目录结构如下：
``` bash
.
├── README.md
├── environments
│   ├── dev
│   │   ├── main.tf
│   │   └── provider.tf
│   └── prod
│       ├── cicd
│       │   └── main.tf
│       ├── local.tf
│       ├── main.tf
│       ├── provider.tf
│       └── qta
│           └── main.tf
└── modules
    ├── network
    │   ├── main.tf
    │   ├── outputs.tf
    │   ├── provider.tf
    │   └── variables.tf
    ├── security_group
    │   ├── main.tf
    │   ├── outputs.tf
    │   ├── provider.tf
    │   └── variables.tf
    └── tke
        ├── main.tf
        ├── outputs.tf
        ├── provider.tf
        └── variables.tf
```

目录结构说明：
1. 项目结构主要分为`environments`和`modules`两个目录。

2. `environments`为目录方式隔离环境`dev`和`prod`，用来给不同环境设置各自的配置，每个环境目录都是独立的根模块。
   

   >?
   >- dev 中演示创建一个 vpc。
   >- prod 中演示通过 workespace 进行业务隔离。在 cicd 目录中创建 vpc， 在 qta 目录下创建容器集群。

3. `modules`为封装的资源信息，用以复用。本目录中包含 vpc、安全组和容器服务 TKE 的 Module 演示。

4. 完整代码请参考[ gitops-terraform](https://github.com/tencentcloudstack/gitops-terraform)。


## 流水线配置
1. 为防止 AKSK 等安全信息泄流造成安全问题，您需要在`https://github.com/${USER}/${PROJECT}/settings/secrets/actions`设置环境变量。请替换为已复制的 SecretId 和 SecretKey。
![](https://qcloudimg.tencent-cloud.cn/image/document/992dfd2e021321be3cfc0b9054496bc7.png)

2. 通过 [GitHub Actions](https://docs.github.com/cn/actions) 配置流水线。

   您可以在项目中的 actions 选项处单击 **New workflow**，也可以在`.github/workflows/`目录里通过添加 yml 文件创建，流水线配置详情可以参考[相关操作](https://www.tencentcloud.com/document/product/1172/52324)。
![](https://qcloudimg.tencent-cloud.cn/image/document/dd8c6ae74419d4e923148a7688e5231b.jpeg)


### 检查流水线
1. Terraform 根模块资源不能过多。同理，在执行检查的时候也应该尽可能的避免全部资源的读取，需要以细粒度的方式触发检查。

2. 本文档采用按分支区分触发的环境。例如，dev 中的配置需要更新时，只能在 dev 分支上进行更新。配置更新完成后提交 PR 将代码合入到 main（主分支）。目的是每次更新的检查不需要全量扫描 environments 下的所有子目录（环境），减少不必要的状态同步消耗。

3. 该流水线主要通过执行`terraform fmt`、`terraform init`、`terraform validate`、`terraform plan`来检查代码和展示构建计划，方便判断是否执行部署。


### 部署流水线
1. 如果检查流水线中的检查操作都成功且`terraform plan`的输出复合预期，那么就可以进行 merge 操作。

2. 在 merge 完成的时候触发部署（即`terraform apply`）的操作。示意图如下：


   ![](https://qcloudimg.tencent-cloud.cn/image/document/0a3cae8d42b48ef502824d7e58a8b9a7.jpeg)


## 相关操作

在进入 environment 的指定环境目录后，会判断是否还有子目录，如果有则通过 workspace 隔离不同业务环境（例如 qta，ci），如果没有则等价于普通的根模块。

#### 创建校验流水线

参考以下代码，下载 Terraform 和校验 Terraform  代码：
``` bash
# This is a basic workflow to help you get started with Actions

name: CI

# Controls when the workflow will run
on:
  pull_request:


# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest
    env: 
      TENCENTCLOUD_SECRET_KEY: ${{ secrets.TENCENTCLOUD_SECRET_KEY }}
      TENCENTCLOUD_SECRET_ID: ${{ secrets.TENCENTCLOUD_SECRET_ID }}

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      - uses: actions/checkout@v3
      - uses: hashicorp/setup-terraform@v2
        with:
          terraform_wrapper: false
      
      - name: check env
        run: |
          if [ ! -d "environments/$GITHUB_HEAD_REF" ]; then
            echo "*************************SKIPPING************************************"
            echo "Branch '$GITHUB_HEAD_REF' does not represent an oficial environment."
            echo "*********************************************************************"
            exit 1
          fi
      
      - name: terraform fmt
        id: fmt
        run: terraform fmt -recursive -check

      - name: terraform init
        id: init
        working-directory: environments/${{ github.head_ref    }}
        run: terraform init

      - name: terraform validate
        id: validate
        working-directory: environments/${{ github.head_ref    }}
        run: terraform validate
          
      - name: terraform plan
        id: plan
        if: github.event_name == 'pull_request'
        working-directory: environments/${{ github.head_ref    }}
        run: |
          plan_info=""
          dir_count=`ls -l | grep "^d" | wc -l`
          if [ $dir_count -gt 0 ]; then
            for dir in ./*/
            do
              env=${dir%*/}
              env=${env#*/}
              echo ""
              echo "========> Terraform Plan <========"
              echo "At environment: ${{ github.head_ref    }}"
              echo "At workspace: ${env}"
              echo "=================================="
              terraform workspace select ${env} || terraform workspace new ${env}
              plan_info="$plan_info\n$(terraform plan -no-color)"
            done
          else
            plan_info="$(terraform plan -no-color)"
          fi
          plan_info="${plan_info//'%'/'%25'}"
          plan_info="${plan_info//$'\n'/'%0A'}"
          plan_info="${plan_info//$'\r'/'%0D'}"
          echo "::set-output name=plan_info::$plan_info"
        continue-on-error: true

      - uses: actions/github-script@v6
        if: github.event_name == 'pull_request'
        with:
          script: |
            const output = `#### Terraform Format and Style 🖌\`${{ steps.fmt.outcome }}\`
            #### Terraform Initialization ⚙️\`${{ steps.init.outcome }}\`
            #### Terraform Validation 🤖\`${{ steps.validate.outcome }}\`
            #### Terraform Plan 📖\`${{ steps.plan.outcome }}\`
            <details><summary>Show Plan</summary>
            \`\`\`\n
            ${{ steps.plan.outputs.plan_info }}
            \`\`\`
            </details>
            *Pushed by: @${{ github.actor }}, Action: \`${{ github.event_name }}\`*`;
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: output
            })
```

#### 创建部署流水线
``` bash
name: Apply

on:
  pull_request:
    types:
      - closed
    branches:
      - main


jobs:
  build:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest
    env: 
      TENCENTCLOUD_SECRET_KEY: ${{ secrets.TENCENTCLOUD_SECRET_KEY }}
      TENCENTCLOUD_SECRET_ID: ${{ secrets.TENCENTCLOUD_SECRET_ID }}

    steps:
      - uses: actions/checkout@v3
      - uses: hashicorp/setup-terraform@v2

      - name: terraform init
        id: init
        working-directory: environments/${{ github.head_ref    }}
        run: terraform init

      - name: terraform apply
        working-directory: environments/${{ github.head_ref }}
        run: |
          dir_count=`ls -l | grep "^d" | wc -l`
          if [ $dir_count -gt 0 ]; then
            for dir in ./*/
            do
              env=${dir%*/}
              env=${env#*/}
              echo ""
              echo "========> Terraform Apply <========"
              echo "At environment: ${{ github.head_ref    }}"
              echo "At workspace: ${env}"
              echo "=================================="
              
              terraform workspace select ${env} || terraform workspace new ${env}
              terraform apply -auto-approve
            done
          else
            terraform apply -auto-approve
          fi
```

