本文介绍如何将 Terraform 结合 Coding 实现自动化部署。

## 前置条件
1. 注册 [Coding 账号](https://coding.net/help/docs/start/register-invite.html)。

2. 在 [Coding 中创建团队](https://coding.net/help/docs/start/register-invite.html)，并创建一个项目。

3. 注册 [腾讯云账号](https://www.tencentcloud.com/document/product/378/17985)。

4. 获取凭证，在 [API密钥管理](https://console.cloud.tencent.com/cam/capi) 页面中创建并复制 SecretId 和 SecretKey。


## Coding 中创建代码库

在 Coding 中创建代码库，用于保存 Terraform 相关的代码信息，创建方式参考 [代码库创建](https://coding.net/help/docs/start/repository.html#repo)。

#### 目录结构如下：
``` bash
.
├── README.md
├── environments
│   ├── dev
│   │   ├── main.tf
│   │   └── provider.tf
│   └── prod
│       ├── main.tf
│       └── provider.tf
└── modules
 ├── network
 │   ├── main.tf
 │   ├── outputs.tf
 │   ├── provider.tf
 │   └── variables.tf
 ├── security_group
 │   ├── main.tf
 │   ├── outputs.tf
 │   ├── provider.tf
 │   └── variables.tf
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
1. 选择已创建的项目并在项目中的持续集成中创建构建计划，操作可参考 [创建构建计划](https://coding.net/help/docs/start/ci.html#create)模板选择“自定义构建过程”。

2. 构建计划详细信息。

  - 在基础信息页，选择代码库和节点信息（如果下载慢或者无法访问，可以选择香港节点）。
      
  - 在流程配置页，可以选择文本编辑器，复制下文 [相关操作](https://www.tencentcloud.com/document/product/1172/52325) 中的配置直接使用。
      
  - 在触发规则页，检查流水线选择**创建合并请求时触发构建**和**源分支变更时触发构建。**部署流水线选择**合并合并请求时触发构建**。
      
  - 在变量与缓存页，需要配置`TENCENTCLOUD_SECRET_ID`和`TENCENTCLOUD_SECRET_KEY`。


### 相关操作

在进入 environment 的指定环境目录后，会判断是否还有子目录，如果有则通过 workspace 隔离不同业务环境（例如 qta，ci），如果没有则等价于普通的根模块。

#### 创建校验流水线

参考以下代码，下载 Terraform 和校验 Terraform  代码：
``` bash
pipeline {
  agent any
  stages {
    stage('检出') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: GIT_BUILD_REF]],
          userRemoteConfigs: [[
            url: GIT_REPO_URL,
            credentialsId: CREDENTIALS_ID
          ]]])
          sh '''wget https://releases.hashicorp.com/terraform/1.0.10/terraform_1.0.10_linux_amd64.zip -O terraform_linux_amd64.zip
unzip -o -d /usr/bin/ terraform_linux_amd64.zip
env'''
        }
      }

      stage('terraform验证') {
        steps {
          sh '''cd environments/${MR_SOURCE_BRANCH}

/usr/bin/terraform -version
/usr/bin/terraform fmt -recursive -check
/usr/bin/terraform init
/usr/bin/terraform validate

plan_info=""
dir_count=$(ls -l | grep "^d" | wc -l)
if [ $dir_count -gt 0 ]; then
for dir in ./*/; do
env=${dir%*/}
env=${env#*/}
echo ""
echo "========> Terraform Plan <========"
echo "At environment: ${MR_SOURCE_BRANCH}"
echo "At workspace: ${env}"
echo "=================================="
/usr/bin/terraform workspace select ${env} || /usr/bin/terraform workspace new ${env}
plan_info="$plan_info\\n$(/usr/bin/terraform plan -no-color)"
done
else
plan_info="$(/usr/bin/terraform plan -no-color)"
fi
echo plan_info
'''
        }
      }

    }
  }
```

#### 创建部署流水线
``` bash
pipeline {
  agent any
  stages {
    stage('检出') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: GIT_BUILD_REF]],
          userRemoteConfigs: [[
            url: GIT_REPO_URL,
            credentialsId: CREDENTIALS_ID
          ]]])
          sh '''wget https://releases.hashicorp.com/terraform/1.0.10/terraform_1.0.10_linux_amd64.zip -O terraform_linux_amd64.zip
unzip -o -d /usr/bin/ terraform_linux_amd64.zip
env'''
        }
      }

      stage('terraform-apply') {
        steps {
          sh '''cd environments/${MR_SOURCE_BRANCH}

/usr/bin/terraform init

apply_info=""
dir_count=`ls -l | grep "^d" | wc -l`
if [ $dir_count -gt 0 ]; then
for dir in ./*/
do
env=${dir%*/}
env=${env#*/}
echo ""
echo "========> Terraform Apply <========"
echo "At environment: ${MR_SOURCE_BRANCH}"
echo "At workspace: ${env}"
echo "=================================="
/usr/bin/terraform workspace select ${env} || /usr/bin/terraform workspace new ${env}
apply_info="$apply_info\\n$(/usr/bin/terraform apply -auto-approve)"
done
else
apply_info="$(/usr/bin/terraform apply -auto-approve)"
fi
echo apply_info'''
        }
      }

    }
  }
```

