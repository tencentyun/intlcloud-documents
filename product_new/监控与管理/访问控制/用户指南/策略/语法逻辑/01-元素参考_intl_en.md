A policy is made up of elements that describe specific information about authorization. Core elements include `principal`, `action`, `resource`, `condition`, and `effect`. These elements must be lowercase. The order of the elements does not matter. The `condition` element is optional. The `principal` element cannot be used in the console and can only be used through policy management API and policy syntax-related parameters.

### 1. Version

This element defines the version of policy syntax. This element is required. At present, the only available value is "2.0".

### 2. Principal
This element specifies the entity to be authorized by the policy. This includes users (root accounts, sub-accounts, anonymous users). In the future, more entities will be included, such as roles and federated users. This element can only be used in trust policies for roles and COS buckets policies.

### 3. Statement
This element describes the detailed information of one or more permissions. It includes permissions or a permission set of multiple elements such as `action`, `resource`, `condition`, and `effect`. A policy has only one `statement` element.

### 4. Action
This element describes the action to be allowed or denied. An action can be an API (described using the prefix `name`) or a feature set (a set of specific APIs, described using the prefix `permid`). This element is required.

### 5. Resource
This element describes the objects the statement covers. A resource is described using 6-piece format. The detailed resource definition for each product is different. For information on how to specify a resource, see the documentation for the product whose resources you are writing a statement for. This element is required.

### 6. Condition
This element specifies the conditions for when a policy is in effect. A condition consists of condition operators, condition keys, and condition values. A condition value may include information such as time and IP address. In some services, you can specify other types of condition values. This element is optional.

### 7. Effect
This element describes whether the statement results in an **allow** or an explicit **deny**. This element is required.

### 8. Sample Policy
The policy in this example grants sub-account (ID 3232523) of the root account (ID 1238423) permissions to use all COS-read APIs, write objects, and send message queues, for the Beijing region COS bucket "bucketA" and the Guangzhou region COS object "object2" in bucket “bucketB”, when the access IP falls within the IP range of `10.121.2.*`. 
```
{     
        "version":"2.0",
        "statement": 
        [ 
             {  
                    "principal":{"qcs":["qcs::cam::uin/1238423:uin/3232523"]}, 
                    "effect":"allow", 
                    "action":["name/cos:PutObject","permid/280655"], 
                    "resource":["qcs::cos:bj:uid/1238423:prefix//1238423/bucketA/*", 
                                        "qcs::cos:gz:uid/1238423:prefix//1238423/bucketB/object2"], 
                     "condition": {"ip_equal":{"qcs:ip":"10.121.2.10/24"}} 
             }, 
            {  
                 "principal":{"qcs":["qcs::cam::uin/1238423:uin/3232523"]}, 
                 "effect":"allow", 
                 "action":"name/cmqqueue:Sendmessages", 
                 "resource":"*" 
            } 
     ] 
}
```
