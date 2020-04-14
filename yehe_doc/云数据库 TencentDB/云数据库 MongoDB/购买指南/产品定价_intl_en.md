## Billing Mode
TencentDB for MongoDB offers the following billing mode:

| Billing Mode | Payment Mode | Use Case |
|---------|---------|---------|
| Pay-as-you-go | Postpaid. You can apply for resources for on-demand use and will be charged based on the actual usage upon settlement. | It is suitable for businesses that may fluctuate greatly and instantaneously. In this mode, instances can be released immediately after use so as to reduce the costs. |

Depending on the usage duration, the prices in pay-as-you-go mode divide into three tiers:

| Usage Duration | Tiered Pricing |
|---------|---------|
| 0 hours < duration ≤ 96 hours | Tier 1 pay-as-you-go price applies |
| 96 hours < duration ≤ 360 hours | Tier 2 pay-as-you-go price applies |
| Duration > 360 hours | Tier 3 pay-as-you-go price applies |

## Instance Price

### Billing formula
**Total fees = memory specification fees + storage capacity fees + backup capacity fees + traffic fees**

### Billable items
<table>
<thead>
<tr>
<th width="15%">Billable Item</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Memory specification fees<br></td>
<td>The instance specification selected on the purchase page is pay-as-you-go and supports tiered pricing.</td>
</tr>
<tr>
<td>Storage capacity fees</td>
<td>The disk size selected on the purchase page is pay-as-you-go.</td>
</tr>
<tr>
<td>Backup capacity fees</td>
<td>Backup capacity refers to the backup and log capacity. It mainly stores key logs (such as slow logs) generated during the operation of MongoDB and backup files. It is free of charge for now.</td>
</tr>
<tr>
<td>Traffic fees</td>
<td>This refers to the fees of public network traffic (free of charge for now).</td>
</tr>
</tbody>
</table>

## Pay-as-You-Go Pricing
### 4–64 GB specification

<table >
  <td rowspan=2>Region</td>
  <td colspan=3 >Memory (USD/GB/Hour)</td>
  <td rowspan=2 >Disk (USD/GB/Hour)</td>
 <tr height=21 >
  <td height=21 >Tier 1</td>
  <td>Tier 2</td>
  <td>Tier 3</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Guangzhou<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Shanghai<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Beijing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Chengdu<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Chongqing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Tokyo<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Nanjing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Hong Kong (China)<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0375</td>
  <td class=xl68 align=right>0.0281</td>
  <td class=xl68 align=right>0.0188</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Singapore<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0375</td>
  <td class=xl68 align=right>0.0281</td>
  <td class=xl68 align=right>0.0188</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Bangkok<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0608</td>
  <td class=xl68 align=right>0.0456</td>
  <td class=xl68 align=right>0.0304</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl67 style='height:15.75pt'>Mumbai<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Seoul<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0339</td>
  <td class=xl68 align=right>0.0254</td>
  <td class=xl68 align=right>0.0170</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Silicon Valley<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0375</td>
  <td class=xl68 align=right>0.0281</td>
  <td class=xl68 align=right>0.0188</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Virginia<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0420</td>
  <td class=xl68 align=right>0.0315</td>
  <td class=xl68 align=right>0.0210</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Frankfurt<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0400</td>
  <td class=xl68 align=right>0.0300</td>
  <td class=xl68 align=right>0.0200</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Moscow<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
 </tr>
</table>

