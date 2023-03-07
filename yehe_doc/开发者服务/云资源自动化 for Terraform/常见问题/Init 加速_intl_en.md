## Symptom

The following error message is returned when a provider is downloaded or updated:
``` bash
Initializing the backend...

Initializing provider plugins...
- Finding latest version of tencentcloudstack/tencentcloud...
╷
│ Error: Failed to install provider
│ 
│ Error while installing tencentcloudstack/tencentcloud v1.78.5: could not query provider registry for registry.terraform.io/tencentcloudstack/tencentcloud: failed to retrieve authentication checksums for provider: the request failed after 2 attempts, please try again later: Get
│ "https://github.com/tencentcloudstack/terraform-provider-tencentcloud/releases/download/v1.78.5/terraform-provider-tencentcloud_1.78.5_SHA256SUMS": context deadline exceeded
╵
```

Or the download is slow:
``` bash
Initializing the backend...

Initializing provider plugins...
- Finding latest version of tencentcloudstack/tencentcloud...
╷
│ Error: Failed to query available provider packages
│ 
│ Could not retrieve the list of available versions for provider tencentcloudstack/tencentcloud: could not connect to registry.terraform.io: Failed to request discovery document: Get "https://registry.terraform.io/.well-known/terraform.json": net/http: request canceled while waiting for connection
│ (Client.Timeout exceeded while awaiting headers)
╵
```

## Troubleshooting the Issue

The `registry.terraform.io` default image source of Terraform is deployed outside the Chinese mainland, which means image pull from the Chinese mainland may be slow or fail due to network issues. In this case, you can use the [image source](https://www.tencentcloud.com/document/product/1172/52391) provided by Tencent Cloud.

## Directions

### Creating the Terraform CLI configuration file

Create the `.terraformrc` or `terraform.rc` configuration file as needed and put it together with other configuration files in the same folder. The path varies by server operating system:
- **In the Windows system**, the file must be named `terraform.rc` and put in the `%APPDATA%` directory of the user. The physical path of the directory varies by Windows version and system configuration and can be located through `$env:APPDATA` in PowerShell.

- **In other operating systems**, the file must be named `.terraformrc` and put in the root directory of the user. You can also use the `TF_CLI_CONFIG_FILE` environment variable to specify the path of the Terraform CLI  configuration file. Any file of this type should follow the `*.tfrc` naming convention. For more information, see [CLI Configuration File](https://developer.hashicorp.com/terraform/cli/config/config-file).


   Taking macOS as an example, create the `.terraformrc` file in the root directory of the user as follows:

   ``` bash
   provider_installation {
       network_mirror {
           url = "https://mirrors.tencent.com/terraform/"
       }
   }
   ```

### Running `terraform init`

In the directory of the Terraform configuration file, run the `terraform init` command to initialize the configuration.

In this step, Terraform will automatically check the `provider` field in the configuration file and download the latest module and plugin. If the following message is printed, the initialization is successful.
``` shell
Initializing the backend...

Initializing provider plugins...
- Finding latest version of tencentcloudstack/tencentcloud...
- Installing tencentcloudstack/tencentcloud v1.78.5...
- Installed tencentcloudstack/tencentcloud v1.78.5 (verified checksum)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

╷
│ Warning: Incomplete lock file information for providers
│ 
│ Due to your customized provider installation methods, Terraform was forced to calculate lock file checksums locally for the following providers:
│   - tencentcloudstack/tencentcloud
│ 
│ The current .terraform.lock.hcl file only includes checksums for darwin_amd64, so Terraform running on another platform will fail to install these providers.
│ 
│ To calculate additional checksums for another platform, run:
│   terraform providers lock -platform=linux_amd64
│ (where linux_amd64 is the platform to generate)
╵

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

