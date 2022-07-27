This document describes the release notes of the CKafka kernel minor version.

## v2.8.1
<table>
<thead>
<tr>
<th style = "width:20%">Version</th>
<th>Feature</th>
<th style = "width:30%">Remarks</th>
</tr>
</thead>
<tbody><tr>
<td>2.8.1_1.0.3</td>
<td>Prohibited the # symbol in consumer group names.</td>
<td>None</td>
</tr>
<tr>
<td>2.8.1_1.0.4</td>
<td>1. Added the <b>Auto-Create Consumer Group</b> switch. <br>2. Added the support for SCRAM authentication. <br> 3. Added the support for displaying the number of producer connections.</td>
<td>None</td>
</tr>
</tbody></table>

## v2.4.2
<table>
<thead>
<tr>
<th style = "width:20%">Version</th>
<th>Feature</th>
<th style = "width:30%">Remarks</th>
</tr>
</thead>
<tbody><tr>
<td>2.12-2.4.2_1.0.5</td>
<td>Added the support for collecting producer connection statistics.</td>
<td>None</td>
</tr>
<tr>
<td>2.12-2.4.2_1.0.6</td>
<td>1. Added the support for outputting slow production logs. <br>2. Prohibited the # symbol in consumer group names.</td>
<td>None</td>
</tr>
<tr>
<td>2.12-2.4.2_1.0.7</td>
<td>Added the support for token authentication.</td>
<td>None</td>
</tr>
<tr>
<td>2.12-2.4.2_1.0.8</td>
<td>1. Added the support for disabling <b>Auto-Create Consumer Group</b>. <br>2. Added the support for SCRAM authentication.</td>
<td>None</td>
</tr>
<tr>
<td>2.12-2.4.2_1.1.1</td>
<td>Placed <code>listenerName</code> and <code>listenersSize</code> in the variable first when checking whether a port is protected, so as to avoid a high CPU usage caused by too many requests.</td>
<td>None</td>
</tr>
<tr>
<td>2.12-2.4.2_1.1.2</td>
<td>Fixed a bug (consumer offset reset after new segment rolling) in the community as described at <a href = "https://issues.apache.org/jira/browse/KAFKA-9543">KAFKA-9543</a>.</td>
<td>None</td>
</tr>
</tbody></table>

## v1.1.1

<table>
<thead>
<tr>
<th style = "width:20%">Version</th>
<th>Feature</th>
<th style = "width:30%">Remarks</th>
</tr>
</thead>
<tbody><tr>
<td>2.11-1.1.1_1.0.11</td>
<td>Added the support for collecting producer connection statistics.</td>
<td>None</td>
</tr>
<tr>
<td>2.11-1.1.1_1.0.12</td>
<td>Added the support for outputting slow production logs.</td>
<td>None</td>
</tr>
<tr>
<td>2.11-1.1.1_1.0.13</td>
<td>Added the support for token authentication.</td>
<td>None</td>
</tr>
<tr>
<td>2.11-1.1.1_1.1.0</td>
<td>Optimized the <code>getMetadata</code> lock performance.</td>
<td>None</td>
</tr>
<tr>
<td>2.11-1.1.1_1.1.1</td>
<td>Added the support for downgrading to <code>ack=1</code> from <code>ack=all</code> in case of large traffic.</td>
<td>1. Separated this version from the branch 1.1.1_1.1.1-ackDowngrade. <br>2. Canceled the code merge to 1.1.1-publish. <br>3. Added the support for submitting a ticket for upgrade.</td>
</tr>
<tr>
<td>2.11-1.1.1_1.1.2</td>
<td>Added the client IP log for <code>getMetadata</code>.</td>
<td>None</td>
</tr>
</tbody></table>





## v0.10.2

<table>
<thead>
<tr>
<th style = "width:20%">Version</th>
<th>Feature</th>
<th style = "width:30%">Remarks</th>
</tr>
</thead>
<tbody><tr>
<td>0.10.2.1_1.2.8</td>
<td>Added the support for collecting producer connection statistics.</td>
<td>None</td>
</tr>
</tbody></table>



