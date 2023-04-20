This document describes how to implement automated deployment with Terraform and GitHub Actions.

### Prerequisites
1. Register at [GitHub](https://github.com/join).

2. Register at [Tencent Cloud](https://www.tencentcloud.com/zh/document/product/378/17985).

3. Get the credentials. Create and copy `SecretId` and `SecretKey` on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page.


## Creating a Project

Create a code repository on GitHub. Below is the directory structure:
``` bash
.
├── README.md
├── environments
│   ├── dev
│   │   ├── main.tf
│   │   └── provider.tf
│   └── prod
│       ├── cicd
│       │   └── main.tf
│       ├── local.tf
│       ├── main.tf
│       ├── provider.tf
│       └── qta
│           └── main.tf
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
1. To avoid security issues due to AK/SK leakage, you need to set environment variables in `https://github.com/${USER}/${PROJECT}/settings/secrets/actions`. Replace the secrets with the copied `SecretId` and `SecretKey`.
![](https://qcloudimg.tencent-cloud.cn/image/document/992dfd2e021321be3cfc0b9054496bc7.png)

2. Configure the workflow through [GitHub Actions](https://docs.github.com/cn/actions).

   Click **New workflow** next to **Actions**, or create a workflow by adding a YAML file in the `.github/workflows/` directory. For more information on the workflow configuration, see [Related Operations](https://www.tencentcloud.com/document/product/1172/52324).
![](https://qcloudimg.tencent-cloud.cn/image/document/dd8c6ae74419d4e923148a7688e5231b.jpeg)


### Check workflow
1. Terraform should not have too many root module resources. Similarly, avoid reading all resources during a check, which should be triggered in a fine-grained manner.

2. In this document, environments are distinguished by branch. For example, if the configuration in the `dev` branch needs to be updated, the update will be triggered only in `dev`. After the configuration update, submit the pull request and merge the code into `main` (main branch). In this way, the system does not need to scan all the sub-directories of `environments` for update checks, reducing unnecessary state sync operations.

3. The workflow mainly runs `terraform fmt`, `terraform init`, `terraform validate`, and `terraform plan` to check the code and display the build plan, so as to determine whether to execute the deployment.


### Deployment workflow
1. If all operations in the check workflow are successful and the output of `terraform plan` is as expected, you can perform the merge operation.

2. After the merge is completed, trigger the deployment operation (i.e., `terraform apply`) as shown below:


   ![](https://qcloudimg.tencent-cloud.cn/image/document/0a3cae8d42b48ef502824d7e58a8b9a7.jpeg)


## Related Operations

After the environment directory specified by `environment` is entered, the system will check whether a sub-directory exists, and if so, the system will isolate different business environments (such as `qta` and `ci`) through `workspace`; if not, the specified directory is equivalent to a common root module.

#### Creating a check workflow

Download Terraform and verify the Terraform code as follows:
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
            const output = `#### Terraform Format and Style \`${{ steps.fmt.outcome }}\`
            #### Terraform Initialization \`${{ steps.init.outcome }}\`
            #### Terraform Validation \`${{ steps.validate.outcome }}\`
            #### Terraform Plan \`${{ steps.plan.outcome }}\`
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

#### Creating a deployment workflow
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

