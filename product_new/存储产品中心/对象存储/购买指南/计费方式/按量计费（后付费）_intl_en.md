COS is billed in a pay-as-you-go manner. This document describes the pay-as-you-go billing details. This billing method is applicable to all regions where the COS service is provided. COS fees are charged for billable items such as storage capacity, requests, and traffic daily or monthly.


## Billable Items

The billable items in COS and their billing formulas are as detailed below:
<table>
   <tr>
      <th>Billable Item</th>
      <th>Description</th>
      <th>Billing Formula</th>
   </tr>
   <tr>
      <td>Storage capacity fees</td>
      <td>Calculated based on the storage capacity used at a unit price that varies by storage class</td>
      <td>Storage capacity fees = storage capacity unit price * monthly storage capacity used</td>
   </tr>
   <tr>
      <td>Request fees</td>
      <td>Calculated based on the number of requests at a unit price that varies by storage class</td>
      <td>Request fees = unit price per 10,000 requests * monthly accumulated number of requests / 10,000</td>
   </tr>
   <tr>
      <td>Data retrieval fees</td>
      <td>Calculated based on the volume of data retrieved at a unit price that varies by storage class. This billable item applies when data in standard_IA and archive storage classes is downloaded</td>
      <td>Data retrieval fees = unit price per GB * monthly amount of data retrieved </td>
   </tr>
   <tr>
      <td>Traffic fees</td>
      <td>Calculated based on the public network downstream traffic, CDN origin-pull traffic, and cross-region replication traffic at a unit price that varies by traffic type</td>
      <td>Traffic fees = unit price per GB * daily accumulated traffic</td>
   </tr>
   <tr>
      <td>Administrative Feature Fees</td>
      <td>Calculated based on the use of enabled administrative features. Current features include inventory and data extraction</td>
      <td>Inventory feature fees = number of objects listed / million * unit price<br>
Select feature  fees = unit price per GB * daily accumulated extracted data

</td>
   </tr>
</table>



>
> - For detailed descriptions of billable items and billing restrictions, please see [Billable Items](https://intl.cloud.tencent.com/document/product/436/33776).
> - For detailed pricing information on different billable items, please see [Product Pricing](https://intl.cloud.tencent.com/document/product/436/6239).

## Example

John Smith uploaded files of 100 GB in standard storage class on March 1, 2019 and downloaded 10 GB of data through the public network on March 15. The following fees were incurred in March:

- Standard storage capacity fees: the total storage capacity used in the month was 100 GB.
- Traffic fees: the total public network downstream traffic generated in the month was 10 GB.
- Request fees: the data uploading and downloading requests in this month were billed.

