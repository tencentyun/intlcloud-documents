
## [CAM Policy Syntax](id:yufa)
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
- **version** is required. Currently, only the value "2.0" is allowed.
- **statement** describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.
 - **effect** is required. It describes the result of a statement. The result can be "allow" or an "explicit deny".
 - **action** is required. It describes the allowed or denied operation. An operation can be an API or a feature set (a set of specific APIs prefixed with "permid").
 - **resource** is required. It describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product.
 - **condition** is required. It describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address. Some services allow you to specify additional values in a condition.

## [CTSDB Operations](id:caozuo)
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with `name/ctsdb:` should be used for CTSDB. To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["name/ctsdb:action1","name/ctsdb:action2"]
```
You can also specify multiple operations by using a wildcard. For example, you can specify all operations beginning with "Describe" in the name as shown below:
```
"action":["name/ctsdb:Describe*"]
```
If you want to specify all operations in CTSDB, use the `*` wildcard as shown below:
```
"action":["name/ctsdb:*"]
```

## [CTSDB Resource Path](id:lujing)
Each CAM policy statement has its own applicable resources.
Resource paths are generally in the following format:
```
qcs:project_id:service_type:region:account:resource
```
- **qcs**: is the abbreviation of `qcloud service` and indicates that the resource is a Tencent Cloud resource. It is required.
- **project_id**: describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type**: describes the product abbreviation such as `ctsdb`.
- **region**: describes the region information, such as `bj`.
- **account**: describes the root account of the resource owner, such as `uin/12345678`.
- **resource**: describes the detailed resource information of each product, such as `instance/instance_id` or `instance/*`.
