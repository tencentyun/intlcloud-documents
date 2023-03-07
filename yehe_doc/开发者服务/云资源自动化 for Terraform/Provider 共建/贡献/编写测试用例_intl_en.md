Complete test cases are necessary for a comprehensive program system. The SDK for Terraform integrates a test suite to verify written Terraform resources and data sources. This document describes how to write a test case for TencentCloud Provider.

## Acceptance test

An acceptance test covers the entire lifecycle of a resource, including creation, query, update, import, and deletion. You need to write at least one test case for a resource. Running the acceptance test will **initiate an actual API call and affect Tencent Cloud resources**. Check your account costs before running the test, which can be written in the following steps:

Set environment variables and toggle on acceptance test execution:
``` shell
export TF_ACC=true
```

Set the environment variables of the credential and specify an account to run the test:
``` shell
export TENCENTCLOUD_SECRET_ID=xxxx
export TENCENTCLOUD_SECRET_KEY=yyyy
```

Set the log output level and directory for easier debugging:
``` shell
export TF_LOG=DEBUG
export TF_LOG_PATH=./terraform.log
```

For example, test the input parameters of a VPC resource to check whether the created and updated resource is as expected.
Create the `resource_tc_vpc_test.go` file in the `tencentcloud` directory, specify a VPC resource, and write its initial configuration and updated configuration:
``` go
// filename: tencentcloud/resource_tc_vpc_test.go
const testAccVpcConfig = `
resource "tencentcloud_vpc" "foo" {
  name       = "test-vpc"
  cidr_block = "172.16.0.0/16"
}
`

const testAccVpcConfigUpdate = `
resource "tencentcloud_vpc" "foo" {
  name       = "test-vpc__update"
  cidr_block = "172.16.0.0/22"
  is_multicast = true
}
`
```

Write the function of the case. A function name starting with `TestAccTencentCloud` indicates an acceptance test. The function name format is `TestAccTencentCloud${Module name}${Resource type}_${Subname}`, and the regex is `TestAccTencentCloud[a-zA-Z]+(Resource|DataSource)_[a-zA-Z]+`. Call the function to import the two configuration items and add the assertions in `resource.Test`:
``` go
package tencentcloud

import (
  "testing"

  "github.com/hashicorp/terraform-plugin-sdk/helper/resource"
  "github.com/hashicorp/terraform-plugin-sdk/terraform"
)

func TestAccTencentCloudVpcResource_Basic(t *testing.T) {
  resource.Test(t, resource.TestCase{
    Providers:    testAccProviders,
    Steps: []resource.TestStep{
      {
        // The initial configuration declared above
        Config: testAccVpcConfig,
        Check: resource.ComposeTestCheckFunc(
          testAccCheckVpcExists("tencentcloud_vpc.foo"),
          resource.TestCheckResourceAttr("tencentcloud_vpc.foo", "cidr_block", "172.16.0.0/16"),
          resource.TestCheckResourceAttr("tencentcloud_vpc.foo", "name", "test-vpc"),
        ),
      },
      {
        // The updated configuration declared above
        Config: testAccVpcConfig,
        Check: resource.ComposeTestCheckFunc(
          testAccCheckVpcExists("tencentcloud_vpc.foo"),
          resource.TestCheckResourceAttr("tencentcloud_vpc.foo", "cidr_block", "172.16.0.0/22"),
          resource.TestCheckResourceAttr("tencentcloud_vpc.foo", "name", "test-vpc__update"),
          resource.TestCheckResourceAttr("tencentcloud_vpc.foo", "is_multicast", "true"),
        ),
      },
    },
  })
}
```

Then, run `go test -v -run TestAccTencentCloudVpcResource ./tencentcloud` in the root directory of the project to check the test result:
``` bash
TestAccTencentCloudVpcResource_Basic
=== RUN   TestAccTencentCloudVpcResource_Basic
=== PAUSE TestAccTencentCloudVpcResource_Basic
=== CONT  TestAccTencentCloudVpcResource_Basic
--- PASS: TestAccTencentCloudVpcResource_Basic (26.30s)
PASS
ok      github.com/tencentcloudstack/terraform-provider-tencentcloud/tencentcloud       27.153s
```

If log environment variables are set, the log details will be written into the `tencentcloud/terraform.log`.

## Unit test

Compared to an acceptance test, a unit test is more refined and cheaper, which is suitable for checking whether logically complex code can be correctly executed.
For example, to use the `isExpectError(err)` function to check the TencentCloud API error code in the project in order to decide whether the program should retry (due to unstable client network connection, for example) or exit abnormally, write the following test case starting with `Test*`:
``` go
package tencentcloud

import (
  "testing"
  sdkErrors "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common/errors"
  "github.com/stretchr/testify/assert"
)

func TestIsExpectError(t *testing.T) {

  err := sdkErrors.NewTencentCloudSDKError("ClientError.NetworkError", "", "")

  // Expected
  expectedFull := []string{"ClientError.NetworkError"}
  expectedShort := []string{"ClientError"}
  assert.Equalf(t, isExpectError(err, expectedFull), true, "")
  assert.Equalf(t, isExpectError(err, expectedShort), true, "")

  // Unexpected
  unExpectedMatchHead := []string{"ClientError.HttpStatusCodeError"}
  unExpectedShort := []string{"SystemError"}
  assert.Equalf(t, isExpectError(err, unExpectedMatchHead), false, "")
  assert.Equalf(t, isExpectError(err, unExpectedShort), false, "")
}
```

Run `go test -v -run TestIsExpectError ./tencentcloud` in the root directory of the project to view the result:
``` txt
=== RUN   TestIsExpectError
--- PASS: TestIsExpectError (0.00s)
PASS
ok      github.com/tencentcloudstack/terraform-provider-tencentcloud/tencentcloud       1.312s
```

## Cleaning up test resources

Terraform provides a mechanism called sweepers to clean up test resources, specifically, those not repossessed due to a test exception.  
Sweepers are a group of functions that can be filtered by parameter for selective execution. You need to declare and write the specific deletion logic. For example, to clean up VPC resources, add the `init` function to `tencentcloud/resource_tc_vpc_test.go` and register a sweeper named `tencentcloud_vpc`:
``` go
func init() {
  resource.AddTestSweepers("tencentcloud_vpc", &resource.Sweeper{
    Name: "tencentcloud_vpc",
    F:    testSweepVpcInstance,
  })
}

// Pseudocode logic for implementing the cleanup of VPC resources starting with `test` in a specified region
func testSweepVpcInstance(region string) {
  vpcs := getAllVpc(region)
  for _, vpc in range vpcs {
    if vpc.name == "test" {
      deleteVpc(vpc.id)
    }
  }
}
```

To clean up VPC instances in a specified region (such as Guangzhou), run `go test -v ./tencentcloud -sweep=ap-guangzhou -sweep-run=tencentcloud_vpc`. Then, the SDK for Terraform will match the `tencentcloud_vpc` sweeper, pass in the region specified by `-sweep` to the function, and execute the function to clean up the resources in the region.