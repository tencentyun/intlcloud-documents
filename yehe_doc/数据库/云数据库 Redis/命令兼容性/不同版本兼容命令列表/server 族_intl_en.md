<table>
<thead><tr>
th>Command</th><th>2.8 Memory Edition (Standard Architecture)</th><th>4.0 Memory Edition (Standard Architecture)</th><th>4.0 Memory Edition (Cluster Architecture)</th><th>5.0 Memory Edition (Standard Architecture)</th><th>5.0 Memory Edition (Cluster Architecture)</th><th>Memory Edition (Cluster Architecture) with Cross-Slot Support</th></tr></thead>
<tr>
<td>bgrewriteaof</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>bgsave</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>client kill</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>sync</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>psync</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>client list</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>client getname</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>client pause</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>client reply</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>client setname</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>command count</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>command getkeys</td>
<td>x</td><td>&#10003;</td><td>&#10003;</td><td>&#10003</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>command info</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>slaveof</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>config rewrite</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>config set</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>config resetstat</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>debug object</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>debug segfault</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>role</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>save</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>lastsave</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>shutdown</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>MEMORY</td>
<td>x</td><td>&#10003</td><td>x</td><td>&#10003</td><td>x</td><td>-</td></tr>
<tr>
<td>command</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td>/td><td>-</td></tr>
<tr>
<td>dbsize</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>info</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>time</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>config get</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>monitor</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>flushdb</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>flushall</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>slowlog</td>
<td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>cluster keyslot</td>
<td>x</td><td>x</td><td>&#10003;</td><td>x</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>cluster nodes</td>
<td>x</td><td>x</td><td>&#10003;</td><td>x</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>cluster getkeysinslot</td>
<td>x</td><td>x</td><td>&#10003;</td><td>x</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>cluster slots</td>
<td>x</td><td>x</td><td>&#10003;</td><td>x</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>cluster info</td>
<td>x</td><td>x</td><td>&#10003;</td><td>x</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>cluster countkeysinslot</td>
<td>x</td><td>x</td><td>&#10003;</td><td>x</td><td>&#10003;</td><td>-</td></tr>
<tr>
<td>cluster (others)</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>module</td>
<td>x</td><td>x</td><td>x</td><td>x</td><td>x</td><td>-</td></tr>
<tr>
<td>lolwut</td>
<td>x</td><td>x</td><td>x</td><td>&#10003;</td><td>&#10003;</td><td>-</td></tr>
</table>