### 128 GB specification
<table >
   <td rowspan=2>Region</td>
  <td colspan=3 >Memory (USD/GB/Hour)</td>
  <td rowspan=2 >Disk (USD/GB/Hour)</td>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Tier 1</td>
  <td>Tier 2</td>
  <td>Tier 3</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Guangzhou<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Shanghai<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Beijing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Chengdu<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Chongqing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Tokyo<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Nanjing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Hong Kong (China)<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0333</td>
  <td class=xl68 align=right>0.0250</td>
  <td class=xl68 align=right>0.0167</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Singapore<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0333</td>
  <td class=xl68 align=right>0.0250</td>
  <td class=xl68 align=right>0.0167</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Bangkok<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0530</td>
  <td class=xl68 align=right>0.0398</td>
  <td class=xl68 align=right>0.0265</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl67 style='height:15.75pt'>Mumbai<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0310</td>
  <td class=xl68 align=right>0.0207</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Seoul<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0253</td>
  <td class=xl68 align=right>0.0190</td>
  <td class=xl68 align=right>0.0127</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Silicon Valley<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.3190</td>
  <td class=xl68 align=right>0.2393</td>
  <td class=xl68 align=right>0.1595</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Virginia<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0312</td>
  <td class=xl68 align=right>0.0234</td>
  <td class=xl68 align=right>0.0156</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Frankfurt<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0300</td>
  <td class=xl68 align=right>0.0225</td>
  <td class=xl68 align=right>0.0150</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Moscow<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0480</td>
  <td class=xl68 align=right>0.0360</td>
  <td class=xl68 align=right>0.0240</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
</table>

### 240 GB specification
<table>
  <td rowspan=2>Region</td>
  <td colspan=3 >Memory (USD/GB/Hour)</td>
  <td rowspan=2 >Disk (USD/GB/Hour)</td>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Tier 1</td>
  <td>Tier 2</td>
  <td>Tier 3</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Guangzhou<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Shanghai<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Beijing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Chengdu<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Chongqing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Tokyo<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Nanjing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Hong Kong (China)<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0319</td>
  <td class=xl68 align=right>0.0239</td>
  <td class=xl68 align=right>0.0160</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Singapore<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0319</td>
  <td class=xl68 align=right>0.0239</td>
  <td class=xl68 align=right>0.0160</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Bangkok<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0450</td>
  <td class=xl68 align=right>0.0338</td>
  <td class=xl68 align=right>0.0225</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl67 style='height:15.75pt'>Mumbai<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0215</td>
  <td class=xl68 align=right>0.0161</td>
  <td class=xl68 align=right>0.0108</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Seoul<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0215</td>
  <td class=xl68 align=right>0.0161</td>
  <td class=xl68 align=right>0.0108</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Silicon Valley<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0317</td>
  <td class=xl68 align=right>0.0238</td>
  <td class=xl68 align=right>0.0159</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Virginia<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0265</td>
  <td class=xl68 align=right>0.0199</td>
  <td class=xl68 align=right>0.0133</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Frankfurt<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0255</td>
  <td class=xl68 align=right>0.0191</td>
  <td class=xl68 align=right>0.0128</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Moscow<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0410</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0205</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
</table>

### 512 GB specification
<table>
  <td rowspan=2>Region</td>
  <td colspan=3 >Memory (USD/GB/Hour)</td>
  <td rowspan=2 >Disk (USD/GB/Hour)</td>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Tier 1</td>
  <td>Tier 2</td>
  <td>Tier 3</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Guangzhou<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Shanghai<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Beijing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>Chengdu<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Chongqing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Tokyo<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Nanjing<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Hong Kong (China)<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0278</td>
  <td class=xl68 align=right>0.0209</td>
  <td class=xl68 align=right>0.0139</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Singapore<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0278</td>
  <td class=xl68 align=right>0.0209</td>
  <td class=xl68 align=right>0.0139</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Bangkok<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0397</td>
  <td class=xl68 align=right>0.0298</td>
  <td class=xl68 align=right>0.0199</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl67 style='height:15.75pt'>Mumbai<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0327</td>
  <td class=xl68 align=right>0.0245</td>
  <td class=xl68 align=right>0.0164</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Seoul<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0200</td>
  <td class=xl68 align=right>0.0150</td>
  <td class=xl68 align=right>0.0100</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Silicon Valley<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0292</td>
  <td class=xl68 align=right>0.0219</td>
  <td class=xl68 align=right>0.0146</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Virginia<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0246</td>
  <td class=xl68 align=right>0.0185</td>
  <td class=xl68 align=right>0.0123</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Frankfurt<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0239</td>
  <td class=xl68 align=right>0.0179</td>
  <td class=xl68 align=right>0.0120</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>Moscow<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
</table>
