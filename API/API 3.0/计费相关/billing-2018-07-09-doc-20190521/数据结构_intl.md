## ActionSummaryOverviewItem

ActionSummaryOverviewItem contains a detailed summary of costs by transaction type

Referenced by the following API(s): DescribeBillSummaryByPayMode。

| Name | Type | Description |
|------|------|-------|
| ActionType | String | Transaction type: Pay-as-you-go deduction, or account adjustment credit/deduction. |
| ActionTypeName | String | Transaction type |
| RealTotalCost | String | Actual cost |
| RealTotalCostRatio | String | Cost ratio, to two decimal points |
| CashPayAmount | String | Amount paid in cash |
| IncentivePayAmount | String | Amount paid in test credits |
| VoucherPayAmount | String | Amount paid in voucher |
| BillMonth | String | Billing month, format: 2019-08 |

## BillDetail

BillDetail contains billing details.

Referenced by the API DescribeBillDetail.

| Name | Type | Description |
|------|------|-------|
| BusinessCodeName | String | Product name: Cloud product category, such as CVM and CDB MySQL |
| ProductCodeName | String | Subproduct name: Cloud product subtype, such as CVM-Standard S1 |
| PayModeName | String | Billing mode: Pay-as-You-Go |
| ProjectName | String | Project name |
| RegionName | String | Region, e.g. South China (Guangzhou) |
| ZoneName | String | Availability zone, e.g. Guangzhou Zone 1 |
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
| Tags | Array of [BillTagInfo](#BillTagInfo) | Tag information<br/>Note: This field may return null, indicating that no valid values can be obtained. |

## BillDetailComponent

BillDetailComponent contains a breakdown of the bill.

Referenced by the API DescribeBillDetail.

| Name | Type | Description |
|------|------|-------|
| ComponentCodeName | String | Component type: Name of resource component type, such as memory or disk. |
| ItemCodeName | String | Component name: Name of resource component, such as CDB MySQL memory |
| SinglePrice | String | Component published price: Original price of resource components, keeping original granularity |
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
| VoucherPayAmount | String | Amount paid in voucher |
| CashPayAmount | String | Amount paid in cash |
| IncentivePayAmount | String | Amount paid in trial credit |

## BillResourceSummary

BillResourceSummary contains details of the resources in the bill. 

Referenced by the API DescribeBillResourceSummary.

| Name | Type | Description |
|------|------|-------|
| BusinessCodeName | String | Product name: Cloud product category, such as CVM and CDB MySQL |
| ProductCodeName | String | Subproduct: Product subtype, such as CVM-Standard S1; returns as “-” when no subproduct name is obtained |
| PayModeName | String | Billing mode: Pay-as-You-Go |
| ProjectName | String | Project name |
| RegionName | String | Region |
| ZoneName | String | AZ |
| ResourceId | String | Resource instance ID |
| ResourceName | String | Resource instance name |
| ActionTypeName | String | Transaction type: Pay-as-you-go deduction, or account adjustment credit/deduction. |
| OrderId | String | Order ID |
| PayTime | Timestamp | Payment time |
| FeeBeginTime | Timestamp | Service start time |
| FeeEndTime | Timestamp | Service end time |
| ConfigDesc | String | Configuration description |
| ExtendField1 | String | Extended field 1 |
| ExtendField2 | String | Extended field 2 |
| TotalCost | String | Original price in USD |
| Discount | String | Discount |
| ReduceType | String | Offer type |
| RealTotalCost | String | Total discounted price (USD) |
| VoucherPayAmount | String | Amount paid in voucher (USD) |
| CashPayAmount | String | Amount paid in cash (USD) |
| IncentivePayAmount | String | Amount paid in test credits (USD) |
| ExtendField3 | String | Extended field 3 |
| ExtendField4 | String | Extended field 4 |
| ExtendField5 | String | Extended field 5 |
| Tags | Array of [BillTagInfo](#BillTagInfo) | Tag information<br/>Note: This field may return null, indicating that no valid values can be obtained. |
| PayerUin | String | Payer UIN |
| OwnerUin | String | Resource owner UIN, returns “-” if value is null |
| OperateUin | String | Operator UIN, returns “-” if value is null |

## BillTagInfo

BillTagInfo contains cost allocation tags information.

Referenced by the following API(s): DescribeBillDetail, DescribeBillResourceSummary.

| Name | Type | Description |
|------|------|-------|
| TagKey | String | Cost allocation tag key |
| TagValue | String | Tag value |

## BusinessSummaryOverviewItem

Summarize product details by product

Referenced by the following API(s): DescribeBillSummaryByProduct.

| Name | Type | Description |
|------|------|-------|
| BusinessCode | String | Product code<br/>Note: This field may return null, indicating that no valid values can be obtained. |
| BusinessCodeName | String | Product name: Cloud product category, such as CVM and CDB MySQL |
| RealTotalCost | String | Actual cost |
| RealTotalCostRatio | String | Cost ratio, to two decimal points |
| CashPayAmount | String | Amount paid in cash |
| IncentivePayAmount | String | Amount paid in test credits |
| VoucherPayAmount | String | Amount paid in voucher |
| BillMonth | String | Billing month, format: 2019-08 |

## BusinessSummaryTotal

BusinessSummaryTotal summarizes the total cost by product.

Referenced by the following API(s): DescribeBillSummaryByProduct.

| Name | Type | Description |
|------|------|-------|
| RealTotalCost | String | Total cost |
| VoucherPayAmount | String | Amount paid in voucher |
| IncentivePayAmount | String | Amount paid in test credits |
| CashPayAmount | String | Amount paid in cash |

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

DetailPoint contains time and value information

Referenced by the API DescribeDosageDetailByDate.

| Name | Type | Description |
|------|------|-------|
| Time | String | Time |
| Value | String | Value |

## DetailSet

DetailSet contains information about domain name and usage details

Referenced by the API DescribeDosageDetailByDate.

| Name | Type | Description |
|------|------|-------|
| Domain | String | Domain name |
| DetailPoints | Array of [DetailPoint](#DetailPoint) | Usage data details |
| InstanceID | String | Instance ID <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## PayModeSummaryOverviewItem

PayModeSummaryOverviewItem contains a detailed summary of purchases by billing mode

Referenced by the following API(s): DescribeBillSummaryByPayMode。

| Name | Type | Description |
|------|------|-------|
| Paymode | String | Billing mode |
| PayModeName | String | Billing mode name |
| RealTotalCost | String | Actual cost |
| RealTotalCostRatio | String | Cost ratio, to two decimal points |
| Detail | Array of [ActionSummaryOverviewItem](#ActionSummaryOverviewItem) |  By transaction type: Detailed summary of purchases by type, such as pay-as-you-go deduction, or account adjustment credit/deduction. |
| CashPayAmount | String | Amount paid in cash |
| IncentivePayAmount | String | Amount paid in test credits |
| VoucherPayAmount | String | Amount paid in voucher |

## ProductInfo

ProductInfo contains product details

Referenced by the API DescribeDealsByCond.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes |  ID of the product detail |
| Value | String | Yes | Product details |

## ProjectSummaryOverviewItem

ProjectSummaryOverviewItem contains a detailed summary of costs by project

Referenced by the following API(s): DescribeBillSummaryByProject.

| Name | Type | Description |
|------|------|-------|
| ProjectId | String | Project ID |
| ProjectName | String | Project name |
| RealTotalCost | String | Actual cost |
| RealTotalCostRatio | String | Cost ratio, to two decimal points |
| CashPayAmount | String | Amount paid in cash |
| IncentivePayAmount | String | Amount paid in test credits |
| VoucherPayAmount | String | Amount paid in voucher |
| BillMonth | String | Billing month, format: 2019-08 |

## RegionSummaryOverviewItem

RegionSummaryOverviewItem contains a detailed summary of costs by region

Referenced by the following API(s): DescribeBillSummaryByRegion.

| Name | Type | Description |
|------|------|-------|
| FileId | String | Region ID <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RegionName | String | Region name |
| RealTotalCost | String | Actual cost |
| RealTotalCostRatio | String | Cost ratio, to two decimal points |
| CashPayAmount | String | Amount paid in cash |
| IncentivePayAmount | String | Amount paid in test credits |
| VoucherPayAmount | String | Amount paid in voucher |
| BillMonth | String | Billing month, format: 2019-08 |

## TagSummaryOverviewItem

TagSummaryOverviewItem contains a detailed summary of costs by tags

Referenced by the following API(s): DescribeBillSummaryByTag.

| Name | Type | Description |
|------|------|-------|
| TagValue | String | Tag value<br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RealTotalCost | String | Actual cost<br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RealTotalCostRatio | String | Cost ratio, to two decimal points<br/>Note: This field may return null, indicating that no valid values can be obtained. |

