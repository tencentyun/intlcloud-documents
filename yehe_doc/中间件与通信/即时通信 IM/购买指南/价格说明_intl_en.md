>! 
>- The original billing mode of IM was disused on December 26, 2022.
>- Customers who created IM applications before December 26, 2022 use the original billing mode ([details](https://www.tencentcloud.com/document/product/1047/34350)) by default. If you want to migrate to the current billing mode, [contact sales](https://www.tencentcloud.com/contact-us) or [submit a ticket](https://console.tencentcloud.com/workorder). Once migrated, the billing mode cannot be restored.
## IM Service Pricing
The IM service pricing consists of two parts: [basic service fee](#jc) and [value-added service fee](#zz).

### Basic service fee[](id:jc)
The basic service fee covers two parts: the **resource plan** fee and **out-of-plan resource usage** fee.
- Resource plan fee: IM offers the Developer, Standard, and Premium editions. The edition for a created application defaults to the Developer edition (free). You can choose a plan based on your needs. For resource plan comparison, see [Comparison of billing plans](#tc).
- Out-of-plan resource usage fee: The fee charged for resource usage that exceeds the free quota of the Standard or Premium edition plan.


The billing details are as follows:

<table >
<tbody>
 <tr>
<th colspan="2" rowspan="2" >Billable Item</td>

<th colspan="3">Plan Type</td>
 </tr>
 <tr >
<th  >Developer Edition</td>
<th  >Standard Edition</td>
<th  >Premium Edition</td>
 </tr>
 <tr>
<td colspan="2" >Resource plan fee</td>

<td>Free of charge</td>
<td  >399 USD/month</td>
<td  >699 USD/month</td>
 </tr>
 <tr  >
<td rowspan="2" >Out-of-plan resource usage fee</td>
<td  >Peak MAU</td>
<td rowspan="2" >-</td>
<td colspan="2"  >0.015 USD/user/month</td>
 </tr>
 <tr >
<td  >Peak concurrent connections (PCC)</td>
<td colspan="2"> <strike></strike> Free for a limited time</td>
 </tr>
</tbody></table>

>?
>- MAU calculates the number of unique users that log in to your IM app in a given month. After a user logs in successfully by calling the `login` function of the IM SDK to establish a persistent connection with the IM backend, MAU will be increased by one. A user that logs in repeatedly in the same month is considered as one user only for MAU. Use the `login` function appropriately according to business scenarios to avoid an excessively high MAU.

### Value-added service fees[](id:zz)

<table>
<tr>
<th width="30%">Billable Item</th>
<th width="70%">Description</th>
</tr><tr>
<tr>
<td>Audio/video call feature</td>
<td ><b>The audio/video call feature is currently in beta, with a 60-day free edition provided</b>.</td>
</tr></table>

>?More value-added services are under development. If you have additional value-added service requirements when using IM, [contact us](https://www.tencentcloud.com/document/product/1047/41676).