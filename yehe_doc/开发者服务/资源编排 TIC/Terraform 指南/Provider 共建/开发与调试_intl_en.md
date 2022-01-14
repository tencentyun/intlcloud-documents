
This document describes how to perform basic Terraform development and debugging locally.

## Step 1. Install Terraform
Install Terraform and configure global paths as instructed in [Installing Terraform](https://intl.cloud.tencent.com/document/product/1043/44197).

## Step 2. Pull the provider
1. Go to [terraform-provider-tencentcloud](https://github.com/tencentcloudstack/terraform-provider-tencentcloud/) and fork the provider code to your personal repository.
2. Run the following commands in sequence to pull and set the upstream remote repository locally.
```shell
$ git clone https://github.com/{your username}/terraform-provider-tencentcloud # The code path here is the personal code repository after the fork operation, which should be modified to the actual path
```
```
$ cd terraform-provider-tencentcloud
```
```
$ git remote add upstream https://github.com/tencentcloudstack/terraform-provider-tencentcloud
```
After a successful pull, the following code structure can be viewed:
```txt
.
├── .githooks/
├── .github/
├── examples/ # Sample code. In principle, ensure that users can directly copy and paste the output code for use
├── gendoc/ # Document generator
├── scripts/
├── tencentcloud/ # Product logic
├── vendor/ # Local dependency cache
├── website/ # Generated document directory
├── .gitignore
├── .go-version
├── .golangci.yml
├── .goreleaser.yml
├── .travis.yml
├── AUTHORS
├── CHANGELOG.md
├── GNUmakefile
├── LICENSE
├── README.md
├── go.mod
├── go.sum
├── main.go
├── staticcheck.conf
└── tools.go
```

## Step 3. Debug locally
1. Run the following command in the project's root directory to build the `terraform-provider-tencentcloud` binary file.
```bash
go build
```
2. Create the `dev.tfrc` file with the following content and set `tencentcloudstack/tencentcloud` to point to the location of the binary file.
```hcl
provider_installation {
	# Use /home/developer/tmp/terraform-null as an overridden package directory
	# for the hashicorp/null provider. This disables the version and checksum
	# verifications for this provider and forces Terraform to look for the
	# null provider plugin in the given directory.
	dev_overrides {
	    "tencentcloudstack/tencentcloud" = "path/to/your/provider/terraform-provider-tencentcloud"
	}
}
```
3. Set the following environment variables.
 - Set the `TF_CLI_CONFIG_FILE` environment variable to point to the location of `dev.tfrc`.
```shell
$ export TF_CLI_CONFIG_FILE=/Users/you/dev.tfrc
```
 - Set the `TF_LOG` environment variable to enable logging.
```shell
$ export TF_LOG=TRACE 
```
 - Set your personal Tencent Cloud credentials, which can be obtained on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.
```shell
$ export TENCENTCLOUD_SECRET_ID=xxx
$ export TENCENTCLOUD_SECRET_KEY=xxx
```
4. At this point, the provider has been replaced locally. You can write your own `.tf` file and run commands such as `terraform plan/apply/destroy` for debugging.


## Step 4. Perform unit testing

<dx-alert infotype="explain" title="">
- We strongly recommend you write your own unit test cases. You can view many `*_test.go` test cases under `tencentcloud/`.
- A Terraform certified provider must have unit test cases.
</dx-alert>
1. The code of NAT Gateway is as follows:
```go
package tencentcloud

import (
    "encoding/json"
    "fmt"
    "log"
    "testing"

    "github.com/hashicorp/terraform/helper/resource"
    "github.com/hashicorp/terraform/terraform"
    "github.com/zqfan/tencentcloud-sdk-go/common"
    vpc "github.com/zqfan/tencentcloud-sdk-go/services/vpc/unversioned"
)

func TestAccTencentCloudNatGateway_basic(t *testing.T) {
    resource.Test(t, resource.TestCase{
        PreCheck:     func() { testAccPreCheck(t) },
        Providers:    testAccProviders,
        // Configure the function for checking resource termination results
        CheckDestroy: testAccCheckNatGatewayDestroy,
        // Configure test steps
        Steps: []resource.TestStep{
            {
                // Configure the configuration content
                Config: testAccNatGatewayConfig,
                // Configure the validation function
                Check: resource.ComposeTestCheckFunc(
                    // Verify resource IDs
                    testAccCheckTencentCloudDataSourceID("tencentcloud_nat_gateway.my_nat"),
                    // Verify resource attributes (a match indicates successful creation)
                    resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "name", "terraform_test"),
                    resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "max_concurrent", "3000000"),
                    resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "bandwidth", "500"),
                    resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "assigned_eip_set.#", "2"),
                ),
            },
            {
                // Configure the configuration content
                Config: testAccNatGatewayConfigUpdate,
                Check: resource.ComposeTestCheckFunc(
                    testAccCheckTencentCloudDataSourceID("tencentcloud_nat_gateway.my_nat"),
                    // Verify the value of modified attributes (a match indicates successful modification)
                    resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "name", "new_name"),
                    resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "max_concurrent", "10000000"),
                    resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "bandwidth", "1000"),
                    resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "assigned_eip_set.#", "2"),
                ),
            },
        },
    })
}

// `testAccProviders` creates test resources based on Config before testing and terminates them all after testing
// This function is to check whether resources are terminated. The code logic is easy to understand, where the existence of a resource is queried by ID
func testAccCheckNatGatewayDestroy(s *terraform.State) error {

    conn := testAccProvider.Meta().(*TencentCloudClient).vpcConn

    // This uses the `s.RootModule().Resources` array
    // The attributes of this array reflect the `terraform.tfstate` resource state file
    for _, rs := range s.RootModule().Resources {
        if rs.Type != "tencentcloud_nat_gateway" {
            continue
        }

        descReq := vpc.NewDescribeNatGatewayRequest()
        descReq.NatId = common.StringPtr(rs.Primary.ID)
        descResp, err := conn.DescribeNatGateway(descReq)

        b, _ := json.Marshal(descResp)

        log.Printf("[DEBUG] conn.DescribeNatGateway response: %s", b)

        if _, ok := err.(*common.APIError); ok {
            return fmt.Errorf("conn.DescribeNatGateway error: %v", err)
        } else if *descResp.TotalCount != 0 {
            return fmt.Errorf("NAT Gateway still exists.")
        }
    }
    return nil
}

// Basic usage configuration file, which is consistent with the debugged TF file
const testAccNatGatewayConfig = `
resource "tencentcloud_vpc" "main" {
  name       = "terraform test"
  cidr_block = "10.6.0.0/16"
}
resource "tencentcloud_eip" "eip_dev_dnat" {
  name = "terraform_test"
}
resource "tencentcloud_eip" "eip_test_dnat" {
  name = "terraform_test"
}

resource "tencentcloud_nat_gateway" "my_nat" {
  vpc_id           = "${tencentcloud_vpc.main.id}"
  name             = "terraform_test"
  max_concurrent   = 3000000
  bandwidth        = 500 
  assigned_eip_set = [ 
    "${tencentcloud_eip.eip_dev_dnat.public_ip}",
    "${tencentcloud_eip.eip_test_dnat.public_ip}",
  ]
}
`

// Modify the usage configuration file to match the debugged TF file
const testAccNatGatewayConfigUpdate = `
resource "tencentcloud_vpc" "main" {
  name       = "terraform test"
  cidr_block = "10.6.0.0/16"
}
resource "tencentcloud_eip" "eip_dev_dnat" {
  name = "terraform_test"
}
resource "tencentcloud_eip" "eip_test_dnat" {
  name = "terraform_test"
}
resource "tencentcloud_eip" "new_eip" {
  name = "terraform_test"
}

resource "tencentcloud_nat_gateway" "my_nat" {
  vpc_id           = "${tencentcloud_vpc.main.id}"
  name             = "new_name"
  max_concurrent   = 10000000
  bandwidth        = 1000 
  assigned_eip_set = [ 
    "${tencentcloud_eip.eip_dev_dnat.public_ip}",
    "${tencentcloud_eip.new_eip.public_ip}",
  ]
}
`
```
2. Run the `TestAccTencentCloudNatGateway_basic` function to perform the unit test.
```shell
$ export TF_ACC=true
$ cd tencentcloud
$ go test -i; go test -test.run TestAccTencentCloudNatGateway_basic -v
```
This example shows that in addition to automatic compilation, the official `testAccProviders` has a more standardized testing process covering CRUD. You can write a more complex scenario for the same resource manager and then add it to steps or divide it into multiple test cases to make the testing more comprehensive.
