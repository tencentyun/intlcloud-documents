Resource-Level permission can be used to specify which resources a user can manipulate. Most APIs of Private DNS support resource-level authorization to allow users to operate on specific private domains.

## Private DNS Resources That Can Be Authorized in CAM

| Resource Type | Six-Segment Resource Format |
|---------|---------|
| Private domain | `qcs::privatedns::$accountid:zone/$zoneId` |

Here:
 - `$accountid` should always be the `AccountId` of the resource owner or left empty.
 - `$zoneId` should always be the ID of a specific private domain. If you want to authorize all private domains, you can enter `*`.


## Private DNS Operations That Can Be Authorized in CAM
| API Operation | API Description | Resource Path |
|---------|---------|---------|
|DescribeUserConfig | Gets current user configuration | * |
|DescribeAuditLog | Gets the list of operation logs | `qcs::privatedns::zone/${ZoneId}` |
|DescribePrivateZoneList | Gets the list of private domains | `qcs::privatedns::zone/${ZoneId}` |
|ModifyPrivateZoneVpc | Modifies VPC associated with private domain | `qcs::privatedns::zone/${ZoneId}` |
|DeletePrivateZoneRecord| Deletes DNS record for private domain | `qcs::privatedns::zone/${ZoneId}` |
|ModifyPrivateZoneRecord | Modifies DNS record for private domain |`qcs::privatedns::zone/${ZoneId}` |
|DeletePrivateZone| Deletes private domain | `qcs::privatedns::zone/${ZoneId}` |
|DescribeRequestData | Gets the DNS request volume of private domain | `qcs::privatedns::zone/${ZoneId}` |
|DescribePrivateZone| Gets private domain information | `qcs::privatedns::zone/${ZoneId}` |
|DescribePrivateZoneRecordList | Gets the list of records for private domain | `qcs::privatedns::zone/${ZoneId}` |
|ModifyPrivateZone | Modifies private domain | `qcs::privatedns::zone/${ZoneId}` |
|CreatePrivateZoneRecord| Adds DNS record for private domain | `qcs::privatedns::zone/${ZoneId}` |
|DescribeDashboard| Gets the overview of Private DNS | * |
|DescribePrivateZoneService| Queries Private DNS activation status | * |
|SubscribePrivateZoneService| Activates Private DNS | * |
|ModifyUserConfig| Modifies current user configuration | * |
|CreatePrivateZone| Creates private domain | * |
