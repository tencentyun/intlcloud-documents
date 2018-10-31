## Description

CAS APIs are lightweight APIs without connection status. You can call these APIs to send requests and receive responses directly via http/https, in order to interact with the backend of Tencent Cloud CAS. The request and response contents for CAS APIs are in JSON format.

See Verification and Authentication for details before reading other API documents.

## Basic Information

This section explains the key concepts and terms that you must understand to use CAS efficiently.

| Name | Description |
| ---------- | ---------------------------------------- |
| APPID (UID) | The user ID assigned to each developer when he or she accesses the CAS service. Each user has a UID to record the account to which the resources belong. |
| secret_id | The identity ID owned by a developer, which is used for identity authentication |
| SecretKey   | The identity key owned by a developer |
| Vault | The container for storing archives and the first-level directory under a user's UID. All archives are stored in vaults. |
| Archive | A file stored in CAS, which is the basic storage unit. |
| Region     | Region information in the domain name. Enumerated values: ap-chengdu, ap-beijing, ap-guangzhou, and ap-shanghai. |
| Job        | Job instance used to obtain archives. You can obtain the data stored in CAS by initiating download jobs. |

## Naming Rules

When you create a vault, the vault name is required. The naming rules of a vault are as follows:

-  The name should be a combination of 1-255 characters.
-  Allowed characters are `a-z`, `A-Z`, `0-9`, `_`, `-` and `.`.




## Getting Started

Follow the steps below before using CAS APIs:

1. Obtain Uid, SecretID and SecretKey.
2. Download the SDK and write an algorithm program for signature authentication (or use a server SDK).
3. Compute the signature and call the APIs to perform operations.

