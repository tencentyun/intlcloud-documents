### Bill details
| Field |	 Description |
|---------|---------|
|Instance ID|	 Instance ID, which can be viewed in the console. |
|Instance Name|	Resource alias, which can be customized and is null if not set. |
|Product Name	| Tencent Cloud product, such as CVM or TencentDB for MySQL. |
|Payer Account ID|	Account ID of the payer, which is a user's unique ID at Tencent Cloud and is a reseller ID here. |
|Owner Account ID|	Account ID of the resource owner, which is a customer ID here. |
|Operator Account ID|	Account ID of the operator or the user who purchases or activates a product, which is a customer ID here. |
|Reseller Account ID|	A reseller account ID is the ID of the reseller who directly manages the resource owner. |
|Billing Mode|	Resource billing mode, which can be monthly subscription or pay-as-you-go. |
|Project Name|	Project to which a resource belongs. This is user-designated. If a resource has not been assigned to a project, it will automatically belong to the default project.  |
|Region|	Resource region, such as South China (Guangzhou). |
|Availability Zone|	Resource AZ, such as Guangzhou Zone 3. |
|Subproduct Name|	Tencent Cloud product subcategory, such as CVM - Standard S1. |
|Transaction Type|	Transaction type, such as purchase, activation, renewal, and refund. For details, see "Enumerated values of key fields" below. |
|Transaction ID|	Unique transaction ID. |
|Transaction Time	| Resource cost deduction time. |
|Usage Start Time|	Resource usage start time. |
|Usage End Time|	Resource usage end time. |
|Component Type|	Component type, such as CPU, memory, bandwidth, and system disk. |
|Component Name|	Component name, such as Memory - Standard S2 and Premium Cloud Storage - Storage Space. |
|Component List Price	|Published component price. |
|Component Price Measurement Unit|	Published component price unit. |
|Component Usage|	Component usage. |
|Component Usage Unit|	Component usage unit. |
|Usage Duration|	Resource usage duration. |
|Duration Unit|	Resource usage duration unit. |
|Reserved Instances|	ID of the matched RI, such as s2-RI-1234567890. |
|Original Cost|	Original resource cost, which is "published price * usage * usage duration". |
|Currency	| The currency used for component cost settlement, which is USD here. |

<table>
<thead>
<tr>
<th><b>Field</b></th>
<th><b>Description</b></th>
</tr>
</thead>
<tbody>
<tr>
<td>Transaction Type</td>
<td>Enumerated values:<br>Purchase<br>Renewal<br>Modify<br>Refund<br>Deduction<br>Hourly settlement<br>Daily settlement<br>Monthly settlement<br>Offline project deduction<br>Offline deduction<br>adjust-CR<br>adjust-DR<br>One-off RI Fee<br>Spot<br>Hourly RI fee<br>New monthly subscription<br>Monthly subscription renewal<br>Monthly subscription specification adjustment<br>Monthly subscription specification adjustment<br>Monthly subscription refund</td>
</tr>
</tbody></table>
