You can select a WAF type and region according to the deployment method and region of your business. WAF currently supports service in the following regions:

<table>
<thead>
<tr>
<th>Product Type</th>
<th>Supported Region</th>
<th>Details</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=12 >SaaS WAF</td>
<td rowspan=4 >Chinese mainland</td>
<td>South China: Guangzhou</td>
</tr>
<tr>
<td>East China: Shanghai</td>
</tr>
<tr>
<td>North China: Beijing</td>
</tr>
<tr>
<td>Southwest China: Chengdu</td>
</tr>
<tr>
<td rowspan=8 >Outside Chinese mainland</td>
<td>Hong Kong/Macao/Taiwan (China): Hong Kong (China)</td>
</tr>
<tr>
<td>Southeast Asia: Singapore, Bangkok, and Jakarta</td>
</tr>
<tr>
<td>Northeast Asia: Seoul and Tokyo</td>
</tr>
<tr>
<td>West US: Silicon Valley</td>
</tr>
<tr>
<td>North America: Toronto</td>
</tr>
<tr>
<td>Europe: Moscow and Frankfurt</td>
</tr>
<tr>
<td>East US: Virginia</td>
</tr>
<tr>
<td>South America: Sao Paulo</td>
</tr>
<tr>
<td rowspan=12 >CLB WAF</td>
<td rowspan=4 >Chinese mainland</td>
<td>South China: Guangzhou and Shenzhen Finance</td>
</tr>
<tr>
<td>East China: Shanghai, Nanjing, and Shanghai Finance</td>
</tr>
<tr>
<td>North China: Beijing and Beijing Finance</td>
</tr>
<tr>
<td>Southwest China: Chengdu and Chongqing</td>
</tr>
<tr>
<td rowspan=12 >Outside Chinese mainland</td>
<td>Hong Kong/Macao/Taiwan (China): Hong Kong (China)</td>
</tr>
<tr>
<td>Southeast Asia: Singapore, Bangkok, and Jakarta</td>
</tr>
<tr>
<td>South Asia: Mumbai</td>
</tr>
<tr>
<td>Northeast Asia: Seoul and Tokyo</td>
</tr>
<tr>
<td>West US: Silicon Valley</td>
</tr>
<tr>
<td>East US: Virginia</td>
</tr>
<tr>
<td>North America: Toronto</td>
</tr>
<tr>
<td>Europe: Moscow and Frankfurt</td>
</tr>
</tbody></table>

>?
>- We recommend you place your SaaS WAF instance and web real server in the same region to reduce business latency.
>- CLB WAF supports binding IPv6 CLB instances to protect IPv6 websites. If you want to use IPv6 web protection, make sure that the selected region supports IPv6 CLB instances and IPv6 web deployment has been completed.
>- IPv6 CLB instances currently support main regions. The supported regions are subject to the ones on the [CLB purchase page](https://buy.cloud.tencent.com/lb). For more information on IPv6 CLB, see [Getting Started with IPv6 CLB](https://intl.cloud.tencent.com/document/product/214/34560).
>- If you have never added a protected domain name in WAF, you can [contact us](https://intl.cloud.tencent.com/contact-us) to change the region. Otherwise, you cannot change the region.
