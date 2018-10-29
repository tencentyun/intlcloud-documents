## Billing

**Pay-per-use**: Fees are charged every hour on the hour with no need to pay in advance.
A GCC instance includes network, storage (system disk and data disk), and hardware (CPU, memory, and GPU). For more information on the network price, see [Network Price Overview](/doc/product/213/509). For more information on the disk price, please see [Disk Price Overview](/doc/product/213/2255).




### Computing GN8 instance
<table>
		<thead>
		<tr>
			<th width=10%>Model</th>
			<th width=20%>GPU<br>(Tesla P40)</th>
			<th width=11%>GPU Memory<br>(GDDR5)</th>
			<th width=12%>vCPU<br>(Xeon E5 v4)</th>
			<th>Memory<br>(DDR4)</th>
			<th>Postpaid*</th>
		</tr>
		</thead>
			<tbody>
					<tr>
					<td>GN8.LARGE56</td>
					<td>&nbsp;One</td>
					<td>&nbsp;24 GB</td>
					<td>&nbsp;Six cores</td>
					<td>&nbsp;&nbsp;&nbsp;56 GB</td>
					<Td><b>From 1.98 USD/hour</b></td>
					</tr>
				<tr>
				<td>GN8.3XLARGE112</td>
				<td>&nbsp;Two</td>
				<td>&nbsp;48 GB</td> 
				<td>&nbsp;14 cores</td>
				<td>&nbsp;112 GB</td>
				<Td><b>From 4.01 USD/hour</b></td>
				</tr>
				<tr>
				<td>GN8.7XLARGE224</td>
				<td>&nbsp;Four</td>
				<td>&nbsp;96 GB</td> 
				<td>&nbsp;28 cores</td>
				<td>&nbsp;224 GB</td>
				<Td><b>From 8.01 USD/hour</b></td>
				</tr>
				<tr>
				<td>GN8.14XLARGE448</td>
				<td>&nbsp;Eight</td>
				<td>&nbsp;192 GB</td> 
				<td>&nbsp;56 cores</td>
				<td>&nbsp;448 GB</td>
				<Td><b>From 16.02 USD/hour</b></td>
				</tr>
			</tbody>
</table>


Computing performance:
- The peak computing capacity of a single GN8.LARGE56: over 12 TFLOPS for single-precision floating point computing and over 47 TOPS for integer computing (INT8)

- The peak computing capacity of a single GN8.3XLARGE112: over 24 TFLOPS for single-precision floating point computing and over 94 TOPS for integer computing (INT8)

- The peak computing capacity of a single GN8.7XLARGE224: over 48 TFLOPS for single-precision floating point computing and over 188 TOPS for integer computing (INT8)

- The peak computing capacity of a single GN8.14XLARGE448: over 96 TFLOPS for single-precision floating point computing and over 376 TOPS for integer computing (INT8)


## Renewal
- A GCC instance is shut down on the expiry date and put into the recycle bin automatically. It will be retained for 7 calendar days during which you can choose to renew it. The instance is terminated if it is not renewed within 7 calendar days.
- You can set auto renewal for it when purchasing an instance.

You are recommended to renew an instance before its expiration to avoid service interruption caused by a shutdown when it expires. For more information on renewal, see [How to Renew](/document/product/560/8052).
## Reclaiming
 GPU instances are reclaimed in the same way as with CVM instances. For more information, see CVM [Instance Reclaim](/doc/product/213/4931#.E5.AE.9E.E4.BE.8B.E5.9B.9E.E6.94.B6).

## Arrears
GCC instances in arrears are in the same way as with CVMs in arrears. For more information, see CVM [Arrears](/document/product/213/2181).

## *Note
The above price is the standard published price. For price changes caused by price reduction activities or other factors, see the purchase page.

