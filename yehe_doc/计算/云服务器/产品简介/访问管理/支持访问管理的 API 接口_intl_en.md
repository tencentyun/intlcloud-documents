## Basic information
<table>
<thead>
<tr>
<th>Product Name</th>
<th>Abbreviation</th>
<th>Authorization Granularity</th>
</tr>
</thead>
<tbody><tr>
<td>Cloud Virtual Machine</td>
<td>CVM</td>
<td>Resource-level</td>
</tr>
</tbody></table>


<dx-alert infotype="explain" title="">
Three authorization granularity levels are supported by the Tencent Cloud product: service level, operation level, and resource level.
- **Service level**: It defines whether a user has the permission to access the service as a whole. A user can have either full access or no access to the service. The Tencent Cloud product at the service level doesn't support authorization of specific APIs.
- **Operation level**: It defines whether a user has the permission to call a specific API of the service. For example, granting an account read-only access to the CVM service is an authorization at the operation level.
- **Resource level**: It is the finest authorization granularity which defines whether a user has the permission to access specific resources. For example, granting an account read/write access to a specific CVM instance is an authorization at the resource level. The Tencent Cloud product that supports resource-level API authorization supports resource-level authorization.
</dx-alert>


## API authorization granularity

- **Resource-level API**: It supports the authorization of a specific resource.
- **Operation-level API**: It doesn't support the authorization of a specific resource.

For authentication through a resource-level API, the Tencent Cloud product will deliver the six-segment format of the specific resource to CAM for authentication, thereby supporting authorization and authentication of the specific resource.
For authentication through an operation-level API, the Tencent Cloud product will not deliver the six-segment format of the specific resource to CAM for authentication. Instead, it will deliver the `*` of any resource. To be more specific, if a resource is specified in the policy syntax during authorization but not delivered through the API for authentication, CAM will identify the API as out of the authorization scope, that is, having no permission.


