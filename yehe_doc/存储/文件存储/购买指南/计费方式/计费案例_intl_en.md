## Billing Description

<table>
   <tr>
      <th>Billable Item</th>
      <th>Billing Method</th>
      <th>Billing Cycle</th>
      <th>Description</th>
      <th>Price</th>
   </tr>
   <tr>
      <td>Storage usage</td>
      <td>Pay-as-you-go (postpaid)</td>
      <td>Hourly</td>
      <td>Billed according to the maximum hourly usage</td>
			<td><a href="https://cloud.tencent.com/document/product/582/47378#.E5.90.8E.E4.BB.98.E8.B4.B9.E4.BB.B7.E6.A0.BC.E8.AF.A6.E6.83.85">Pay-as-you-go billing details</a></td>
   </tr>
     <tr>
      <td>Storage usage</td>
      <td>Resource pack (prepaid)</td>
      <td>Monthly subscription</td>
      <td>A valid resource pack can be used to offset the corresponding pay-as-you-go fees.</td>
			<td><a href="https://cloud.tencent.com/document/product/582/47379#.E8.B5.84.E6.BA.90.E5.8C.85.E4.BB.B7.E6.A0.BC.E8.AF.A6.E6.83.85">Resource pack billing details</a></td>
   </tr>
</table>



## Billing Examples

Assume that an organization’s 20 CVMs access two file systems (A and B) in the Chinese mainland. File system A (usage: 11 TB; storage class: Standard) is used to store a fixed amount of cold data, while file system B (storage class: High-Performance; storage pack bound: 50 GB) is used for enterprise cloud storage, whose maximum hourly usage is 105.6 GB.  

Total hourly CFS fees = 11 × 1024 × 0.00008056 + (105.6 − 50) × 0.00031944 = 1.085 USD

#### Storage fees description
- Standard storage class:
Storage fees = 11 × 1024 × 0.00008056 = 0.90742784 USD

- High-Performance storage class: File system B uses a total of 105.6 GB and is bound to a 50 GB storage pack. Therefore, 50 GB should be deducted first. The fees are calculated as follows:
High-Performance storage fees =（105.6 − 50）× 0.00222222 = 0.17760864 USD
- Total fees = 11 × 1024 × 0.00008056 + (105.6 − 50) × 0.00031944 = 1.085 USD

  

