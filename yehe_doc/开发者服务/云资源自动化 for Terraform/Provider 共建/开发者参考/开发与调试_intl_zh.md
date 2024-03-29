本文介绍如何在本地进行基本的 Terraform 开发与调试工作。

## 步骤1：安装 Terraform

参考 [安装 Terraform](https://www.tencentcloud.com/document/product/1172/52304)，完成 Terraform 安装及全局路径配置。

## 步骤2：Provider 拉取
1. 前往 [terraform-provider-tencentcloud](https://github.com/tencentcloudstack/terraform-provider-tencentcloud/)，将  provider 代码 fork 到个人仓库。

2. 依次执行以下命令，本地拉取并设置上游远程仓库。

   ``` shell
   $ git clone https://github.com/{您的用户名}/terraform-provider-tencentcloud # 这里的代码路径为上述fork后的个人代码仓库，根据实际情况修改
   ```
   ``` bash
   $ cd terraform-provider-tencentcloud
   ```
   ``` bash
   $ git remote add upstream https://github.com/tencentcloudstack/terraform-provider-tencentcloud
   ```

   拉取成功后，可查看代码结构如下：

   ``` txt
   .
   ├── .githooks/
   ├── .github/
   ├── examples/ # 示例代码，原则上请确保产出的代码用户可以直接复制粘贴使用
   ├── gendoc/ # 文档生成工具
   ├── scripts/
   ├── tencentcloud/ # 产品逻辑
   ├── vendor/ # 本地依赖缓存
   ├── website/ # 生成的文档目录
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

## 步骤3：本地调试
1. 在项目根目录执行以下命令，构建二进制文件 `terraform-provider-tencentcloud`。

   ``` bash
   go build
   ```
2. 创建 `dev.tfrc` 文件，并写入以下内容，设置 `tencentcloudstack/tencentcloud` 指向二进制文件的位置。

   ``` hcl
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
3. 设置以下环境变量。

- 设置 `TF_CLI_CONFIG_FILE` 环境变量，指向 `dev.tfrc` 所在位置。

   ``` shell
   $ export TF_CLI_CONFIG_FILE=/Users/you/dev.tfrc
   ```
- 设置 `TF_LOG` 环境变量，以打开日志。

   ``` shell
   $ export TF_LOG=TRACE 
   ```
- 设置个人的腾讯云凭证。可前往 [API密钥管理](https://console.cloud.tencent.com/cam/capi) 页面获取。

   ``` shell
   $ export TENCENTCLOUD_SECRET_ID=xxx
   $ export TENCENTCLOUD_SECRET_KEY=xxx
   ```
4. 至此，provider 已完成本地替换，您可自行编写 `.tf` 文件，执行 `terraform plan/apply/destroy` 等命令进行调试。


## 步骤4：单元测试

>?
> - 强烈建议您自行编写单元测试用例进行测试。您可在 `tencentcloud/` 下查看众多 `*_test.go` 单元测试用例。
> - 如需成为 Terraform 官方认证的 provider，则必须具备单元测试用例。

1. 以 NAT 网关为例，代码如下：

   ``` go
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
           // 配置 资源销毁结果检查函数
           CheckDestroy: testAccCheckNatGatewayDestroy,
           // 配置 测试步骤
           Steps: []resource.TestStep{
               {
                   // 配置 配置内容
                   Config: testAccNatGatewayConfig,
                   // 配置 验证函数
                   Check: resource.ComposeTestCheckFunc(
                       // 验证资源ID
                       testAccCheckTencentCloudDataSourceID("tencentcloud_nat_gateway.my_nat"),
                       // 验证资源属性，能匹配到，肯定就是创建成功了
                       resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "name", "terraform_test"),
                       resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "max_concurrent", "3000000"),
                       resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "bandwidth", "500"),
                       resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "assigned_eip_set.#", "2"),
                   ),
               },
               {
                   // 配置 配置内容
                   Config: testAccNatGatewayConfigUpdate,
                   Check: resource.ComposeTestCheckFunc(
                       testAccCheckTencentCloudDataSourceID("tencentcloud_nat_gateway.my_nat"),
                       // 验证修改后的属性值，如果能匹配到，肯定就是修改成功了
                       resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "name", "new_name"),
                       resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "max_concurrent", "10000000"),
                       resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "bandwidth", "1000"),
                       resource.TestCheckResourceAttr("tencentcloud_nat_gateway.my_nat", "assigned_eip_set.#", "2"),
                   ),
               },
           },
       })
   }
   
   // testAccProviders 在测试前会根据 Config 建立测试资源，测试结束后又会全部销毁
   // 这个函数就是检查资源是否销毁用的，代码逻辑比较好理解，就是根据ID查询资源是否存在
   func testAccCheckNatGatewayDestroy(s *terraform.State) error {
   
       conn := testAccProvider.Meta().(*TencentCloudClient).vpcConn
   
       // 这用到了 s.RootModule().Resources 数组
       // 这个数组的属性反应的就是资源状态文件 terraform.tfstate
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
   
   // 基本用法配置文件，与debug的tf文件一致
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
   
   // 修改用法配置文件，与debug修改后的tf文件一致
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
2. 执行`TestAccTencentCloudNatGateway_basic`函数，进行单元测试。

   ``` go
   $ export TF_ACC=true
   $ cd tencentcloud
   $ go test -i; go test -test.run TestAccTencentCloudNatGateway_basic -v
   ```

   通过该示例可得知官方的 testAccProviders 除自动编译外，测试流程也更加标准化，全面覆盖 Create/Read/Update/Delete。您可针对同一个资源管理程序，编写更多复杂的场景，并将其加入 Steps 或分为多个测试用例，使得测试更加全面。
