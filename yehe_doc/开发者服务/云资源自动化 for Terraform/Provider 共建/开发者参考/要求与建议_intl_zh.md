## 资源约束

由于本项目是开源项目，欢迎个人或团队贡献代码。为了减少沟通成本，提升贡献者的开发效率和用户体验，请查阅并遵守以下原则：
- 输出产品详细说明、字段清单以及对应 API 接口。

- 由于产品的增删改查需通过调用云 API 实现，云 API 需要暴露增删改查接口，至少支持 API 添加和删除。

- Resource 资源创建后必须要返回唯一 ID，如没有 ID 可使用 Name、序号等唯一值代替。

- 输入参数必须能够查询，以保证配置和实际资源状态一致。

- 必须提供单元测试并保证测试通过。

- 职责单一原则：每次变更仅做一件事，避免依赖或影响其他变更。


## 慎用 ForceNew

设置了 ForceNew 的字段，如果检测出变更**会导致资源销毁重建**。如果需要设置，请确保本地的输入和远端状态始终一致。避免出现资源创建后，远端返回状态与用户输入不一致产生的 Diff 从而被判定为销毁重建。

## 默认值 Import

某些资源定义了默认值：
``` go
map[string]*schema.Schema{
  "create_strategy": {
    Type: schema.TypeBool,
    Optional: true,
    Default:  "foo",
    Description: "Available `foo`, `bar`.",
  },
}
```

假设 `create_strategy` 仅作为创建时传入的只写参数，创建后无法获取，那么这个参数在导入的时候， Value 为空，会导致比对默认值 `foo` 时产生 `+diff`，所以在实现导入的时候，应该主动设置为它的默认值：
``` go
&schema.Resource{
  Importer: &schema.ResourceImporter{
    // helper.ImportWithDefaultValue 在 provider 已封装，可以直接使用
    State: helper.ImportWithDefaultValue(map[string]interface{}{
      "create_strategy": "foo",
    }),
  },
```

## 避免自行约束入参

以 CVM 为例，[购买实例](https://www.tencentcloud.com/document/product/213/33237) API 文档中，对数据盘的入参有如下说明：
<table>
<tr>
<td rowspan="1" colSpan="1" ><b>参数名称</b></td><td rowspan="1" colSpan="1" ><b>是否必填</b></td><td rowspan="1" colSpan="1" ><b>数据类型</b></td><td rowspan="1" colSpan="1" ><b>参数说明</b></td>
</tr><tr>
<td rowspan="1" colSpan="1" >DataDisks.N</td><td rowspan="1" colSpan="1" >否</td><td rowspan="1" colSpan="1" >Array of DataDisk</td><td rowspan="1" colSpan="1" >实例数据盘配置信息。若不指定该参数，则默认不购买数据盘。支持购买的时候指定21块数据盘，其中最多包含1块LOCAL_BASIC数据盘或者LOCAL_SSD数据盘，最多包含20块CLOUD_BASIC数据盘、CLOUD_PREMIUM数据盘或者CLOUD_SSD数据盘。</td>
</tr>
</table>


通过参数可知，数据盘最多支持21块数据盘。通常在 schema 中做如下约束：
``` go
map[string]*schema.Schema{
  "data_disks": {
    Type: schema.TypeList,
    Optional: true,
    Description: "数据盘配置",
      
    MaxItems: 21,
  },
}
```

但不推荐您使用该约束。因为参数限制会根据产品实际情况不定期地更新。假设因为业务拓展，CVM 支持硬盘数超过21块，那么 Terraform 也要被动地进行同步，这些校验滞后的问题积累起来会给开发者和用户造成影响。  
您需要尽量避免此类参数设置输入限制，可以改为在 `Description` 中说明，因为异常输入会被云 API 拦截，Terraform 无需额外加这一层校验。

## 嵌套结构体设计

### TypeList 块和 TypeMap

TypeList 子项支持数字、字符等基本类型。如下所示：
``` hcl
resource "foo" "bar" {
  strs = ["a", "b", "c"]
  nums = [1, 2, 3]
}
```

同时也支持复合 Object 以及嵌套。如下所示：
``` hcl
resource "foo" "bar" {
  list_item {
    name = "l1" # foo.bar.list_item.0.name
  }
  list_item {
    name = "l2" # foo.bar.list_item.1.name
    sub_item {
      name = "l-2-1" # foo.bar.list_item.1.sub_item.0.name
    }
  }
}
```

代码中声明和获取的示例如下：
``` go
var s = map[string]*schema.Schema{
  "list_item": {
    Type: schema.TypeList,
    Elem: &schema.Resource{
      Schema: map[string]*schema.Schema{
        "sub_item": {
          Type: schema.TypeList,
        },
      },
    },
  },
}

func create(d *schema.ResourceData) {
  listItems := d.Get("list_item").([]interface{})
  listItem1 := listItems[1].(map[string]interface{})
  listItem1Sub := listItem1["sub_item"].([]interface{})[0].(map[string]interface{})
}
```

TypeMap 与TypeList 的区别是 TypeMap 在代码 schema 中不支持嵌套，且参数和花括号之间要用等号 `=` 衔接。如下所示：
``` hcl
resource "foo" "bar" {
  map_item = {
    key1: "1", # foo.bar.map_item.key1
    key2: "2"  # foo.bar.map_item.key2
  }
}
```
``` go
var s = map[string]*schema.Schema{
  "map_item": {
    Type: schema.TypeMap,
    Optional: true,
    // Elem: Map 不支持定义 Elem, sdk v1 中无效，v2 中会抛出异常 
  },
}

func create(d *schema.ResourceData) {
  mapItem := d.Get("map_item").(map[string]interface{})
  mapVal1 := mapItem["key1"].(string)
}
```

由于 TypeList 的类型约束更完整，如果您需要实现嵌套类型的参数，建议您优先使用 TypeList。而 Map 适合扁平的键值对，如 Tag 标签。

### TypeSet

TypeSet 是一种特殊的 TypeList ，用法和 TypeList 完全相同，但是具有唯一性和无序性。
``` hcl
resource "foo" "bar" {
  set_list = ["a", "b", "c", "c"] # 实际为 ["a", "b", "c"]
}

resource "foo" "bar_update" {
  set_list = ["c", "b", "a"] # 等效于 ["a", "b", "c"] ，不会产生 Diff
}
```

代码中 schema 可以自定义 `Get` 函数，返回唯一索引，只要索引相同则视为元素相同。如下所示：
``` go
var s = map[string]*schema.Schema{
  "set_list": {
    Type: schema.TypeList,
    Elem: &schema.Schema{Type: schema.TypeString},
    Get: func(v interface) { return getValueHash(v.(string)) },
  },
}

func create(d *schema.ResourceData) {
  setList := d.Get("set_list").(*schema.Set).List()
  setListItemHead := listItems[0].(string)
}
```



