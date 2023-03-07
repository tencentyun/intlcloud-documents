对于构建一套健全的程序系统，完善的测试用例不可或缺，Terraform 的 SDK 集成了一套测试套件，用来验证您编写的 Terraform Resource 和 DataSource ，下文将介绍如何对腾讯云 Provider 编写测试用例。

## 验收测试

验收测试 (Acceptance Test) 覆盖一个资源的完整生命周期：创建、查询、更新、导入和删除，每一个资源都需要编写至少一个测试用例。运行验收测试将 **真实地发起 API 调用，影响云资源** 。运行测试之前请留意您的账号成本消耗。编写验收测试的步骤如下：

设置环境变量，打开执行验收测试开关：
``` shell
export TF_ACC=true
```

设置凭证相关环境变量，指定账户运行测试：
``` shell
export TENCENTCLOUD_SECRET_ID=xxxx
export TENCENTCLOUD_SECRET_KEY=yyyy
```

设置日志输出级别和目录，方便调试：
``` shell
export TF_LOG=DEBUG
export TF_LOG_PATH=./terraform.log
```

以私有网络 VPC 举例，测试该资源传入的参数，创建和更新后是否全部符合预期。
`tencentcloud` 目录下创建 `resource_tc_vpc_test.go` 文件，指定一个 VPC 资源，编写其初始配置和更新配置：
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

编写用例函数，函数名以 `TestAccTencentCloud` 起头表示验收测试，函数名规则为`TestAccTencentCloud${模块名}${资源类型}_${子名称}`，正则表达式: `TestAccTencentCloud[a-zA-Z]+(Resource|DataSource)_[a-zA-Z]+`， 调用 `resource.Test` 中引入这两个配置并添加断言：
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
        // 上文声明的初始配置
        Config: testAccVpcConfig,
        Check: resource.ComposeTestCheckFunc(
          testAccCheckVpcExists("tencentcloud_vpc.foo"),
          resource.TestCheckResourceAttr("tencentcloud_vpc.foo", "cidr_block", "172.16.0.0/16"),
          resource.TestCheckResourceAttr("tencentcloud_vpc.foo", "name", "test-vpc"),
        ),
      },
      {
        // 上文声明的更新配置
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

编写完毕，项目根目录执行 `go test -v -run TestAccTencentCloudVpcResource ./tencentcloud` 验证测试结果：
``` bash
TestAccTencentCloudVpcResource_Basic
=== RUN   TestAccTencentCloudVpcResource_Basic
=== PAUSE TestAccTencentCloudVpcResource_Basic
=== CONT  TestAccTencentCloudVpcResource_Basic
--- PASS: TestAccTencentCloudVpcResource_Basic (26.30s)
PASS
ok      github.com/tencentcloudstack/terraform-provider-tencentcloud/tencentcloud       27.153s
```

如果设置了日志相关的环境变量，日志详情将会在 `tencentcloud/terraform.log` 中写入。

## 单元测试

相比上文的验收测试，单元测试的粒度更细，测试成本更低，当您对于某些复杂逻辑代码难以确认是否能正确执行，编写单元测试是一个很好的验证方式。
例如，项目中有函数 `isExpectError(err)` 用来检查云 API 的错误码决定程序应该重试（比如客户端网络不稳定）还是异常退出，可以编写以下测试用例。以 `Test*` 开始：
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

项目根目录下执行 `go test -v -run TestIsExpectError ./tencentcloud` ，查看结果：
``` txt
=== RUN   TestIsExpectError
--- PASS: TestIsExpectError (0.00s)
PASS
ok      github.com/tencentcloudstack/terraform-provider-tencentcloud/tencentcloud       1.312s
```

## 清理测试资源

Terraform 提供主动清理测试资源的机制 Sweeper ，当某些资源测试过程中出现异常导致资源没有进行最后的回收步骤，需要我们进行主动清理。  
Sweeper 是一组可以通过参数过滤选择性执行的函数，开发者需要主动声明并编写具体的删除逻辑。以清理 Vpc 为例，在 `tencentcloud/resource_tc_vpc_test.go` 中加入 init 函数，注册一个名为 `tencentcloud_vpc` 的 Sweeper：
``` go
func init() {
  resource.AddTestSweepers("tencentcloud_vpc", &resource.Sweeper{
    Name: "tencentcloud_vpc",
    F:    testSweepVpcInstance,
  })
}

// 伪代码逻辑，实现指定地域下 test 开头的 VPC 清理
func testSweepVpcInstance(region string) {
  vpcs := getAllVpc(region)
  for _, vpc in range vpcs {
    if vpc.name == "test" {
      deleteVpc(vpc.id)
    }
  }
}
```

如果要清理特定地域（如广州）的 VPC 实例，则执行 `go test -v ./tencentcloud -sweep=ap-guangzhou -sweep-run=tencentcloud_vpc` ， Terraform SDK 会匹配名称为 `tencentcloud_vpc` 的 Sweeper 并传入 `-sweep` 指定的地域给函数并执行，完成该地域的资源清理。