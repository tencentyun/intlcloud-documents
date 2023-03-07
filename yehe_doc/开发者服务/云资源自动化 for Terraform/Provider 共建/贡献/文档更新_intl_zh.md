腾讯云 Provider 的 [文档](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs) ，原文件位于项目根目录 `website` 下，且全部由代码中的注释和 Schema 的描述中提取并自动生成，下文将介绍文档页面中的侧边栏、示例代码和参数描述的生成机制。

## 文档生成

观察文档页面，可以看见页面由以下几个部分组成。

### 目录

在 `tencentcloud/provider.go` 文件顶部注释，以 `Resources List` 开始解析，格式如下：
``` go
/*
Resources List

产品名称
  Data Source
    tencentcloud_foos
    tencentcloud_bars
  Resource
    tencentcloud_baz
    
*/

package tencentcloud
```

以上文本会解析成 `产品名称 -> DataSource / Resource -> tencentcloud_*` 的树形结构，在文档左侧边栏展示。

### 示例

文档的主题页由简介、用法示例和参数说明组成，所有示例都由每个模块的 `.go` 文件头部注释生成，模板如下：
``` go
/*
Provides a resource/datasource to create/query something.

~> **NOTE:** This is an optional TIPS, add it if needed.

Example Usage

Basic usage

   hcl
resource "tencentcloud_foo" "foo" {
  name       = "baz"
}

Another usage

    hcl
resource "tencentcloud_foo" "foo" {
  name = "baz"
  another = 12345
}

Import
This resource can be imported, e.g.

   bash
$ terraform import tencentcloud_foo.foo foo_id

*/
package tencentcloud
// ...
```

首先简单介绍 Resource / DataSource 的用法和注意事项（如果有），接着以 `Example Usage` 起头，附上示例代码块。最后，如果是 Resource 类型且提供了导入方法，就写上导入命令。 

### 参数说明

每个资源下的参数说明都由 `Description` 解析并且紧跟在当前资源的示例代码下：

``` 
map[string]*schema.Schema{
  "name": {
    Type: schema.TypeString,
    Description: "This is what will generated.",
  }
}
```

脚本会通过读取 Provider 中 Schema ，输出格式为 `名称 - (约束, 类型) 介绍文字` 的条目。

## 文档更新

### 主动更新

生成文档的脚本位于 `./gendoc` 下。当上述位置的代码有变更时， cd 到 `./gendoc` 并运行 `go run .../.` 可以执行文档生成操作，也可以直接在项目目录下执行 `make doc`，二者等效。

### 提交检查

如果您配置了项目中的提交 hook，即使没有运行 `gendoc` ，提交 hook 也会自动帮您检查是否同步。如果提交 hook 执行后，文档出现了变更，说明您尚未把改动的文档同步到暂存区，本次提交操作将会中止。即便您绕过 hook，合并检查也会执行这一步骤，取保您涉及到文档的变更能准确同步。

