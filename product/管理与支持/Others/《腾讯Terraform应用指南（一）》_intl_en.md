# Summary

The “Tencent Cloud Terraform Application Guide” series of articles helps Tencent Cloud users define, preview, and deploy cloud infrastructure through a simple template language. It teaches users to leverage Tencent Cloud’s Open API and use Infrastructure as Code (IaC) to create and destroy multi-channel resources with one click. With Terraform, users can conserve resources and improve automated productivity. 

As the first in the series, this article introduces the steps to manage Tencent Cloud resources using Terraform. 

# One. Installing Terraform

---

>`NOTES` To address the need to add, overwrite, or delete files in the process of using Terraform and ensure the robustness in security and deployment, we recommend developers to avoid using Terraform locally while managing Tencent Cloud resources. Tencent Cloud’s Cloud Virtual Machine is more convenient and reliable in this regard. It offers fully cloud-based services with top user experience. 

The detailed steps for configuring and installing Terraform on the Tencent Cloud Virtual Machine are as follows:

## 1. Downloading Terraform

Find the latest official version of Terraform here: [Download Terraform] (https://www.terraform.io/downloads.html). Choose the download package that fits your development environment. If you want to install other Terraform versions, check the release history and select the correct link. 

Enter the download and installation command lines

```
    // download terraform
    $ wget https://releases.hashicorp.com/terraform/0.12.5/terraform_0.12.5_linux_amd64.zip
```

![Download Terraform](https://ask.qcloudimg.com/draft/5830525/aizam3xptw.png)

```
    // Install terraform
    $ unzip terraform_0.12.5_linux_amd64.zip
```

![Install Terraform](https://ask.qcloudimg.com/draft/5830525/zaupr4et7n.png)

## 2. Configuring Environment Variables

Create a new directory, `downloads`. Save the installed `terraform` file in this directory.

```
    // Move terraform
    $ mkdir downloads
    $ mv terraform downloads/
```

![Save Terraform in a custom directory](https://ask.qcloudimg.com/draft/5830525/0ki6ca017p.png)

Go to the configuration file `~/.profile`, and add the Terraform environment variables.

```
    $ vim ~/.profile

    // Add Terraform PATH
    export PATH="$PATH:~/downloads"
```

![Add environment variables](https://ask.qcloudimg.com/draft/5830525/5f0mjxbbpd.png)

Reload the `~/.profile` file

```
    $ source ~/.profile
```

View the current version of Terraform

```
    $ terraform -version
```

![Complete the configuration of the environment variables](https://ask.qcloudimg.com/draft/5830525/8l1pkdepa3.png)

 For information on how to configure environment variables in Windows, click [here](https://jingyan.baidu.com/article/9f63fb91d87fb0c8400f0e93.html).

# Two. Using Terraform to Manage Tencent Cloud

---

The specific method for using Terraform to manage Tencent Cloud resources is as follows:

##1. Terraform Workflow

Structural diagram of Terraform usage in deploying Tencent Cloud resources

![Tencent Cloud Terraform Workflow Diagram](https://ask.qcloudimg.com/draft/5830525/wa7ridhoqw.png)

① Configure the `provider` file to support Tencent Cloud’s OpenAPI

② Use the Terraform configuration syntax to generate a `.tf` resource file

③ Use CLI to manage Tencent Cloud resources

Terraform updates the deployment status of all resources in the `*.tf.state` file. This allows users to clearly control their cloud resources on both the frontend console and the backend platform.

## 2. Configuring the Tencent Cloud Provider File

Log in to Tencent Cloud. In Access Management, select API Key Management

![Tencent Cloud Console](https://ask.qcloudimg.com/draft/5830525/um2jbqi3mu.png)

Create keys to obtain Secret\_Id and Secret\_Key

![Create keys](https://ask.qcloudimg.com/draft/5830525/84g878sgt3.png)

Create a `provider.tf` file in the new directory. Enter the key and region information

```
    $ vim provider.tf
    
    //provider.tf
    provider "tencentcloud" {
        secret_id  = "AKID****************"
        secret_key = "QdcM***************"
        region     = "ap-hongkong"
    }
```

![provider.tf](https://ask.qcloudimg.com/draft/5830525/9mcx0p6pyy.png)

Save the file. Execute `terraform init` to initialize Terraform. In this step, Terraform will automatically detect the `provider` field in the `provider.tf` file and send a request to the official Terraform GitHub to download the latest version of modules and plugins for Tencent Cloud resources. When the initialization is successful, the version information of the current script will appear.

```
    // Initialize
    $ terraform init
```

![Initialization successful](https://ask.qcloudimg.com/draft/5830525/4r4mv4dkmk.png)

When a new version of the Tencent Cloud script is released, upgrade the script using the `terraform init -upgrade` command to obtain the latest application.

At the same time, you can use `terraform plan` to preview the operations to be completed. When you are prepared to create resources, you can use  `terraform apply` to deploy resources. For more information related to Terraform CLI, click [here](https://www.terraform.io/docs/commands/index.html).

> `NOTES` Inputting the secret key directly into the .tf file is very unsafe. If multiple users are managing resources together, we do not recommend writing the secret key of the Tencent Cloud API into the source code as it can be accidentally released with the public version through an update, creating a security risk.

Tencent cloud provides a safer and more reliable method of configuring key information in environment variables.

```
    // Configure the secret key in the environment path
    $ export TENCENTCLOUD_SECRET_ID="your_fancy_accessid"
    $ export TENCENTCLOUD_SECRET_KEY="your_fancy_accesskey"
    $ export TENCENTCLOUD_REGION="ap-hongkong"
```

This way, the related information can be omitted from the `provider.tf` file

```
    $ vim provider.tf
    
    // provider.tf
    provider "tencentcloud" {}
```

Tencent Cloud is committed to protecting the privacy and security of our users, and we will continue to update and add more secure and reliable methods for the configuration of key information.

## 3. Deploying Tencent Cloud Resources

This section provides a simple use case for creating a Tencent Cloud Virtual Machine (CVM) in a Virtual Private Cloud (VPC)

Create a resource file for a CVM instance

```
    $ vim cvm.tf
    
    // Create a cvm
    resource "tencentcloud_instance" "cvm_test" {
        instance_name = "cvm-test"
        availability_zone = "ap-hongkong-1"
        image_id = "img-pi0ii46r"
        instance_type = "S2.SMALL1"
        system_disk_type = "CLOUD_PREMIUM"
      
        security_groups = [
            "${tencentcloud_security_group.sg_test.id}"
        ]

        vpc_id = "${tencentcloud_vpc.vpc_test.id"
        subnet_id = "${tencentcloud_subnet.subnet_test.id}"
        internet_max_bandwidth_out = 10
        count = 1
    }
```

![cvm.tf](https://ask.qcloudimg.com/draft/5830525/8ucwwo2w44.png)

You can see that the specific parameter information for the security group, VPC, and subnet of this CVM are not directly entered. You can allocate specific resources by calling the contents of the `id` field in the .tf file of the related resource. In this example, the following resources are called: the security group .tf file, `sg_test`; the VPC .tf file, `vpc_test`; the route table .tf file, `route_table.tf`; and the subnet .tf file, `subnet_test`. The specific content is as follows:

Create a resource file for a VPC

```
    $ vim vpc.tf
    
    // Create a vpc
    resource "tencentcloud_vpc" "vpc_test" {
        name = "vpc-test"
        cidr_block = "10.0.0.0/16"
    }
```

Create a resource file for a subnet

```
    $ vim subnet.tf
    
    // Create a subnet
    resource "tencentcloud_subnet" "subnet_test" {
        name = "subnet-test"
        cidr_block = "10.0.1.0/24"
        availability_zone = "ap-hongkong-1"
        vpc_id = "${tencentcloud_vpc.vpc_test.id}"
        route_table_id = "${tencentcloud_route_table.rtb_test.id}"
    }
```

Create a resource file for a route table

```
    $ vim route_table.tf
     
    // Create a route table
    resource "tencentcloud_route_table" "rtb_test" {
        name = "rtb-test"
        vpc_id = "${tencentcloud_vpc.vpc_test.id}"
    }
```

Create a resource file for a security group and security rules

```
    $ vim security_group.tf
    
    // Create a security group and rule
    resource "tencentcloud_security_group" "sg_test" {
        name = "sg-test"    
    }

    resource "tencentcloud_security_group_rule" "sg_rule_test" {
        security_group_id = "${tencentcloud_security_group.sg_test.id}"
        type = "ingress"
        cidr_ip = "0.0.0.0/0"
        ip_protocol = "tcp"
        port_range = "22,80"
        policy = "accept"
    }
```

Execute `terraform plan` to view the deployment plan. 6 resources in total are to be created.

![](https://ask.qcloudimg.com/draft/5830525/aqprzkly8a.png)

![Terraform plan](https://ask.qcloudimg.com/draft/5830525/249g7iehqw.png)

Here, a plus sign `+` in front of a parameter indicates that it is a newly added resource. When the resource is destroyed, the sign in front of the parameter changes to a minus sign `-`. When the resource needs to be redeployed to modify some parameters, the symbols in front of the resource are `-/+`. An arrow symbol, `→`, appears between old and new parameters.

![Resource Modification](https://ask.qcloudimg.com/draft/5830525/l8vddue0q5.png)

Execute `terraform apply` to create resources

![You are asked if you want to create the resources](https://ask.qcloudimg.com/draft/5830525/i15qb31dq.png)

Enter `yes`. “Resource created successfully” appears.

![Resource created successfully](https://ask.qcloudimg.com/draft/5830525/wdspnxq47b.png)

Return to the console. You can see that the newly deployed resources have already taken effect

![Console synchronized to creation operations](https://ask.qcloudimg.com/draft/5830525/7820bqejp0.png)

Execute `terraform destroy` to destroy resources

![You are asked if you want to destroy the resource](https://ask.qcloudimg.com/draft/5830525/9bapbljfr8.png)

Enter `yes`. “Resource destroyed successfully” appears.

![Resource destroyed successfully](https://ask.qcloudimg.com/draft/5830525/wt6hze2znz.png)

The destroy operation is also synchronized in the console

![Console synchronized to destruction operations](https://ask.qcloudimg.com/draft/5830525/jgidthue2l.png)

# Three. Conclusion

This article has prepared you to use Terraform to manage Tencent Cloud. Continue to follow Tencent Cloud + Community. The ecosystem products column “Tencent Cloud Terraform Application Guide” series and the ecosystem products team will continue to help users get started and master their Terraform application skills.

> “Write, Plan, and create Infrastructure as Code” helps every Tencent Cloud user deploy resources efficiently and quickly.