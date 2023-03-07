标签（Tag）是腾讯云提供的云资源管理工具，以 `key:values` 的形式存在，用来关联您的绝大部分云资源，对于资源的分类、搜索和聚合十分有用。  
在 Terraform 中，通过 Map 来定义一个资源的 Tag ：
``` hcl
resource "tencentcloud_instance" "cvm" {
  tags = {
    key1: "val1",
    key2: "val2"
  }
}
```

## Tag 代码实现

通过云 API 对资源添加 Tag ，有两种实现方式，一种是通过 CreateAPI 参数传入：
``` bash
rsType := "instance"

request := cvm.NewRunInstanceRequest()
request.TagSpecification = append(request.TagSpecification, &cvm.TagSpecification{
  ResourceType: &rsType,
  Tags: []*cvm.Tag{
    {
      Key: &key,
      Value: &value,
    },
  },
})
```

目前仅有部分资源的创建 API 支持传入 Tag ，且数据结构也有所出入。为了统一管理 Tag 代码，我们采用第二种方式，即创建后单独调用 Tag API 关联，入参为 [资源六段式](https://www.tencentcloud.com/document/product/598/10606) ，格式为：
``` html
qcs:<project_id，此处置空>:<模块>:<地域>:<账号/uin>:<资源/ID>
```

以 VPC 举例，如要修改 VPC 实例关联的 Tag ，入参如下：
``` html
qcs::vpc:ap-singapore:uin/:vpc/vpc-xxxxxxxx
```

代码中则调用封装好的 ModifyTags 即可：
``` go
package main

func ResourceTencentCloudVPCUpdate(d *schema.ResourceData, meta interface{}) {
  ctx := context.TODO()
  region := meta.(*TencentCloudClient).apiV3Conn.Region
  id := d.Id()

  resourceName := fmt.Sprintf("qcs::vpc:%s:uin/:vpc/%s", region, id)
  replaceTags, deleteTags := diffTags(oldTags.(map[string]interface{}), newTags.(map[string]interface{}))
  
  if err := tagService.ModifyTags(ctx, resourceName, replaceTags, deleteTags); err != nil {
    return err
  }
}
```

