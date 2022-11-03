## Overview
Based on Tencent Cloud's globally deployed acceleration network, client upload acceleration intelligently selects the optimal access point and route for data transfer, increasing upload speed and success rate. In addition, using the QUIC protocol for transmission makes for more reliable data transfers under poor network conditions.
VOD uses the following methods to accelerate video upload from clients.
<table ><thead ><tr>
<th style="width:200px">Method</th><th >Description</th></tr>
</thead><tbody ><tr>
<td>Upload data to the nearest edge node</td>
<td>VOD has deployed edge nodes globally and can route an upload request to the nearest edge node.</td>
</tr>
<tr>
<td>Smart acceleration network</td>
<td>Leveraging Tencent Cloud's acceleration network, VOD can intelligently select the optimal route to transfer data to the storage center.</td>
</tr>
<tr>
<td>Support for transfer over the QUIC protocol</td>
<td>The QUIC protocol allows multiplexing and connection migration. It transfers data more efficiently and is more stable under poor network conditions.</td>
</tr>
</tbody>
</table>

 

## Use Cases
<table ><thead ><tr>
<th style="width:200px">Scenario</th><th >Description</th></tr>
</thead><tbody ><tr>
<td>Long-distance data upload</td>
<td>Upload performance tends to be poor if an end user is far away from a VOD storage center (for example, if they are located in a different region or continent). If you enable client upload acceleration, Tencent Cloud will route an upload request to its nearest edge node and use its acceleration network for data transfer, greatly improving the upload performance.</td>
</tr>
<tr>
<td>Data upload under poor network conditions</td>
<td>Mobile users may experience unstable network connection and high packet loss due to frequent network changes and weak signal. VOD supports QUIC transmission, which ensures more reliable data transfer under poor network conditions.</td>
</tr>
<tr>
<td>General data upload</td>
<td>If you do not enable upload acceleration, HTTP 1.1 is used for data transfer, which is weak when dealing with a large amount of data. In contrast, the QUIC protocol allows multiplexing and features zero RTT, making it more efficient at transferring data.</td>
</tr>

</tbody>
</table>


## Directions
- For directions on how to use the feature, see [Client Upload Acceleration](https://intl.cloud.tencent.com/document/product/266/49083).
- For the billing details, see [Value-Added Services](https://intl.cloud.tencent.com/document/product/266/38162#.E5.AE.A2.E6.88.B7.E7.AB.AF.E4.B8.8A.E4.BC.A0.E5.8A.A0.E9.80.9F).
