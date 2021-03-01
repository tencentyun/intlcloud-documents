Dedicated tunnel supports resource-level permissions, allowing the user to perform operations or use specific resources.

## Access Policy

Cloud Access Management (CAM) allows you to grant access permissions to the following resources

| Resource Type | Resource Description Method in Access Policies |
| :--------------- | :----------------------------------------------- |
| Dedicated tunnel | qcs::dc::uin/${Uin}/dcx/${DirectConnectTunnelId} |

- Replace `${Uin}` with the resource owner’s AccountId or “*”.
- Replace `${DirectConnectTunnelId}` with the dedicated tunnel ID or “*”.

## Dedicated Tunnel Operations

| API Name                               | API Description             | Six-segment Format                                 |
| --------------------------------------- | -------------------- | ------------------------------------------ |
| CreatePublicDirectConnectTunnel         | Creates an Internet tunnel   | qcs::dc::uin/:dcx/*                        |
| DescribeDirectConnectTunnels            | Obtains the list of dedicated tunnels     | qcs::dc::uin/:dcx/*                        |
| AcceptDirectConnectTunnel               | Accepts a dedicated tunnel         | qcs::dc::uin/:dcx/${DirectConnectTunnelId} |
| DeleteDirectConnectTunnel               | Deletes a dedicated tunnel         | qcs::dc::uin/:dcx/${DirectConnectTunnelId} |
| ModifyDirectConnectTunnelAttribute      | Modifies the dedicated tunnel attributes.     | qcs::dc::uin/:dcx/${DirectConnectTunnelId} |
| CreateDirectConnectTunnel               | Creates a dedicated tunnel        | qcs::dc::uin/:dcx/*                        |
| RejectDirectConnectTunnel               | Rejects an application for a dedicated tunnel     | qcs::dc::uin/:dcx/${DirectConnectTunnelId} |
| DescribePublicDirectConnectTunnelRoutes | Queries the route table of an Internet tunnel | qcs::dc::uin/:dcx/${DirectConnectTunnelId} |
| DescribeDirectConnectTunnelExtra        | Queries the extended information of a dedicated tunnel | qcs::dc::uin/:dcx/${DirectConnectTunnelId} |
| ModifyDirectConnectTunnelExtra          | Modifies the extended information of a dedicated tunnel | qcs::dc::uin/:dcx/${DirectConnectTunnelId} |

