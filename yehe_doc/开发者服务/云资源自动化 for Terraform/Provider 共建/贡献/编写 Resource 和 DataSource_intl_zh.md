Terraform 中 Resource 和 DataSource 是最基本的可拓展数据集合。您可以通过这两种集合管理资源。

## 编写 Resource

Resource 用来描述一类资源实体，这类实体可以被添加、查询、修改和移除，例如云服务器 CVM、硬盘、数据库、TKE 集群、COS 桶等可以被增删改查的实体都是典型的 Resource。

本文以 CVM 为例。一台 CVM 实例的简单配置如下：
- 名称： my-cvm

- 可用区： 广州四区

- 机型： SA2.MEDUIM2

- 镜像： TencentOS Server 3.2 (Final)

- 所属网络： vpc-xxxxxxxx

- 所属子网： subnet-xxxxyyyy

- 计费类型： 按量计费

- 是否分配公网IP： 是

- 公网带宽： 10M


   您可以使用高级配置语法 HCL 进行描述，代码示例如下：

   ``` hcl
   resource "tencentcloud_instance" "cvm1" {
     instance_name              = "my-cvm"
     availability_zone          = "ap-guangzhou-4"
     instance_type              = "SA2.MEDIUM2"
     instance_charge_type       = "POSTPAID_BY_HOUR"
     image_id                   = "img-9qrfy1xt"
     allocate_public_ip         = true
     internet_max_bandwidth_out = 10
   }
   ```

   当您第一次执行命令 `terraform apply` 时，已声明的资源会发起创建流程。在创建完毕后，若您改动这段代码中的配置，并再次执行命令 `terraform apply`，将会发起更新流程。执行命令 `terraform destroy` 则会进入销毁流程。


### 编写 Resource 代码

