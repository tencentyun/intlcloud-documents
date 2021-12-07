[](id:que1) 
### How do I test email sending in some simple ways?
You can use your own accounts for testing. SES offers a free tier of 1,000 emails currently but does not offer test accounts.

[](id:que5) 
### Can I send a large number of emails right from the start?
No. The sending volume must be increased gradually day by day, and cannot be lifted to the desired level at a stroke. To gain a good reputation with your ISP, automatic warm-up is required before email sending. Standard warm-up rules apply by default under batch sending mode. Please refer to [Features](https://intl.cloud.tencent.com/document/product/1084/43285).

[](id:que6) 
### What is warm-up?
Warm-up is a way to establish a reputation for a new IP. Generally, all email service providers have a limit on the daily number of emails sent from an IP. You need to start with a smaller number of emails and gradually increase the number each day.

[](id:que7) 
Standard warm-up rules apply by default under batch sending mode. The backend will determine the warm-up progress based on a series of policies and automatically assign the daily sending quota. The entire process is completely automatic. When the maximum number of sent emails allowed per day is reached, email sending will stop and extra emails will enter the cache queue and be sent 24 hours later. The standard warm-up plan is as follows:
<table style="width: 200px;">
   <tr>
      <th width="0px" style="text-align:center">Day</td>
      <th width="0px" style="text-align:center">Sending Volume/Day</td>
   </tr>
	<tr>
		<td style="text-align:center"style="text-align:center">1</td>
		<td style="text-align:center">100</td>
	</tr>
	<tr>
		<td style="text-align:center">2</td>
		<td style="text-align:center"sdval="200" >200</td>
	</tr>
	<tr>
		<td style="text-align:center">3</td>
		<td style="text-align:center"sdval="500" >500</td>
	</tr>
	<tr>
		<td style="text-align:center">4</td>
		<td style="text-align:center"sdval="1000" >1,000</td>
	</tr>
	<tr>
		<td style="text-align:center">5</td>
		<td style="text-align:center"sdval="2000" >2,000</td>
	</tr>
	<tr>
		<td style="text-align:center">6</td>
		<td style="text-align:center"sdval="5000" >5,000</td>
	</tr>
	<tr>
		<td style="text-align:center">7</td>
		<td style="text-align:center"sdval="10,000" >10000</td>
	</tr>
	<tr>
		<td style="text-align:center">8</td>
		<td style="text-align:center"sdval="20,000" >20000</td>
	</tr>
	<tr>
		<td style="text-align:center">9</td>
		<td style="text-align:center"sdval="30000" >30,000</td>
	</tr>
	<tr>
		<td style="text-align:center">10</td>
		<td style="text-align:center"sdval="40000" >40,000</td>
	</tr>
	<tr>
		<td style="text-align:center">11</td>
		<td style="text-align:center"sdval="60000" >60,000</td>
	</tr>
	<tr>
		<td style="text-align:center">12</td>
		<td style="text-align:center"sdval="80000" >80,000</td>
	</tr>
	<tr>
		<td style="text-align:center">13</td>
		<td style="text-align:center"sdval="100000" >100,000</td>
	</tr>
	<tr>
		<td style="text-align:center">14</td>
		<td style="text-align:center"sdval="120000" >120,000</td>
	</tr>
	<tr>
		<td style="text-align:center">15</td>
		<td style="text-align:center"sdval="150000" >150,000</td>
	</tr>
	<tr>
		<td style="text-align:center">16</td>
		<td style="text-align:center"sdval="200000" >200,000</td>
	</tr>
	<tr>
		<td style="text-align:center">17</td>
		<td style="text-align:center"sdval="400000" >400,000</td>
	</tr>
	<tr>
		<td style="text-align:center">18</td>
		<td style="text-align:center"sdval="600000" >600,000</td>
	</tr>
	<tr>
		<td style="text-align:center">19</td>
		<td style="text-align:center"sdval="800000" >800,000</td>
	</tr>
		<tr>
		<td style="text-align:center">20</td>
		<td style="text-align:center"sdval="800000" >1,000,000</td>
	</tr>
</table>

Custom rules:

For high-quality emails, if the standard warm-up plan cannot satisfy your needs, you can pursue a custom warm-up plan. For details, please contact your sales rep to apply.
