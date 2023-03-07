The source files of the TencentCloud Provider [documentation page](https://registry.terraform.io/providers/tencentcloudstack/tencentcloud/latest/docs) are in the `website` root directory of the project and are extracted and generated automatically from the code comments and schema description. This document describes the mechanism for generating the sidebar, sample code, and parameter description on the documentation page.

## Documentation Page Generation

The documentation page consists of the following sections.

### Directory

In the `tencentcloud/provider.go` file, the top comment starts with `Resources List` in the following format:
``` go
/*
Resources List

Product name
  Data Source
    tencentcloud_foos
    tencentcloud_bars
  Resource
    tencentcloud_baz
    
*/

package tencentcloud
```

The above text will be parsed into the `Product name -> DataSource / Resource -> tencentcloud_*` tree structure displayed on the left sidebar of the documentation page.

### Sample

The topic page of the documentation consists of the overview, sample use, and parameter description. All samples are generated from the header comments in the `.go` file of each module. Below is a template:
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

First, the resource/data source use and instructions (if any) are presented, followed by the sample code block starting with `Example Usage`. Then, the import command is written if the type is `Resource` and the import method is provided. 

### Parameter description

The parameter description of each resource is parsed from the value of `Description` and closely follows the sample code:

``` 
map[string]*schema.Schema{
  "name": {
    Type: schema.TypeString,
    Description: "This is what will generated.",
  }
}
```

The script will read the `Schema` from the `Provider` to output the `Name - (Constraint, type) introductory text` item.

## Documentation Update

### Active update

The script generating the documentation is in `./gendoc`. If the code in the above location changes, run `cd` to enter `./gendoc` and run `go run .../.` to generate the documentation. Or you can run `make doc` in the project directory.

### Commit for check

If you have configured the commit hook in the project, even if you don't run `gendoc`, the commit hook will automatically check for sync. If the documentation changes after the execution of the commit hook, you haven't synced the changed documentation to the index, and the commit operation will stop. Even if the hook is not configured, the merge check will do the job to ensure that your changes are accurately synced.

