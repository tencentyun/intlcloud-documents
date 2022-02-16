<span id = "clyf"></span>
### Policy Syntax
CAM policy:
```
{	 
        "version":"2.0", 
        "statement": 
        [ 
           { 
              "effect":"effect", 
              "action":["action"], 
              "resource":["resource"], 
               "condition": {"key":{"value"}} 
           } 
       ] 
} 
```

- **version** is required. Currently, only "2.0" is allowed.
- **statement** describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.
 - **effect** describes whether the statement results is an "allow" or "explicitly deny". This element is required.
 - **action** describes the action (operation) to be allowed or denied. An operation can be an API or a feature set (a set of specific APIs prefixed with `permid`). This element is required.
 - **resource** describes the objects the statement covers. A resource is described in a six-segment format. Detailed resource definitions vary by product. This element is required.
 - **condition** describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. TcaplusDB currently does not support special conditions, so this item is not configurable. This element is required.

<span id = "cz"></span>
### TcaplusDB Operations
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with `name/tcaplusdb:` should be used for TcaplusDB, such as `name/tcaplusdb:DescribeClusters` or `name/tcaplusdb:DeleteCluster`.
To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["name/tcaplusdb:action1","name/tcaplusdb:action2"]
```

You can also specify multiple operations by using a wildcard. For example, you can specify all operations beginning with "Describe" in the name as shown below:
```
"action":["name/tcaplusdb:Describe*"]
```

If you want to specify all operations in TcaplusDB, use a wildcard "*" as shown below:
```
"action":["name/tcaplusdb:*"]
```

<span id = "zylj"></span> 
### TcaplusDB Resource Path

Each TcaplusDB policy statement has its own resources.
Resource paths are generally in the following format:

```
qcs:project_id:service_type:region:account:resource
```

**project_id** describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
**service_type** describes the product abbreviation such as `tcaplusdb`.
**region** describes the [region information](https://intl.cloud.tencent.com/document/product/213/6091), such as ap-shanghai. If a specific resource is specified, there is no need to enter `region`.
**account** is the root account of the resource owner, such as `uin/164xxx472`.
**resource** describes detailed resource information of each product, such as cluster/19168929215 or cluster/\* for cluster resource, where cluster, table group, and table cannot be authenticated in a cascading manner. If you want to control access to all tables or table groups in a specified cluster, you need to configure authentication for the tables or table groups in addition to the cluster. The table below describes the resources that can be used by TcaplusDB and the corresponding resource description methods.


| Resource   | Resource Description Method in Authorization Policy                                     |
| ------ | ------------------------------------------------------------ |
| Cluster    | qcs::tcaplusdb:$region:$account:cluster/$clusterId           |
| Table group | qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId |
| Table    | qcs::tcaplusdb:$region:$account:table/$tableId |

For example, you can specify a resource for a specific cluster (cluster ID: 19168929215) in a statement as shown below:
```
"resource":[ "qcs::tcaplusdb:ap-shanghai:uin/164xxx472:cluster/19168929215"]
```

You can also use the wildcard "*" to specify it for all clusters in the Shanghai region that belong to a specific account as shown below:
```
"resource":[ "qcs::tcaplusdb:ap-shanghai:uin/164xxx472:cluster/*"]
```

If you want to specify all resources or if a specific API operation does not support resource-level permission control, you can use the wildcard "*" in the `resource` element as shown below:
```
"resource": ["*"]
```

To specify multiple resources in a single command, separate them with commas. Below is an example where two clusters are specified:
```
"resource":["qcs::tcaplusdb::uin/164xxx472:cluster/19168929215","qcs::tcaplusdb::uin/164xxx472:cluster/21168929215"]
```
