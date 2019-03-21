### Maximum Outbound Bandwidth (Downstream Bandwidth)
Maximum public network bandwidth is the maximum default outbound bandwidth (the bandwidth flowing out of CVM). The maximum public network bandwidth varies with different network methods. See below for details:
<table border="3">
    <tr>
       <th rowspan="2"><b>Network Billing Method</b></th> 
       <th colspan="2" ><b>CVM</b></th>
       <th rowspan="2"><b>Available range of the maximum bandwidth (Mbps)</b></th>	
   </tr>
    <tr>
       <th><b>CVM Billing Method</b></th> 
       <th><b>CVM Configuration</b></th> 
    </tr>
	<tr>
	      <td rowspan="4">Bill-by-Traffic</td> 
        <td >Postpaid CVM</td> 
        <td >ALL</td> 
				<td>0-100</td>    
   </tr>
	  <tr>
        <td rowspan="3">Prepaid CVM</td> 
        <td>Cores ≤ 8</td> 
				<td>0-200</td>        
   </tr>
	  <tr>
        <td>8 < Cores < 24</td> 
        <td>0-400</td> 
   </tr> 
	 <tr>
        <td>Cores ≥ 24</td> 
        <td>0-400 or no speed limit</td> 
   </tr>
	 <tr>
		    <td rowspan="3">Bill-by-Bandwidth</td> 
        <td >Postpaid CVM</td> 
        <td >ALL</td> 
				<td>0-100</td>      
   </tr>
	 <tr>
		    <td rowspan="2">Prepaid CVM</td> 
        <td >Guangzhou Zone 1<br>Guangzhou Zone 2<br>Shanghai Zone 1<br>Hong Kong Zone 1<br>Toronto Zone 1</td> 
				<td>0-200</td>      
   </tr>
	 <tr>
        <td>Other availability zones</td> 
        <td>0-1000</td> 
   </tr>
    <tr>
		    <td>Shared bandwidth</td> 
        <td colspan="2">ALL</td> 
        <td>0-200 or no speed limit</td>    
    </tr>
</table>

### Maximum Inbound Bandwidth (Upstream Bandwidth)
Inbound bandwidth of public network is the bandwidth that flows into CVM instance.

- If fixed bandwidth purchased by a user is larger than 10 Mbps, Tencent Cloud assigns a public network inbound bandwidth equal to the purchased bandwidth.
- If fixed bandwidth purchased by a user is less than 10 Mbps, Tencent Cloud assigns 10 Mbps public network inbound bandwidth.

