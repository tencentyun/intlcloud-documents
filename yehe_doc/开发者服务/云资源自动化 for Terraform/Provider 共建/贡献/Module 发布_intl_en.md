## Overview

Modules are Terraform configurations that allow you to manage a group of resources and can provide better business abstraction and lower costs in some multi-resource scenarios. In addition, you can publish modules on GitHub on the [Terraform registry](https://registry.terraform.io/). This document describes how to create and publish a Terraform TencentCloud module.

## Directions

### Creating a public module

Create a code repository on GitHub.
- The name should be in the format of `terraform-<PROVIDER>-<NAME>`, such as [terraform-tencentcloud-vpc](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-vpc).

- A basic module contains the following files:

   ``` bash
   .
   ├── main.tf # Write module resources
   ├── variables.tf # Declare module variables
   ├── outputs.tf # Declare module outputs
   ├── LICENCE # Declare license
   └── README.md # Readme
   ```

   >?
   > We recommend you add the `example` directory as instructed in [terraform-tencentcloud-vpc/examples](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-vpc/tree/master/examples) to store the examples for importing and using the module.

### Publishing the module
1. Log in to [registry.terraform.io](https://registry.terraform.io/), select **Publish** in the top-right corner of the page, and click **Module** from the drop-down list as shown below: ![](https://qcloudimg.tencent-cloud.cn/image/document/98796ead2fca3f29e837b42c88f054dd.png)

2. Expand the **Select Repository on GitHub** drop-down list to view all the module repositories that you have management permissions for and select the target module as shown below:


   ![](https://qcloudimg.tencent-cloud.cn/image/document/e4f81682690e3b037a7f89dc4c81df74.png)


   >!
   > You can also publish a module through a personal GitHub repository. The modules whose repositories are named in the format of `terraform-tencentcloud-<NAME>` will also be included in the tencentcloud modules.

3. Select **I agree to the Terms of Use.** and click **PUBLISH MODULE**.

4. The repository will be automatically synced to the Terraform registry in a few minutes as shown below: ![](https://qcloudimg.tencent-cloud.cn/image/document/4d28ea3da90c2eb1ccb775ea11f7fd41.png)


### (Optional) Adding repository merge check

If your module involves multi-person collaboration, you can use GitHub Actions to preliminarily check the code with merge requests.

Here, [terraform-tencentcloud-vpc](https://github.com/terraform-tencentcloud-modules/terraform-tencentcloud-vpc) is used as an example. Create the `.github/workflow` directory in the root directory of the repository and create the `pull-request.yml` file. Below is the sample code:
``` yaml
name: MR_CHECK

on:
  pull_request:
    branches: [ master ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: hashicorp/setup-terraform@v1
      - name: Module Files Checking
        run: |
          files=(
            LICENSE
            main.tf
            version.tf
            variables.tf
            outputs.tf
            README.md
          )

          test -d examples || echo "[WARN] Missing ./examples in modules directory, we strongly recommend you to provide example usage of this module."

          for i in ${files[@]} ; do
            fileCount=$(find ./ -name $i | wc -l)
            if [[ $fileCount -gt 0 ]]; then
              echo "[INFO] File: $i exist."
            else
              echo "[ERROR] Missing $i, a recommend module should include these files:\n ${files[@]}"
              exit -1
            fi
          done
      - name: Terraform Validate
        run: |
          terraform init
          terraform validate

      - name: Terraform Format Check
        run: |
          terraform fmt -diff -check -recursive

```

The description is as follows:
- `Module Files Checking`: Check whether the directory contains the file needed above.

- `Terraform Validate`: Check the module parameters.

- `Terraform Format Check`: Verify the Terraform code format in the module. 
