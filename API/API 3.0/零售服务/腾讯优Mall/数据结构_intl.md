## CameraPersonInfo

Visitor attributes captured by camera

Referenced by: DescribeCameraPerson.

| Name | Type | Description |
|------|------|-------|
| TempId | String | Temporary id, returned if face ID hasn't been generated yet |
| FaceId | Integer | Face id |
| IdType | Integer | Determine which ID returned this time is valid; 1 - FaceId, 2 - TempId |
| FacePic | String | Base encoding of the face photo captured this time|
| Time | Integer | Current capture timestamp |

## GenderAgeTrafficDetail

Visitor traffic information in gender/age groups

Referenced by: DescribeShopTrafficInfo.

| Name | Type | Description |
|------|------|-------|
| Gender | Integer | Gender: 0 for male, 1 for female |
| AgeGap | String | Age group; enumeration values: 0-17, 18-23, 24-30, 31-40, 41-50, 51-60, >60 |
| TrafficCount | Integer | Number of visitors |

## HourTrafficInfoDetail

Hourly visitor traffic details

Referenced by: DescribeShopHourTrafficInfo.

| Name | Type | Description |
|------|------|-------|
| Hour | Integer | Hour; values: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23 |
| HourTrafficTotalCount | Integer | Number of hourly visitors |

## NetworkHistoryInfo

Output of queried network status history data

Referenced by: DescribeHistoryNetworkInfo.

| Name | Type | Description |
|------|------|-------|
| Count | Integer | Total number |
| CompanyId | String | Company ID |
| ShopId | Integer | Shop ID |
| Province | String | Shop province |
| City | String | Shop city |
| ShopName | String | Shop name |
| Infos | Array of [NetworkInfoNoShop](#NetworkInfoNoShop) | Network information |

## NetworkInfo

Network status

Referenced by: DescribeNetworkInfo.

| Name | Type | Description |
|------|------|-------|
| CompanyId | String | Company ID |
| ShopId | Integer | Shop ID |
| Province | String | Shop province |
| City | String | Shop city |
| ShopName | String | Shop name |
| Upload | Float | Upload bandwidth in Mb/s; -1: unknown |
| Download | Float | Download bandwidth in Mb/s; -1: unknown |
| MinRtt | Float | Minimum delay in ms; -1: unknown |
| AvgRtt | Float | Average delay in ms; -1: unknown |
| MaxRtt | Float | Maximum delay in ms; -1: unknown |
| MdevRtt | Float | Average deviation delay in ms; -1: unknown |
| Loss | Float | Packet loss percentage; -1: unknown |
| UpdateTime | Integer | Update timestamp |
| Mac | String | Device reporting network status |

## NetworkInfoNoShop

Network status without shop information

Referenced by: DescribeHistoryNetworkInfo.

| Name | Type | Description |
|------|------|-------|
| Upload | Float | Upload bandwidth in Mb/s; -1: unknown |
| Download | Float | Download bandwidth in Mb/s; -1: unknown |
| MinRtt | Float | Minimum delay in ms; -1: unknown |
| AvgRtt | Float | Average delay in ms; -1: unknown |
| MaxRtt | Float | Maximum delay in ms; -1: unknown |
| MdevRtt | Float | Average deviation delay in ms; -1: unknown |
| Loss | Float | Packet loss percentage; -1: unknown |
| UpdateTime | Integer | Update timestamp |
| Mac | String | Device reporting network status |

## NetworkLastInfo

To get the latest network status data of the current shop

Referenced by: DescribeNetworkInfo.

| Name | Type | Description |
|------|------|-------|
| Count | Integer | Total number |
| Infos | Array of [NetworkInfo](#NetworkInfo) | Network status |

## PersonInfo

Visitor information

Referenced by: DescribePersonInfo.

| Name | Type | Description |
|------|------|-------|
| PersonId | Integer | Visitor ID |
| PersonPicture | String | Base64 content of a face photo; deprecated; null returned by default |
| Gender | Integer | Gender: 0 for male, 1 for female |
| Age | Integer | Age |
| PersonType | Integer | Identity type: 0 - ordinary visitor, 1~10 - blacklist, 11~20 - whitelist, 11 - sales associate |
| PersonPictureUrl | String | Face photo URL, which can be accessed and downloaded before expiry |

## PersonTagInfo

To modify visitor attribute parameters

Referenced by: ModifyPersonTagInfo.

| Name | Type | Required | Description |
|------|------|----------|------|
| OldType | Integer | Yes | Visitor's old type |
| NewType | Integer | Yes | Visitor's new type |
| PersonId | Integer | Yes | Visitor's face ID |

## PersonVisitInfo

Visit details

Referenced by: DescribePersonVisitInfo.

| Name | Type | Description |
|------|------|-------|
| PersonId | Integer | Visitor ID |
| VisitId | Integer | Visit ID |
| InTime | Integer | Visit time: Unix timestamp |
| CapturedPicture | String | Base64 content of a captured headshot; deprecated; null returned by default |
| MaskType | Integer | Mask type: 0 - without mask, 1 - with mask |
| GlassType | Integer | Glasses type: 0 - without glasses, 1 - regular glasses, 2 - sunglasses |
| HairType | Integer | Hairstyle: 0 - short hair, 1 - long hair |
| CapturedPictureUrl | String | URL of captured headshot; which can be accessed and downloaded before expiry |

## ShopDayTrafficInfo

Shop visitor traffic list information

Referenced by: DescribeShopTrafficInfo.

| Name | Type | Description |
|------|------|-------|
| Date | Date | Date |
| DayTrafficTotalCount | Integer | Number of visitors |
| GenderAgeTrafficDetailSet | Array of [GenderAgeTrafficDetail](#GenderAgeTrafficDetail) | Visitor traffic information in gender/age groups |

## ShopHourTrafficInfo

Hourly visitor traffic information

Referenced by: DescribeShopHourTrafficInfo.

| Name | Type | Description |
|------|------|-------|
| Date | Date | Date in yyyy-MM-dd format |
| HourTrafficInfoDetailSet | Array of [HourTrafficInfoDetail](#HourTrafficInfoDetail) | Hourly visitor traffic details |

## ShopInfo

A company's shop information

Referenced by: DescribeShopInfo.

| Name | Type | Description |
|------|------|-------|
| CompanyId | String | Company ID |
| ShopId | Integer | Shop ID |
| ShopName | String | Shop name |
| ShopCode | String | Shop code |
| Province | String | Province |
| City | String | City |
| CompanyName | String | Company name |

## ZoneTrafficInfo

Zone-specific visitor traffic information in a shop

Referenced by: DescribeZoneTrafficInfo.

| Name | Type | Description |
|------|------|-------|
| Date | Date | Date |
| ZoneTrafficInfoDetailSet | Array of [ZoneTrafficInfoDetail](#ZoneTrafficInfoDetail) | Zone-specific visitor traffic details in a shop |

## ZoneTrafficInfoDetail

Zone-specific visitor traffic details in a shop

Referenced by: DescribeZoneTrafficInfo.

| Name | Type | Description |
|------|------|-------|
| ZoneId | Integer | Zone ID |
| ZoneName | String | Zone name |
| TrafficTotalCount | Integer | Number of visitor |
| AvgStayTime | Integer | Average stay time |


