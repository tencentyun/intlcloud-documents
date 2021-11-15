
<span id="yufa"></span>
## CAM Policy Syntax
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


<span id="caozuo"></span>
## TDSQL-A for PostgreSQL Operations
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with `name/tdapg:` should be used for TDSQL-A for PostgreSQL. To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["name/tdapg:action1","name/tdapg:action2"]
```
You can also specify multiple operations by using a wildcard. For example, you can specify all operations beginning with "Describe" in the name as shown below:
```
"action":["name/tdapg:Describe*"]
```
If you want to specify all operations in TDSQL-A for PostgreSQL, use the `*` wildcard as shown below:
```
"action":["name/tdapg:*"]
```

<span id="lujing"></span>
## TDSQL-A for PostgreSQL Resource Path
Each CAM policy statement has its own applicable resources.
Resource paths are generally in the following format:
```
qcs:project_id:service_type:region:account:resource
```
- **qcs**: is the abbreviation of `qcloud service` and indicates that the resource is a Tencent Cloud resource. It is required.
- **project_id**: describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type**: describes the product abbreviation such as `tdapg`.
- **region**: describes the region information, such as `bj`.
- **account**: describes the root account of the resource owner, such as `uin/12345678`.
- **resource**: describes the detailed resource information of each product, such as `instance/instance_id` or `instance/*`.