若要使上面这段 HCL 生效，您需要注册腾讯云 Provider，在 [tencentcloud/provider.go](https://github.com/tencentcloudstack/terraform-provider-tencentcloud/blob/master/tencentcloud/provider.go) 中找到 `Provider/ResourceMap` 字段，添加名为 `tencentcloud_instance` 的资源结构体，按照 HCL 定义参数样板 (Schema)，代码如下：
``` go
package tencentcloud

import (
  "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
  "github.com/hashicorp/terraform-plugin-sdk/terraform"
)

func Provider() *schema.Provider {
  return &schema.Provider{
    ResourcesMap: map[string]*schema.Resource{
      "tencentcloud_xxx": { /* 其他声明好的资源 */ },
      "tencentcloud_yyy": { /* 其他声明好的资源 */ },
      "tencentcloud_instance": {
        Schema: map[string]*schema.Schema{
          "instance_name": {
            Optional: true, // 可选字段
            Type:     schema.TypeString, // 字段类型
            Description: "Instance Name.",
          },
          "availability_zone": {
            Required: true, // 必填字段
            Type:     schema.TypeString,
            ForceNew: true, // 当这个字段更改，提交变更后资源销毁重建，因为服务器实例无法切换可用区。
            Description: "Instance available zone.",
          },
          "instance_type": {
            Optional: true,
            Type:     schema.TypeString,
            Description: "Instance Type.",
          },
          "instance_charge_type": {
            Optional: true,
            Type:     schema.TypeString,
            Description: "Instance charge type.",
          },
          "image_id": {
            Required: true,
            Type:     schema.TypeString,
            Description: "Instance OS image Id.",
          },
          "allocate_public_ip": {
            Optional: true,
            Type:     schema.TypeBool, // 布尔类型
            Description: "Specify whether to allocate public IP.",
          },
          "internet_max_bandwidth_out": {
            Optional: true,
            Type:     schema.TypeInt, // 整数类型
            Description: "Specify maximum bandwith.",
          },
        },
      },
    },
  }
}
```

声明资源和参数样板后，Terraform 执行 `apply` / `plan` / `destroy` 时触发资源的增、删、改和同步逻辑也需要您自行定义。Terraform SDK (v1) 中定义了资源的 CRUD 四种方法：
- `Create` 执行 `terraform apply` 且为新建时调用。

- `Read`   执行 `terraform plan / import` 时调用，用来同步远端状态。

- `Update` 执行 `terraform apply` 且为更新时调用。

- `Delete` 执行 `terraform destroy` 时调用。


   接下来向`schema.Resource` 结构体中添加这四个方法，代码如下：

   ``` go
   package tencentcloud
   
   import (
     "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
     "github.com/hashicorp/terraform-plugin-sdk/terraform"
   )
   
   func Provider() *schema.Provider {
     return &schema.Provider{
       ResourcesMap: map[string]*schema.Resource{
         "tencentcloud_xxx": { /* 其他声明好的资源 */ },
         "tencentcloud_yyy": { /* 其他声明好的资源 */ },
         "tencentcloud_instance": {
           Create: resourceTencentCloudInstanceCreate,
           Read:   resourceTencentCloudInstanceRead,
           Update: resourceTencentCloudInstanceUpdate,
           Delete: resourceTencentCloudInstanceDelete,
           Schema: map[string]*schema.Schema{
             // 上文写好的声明，略
           },
         },
       },
     }
   }
   
   func resourceTencentCloudInstanceCreate (d *schema.ResouceData, m interface{}) error {
     instanceName := d.Get("instance_name").(string)
     instanceType := d.Get("instance_type").(string)
     // ...
     
     // terraform apply 新建资源的时候执行
     instanceId := createInstance(&param{
       Name: &instanceName,
       Type: &instanceType,
       // ...
     })
     
     // 创建完成后，给资源设置唯一 Id
     d.SetId(instanceId)
   
     // 资源创建完毕后，需要再次同步远端状态，验证是否一致
     return resourceTencentCloudInstanceRead(d, m)
   }
   
   func resourceTencentCloudInstanceRead (d *schema.ResouceData, m interface{}) error {
     // terraform plan 时和 terraform 创建/更新资源完毕时执行
     
     instanceId := d.Id() // Create 中设置的 Id
     instanceInfo := getInstance(instanceId)
     
     d.Set("instance_name", instanceInfo.Name)
     d.Set("instance_type", instanceInfo.Type)
     
     return nil
   }
   
   func resourceTencentCloudInstanceUpdate (d *schema.ResouceData, m interface{}) error {
     // terraform apply 更新已有资源时执行
     
     updateParam := &param{}
     
     // 逐项检查字段是否更新，组合更新参数
     if d.HasChange("instance_name") {
       name := d.Get("instance_name").(string)
       updateParam.Name = &name
     }
     
     if d.HasChange("instance_type") {
       insType := d.Get("instance_type").(string)
       updateParam.Type = &insType
     }
     // ...
     updateInstance(d.Id(), updateParam)
     
     // 资源创建完毕后，需要再次同步远端状态，验证是否一致
     return resourceTencentCloudInstanceRead(d, m)
   }
   
   func resourceTencentCloudInstanceDelete (d *schema.ResouceData, m interface{}) error {
     // terraform destroy 时执行
     destroyInstance(d.Id())
     
     return nil
   }
   ```

   可以看到在函数中，引用 `d.Get` 参数可以获取 HCL 字段的值，`d.Set` 可以回写（同步）这些值，此外每个资源创建完毕后还要调用 `d.SetId` 设置资源的唯一索引，以保证后续操作和远程真实资源的映射关系一致。  
完成四个函数的主逻辑骨架后，terraform 执行 `plan apply destroy` 即可正常调用，接下来您可以发起云 API 调用，真实地操作资源。
云服务器的 CVM 的 CRUD 接口分别为：

- [RunInstances](https://www.tencentcloud.com/document/product/213/33237) ：购买新实例

- [DescribeInstances](https://www.tencentcloud.com/document/product/213/33258) ：查询实例列表

- [ModifyInstancesAttribute](https://www.tencentcloud.com/document/product/213/33246) ：修改实例属性

- [TerminateInstances](https://www.tencentcloud.com/document/product/213/33234) ：退还实例


   您可以将从 HCL 获取的参数传给 CVM API 所需参数发起调用，代码如下：

   ``` go
   package main
   
   import (
     cvm "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm/v20170312"
   )
   
   func resourceTencentCloudInstanceCreate(d *schema.ResourceData, meta interface{}) error {
     // 从 HCL 中读取字段的值
     instanceName       := d.Get("instance_name").(string)
     instanceType       := d.Get("instance_type").(string)
     imageId            := d.Get("image_id").(string)
     instanceChargeType := d.Get("instance_charge_type").(string)
     zone               := d.Get("availability_zone").(string)
     allocatePublicIp   := d.Get("allocate_public_ip").(bool)
     internetBandWith   := int64(d.Get("internet_max_bandwidth_out").(int))
     
     client, _ := cvm.NewClient(credential, "ap-guangzhou")
     request := cvm.NewRunInstancesRequest()
     //  组合创建 CVM 所需的参数
     request.InstanceName       = &instanceName
     request.InstanceType       = &instanceType
     request.ImageId            = &imageId
     request.InstanceChargeType = &instanceChargeType
     request.Placement          = &cvm.Placement {
       Zone: &zone,
     }
     request.InternetAccessible = &cvm.InternetAccessible {
       InternetMaxBandwidthOut: &internetBandWith,
       PublicIpAssigned:        &allocatePublicIp,
     }
       
     // 发起调用
     id, err := client.RunInstances(request)
     if err != nil {
       return err
     }
     
     // 将创建返回的 ID 设置为资源 ID
     d.SetId(id)
     
     // 回写状态
     return resourceTencentCloudInstanceRead(d, meta)
   }
   ```

   实现 Create 后，再接着实现 Read / Update / Delete ：

   ``` go
   package main
   
   import (
     cvm "github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/cvm/v20170312"
   )
   
   func resourceTencentCloudInstanceRead(d *schema.ResourceData, meta interface{}) error {
     // Create 中设置或导入时拿到的 ID
     id := d.Id()
     
     client, _ := cvm.NewClient(credential, "ap-guangzhou")
     request, _ := cvm.NewDescribeInstancesRequest()
     request.InstanceIds = []*string{&id}
     response, err := client.DescribeInstances(request)
     if err != nil {
       return err
     }
     if len(response.Response.InstanceSet) == 0 {
       return fmt.Errorf("instance %s not exists.", id)
     }
     instance := response.Response.InstanceSet[0]
     
     d.Set("instance_name", instance.InstanceName)
     d.Set("instance_type", instance.InstanceType)
     // d.Set 回写其他如 `image_id` `instance_charge_type` `availability_zone` 等字段，略
     
     return nil
   }
   
   func resourceTencentCloudInstanceUpdate(d *schema.ResourceData, meta interface{}) error {
     id := d.Id()
     client, _ := cvm.NewClient(credential, "ap-guangzhou")
     request, _ := cvm.NewModifyInstancesAttributeRequest()
     request.InstanceIds = []*string{&id}
   
     // 检查字段是否变更且添加参数
     if d.HasChange("instance_name") {
       name := d.Get("instance_name").(string)
       request.InstanceName = &name
     }
     
     // 处理其他 HasChange 字段，略
     
     _, err := client.ModifyInstanceAttribute(request)
     if err != nil {
       return err
     }
     
     return resourceTencentCloudInstanceRead(d, meta)
   }
   
   func resourceTencentCloudInstanceDelete(d *schema.ResourceData, meta interface{}) error {
     id := d.Id()
   
     client, _ := cvm.NewClient(credential, "ap-guangzhou")
     request, _ := cvm.NewTerminateInstancesRequest()
     request.InstanceIds = []*string{&id}
     _, err := client.TerminateInstances(request)
     if err != nil {
       return err
     }
     return nil
   }
   ```

   至此，在腾讯云 Provider 下一个包含名称、字段声明和赠删改查逻辑的资源全部实现。


### 实现 Import 逻辑

成功实现了资源的增删改查后，可以实现资源的导入逻辑。导入单个资源的命令格式为`terraform import <type>.<index> <id>`，例如：
``` bash
terraform import tencentcloud_instance.cvm1 ins-abcd1234
```

可以看到，资源导入只有一个 `ins-abcd1234` 输入，回想我们已实现的 Read 方法，可以得知：当 Id 确定时，可以根据 Id 查询远端资源的详细配置，自动将配置同步到本地。所以我们只需要在 schema.Resource 中声明 `Importer` 表示该资源可以被导入，后续同步操作由 Read 接管：
``` go
package tencentcloud

import (
  "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
  "github.com/hashicorp/terraform-plugin-sdk/terraform"
)

func Provider() *schema.Provider {
  return &schema.Provider{
    ResourcesMap: map[string]*schema.Resource{
      "tencentcloud_xxx": { /* 其他声明好的资源 */ },
      "tencentcloud_yyy": { /* 其他声明好的资源 */ },
      "tencentcloud_instance": {
        Create: resourceTencentCloudInstanceCreate,
        Read:   resourceTencentCloudInstanceRead,
        Update: resourceTencentCloudInstanceUpdate,
        Delete: resourceTencentCloudInstanceDelete,
        Schema: map[string]*schema.Schema{
          // 上文写好的声明，略
        },
        // 绝大部分情况，只需要添加 schema.ImportStatePassthrough 即可
        Importer: &schema.ResourceImporter{
          State: schema.ImportStatePassthrough,
        },
      },
    },
  }
}
```

## DataSource

DataSource 代表只读实体，仅用做查询，无论调用多少次都不影响现有资源，如云服务器列表、镜像列表、可用区列表、DB 列表和参数模板、审计日志等。理论上只要能够通过 API 查询出来的数据，都可看作 DataSource ，不知您是否注意到：上文的 CVM 镜像对外显示为 `TencentOS Server 3.2 (Final)`，但是实际传递给 API 的参数却是它的 ID `img-9qrfy1xt`，如何通过镜像名称获取对应的 ID 呢？这时候就可以借助 DataSource 来查询并引用了：
``` javascript
data "tencentcloud_images" "fav_os" {
  filters = {
    image_name: "TencentOS Server 3.2",
    image_type: "PUBLIC_IMAGE"
  }
}

resource "tencentcloud_instance" "cvm1" {
  image_id = data.tencentcloud_images.fav_os.images.0.image_id
}
```

如上所示：将 `image_id` 写成对 `data.tencentcloud_images.fav_os` 的引用，Terraform 就会先读取 DataSource 的信息，再将结果计算求值。相比于静态的写法，编写 DataSource 能有效地将带有依赖的资源组织起来。

### 编写 DataSource

实现 DataSource 的方法和 Resource 差不多，同样需要在腾讯云 Provider 中注册，回到 [tencentcloud/provider.go](https://github.com/tencentcloudstack/terraform-provider-tencentcloud/blob/master/tencentcloud/provider.go) 源码，这次我们找到 `Provider/DataSourceMap` 字段，添加名为 `tencentcloud_images` 的结构体（所有 DataSource 名字都应该以 `s` 结尾），按照 HCL 定义参数样板 (Schema)：
``` go
package tencentcloud

import (
  "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
  "github.com/hashicorp/terraform-plugin-sdk/terraform"
)

func Provider() *schema.Provider {
  return &schema.Provider{
    DataSourceMap: map[string]*schema.Resource{
      "tencentcloud_xxxs": { /* 其他声明好的数据源 */ },
      "tencentcloud_yyys": { /* 其他声明好的数据源 */ },
      "tencentcloud_images": {
        Schema: map[string]*schema.Schema{
          "filters": {
            Optional: true,
            Type:     schema.TypeMap, // 定义为 Map 类型
            Description: "Query filter",
          },
          // 用来将结果以 JSON 的形式保存在本地。
          // TencentCloud Provider 约定每个 DataSource 都应带有 `result_output_file`
          "result_output_file": {
            Optional: true,
            Type: schema.TypeString,
            Description: "Used for store as local file.",
          },
          "result": {
            Computed: true, // Computed 可以表示该字段会进行被动更新
            Type:    schema.TypeList,
            Description: "",
            Elem: &schema.Resource{
              Schema: map[string]*schema.Schema{
                "id": {
                  Type: schema.TypeString,
                  Computed: true,
                  Description: "Image Id.",
                },
                "name": {
                  Type: schema.,
                  Computed: true,
                  Description: "Image name.",
                },
              },
            },
          },
        },
      },
    },
  }
}

```

与 Resource 相比， DataSource 只需要实现 Read 方法即可：
``` go
package tencentcloud

import (
  "encoding/json"
  "github.com/hashicorp/terraform-plugin-sdk/helper/schema"
  "github.com/hashicorp/terraform-plugin-sdk/terraform"
)

const ImgNameFilterKey = "image-name"

func Provider() *schema.Provider {
  return &schema.Provider{
    DataSourceMap: map[string]*schema.Resource{
      "tencentcloud_xxxs": { /* 其他声明好的数据源 */ },
      "tencentcloud_yyys": { /* 其他声明好的数据源 */ },
      "tencentcloud_images": {
        Schema: map[string]*schema.Schema{ /* 略 */},
        Read: func(d *schema.ResourceData, meta interface{}) {
          // 声明 Client 和 request
          client, _ := cvm.NewClient(credential, "ap-guangzhou")
          request := cvm.NewDescribeImagesRequest()
          
          // 获取 Filters ，为 Map 类型
          filters := d.Get("filters").(map[string]interface{})
          
          // 检查 filters["name"] 并添加参数
          if name, ok := filters["name"].(string); ok {
            request.Filters = append(request.Filters, &cvm.Filter{
              Name: &ImgNameFilterKey,
              Values: []*string{&name}
            })
          }
          
          // 发起调用
          response, err := client.DescribeImages(request)
          if err != nil {
            return err
          }
          
          // 组装 `result` 字段并写入
          imageSet := response.Response.ImageSet
          result := make([]map[string]interface{}, 0, len(imageSet))
          for i := range imageSet {
            item := imageSet[i]
            result = append(result, map[string]interface{}{
              "id": *item.Id,
              "name": *item.Name,
            })
          }
          d.Set("result", result)
          
          // 如果 `result_output_file` 有定义，则往指定文件写入结果
          if v, ok := d.GetOk("result_output_file"); ok {
            writeToFile(v.(string), result)
          }
          return nil
        }
      },
    },
  }
}

```

这样我们变完成了 `tencentcloud_images` 的编写，后续可以使用这个 DataSource ，查询特定的 OS 镜像。

## 编写验收测试

为了确保您新增的 Resource 或 DataSource 能正常运作，您需要编写验收测试，详情请参考[编写测试用例](https://www.tencentcloud.com/document/product/1172/52381)。