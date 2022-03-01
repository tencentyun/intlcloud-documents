
## Issue Description
When you apply for a free DV SSL certificate, the domain verification fails and the following message is reported:
```
The domain did not pass the CA security verification. Domain certificate application failed. Please purchase an OV or EV certificate. You can also try to apply for a certificate using another domain.
```

## Common Causes
Due to CA's anti-phishing mechanism, sensitive words contained in domain names, such as "bank" and "pay", can cause security review failure. Some less commonly used root domain names may also result in review failure. For example, root domain names suffixed with .pw, such as `www.qq.pw` and `www.qcloud.pw`, will not pass the review. The following are sensitive words that may cause domain names to fail the security review. They are only examples, and the specific sensitive words are defined by CA.

<table >
<colgroup>
<col >
<col >
<col >
<col >
</colgroup>
<tbody>
  <tr>
    <td>Private/Public IP</td>
    <td>Host name</td>
    <td>live (excluding the .live top-level domain name)</td>
    <td>bank</td>
  </tr>
  <tr>
    <td>banc</td>
    <td>alpha</td>
    <td>test</td>
    <td>example</td>
  </tr>
  <tr>
    <td>credit</td>
    <td>pw (excluding the .pw top-level domain name)</td>
    <td>apple</td>
		<td>ebay</td>
  </tr>
  <tr>
    <td>trust</td>
    <td>root</td>
    <td>amazon</td>
    <td>android</td>
  </tr>
  <tr>
    <td>visa</td>
    <td>google</td>
    <td>discover</td>
		<td>financial</td>
  </tr>
  <tr>
    <td>wordpress</td>
    <td>pal</td>
    <td>hp</td>
    <td>lv</td>
  </tr>
  <tr>
    <td>free</td>
    <td>scp</td>
    <td></td>
		<td></td>
  </tr>
</tbody>
</table>


## Solution
You can:
- Purchase a non-DV SSL certificate to bind to your domain.
- Apply for a domain that does not contain sensitive words.

