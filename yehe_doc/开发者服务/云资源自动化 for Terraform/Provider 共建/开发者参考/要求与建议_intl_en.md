## Resource Constraint

This is an open-source project for both individual and team developers, and we welcome code contribution. Please observe the following rules for more efficient communication and development as well as a better user experience:
- Output product details, field lists, and corresponding APIs.

- Expose TencentCloud APIs for CRUD operations as required by products (at least the APIs for creation and deletion must be supported).

- Unique IDs or values such as names and SNs must be returned after resources are created.

- Input arguments must be able to be queried to ensure that the configuration and actual resource state are consistent.

- You must provide unit tests and ensure that they are passed.

- Single-responsibility principle: Do only one thing per change and avoid relying on or affecting other changes.


## Using `ForceNew` with Caution

If the `ForceNew` field is set, **the resource will be terminated and recreated** if a change is found. If you need to set it, make sure that the local input is consistent with the remote state; otherwise, a `Diff` will be generated, leading to resource termination and recreation after creation.

## Default Value of `Import`

Certain resources define default values:
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

If `create_strategy` is a write-only parameter which is passed in during creation and cannot be obtained after creation, and its value is left empty during import, `+diff` will be generated after comparison with the default value `foo`. Therefore, you need to set it to the default value during import:
``` go
&schema.Resource{
  Importer: &schema.ResourceImporter{
    // `helper.ImportWithDefaultValue` is encapsulated in the provider and can be used directly.
    State: helper.ImportWithDefaultValue(map[string]interface{}{
      "create_strategy": "foo",
    }),
  },
```

## Avoiding Constraining an Input Parameter

Taking a CVM instance as an example, the API documentation [Creating Instance](https://www.tencentcloud.com/document/product/213/33237) describes the input parameter for data disks as follows:
<table>
<tr>
<td rowspan="1" colSpan="1" ><b>Parameter</b></td><td rowspan="1" colSpan="1" ><b>Required</b></td><td rowspan="1" colSpan="1" ><b>Type</b></td><td rowspan="1" colSpan="1" ><b>Description</b></td>
</tr><tr>
<td rowspan="1" colSpan="1" >DataDisks.N</td><td rowspan="1" colSpan="1" >No</td><td rowspan="1" colSpan="1" >Array of DataDisk</td><td rowspan="1" colSpan="1" >The configuration information of instance data disks. If this parameter is not specified, no data disks are purchased by default. Up to 21 data disks can be purchased, including up to one `LOCAL_BASIC` or `LOCAL_SSD` data disk and up to 20 `CLOUD_BASIC`, `CLOUD_PREMIUM`, or `CLOUD_SSD` data disks.</td>
</tr>
</table>


The parameter indicates that up to 21 data disks are supported. The schema usually has the following constraint:
``` go
map[string]*schema.Schema{
  "data_disks": {
    Type: schema.TypeList,
    Optional: true,
    Description: "Data disk configuration",
      
    MaxItems: 21,
  },
}
```

The constraint is not recommended, as the parameter limit will be irregularly updated based on the product situation. If CVM supports more than 21 data disks after business expansion, Terraform needs to sync the update passively. Such verification delays may adversely affect developers and users.  
Instead of setting limits for such parameters, you can use `Description`. Abnormal inputs will be blocked by TencentCloud API, and Terraform does not require this additional layer of verification.

## Nested Structure Design

### `TypeList` block and `TypeMap`

`TypeList` items support basic types such as numbers and characters:
``` hcl
resource "foo" "bar" {
  strs = ["a", "b", "c"]
  nums = [1, 2, 3]
}
```

The complex `Object` and nesting are also supported:
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

Below is the sample code for declaration and acquisition:
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

`TypeMap` differs from `TypeList` in that it does not support nesting in the code schema and requires connecting parameters and braces ({}) with `=` as follows:
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
    // `Elem: Map` does not support defining `Elem`. It is invalid in the SDK v1 and will cause an error in the SDK v2. 
  },
}

func create(d *schema.ResourceData) {
  mapItem := d.Get("map_item").(map[string]interface{})
  mapVal1 := mapItem["key1"].(string)
}
```

`TypeList` is recommended for implementing parameters of the nested type as it has more comprehensive constraints than `TypeMap`, which is more suitable for flat key-value pairs such as tags.

### TypeSet

`TypeSet` is a special ` TypeList`. It is used in the same way as `TypeList` but is unique and orderless.
``` hcl
resource "foo" "bar" {
  set_list = ["a", "b", "c", "c"] # It is ["a", "b", "c"] actually.
}

resource "foo" "bar_update" {
  set_list = ["c", "b", "a"] # It is equivalent to ["a", "b", "c"] and will not generate the `Diff`.
}
```

The code schema can define the `Get` function that returns a unique index. The same index indicates the same element as follows:
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



