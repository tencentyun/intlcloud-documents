Cloud Security Overview provides a comprehensive assessment on overall security protection and risks on Tencent Cloud to users. In this way, the customer can timely respond to various security risks and issues, thus achieving overall security monitoring.

## Security risks
The Security Operation Center comprehensively assesses the risks on the customer's Tencent Cloud based on the monitoring data of all security scenarios.

These risks are evaluated on a 100-point scale, ranging from 20 to 100 points. If the customer has any security risks, the system will deduct the specified points for the risk item from 100 points. If the final score is less than 20 points, the final score is displayed as 20 points. The table below defines the deduction items and penalty points.
<table>
<thead>
<tr>
<th>Risks</th>
<th>Deduction items</th>
<th>Penalty points</th>
<th>Upper limit of penalty points</th>
</tr>
</thead>
<tbody><tr>
<td rowspan=4>Asset protection - server protection</td>
<td>No CWP Pro or CWP Ultimate purchased</td>
<td>-20</td>
<td rowspan=9>45</td>
</tr>
<tr>
 <td>CWP Pro or CWP Ultimate is purchased, but the protection ratio of server assets is less than 30%.</td>
<td>-5</td>
 </tr>
<tr>
 <td>CWP Pro or CWP Ultimate is purchased, but the protection ratio of server assets is greater than or equal to 30% yet less than 89%.</td>
<td>-2</td>
 </tr>
<tr>
 <td>CWP Pro or CWP Ultimate is purchased, but the protection ratio of server assets is greater than or equal to 90%.</td>
<td>0</td>
 </tr>
<tr>
<td rowspan=4>Asset protection - public IP protection</td>
<td>No firewall purchased</td>
<td>-20</td>
 </tr>
<tr>
 <td>Firewall is purchased, but the IP protection ratio is less than 30%.</td>
<td>-5</td>
 </tr>
<tr>
 <td>Firewall is purchased, but the IP protection ratio is greater than or equal to 30% yet less than 89%.</td>
<td>-2</td>
 </tr>
<tr>
<td>Firewall is purchased, but the IP protection ratio is greater than or equal to 89%.</td>
<td>0</td>
</tr>
<tr>
<td>Asset protection - cloud platform protection</td>
<td>No Security Operation Center Premium used</td>
<td>-5</td>
</tr>
<tr>
<td rowspan=2>Exposure of service ports</td>
<td>Each identified port that should be disabled</td>
<td>-5</td>
<td rowspan=2>10</td>
</tr>
<tr>
<td>Each identified port whose access source should be restricted</td>
<td>-3</td>
 </tr>
<tr>
<td rowspan=2>Cloud platform configuration risks</td>
<td>Each noncompliant high-risk configuration item that is identified</td>
<td>-2</td>
<td rowspan=2>10</td>
</tr>
<tr>
 <td>Each noncompliant medium-risk configuration item that is identified</td>
<td>-1</td>
 </tr>
<tr>
<td rowspan=3>Baseline risks</td>
<td>Each critical baseline configuration issue that is identified</td>
<td>-10</td>
<td rowspan=3>10</td>
</tr>
<tr>
 <td>Each high-risk baseline configuration issue that is identified</td>
<td>-5</td>
 </tr>
<tr>
 <td>Each medium-risk baseline configuration issue that is identified</td>
<td>-3</td>
 </tr>
<tr>
<td rowspan=3>Vulnerability risks</td>
<td>Each identified critical vulnerability in server that is not fixed</td>
<td>-10</td>
<td rowspan=3>10</td>
</tr>
<tr>
 <td>Each identified high-risk vulnerability in server that is not fixed</td>
<td>-5</td>
 </tr>
<tr>
 <td>Each identified medium-risk vulnerability in server that is not fixed </td>
<td>-3</td>
 </tr>
<tr>
<td rowspan=2>Intrusion risks</td>
<td>Each unprocessed alert that warns Trojan, successful cracking, or malicious request</td>
<td>-40</td>
<td>40</td>
</tr>
<tr>
 <td>Each unprocessed alert that warns high-risk unusual login, reverse shell, high-risk command, or local privilege escalation</td>
<td>-5</td>
<td>10</td>
 </tr>
<tr>
<td>API key compromise risks</td>
<td>Each API key compromise event detected</td>
<td>-40</td>
<td>40</td>
</tr>
</tbody></table>

>?
>-Each risk item has an upper limit of penalty points. If the total points deducted for all deduction items under this risk exceed the upper limit of penalty points, the points deducted for this risk should be equal to the upper limit.
>- Security score:
>   - A security score less than 60 points indicates poor security. The system displays the score in red.
>   - A security score that is greater than or equal to 60 points yet less than 90 points indicates controllable risks. The system displays the score in orange.
>   - A security score that is greater than 90 points indicates high security. The system displays the score in green.

## Asset protection
The Security Operation Center provides statistics on security protection of various assets to help customers determine whether the current security protection can be optimized.
- Protected server assets: The system is permitted to enable [CWP Pro or CWP Ultimate](https://www.tencentcloud.com/document/product/296/48331) for server assets.
- Protection ratio of server assets: The ratio of the number of protected server assets to the total number of server assets.
- Protected public IP addresses: Edge Firewall is enabled for public IP addresses.
- Protection ratio of public IP addresses: The ratio of the number of protected public IP addresses to the total number of public IP addresses.
