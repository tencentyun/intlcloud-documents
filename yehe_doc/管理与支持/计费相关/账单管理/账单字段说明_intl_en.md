### 1. Fields

|Field|Description| 
|---------|---------|
| Payer Account ID	| The account ID of the payer, which is the unique identifier of a Tencent Cloud user.	|
| Owner Account ID	| The account ID of the actual resource user.	|
| Operator Account ID	| The account or role ID of the operator who purchases or activates a resource.	|
|Product Name	| The name of a Tencent Cloud product purchased by the user, such as CVM.	|
| Subproduct Name	| The subcategory of a Tencent Cloud product purchased by the user, such as CVM – Standard S1.|
|Billing Mode	| The billing mode, which can be monthly subscription or pay-as-you-go.	|
|Transaction Type	| The detailed transaction type, such as pay-as-you-go hourly settlement. For more valid values, see "[Enumerated values of key fields](#key-fields)".	|
|Transaction ID	| The bill number for a deducted payment.	|
|Transaction Time	| The time at which a payment was deducted.	|
|Usage Start Time	| The time at which product or service usage starts. |
|Usage End Time	| The time at which product or service usage ends. |
|Instance ID	| The object ID of a billed resource, such as a CMV instance ID. This object ID may vary due to various forms and contents of resources in different products.	|
|Instance Name| The resource name set by the user in the console. If it is not set, it will be empty by default.	|
|Instance Type	| The instance type of a product or service purchased, which can be resource package, RI, SP, or spot instance. Other instance types are not displayed by default.	|
|Project Name	| The project to which a resource belongs, which is user-designated. If a resource has not been assigned to a project, it will automatically belong to the default project.	|
|Region	| The region to which a resource belongs, such as South China (Guangzhou).	|
|Availability Zone	| The availability zone to which a resource belongs, such as Guangzhou Zone 3.	|
|Component Type	| The component type of a product or service purchased, such as CVM instance components including CPU and memory.	|
|Component Name	| The specific component of a product or service purchased.	|
|Component List Price	| The listed unit price of a component. If a customer has applied for a fixed preferential price or contract price, this parameter will not be displayed by default.	|
| Component Contracted Price	| The contracted unit price of a component, which is "List price x Discount".	|
|Component Price Measurement Unit	| The unit of measurement for a component price, which is composed of USD, usage unit, and duration unit.	|
|Component Usage	| The actually settled usage of a component.	|
|Component Usage Unit	| The unit of measurement for component usage.	|
|Usage Duration	| The resource usage duration.	|
|Duration Unit	| The unit of measurement for usage duration.	|
|Original Cost	| The original cost of a resource, which is "List price x Usage x Usage duration".	|
|RI Deduction (Duration)	| The usage duration deducted by RI. The unit of measurement for deduction is the same as that for usage duration.	|
|RI Deduction (Cost)	| The amount deducted from the original cost by RI.	|
| Savings Plan Deduction	| The savings plan deduction amount.	|
| Savings Plan Deduction Rate	| The discount multiplier that applies to the component based on the remaining commitment of the savings plan.	|
|SP Deduction (Cost)	| The amount of cost deducted by a savings plan based on the component's original cost. SP Deduction (Cost) = Cost deduction by SP / SP Deduction Rate	|
|Discount Multiplier	| The discount multiplier applied to the cost of the resource.	|
|Blended Discount Multiplier	| The final discount multiplier that is applied after combining multiple discount types, which is "Total amount after discount / Original cost".	|
| Currency	| The currency used for the settlement of a component.	|
| Total Amount After Discount (Excluding Tax)	| The total resource cost (not including tax) after discounts have been applied, which is "Component original cost x Discount multiplier" or "Component unit price x Usage x Usage duration".	|
| Voucher Deduction	| The voucher deduction amount.	|
|Amount Before Tax	| The pretax amount after voucher deduction.	|
| Tax Rate	| The tax rate.	|
| Tax Amount	| The tax amount.	|
| Total Cost (Including Tax)	| The total resource cost (including tax) after discounts have been applied, which is "Component original cost x Discount multiplier x (1 + Tax rate)" or "Component unit price x Usage x Usage duration x (1 + Tax rate)".	|
|Additional Attributes	| Attribute remarks, such as the instance type and transaction type of a reserved instance (for example: s1.18px, One-off RI fee) or the two regions associated with a CCN instance (for example: Shanghai - Beijing).	|
|Configuration Description	| The billable item names and usage of a resource, which are displayed on the resource bill only.	|
|Extended Fields 1-5	| Extended attribute information of a product, which is displayed on the resource bill only.	|
|Cost Allocation Tags 1-N	| The cost allocation tags bound to a resource. For details, see [Cost Allocation Tags](https://www.tencentcloud.com/document/product/555/32276).	|

### 2. Enumerated values of key fields[](id:key-fields)

| Field |	 Valid values | 
|---------|---------|
| Transaction Type | PurchaseRenewal,Modify,Refund,Deduction,Hourly settlement,Daily settlement,Monthly settlement,Spot,Offline project deduction,Offline deduction,adjust-CR,adjust-DR,One-off RI Fee,Hourly RI fee,New monthly subscription,Monthly subscription renewal,Monthly subscription specification adjustment,Monthly subscription refund,Hourly Savings Plan fee,Guarantee deduction,Pay-as-you-go reversal | 
