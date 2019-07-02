## BillDetail

BillDetail contains billing details.

Referenced by the API DescribeBillDetail.

| Name | Type | Description |
|------|------|-------|
| BusinessCodeName | String | Product name |
| ProductCodeName | String | Sub-product name |
| PayModeName | String | Billing method |
| ProjectName | String | Project name |
| RegionName | String | Region |
| ZoneName | String | Availability zone |
| ResourceId | String | Resource instance ID |
| ResourceName | String | Instance name |
| ActionTypeName | String | Transaction type |
| OrderId | String | Order ID |
| BillId | String | Transaction ID |
| PayTime | Timestamp | Payment time |
| FeeBeginTime | Timestamp | Service start time |
| FeeEndTime | Timestamp | Service end time |
| ComponentSet | Array of [BillDetailComponent](#BillDetailComponent) | Item list |
| PayerUin | String | Payer UIN |
| OwnerUin | String | User UIN |
| OperateUin | String | Operator UIN |

## BillDetailComponent

BillDetailComponent contains a breakdown of the bill. 

Referenced by the API DescribeBillDetail.

| Name | Type | Description |
|------|------|-------|
| ComponentCodeName | String | Item name |
| ItemCodeName | String | Item type |
| SinglePrice | String | Published price of the item |
| SpecifiedPrice | String | Specified price of the item |
| PriceUnit | String | Price unit |
| UsedAmount | String | Item’s usage |
| UsedAmountUnit | String | Item usage unit |
| TimeSpan | String | Usage duration |
| TimeUnitName | String | Duration unit |
| Cost | String | Original price of the item |
| Discount | String | Discount |
| ReduceType | String | Offer type |
| RealCost | String | Total discounted price |
| CashPayAmount | String | Amount paid in cash |


## BillResourceSummary

BillResourceSummary contains information about resources charged in the bill. 

Referenced by the API DescribeBillResourceSummary.

| Name | Type | Description |
|------|------|-------|
| BusinessCodeName | String | Product |
| ProductCodeName | String | Sub-product |
| PayModeName | String | Billing method |
| ProjectName | String | Project |
| RegionName | String | Region |
| ZoneName | String | Availability zone |
| ResourceId | String | Resource instance ID |
| ResourceName | String | Resource instance name |
| ActionTypeName | String | Transaction type |
| OrderId | String | Order ID |
| PayTime | Timestamp | Payment time |
| FeeBeginTime | Timestamp | Service start time |
| FeeEndTime | Timestamp | Service end time |
| ConfigDesc | String | Configuration description |
| ExtendField1 | String | Extended field 1 |
| ExtendField2 | String | Extended field 2 |
| TotalCost | String | Original price in CNY |
| Discount | String | Discount |
| ReduceType | String | Offer type |
| RealTotalCost | String | Total discounted price (USD) |
| CashPayAmount | String | Amount paid in cash (USD) |
| ExtendField3 | String | Extended field 3 |
| ExtendField4 | String | Extended field 4 |
| ExtendField5 | String | Extended field 5 |

## Deal

Deal contains order details.

Referenced by the API DescribeDealsByCond.

| Name | Type | Description |
|------|------|-------|
| OrderId | String | Order number |
| Status | Integer | Order status |
| Payer | String | Payer |
| CreateTime | Timestamp | Creation time |
| Creator | String | Creator |
| RealTotalCost | Integer | Actual payment amount (cent) |
| VoucherDecline | Integer | Amount paid in voucher (cent) |
| ProjectId | Integer | Project ID |
| GoodsCategoryId | Integer | Product category ID |
| ProductInfo | Array of [ProductInfo](#ProductInfo) | Product details |
| TimeSpan | Float | Duration |
| TimeUnit | String | Time unit |
| Currency | String | Currency |
| Policy | Float | Discount |
| Price | Float | Unit price in cent |
| TotalCost | Float | Original price in cent |

## DetailPoint

DetailPoint contains time and value information.

Referenced by the API DescribeDosageDetailByDate.

| Name | Type | Description |
|------|------|-------|
| Time | String | Time |
| Value | String | Value |

## DetailSet

DetailSet contains information about the domain name and usage details.

Referenced by the API DescribeDosageDetailByDate.

| Name | Type | Description |
|------|------|-------|
| Domain | String | Domain name |
| DetailPoints | Array of [DetailPoint](#DetailPoint) | Usage data details |
| InstanceID | String | Instance ID <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## ProductInfo

ProductInfo contains information about product details.

Referenced by the API DescribeDealsByCond.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes |  ID of the product detail |
| Value | String | Yes | Product details |

