## Basic Information
| Product Name | Abbreviation in CAM | Authorization Granularity |
| -------------- | ------------------------------------------------------------ |-------------- |
| International Partners | Intlpartnersmgt | Operation level |

<dx-alert infotype="explain" title="">
The authorization granularity of Tencent Cloud products includes service, operation, and resource levels.

- Service level: It defines whether a user is authorized to access the service as a whole. A user can have either full access or no access to the service. For Tencent Cloud products with the service-level authorization granularity, permissions cannot be authorized to their specific APIs.
- Operation level: It defines whether a user is authorized to call a specific API of a service. For example, granting an account read-only access to vouchers is an operation-level authorization.
- Resource level: It is the finest authorization granularity that defines whether a user is authorized to access specific resources. For example, granting an account read/write access to a specific voucher is a resource-level authorization. The Tencent Cloud product that supports resource-level APIs will be considered to have used resource-level authorization granularity.
</dx-alert>

## API Authorization Granularity
- Resource-level API: It supports the authorization of a specific resource.
- Operation-level API: It doesn't support the authorization of a specific resource.

For authentication through a resource-level API, the Tencent Cloud product will deliver the six-segment format of the specific resource to CAM for authentication, thereby supporting authorization and authentication of the specific resource.
For authentication through an operation-level API, the Tencent Cloud product will not pass the six-segment format of a specific resource to CAM for authentication but an asterisk (`*`) that indicates all resources. If a resource is specified in the policy syntax during authorization but not passed through the API for authentication, CAM will determine that the API is out of the authorization scope and therefore has no permissions.
