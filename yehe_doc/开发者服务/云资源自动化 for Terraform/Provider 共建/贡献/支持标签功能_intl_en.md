Tag is a cloud resource management tool that exists in the format of `key:values`. It can be associated with most of your Tencent Cloud resources, greatly simplifying resource categorization, search, and aggregation.  
In Terraform, a resource tag is defined through `Map`:
``` hcl
resource "tencentcloud_instance" "cvm" {
  tags = {
    key1: "val1",
    key2: "val2"
  }
}
```

## Tag code implementation

A resource tag can be added via TencentCloud API in two ways. One is using the `CreateAPI` parameter:
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

Currently, only certain resource creation APIs support passing in tags, with different data structures. To unify the management of the tag code, the second way is used, that is, calling the tag API after creation for association. The input parameter is the [six-segment resource description](https://www.tencentcloud.com/document/product/598/10606) in the following format:
``` html
qcs:<project_id, which is left empty here>:<Module>:<Region>:<Account/UIN>:<Resource/ID>
```

For example, to modify the tag associated with a VPC instance, use the following input parameter:
``` html
qcs::vpc:ap-singapore:uin/:vpc/vpc-xxxxxxxx
```

In the code, just call the encapsulated `ModifyTags`:
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

