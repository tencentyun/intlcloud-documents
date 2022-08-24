## Overview
Upload from client acceleration uses the following methods to provide a higher-quality upload service:
<table ><thead ><tr>
<th style="width:200px">Method</th><th >Description</th></tr>
</thead><tbody ><tr>
<td>Data reception by the nearby edge node</td>
<td>Upload requests from terminals are received by nearby edge nodes deployed globally</td>
</tr>
<tr>
<td>Smart acceleration network</td>
<td>Tencent Cloud's acceleration network is used to intelligently select the optimal linkage to transfer the data to the storage center.</td>
</tr>
<tr>
<td>Support for transfer over the QUIC protocol</td>
<td>The QUIC protocol features multiplexing and connection migration, so it has a higher data transfer efficiency and is more stable under poor network conditions.</td>
</tr>
</tbody>
</table>



## Use Cases
<table ><thead ><tr>
<th style="width:200px">Scenario</th><th >Description</th></tr>
</thead><tbody ><tr>
<td>Long-distance data upload</td>
<td>As some end users are far away from the VOD storage center, they have a poor upload quality, especially in cross-region and oversea upload scenarios. After upload from client acceleration is enabled, it will use the Tencent Cloud edge node nearest to the end user to receive the user’s requests and will use the acceleration network for data transfer, greatly improving the upload quality.</td>
</tr>
<tr>
<td>Data upload under poor network conditions</td>
<td>As mobile client users often switch their network or are in places where the base station signal is weak, the network connection is often unstable and has a high packet loss rate. The upload acceleration feature supports the QUIC protocol to make data transfer more stable under poor network conditions.</td>
</tr>
<tr>
<td>General data upload</td>
<td>If a massive amount of data is transferred over HTTP/1.1 through a non-acceleration channel, it can lead to a performance bottleneck. Upload acceleration can upload data over the QUIC protocol and supports features such as multiplexing and 0-RTT to deliver a higher transfer efficiency</td>.
</tr>
</tbody>
</table>

