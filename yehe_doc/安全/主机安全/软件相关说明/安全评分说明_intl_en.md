This topic describes how to calculate the security score for your assets.

## Security Score
The highest security score is 100, and the lowest score is 20. The security level of a server is based on its security score, which is calculated by subtracting the points scored by the types, number, and threat level of security incidents from the total score of 100.
![](https://qcloudimg.tencent-cloud.cn/raw/9d1a5ef6e265669833b7d570693ab180.png)
### Scoring rules
<table>
<thead>
<tr>
<th>Level</th>
<th>Security Incidents (by incident count)</th>
<th>Penalty per incident</th>
<th>Maximum total penalty</th>
</tr>
</thead>
<tbody><tr>
<td>Critical</td>
<td>Trojan files, brute force attacks, and malicious requests</td>
<td>-40</td>
<td>-50</td>
</tr>
<tr>
<td  >High</td>
<td>Critical vulnerabilities, high-risk vulnerabilities, critical baseline items, high-risk baseline items, unusual logins (high risk), local privilege escalation, and reverse shell</td>
<td>-10</td>
<td>-20</td>
</tr>
<tr>
<td>Medium</td>
<td>Medium-risk vulnerabilities and baseline items</td>
<td>-3</td>
<td>-10</td>
</tr>
<tr>
<td>Low</td>
<td>Low-risk vulnerabilities and baseline items</td>
<td>-2</td>
<td>-5</td>
</tr>
<tr>
<td>Other</td>
<td>Only CWPP Basic is implemented, or CWPP Agent is not installed</td>
<td>-1</td>
<td>-5</td>
</tr>
</tbody></table>

### Security level
<table>
<thead>
<tr>
<th>Level</th>
<th>Health check score</th>
<th>Text color</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Good</td>
<td>90-100</td>
<td>Green</td>
<td>The assets have a good security status. Regular inspection is recommended to maintain the good status.</td>
</tr>
<tr>
<td>Medium</td>
<td>60-89</td>
<td>Orange</td>
<td>Many security risks exist in the assets. It is recommended to handle the security incidents in a timely manner.</td>
</tr>
<tr>
<td>Bad</td>
<td>20-59</td>
<td>Red</td>
<td>Critical security risks exist in the assets. It is recommended to handle the security incidents as soon as possible.</td>
</tr>
</tbody></table>
