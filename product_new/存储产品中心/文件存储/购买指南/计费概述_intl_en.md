


## Billing Description

| Billable Item         | Billing Method           | Billing Cycle | Description                                                  |
| :-------------------- | :----------------------- | :------------ | :----------------------------------------------------------- |
| File storage usage | Pay-as-you-go (postpaid) | Hour          | Fees are billed every hour based on the maximum (peak) storage used in an hour |



## Storage Usage

When a file system is created, it consumes 32 MB of storage by default, which will not be counted into the storage usage billed.



## Notes on CIFS/SMB Beta Test

The beta test for CIFS/SMB protocols has ended; the schedule for future tests will be announced later. If you were a beta tester, you can continue to use the CIFS/SMB file systems, which are free of charge currently.



## Pricing Details

Below are the latest unit prices for standard file systems in all regions in Mainland China effective as of 00:00, November 10, 2017.

> The unit prices for NFS and CIFS/SMB file systems are the same.

<table>
   <tr>
      <th>Storage Class </th>
      <th>Region </th>
      <th>Range of Maximum (Peak) Storage Usage</th>
      <th nowrap="nowrap">Unit Price</th>
   </tr>
   <tr>
      <td rowspan="8">Standard storage</td>
      <td rowspan="1">Mainland China</td>
      <td>-</td>
      <td>0.058 USD/GB/month (0.00008056 USD/GB/hour)</td>
   </tr>
   <tr>
      <td >Hong Kong (China) </td>
      <td>-</td>
      <td>0.09 USD/GB/month (0.000125 USD/GB/hour)</td>
   </tr>
      <td>Singapore </td>
      <td>-</td>
      <td>0.09 USD/GB/month (0.000125 USD/GB/hour) </td>
   </tr>
   <tr>
      <td>Tokyo</td>
      <td>-</td>
      <td>0.09 USD/GB/month (0.000125 USD/GB/hour) </td>
   </tr>
     <tr>
      <td>Silicon Valley   </td>
      <td>-</td>
      <td>0.08 USD/GB/month (0.000111111 USD/GB/hour)</td>
   </tr>
     <tr>
      <td>Mumbai</td>
      <td>-</td>
      <td>0.09 USD/GB/month (0.000125 USD/GB/hour)</td>
   </tr>
        <tr>
      <td>Seoul</td>
      <td>-</td>
      <td>0.09 USD/GB/month (0.000125 USD/GB/hour) </td>
   </tr>
      </tr>
        <tr>
      <td>Toronto</td>
      <td>-</td>
      <td>0.09 USD/GB/month (0.00012500 USD/GB/hour)</td>
   </tr>
      <tr>
      <td rowspan="1">High-performance storage</td>
      <td rowspan="2">Mainland China</td>
      <td> - </td>
      <td>0.26 USD/GB/month (0.000361111 USD/GB/hour)</td>
   </tr>
</table>



## Billing Example

An organization has 20 CVM instances that access two file systems in Chinese Mainland. The file system A is used for cold data storage with a maximum standard storage usage of 11 TB. The file system B is used as organizational cloud storage with a peak standard storage usage of 105.6 GB in the current hour.

Total CFS fees for the current hour = (11*1024 + 105.6) * 0.00008056 = 0.92 USD
