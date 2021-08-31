CLB offers two types of instances: CLB (formerly "application CLB") and Classic CLB.
- CLB supports TCP/UDP/HTTP/HTTPS protocols to provide flexible forwarding capabilities based on domain names and URL paths.
- Classic CLB does not support HTTP/HTTPS protocols on the private network but is easy to configure.

CLB has all features of Classic CLB. Given their product features and performance, we recommend that you use CLB. For a detailed comparison, please see below:

<table>
        <tbody>
               <tr>
            <th style="width: 10%;" rowspan="2">Product Type</th>
            <th style="width: 45%;" colspan="2" >CLB</th>
            <th style="width: 45%;" colspan="2">Classic CLB</th>
        </tr>
        <tr>
            <th>Public network</th>
            <th>Private network</th>
            <th>Public network</th>
            <th>Private network</th>
        </tr>
        <tr>
            <td>Layer-7 forwarding (HTTP/HTTPS)</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>×</td>
        </tr>
        <tr>
            <td>Layer-4 forwarding (TCP/UDP)</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
        </tr>  
        <tr>
            <td>Encrypted Layer-4 forwarding (TCP SSL)</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>×</td>
                        <td>×</td>
        </tr>    
                <tr>
            <td>HTTP/2 and WebSocket (Secure) support</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>×</td>
        </tr>
        <tr>
            <td>Load balancing policy</td>
                        <td>IP hash (Layer-7)<br>Weighted round-robin<br>Weighted least-connection scheduling</td>
                        <td>IP hash (Layer-7)<br>Weighted round-robin<br>Weighted least-connection scheduling</td>
                        <td>IP hash (Layer-7)<br>Weighted round-robin<br>Weighted least-connection scheduling</td>
                        <td>Weighted round-robin</td>
        </tr>   
         <tr>
            <td>Session persistence</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
        </tr>   
        <tr>
            <td>Health check</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
        </tr>   
         <tr>
            <td>Custom forwarding rule (domain name/URL)</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>×</td>
                        <td>×</td>
        </tr>   
        <tr>
           <td>SNI multi-certificate support</td>
                       <td>&#10003;</td>
                       <td>&#10003;</td>
                       <td>×</td>
                       <td>×</td>
        </tr>
            <tr>
            <td>Forwarding to different real ports</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>×</td>
                        <td>×</td>
        </tr>   
        <tr>
           <td>Custom Layer-7 configuration</td>
                       <td>&#10003;</td>
                       <td>&#10003;</td>
                       <td>×</td>
                       <td>×</td>
         </tr>  
         <tr>
            <td>Layer-7 redirect (rewrite)</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>×</td>
                        <td>×</td>
        </tr>
             <tr>
            <td>Cross-region binding support</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>×</td>
                        <td>×</td>
        </tr>   
                <tr>
            <td>Storing Layer-7 access logs in CLS</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>&#10003;</td>
                        <td>×</td>
        </tr>   
</tbody></table>

>?  
> - CLB instance: a CLB instance supports enabling or disabling the HTTP/2 protocol.  For more information, see [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516#.E6.AD.A5.E9.AA.A42.EF.BC.9A.E9.85.8D.E7.BD.AE.E7.9B.91.E5.90.AC.E5.99.A8) .
> - Classic CLB instance: HTTPS listeners created for Classic CLB before April 2018 do not support the HTTP/2 protocol. HTTPS listeners created after April 2018 support but cannot disable the HTTP/2 protocol.
