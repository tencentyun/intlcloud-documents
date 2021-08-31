## Sub-user Key
Use a sub-account to log in to the CAM Console, enter **[TencentCloud API Key](https://console.cloud.tencent.com/capi)**, and find the **sub-user key**, which is used to generate a signature for authentication. Successfully authenticated sub-accounts can access relevant Tencent Cloud resources.

**Role of signature**:
- Authenticate requesting user: the user key is used for authentication.
- Prevent content from being tampered with: the request content is signed with the hash algorithm, so that the system can check whether the content has been tampered with based on signature consistency.
- Prevent replay attacks: the signing information contains the request time and signature time and validity period, which can avoid replay of expired requests. In addition, Tencent Cloud services can reject expired requests based on request time.


## Sample API Calls
### API protocol
- Encoding type: UTF-8
- Encoding format: JSON
- Transfer method: POST
- Request protocol: HTTP

Call specification example:
```
{
	"version": 1,
	"componentName": "MC",
	"eventId": 123456,
	"interface": {
		"interfaceName": "API name",
		"para": {
			Corresponding API parameters
		}
	}
}
```

Returned result:
```
{
	"version": 1,
	"eventId": 123456,
	"componentName": "CONSOLE_LOGICAL_SERVER",
	"returnValue": 0,
	"returnCode": 0,
	"returnMessage": "OK",
	"data": {
		"ownerUin": 123,
		"uin": 124,
		"ownerAppid": 323
	}
}
```
If an error is returned, `returnCode ` will not be 0, and `returnMessage` will be the error message.
For more information on `interfaceName` and `para` in the input parameters and `data` in the output parameters, please see [Call Description](#Call Description).

### API description
For more information on CAM user and permission APIs, please see the [CAM API documentation](https://intl.cloud.tencent.com/document/product/598/35830).

### Sample call
#### Adding policy (CreateCamStrategy)
Policy example: this example shows you how to grant a sub-user (Uin: 3232) permission to list all queues under the account and permission to consume messages and delete messages in batches on `horacetest1` in the Beijing region.

- Field description

| Parameter | Description | Example Value |
|---------|---------|---------|
| strategyName | Policy name. | strategy1 |
| strategyInfo | Policy description (a **JSON string** needs to be passed in here). | For more information, please see [Sample code](#Sample Code 1) |
| remark | Policy remarks. | hello test |
| resource | Six-segment description of CMQ resource, such as `qcs::cmqqueue:bj:uin/1238423:queueName/uin/3232/myqueue`. <br>The first segment is fixed to `qcs`;<br>The second segment is empty;<br>The third segment indicates the message queue type, which is `cmqqueue` for the queue model or `cmqtopic` for the topic model;<br>The fourth segment is the region information, such as gz, bj, and sh. If you want to specify all regions, leave this segment empty;<br>The fifth segment is `uin/{root account uin}` of the root account;<br>The sixth segment is the resource description, which is `queueName/uin/{creator Uin}/{queue name}` for the queue model or `topicName/uin/{creator Uin}/{topic name}` for the topic model. The creator `Uin` can be obtained on the details page in the console or through the returned value `createUin` of the `GetQueueAttributes` or `GetTopicAttributes` API. | * |

- Sample code:<span id="Sample code 1"></span>
```
{
"strategyName":"strategy1",
"strategyInfo":{"version":"2.0","principal":{"qcs":["qcs::cam::uin/1238423:uin/3232/myqueue","qcs::cam::uin/1238423:groupid/13"]},"statement":[{"effect":"allow","action":"name/cmqqueue:ListQueue","resource":"*"},{"effect":"allow","action":["name/cmqqueue:ReceiveMessage","name/cmqqueue:BatchDeleteMessage"],"resource":["qcs::cmqqueue:bj:uin/1238423:queueName/uin/3232/myqueue","qcs::cmqqueue:bj:uin/1238423:queueName/uin/3232/*"]}]},
"remark":"horace test"
}
```
>?The creator ID after `uin/` in the resource description in the sixth segment can be found during policy creation.


#### Associating/Unassociating policy with/from sub-account (OperateCamStrategy)
This API is used to associate/unassociate a policy with/from a user or user group.

- Policy example: this example shows you how to associate a policy (ID: 666) with a user (UIN: 123456).

- Field description:

| Parameter | Description | Example Value |
|---------|---------|---------|
| groupId | If the operation object is a user, set `groupId` to `-1`;<br>If the operation object is a user group, set `groupId` to a specific group ID. | -1 |
| relateUin | If the operation object is a user, set `relateUin` to a specific user `uin`; if the operation object is a user group, set `relateUin` to `-1`. | 123456 |
| strategyId | Target policy ID. | 666 |
| actionType | 1: associates policy; 2: unassociates policy. | 1 |

- Sample code:
```
{
	"groupId":-1,
	"relateUin":123456,
	"strategyId":666,
	"actionType":1
}
```


## Call Description<span id="Call Description"></span>
The following description is applicable to user and permission management in various services. When configuring the CMQ service, please select values for CMQ parameters accordingly:
1. You can leave `principal` empty and associate the user by using the policy associating API.
2. If there is only one element in `principal`, `action`, or `resource`, you do not need to add `[]`.
3. `resource` is generally described in a six-segment format of `qcs:project:serviceType:region:account:resource`.
	- project: you can use `id/0`, `*`, or `id/*` to indicate all projects. If `project` is empty during authorization, the value will be `id/0` by default. If `project` is empty during authentication, it indicates that the resource can exist in all projects. This segment is empty by default.
	- serviceType: valid values include `cos`, `cdn`, `vpc`, etc. `*` indicates all services. You cannot leave this segment empty.
	- region: it specifies the region. If this segment is empty, it indicates all regions. It is empty by default. Valid values include `gz`, `st`, `tj`, `sh`, `hk`, `ca`, `shjr`, and `bj`.
	- account: it can be represented as `uin/${uin}` or `uid/${uid}`. If this segment is empty, it will be populated with `uin/${uin}` for resources of services such as CDN and VPC or with `uid/${uid}` for COS resources. `${uin}` and `${uid}` indicate the `uin` and `uid` of the requester, respectively. This segment is empty by default.
	There is a special case: `uin/-1` is generally used in preset policies. After the extension table is expanded, `-1` will be replaced with the developer `uin`. In addition, preset policies support authorization for sub-accounts and roles only; therefore, you can directly replace `-1` with the `uin` of the root account of the sub-account or role.
	- `resource` consists of `name` and `value`. `name` represents the resource definition in the service; for example, it is described as `queueName` or `topicName` for CMQ, `prefix` for COS, and `host` for CDN. `*` indicates all resources, which will be represented as `*/*` uniformly. This segment cannot be empty.
	- Users and policies are also resources. A CAM root account is described as `qcs::cam::uin/1238423: uin/1238423`, a CAM sub-account is described as `qcs::cam::uin/1238423: uin/3236671`, and an anonymous user is described as `qcs::cam::anonymous:anonymous`.
	- If `resource` is empty, it indicates that no objects need to be associated with the operation, which will be represented as `*` in the system uniformly.
	- The service needs to verify whether the `uin` or `uid` in the resource description is the real resource owner. It is required that the service perform verification after successful authentication. It is recommended to perform verification during authentication as well. 
        
