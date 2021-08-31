## Overview
TCR provides container image hosting and distribution services to enterprise users and personal users. The Personal Edition provides users with simple and free basic services, that is, the image repository in TKE.
To provide users with more standardized interface definitions and significantly reduced access delay API services, the APIs of the original Personal Edition image repository (CCR) has been upgraded from version 2.0 to the latest version 3.0, and the API name and authorization solutions have updated accordingly. This document describes the mappings between the new and legacy APIs after the upgrade of the APIs that support resource-level authentication and how to use the new authorization solution.

## Mappings Between the v2.0 and v3.0 APIs
| API Name of v2.0 | API Name of v3.0 | Description | Latest Resource Description Method |
| :-------------------- | :------------------------------ | :----------------------- | :------------------------------------------------ |
| CreateCCRNamespace | CreateNamespacePersonal | Creates a namespace of Personal Edition | `qcs::tcr:$region:$account:repo/$namespace` |
| DeleteUserNamespace | DeleteNamespacePersonal | Deletes a namespace of Personal Edition | `qcs::tcr:$region:$account:repo/$namespace` |
| GetUserRepositoryList | DescribeRepositoryOwnerPersonal | Queries all repositories of Personal Edition | `qcs::tcr:$region:$account:repo/*` |
| CreateRepository | CreateRepositoryPersonal | Creates an image repository of Personal Edition | `qcs::tcr:$region:$account:repo/$namespace/$repo` |
| DeleteRepository | DeleteRepositoryPersonal | Deletes an image repository of Personal Edition | `qcs::tcr:$region:$account:repo/$namespace/$repo` |
| BatchDeleteRepository | BatchDeleteRepositoryPersonal | Deletes image repositories of Personal Edition in batches | `qcs::tcr:$region:$account:repo/$namespace/*` |
| DeleteTag | DeleteImagePersonal | Deletes the repository tag of Personal Edition | `qcs::tcr:$region:$account:repo/$namespace/$repo` |
| BatchDeleteTag | BatchDeleteImagePersonal | Deletes the repository tags of Personal Edition in batches | `qcs::tcr:$region:$account:repo/$namespace/$repo` |
| pull | PullRepositoryPersonal | Pulls the images in the image repository of Personal Edition | `qcs::tcr:$region:$account:repo/$namespace/$repo` |
| push | PushRepositoryPersonal | Pushes the images in the image repository of Personal Edition | `qcs::tcr:$region:$account:repo/$namespace/$repo` |

## Mappings Between the legacy and new Authorization Solutions
Due to the upgrade and update of the product name and API version, the original resource description methods and actions of the TCR Personal Edition have been updated accordingly. Please use the latest resources and action authorization solutions while using the v3.0 APIs.
During the upgrade of APIs, CAM APIs will be compatible with both the legacy and new resource description methods and actions to ensure that the custom policies are still effective. To make it easier for you to manage the APIs and authorization solutions uniformly, we recommend that you upgrade the authorization solution to the latest version. For more information, please see [Example of Authorization Solution of the Personal Edition](https://intl.cloud.tencent.com/document/product/1051/37250).

### The legacy resource-level authorization solution
- **Action**: use `ccr` as the product prefix, and the API name is version 2.0. For example, create a namespace as `ccr:CreateCCRNamespace`.
- **Resource description**: use `ccr` as the product name, and there is only a `repo` resource type. For example, to describe the image repository `repo-b` under the namespace `namespace-a`, it would be `qcs::ccr:::repo/namespace-a/repo-b`. If `$region` and `$account` are left empty, all regions will be used by default, and the account will be the root account of the CAM user who created the policy by default.
For more information on authorization solution, see [TKE Image Registry Resource-level Permission Settings](https://intl.cloud.tencent.com/document/product/457/11527).

### The new resource-level authorization solution
- **Action**: use `tcr` as the product prefix, and the API name is version 3.0. For example, create a namespace of Personal Edition as `tcr:CreateNamespacePersonal`.
- **Resource description**: use `tcr` as the product name, and there are three resource types: `instance`, `repository` and `repo`. Among them, `repo` is a dedicated resource type of the Personal Edition. For example, to describe the image repository `repo-b` under the namespace of Personal Edition `namespace-a`, it would be `qcs::tcr:$region:$account:repo/namespace-a/repo-b`. If `$region` and `$account` are left empty, all regions will be used by default, and the account will be the root account of the CAM user who created the policy by default.
For more information on authorization solution, see [CAM APIs for Personal Edition](https://intl.cloud.tencent.com/document/product/1051/39861) and [Example of Authorization Solution of the Personal Edition](https://intl.cloud.tencent.com/document/product/1051/37250).

### The compatible example of legacy and new authorization solutions
For example, the authorized sub-account can read the image repository of `repo-b` (an image repository of Personal Edition) under the namespace `namespace-a` in the default region. Then this account can only query the repository information and pull the image in the repository, but cannot modify the repository attributes, push images, and delete the repository.
 - **Legacy authorization solution:**
 ```
    {
        "version": "2.0",
        "statement": [{
            "action": [
                "ccr:pull"
            ],
            "resource": "qcs::ccr:::repo/namespace-a/repo-b",
            "effect": "allow"
        }]
    }
 ```
 - **New authorization solution:**
    ```
    {
        "version": "2.0",
        "statement": [{
            "action": [
                "tcr:PullRepositoryPersonal"
            ],
            "resource": "qcs::tcr:::repo/namespace-a/repo-b",
            "effect": "allow"
        }]
    }
    ```


