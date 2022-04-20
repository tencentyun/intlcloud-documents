<span id = "celueyufa"></span>
## Policy Syntax
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
- **version** is required. Currently, only the value "2.0" is allowed.
- **statement** describes the details of one or more permissions. It contains a permission or permission set of multiple other elements such as `effect`, `action`, `resource`, and `condition`. One policy has only one `statement`.
 - **action** is required. It describes the allowed or denied action (operation). An operation can be an API (prefixed with "name") or a feature set (a set of specific APIs prefixed with "permid").
 - **resource** is required. It describes the details of authorization. A resource is described in a six-segment format. Detailed resource definitions vary by product. For more information on how to specify resources, please see the product documentation corresponding to the resource statement you are writing.
 - **condition** is optional. It describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value can be a client IP.
 - **effect** is required. It describes the result of a statement. The result can be "allow" or an "explicit deny".

<span id = "caozuo"></span>
## ASR Operations
In a CAM policy statement, you can specify any API operation from any service that supports CAM. APIs prefixed with `name/asr:` should be used for ASR, such as `name/asr:CreateModel` or `name/asr:CreateAsrVocab`.
- To specify multiple operations in a single statement, separate them with commas as shown below:
```
"action":["name/asr:action1","name/asr:action2"]
```
You can also specify multiple operations by using a wildcard. For example, you can specify all operations beginning with "Describe" in the name as shown below:
```
"action":["name/cvm:Describe*"]
```
- To specify all operations in ASR, use the `*` wildcard as shown below:
```
"action":["name/asr:*"]
```

<span id = "ziyuanlujing"></span>
## ASR Resource Path
Each CAM policy statement has its own applicable resources generally in the following format:
```
qcs:project_id:service_type:region:account:resource
```
- **project_id** describes the project information, which is only used to enable compatibility with legacy CAM logic and can be left empty.
- **service_type** describes the product abbreviation such as `asr`.
- **region** describes the region information, which is not required for ASR.
- **account** describes the root account of the resource owner, such as `uin/164256472`.
- **resource** describes the detailed resource information of each product, such as `model/model_id1` or `model/*`.

For example, you can use a specific self adaptive learning model (15b96676edb211ea9301b49691037310) by specifying it in the statement as shown below:
```
"resource":[ "qcs::asr::uin/164256472:model/15b96676edb211ea9301b49691037310"]
```
You can also use the `*` wildcard to specify all self adaptive learning models that belong to a specific account as shown below:
```
"resource":[ "qcs::asr::uin/164256472:model/*"]
```
If you want to specify all resources or a specific API operation supports only API-level permission control, you can use the `*` wildcard in the `resource` element as shown below:
```
"resource": ["*"]
```
To specify multiple resources in one policy, separate them with commas. In the following example, two resources are specified:
```
"resource":["resource1","resource2"]
```
The table below describes the resources that can be used by ASR and the corresponding resource description methods, where words prefixed with `$` are placeholders and `account` refers to an account ID.

| Resource | Resource Description Method in Authorization Policy |
|---------|---------|
| Self adaptive learning model | `qcs::asr::$account:model/$ModelId` |
| Keyword list | `qcs::asr::$account:vocab/$VocabId` |
