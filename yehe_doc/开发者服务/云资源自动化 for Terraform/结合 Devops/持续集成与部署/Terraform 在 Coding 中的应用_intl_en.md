This document describes how to implement automated deployment with Terraform and CODING.

## Prerequisites
1. Register at [CODING](https://coding.net/help/docs/start/register-invite.html).

2. Create [a team](https://coding.net/help/docs/start/register-invite.html) and a project in CODING.

3. Register at [Tencent Cloud](https://www.tencentcloud.com/document/product/378/17985).

4. Get the credentials. Create and copy `SecretId` and `SecretKey` on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page.


## Creating a Code Repository in CODING

[Create a code repository](https://coding.net/help/docs/start/repository.html#repo) in CODING to store Terraform code information.

#### Directory structure
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

Directory structure description:
1. The project structure mainly consists of `environments` and `modules` directories.

2. The `environments` directory isolates `dev` and `prod` environments and sets different configurations for different environments. Each environment directory is an independent root module.
   

   >?
   >- `dev` demonstrates how to create a VPC.
   >- `prod` demonstrates how to isolate businesses through `workspace`. VPCs are created in the `cicd` directory, and container clusters are created in the `qta` directory.

3. `modules` encapsulates resource information for reuse. Here, it contains demo modules of the VPC, security group, and TKE.

4. For the complete code, see [gitops-terraform](https://github.com/tencentcloudstack/gitops-terraform).


## Workflow Configuration
1. Select a created project and create a build plan from **Continuous Integration** of the project as instructed in [Creating a build plan](https://coding.net/help/docs/start/ci.html#create). Select **Custom build process** for the template. 

2. Configure the details of the build plan.

  - On the **Basic info** tab, select the code repository and node (you can select a node in Hong Kong (China) if the download is slow or inaccessibility occurs).
      
  - On the **Process configuration** tab, select the text editor and copy the configuration in [Related Operations](https://www.tencentcloud.com/document/product/1172/52325) for direct use.
      
  - On the **Trigger rule** tab, select **Trigger build during merge request creation** and **Trigger build upon source branch change** for the check workflow and select **Trigger build during merge request merging** for the deployment workflow.
      
  - On the **Variable and cache** tab, configure `TENCENTCLOUD_SECRET_ID` and `TENCENTCLOUD_SECRET_KEY`.


### Related Operations

After the environment directory specified by `environment` is entered, the system will check whether a sub-directory exists, and if so, the system will isolate different business environments (such as `qta` and `ci`) through `workspace`; if not, the specified directory is equivalent to a common root module.

#### Creating a check workflow

Download Terraform and verify the Terraform code as follows:
``` bash
pipeline {
  agent any
  stages {
    stage('Check out') {
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

      stage('Terraform verification') {
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

#### Creating a deployment workflow
``` bash
pipeline {
  agent any
  stages {
    stage('Check out') {
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

