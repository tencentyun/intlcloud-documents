### What are the differences between the RSA and ECC encryption algorithms?
- RSA (international standard algorithm): one of the earliest-introduced algorithms that is used commonly. It applies to a wider range and offers higher compatibility compared with ECC. However, it is normally 2,048 bits in length, which makes it consume more server resources.
- ECC (Elliptic-curve cryptography): A new mainstream algorithm. It is normally 256 bits in length (a 256-bit ECC key is equivalent to a 3072-bit RSA key), making it securer and able to offer stronger anti-attack capabilities. Moreover, the computation of ECC is faster than RSA, and thus it offers higher efficiency and consumes fewer server resources.


Differences between these two encryption algorithms are described as follows:
<table>
<tr>
<th width="15%">Comparison Item</th>
<th>ECC</th>
<th>RSA</th>
</tr>
<tr>
<td>Key length</td>
<td>256 bits</td>
<td>2,048 bits</td>
</tr>
<tr>
<td>CPU usage</td>
<td>Less</td>
<td>Higher</td>
</tr>
<tr>
<td>Memory usage</td>
<td>Less</td>
<td>Higher</td>
</tr>
<tr>
<td>Network usage</td>
<td>Less</td>
<td>Higher</td>
</tr>
<tr>
<td>Efficiency</td>
<td>High</td>
<td>Normal</td>
</tr>
<td>Anti-attack</td>
<td>High</td>
<td>Normal</td>
</tr>
<tr>
<td>Compatibility</td>
<td>Supports new browsers and OS (some platforms such as cPanel are not supported)</td>
<td>Supports all</td>
</tr>
</table>
