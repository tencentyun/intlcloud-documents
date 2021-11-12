

You can specify annotations in a YAML file to implement capabilities of virtual nodes, such as custom DNS, as shown below:

<table>
<thead>
<tr>
<th width="20%">Annotation Key</th>
<th width="40%">Annotation Value and Description</th>
<th width="40%">Required</th>
</tr>
</thead>
<tbody>
<tr>
<td>eks.tke.cloud.tencent.com/resolv-conf</td>
<td>Queries the list of IP addresses for the DNS server while resolving the domain name, for example <code>nameserver 8.8.8.8</code>.
<br>You can use <code>kubectl edit node eklet-subnet-xxxx</code> to add this annotation.
<br>After the modification, the Pods scheduled to this virtual node will adopt this DNS configuration by default.</td>
<td>No</td>
</tr>
</tr>
</tbody></table>

#### Example
The example of a custom DNS configuration for a virtual node is as follows:

```
apiVersion: v1
kind: Node
metadata:
  annotations:
    eks.tke.cloud.tencent.com/resolv-conf:|
      nameserver 4.4.4.4
      nameserver 8.8.8.8
   
```



