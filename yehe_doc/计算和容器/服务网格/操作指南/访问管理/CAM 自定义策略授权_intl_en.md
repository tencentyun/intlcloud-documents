
If you have custom permission management requirements, you can create a custom CAM policy and associate it with a sub-account to implement custom authorization. You can perform configuration based on actual service requirements by referring to the following description.

## CAM Element Reference

Core elements of a CAM custom policy include: action, resource, condition, and effect.

### 1. Action

This required element describes allowed or denied actions. An action can be an API (described with a name prefix) or a feature set (a set of specific APIs, described with an actionName prefix). You can view [CAM APIs accessed to Tencent Cloud Mesh](#camApi).

### 2. Resource

This element describes specific data that is to be authorized. A resource is described in six paragraphs. You can view [Tencent Cloud Mesh resource description](#camResource).

### 3. Condition

This element describes the condition for the policy to take effect. A condition consists of operator, action key, and action value. A condition value may contain information such as time and IP address.

### 4. Effect

This required element describes whether the statement results in an **allow** or an explicit **deny**.

### 5. Custom policy sample

This policy defines that it is allowed to obtain details about two mesh instances mesh-abcd1234 and mesh-1234abcd in Guangzhou.

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "resource":[
                "qcs::tcm:gz:uin/1234567:mesh/mesh-abcd1234",
                "qcs::tcm:gz:uin/1234567:mesh/mesh-1234abcd"
            ],
            "action": [
                "name/tcm:DescribeMesh"
            ]
        }
    ]
}
```

- For more information about syntax logic of CAM custom policies, see [CAM Syntax Logic](https://intl.cloud.tencent.com/document/product/598/33415).

## Tencent Cloud Mesh Resources That Can Be Authorized on CAM [](id:camResource)

| Resource | Resource Description Method in Authorization Policy |
| :-------- | -------------- |
| Service mesh |  ` qcs::tcm:$region:$account:mesh/$meshid `  |

It includes the following fields:

- `$region`: describes region information. It is an ID of a region. For example, `gz` is the ID of Guangzhou.
- `$account`: describes root account information about a resource owner. It is expressed in the `uin/${uin}` format, for example, `uin/12345678`. If this field is left blank, it indicates the root account to which the CAM user who creates the policy belongs.
- `$meshid`: describes mesh instance information. It is an ID of a mesh, or is set to `*`.

For information on how to describe resources in authorization policies, see [Resource Description Method](https://intl.cloud.tencent.com/document/product/598/10606).

## CAM APIs That Can Authorize Tencent Cloud Mesh [](id:camApi)

On CAM, you can authorize the following actions for Tencent Cloud Mesh mesh resources:

### Mesh Instance

| API  | Description | Resource |
| :-------- | :--------| :------ |
| CreateMesh|  Creating a service mesh | Mesh resource ` qcs::tcm:$region:$account:mesh/* ` |
| DeleteMesh|  Deleting a service mesh | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |
| DescribeMesh |  Obtaining a specified service mesh | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |
| ListMeshes|  Obtaining a service mesh list | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |
| ModifyMesh|  Modifying service mesh configurations | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |
| UpgradeMesh|  Upgrading a service mesh | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |

### Istio Resource

| API  | Description | Resource |
| :-------- | :--------| :------ |
|  ForwardRequestRead |  Reading Istio CRD resources | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |
| ForwardRequestWrite |  Writing Istio CRD resources | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |

### Service Discovery

| API  | Description | Resource |
| :-------- | :--------| :------ |
|  LinkClusterList |  Associating a cluster with a service mesh instance | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |
| UnlinkCluster |  Disassociating a cluster | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |

### Gateway

| API  | Description | Resource |
| :-------- | :--------| :------ |
| CreateIngressGateway |  Creating an ingress gateway | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |
| DeleteGatewayInstance |  Deleting an ingress gateway | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |
| DescribeIngressGatewayList |  Querying an ingress gateway list | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |
| ModifyIngressGateway | Modifying an ingress gateway | Mesh resource ` qcs::tcm:$region:$account:mesh/$meshid ` |

### Sample Deployment

| API  | Description | Resource |
| :-------- | :--------| :------ |
| CreateTrial |  Creating Tencent Cloud Mesh sample deployment | Authorizing only interfaces `*` |
| DeleteTrial |  Deleting Tencent Cloud Mesh sample deployment | Authorizing only interfaces `*` |
| RetryTrialTask |  Retrying creating Tencent Cloud Mesh sample deployment | Authorizing only interfaces `*` |
