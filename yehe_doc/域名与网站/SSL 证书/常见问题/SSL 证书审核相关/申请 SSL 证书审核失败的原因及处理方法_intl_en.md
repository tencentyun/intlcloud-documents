### Causes and Handling Methods for Certificate Review Failures
This document describes the possible causes of and solutions for certificate review failures.

#### Verification file configuration error
>?We recommend running the `curl -k -v` or `wget -S` command to verify whether the file URL is valid for both HTTPS and HTTP.
>
- **Causes:**
If you chose file verification as the method for domain verification when submitting your SSL certificate order for review, the domain may fail the verification due to the following possible causes:
 - HTTPS access is enabled for some pages of the site. However, the verification file is deployed only under the HTTP service path, not under the HTTPS service path. As a result, the verification file will not be found when requested through HTTPS.
 - When the verification file is accessed, the site returns an error code.
 - CDN is enabled, but the verification file is not synchronized to CDN servers outside the Chinese mainland.
- **Solutions:**
 - Deploy the verification file under the HTTP and HTTPS service paths, and confirm that it can be accessed through HTTPS. Alternatively, temporarily disable HTTPS for all of the website pages.
 - Confirm that the correct verification file content can be directly accessed through the verification file URL specified by the CA, instead of through redirection or other methods.
>?Check whether the browser address has changed to determine whether you have been redirected.
>
 - Synchronize the verification file to CDN servers outside the Chinese mainland, or temporarily disable CDN acceleration outside the Chinese mainland.
>?If modification operations cannot be performed on the CDN servers, we recommend using DNS verification for domain verification instead.

#### DNS configuration error
- **Causes**
If you choose DNS verification as the method for domain verification when submitting your SSL certificate order for review, the review may fail due to the following possible causes:
 - The DNS resolution record value is configured incorrectly.
 - For non-existent host records, the domain name resolution services of certain service providers provide query return values that are not as expected. As a result, the CA determines that the return values are incorrect.
 - The DNS resolution record has timed out. After you submit your certificate order for review, you will have 3 calendar days to add the DNS resolution records, otherwise the review will fail.
 - The dynamic domain name resolution service is enabled. However, the corresponding TXT resolution record value has not been synchronized to the DNS servers outside the Chinese mainland in time.
- **Solutions**
 - Configure the correct DNS host records and record values.
 - Ignore the error prompts related to domain name resolution configuration, configure DNS resolution records as required, and complete the domain verification.
 - Resubmit the certificate order for review and add the DNS resolution records within 3 calendar days.
 - Confirm that the dynamic resolution service works properly and ensure that it can resolve newly added TXT resolution records properly outside the Chinese mainland.
>?If you change an existing TXT record value, the time when the changed value takes effect is determined by the TTL value. However, if you add a new TXT record value, the new value takes effect in seconds. Therefore, we recommend completing the domain verification by adding a TXT record value and deleting the TXT resolution record after the domain name passes verification.

#### Empty or invalid company phone number
For OV and EV SSL certificates, if you leave the company phone number field empty or set it to an invalid phone number when submitting the certificate order for review, the review will fail.
- **Causes**
For OV and EV SSL certificates, the company phone number field is required. If it is left empty or set to an invalid value, you need to reset it.
- **Solutions**
Enter the correct company phone number by which you can be contacted for verification by the CA.

#### CSR file already used in other orders
- **Causes**
To ensure certificate key security, CSR information that has been used in earlier orders cannot be reused in new orders.
- **Solutions**
If you have used a CSR file in a successfully submitted order before, generate a new CSR file for each subsequent order. This ensures that each SSL certificate has a unique key pair, ensuring the security of your SSL certificates.

#### Incorrect format of the domain name bound with the certificate
- **Causes**
A valid domain name can be up to 64 characters in length and contain only **letters, digits, and hyphens (-)**.
- **Solutions**
Check that the domain name information in the CSR file and order is correct.

#### Empty or incorrect primary domain name
- **Causes**
The `Common Name` field is empty or not correctly set when the CSR file is created.
>?The `Common Name` field must be set to one of the bound domain names.
- **Solutions**
We recommend using the online CSR file generation feature provided by the system.

#### Domain name security review failure
When you apply for an SSL certificate, you may receive a review failure message.
The message content is similar to the following:
```
The domain did not pass the CA security verification. Domain certificate application failed. Please purchase an OV or EV certificate. You can also try to apply for a certificate using another domain.
```

- **Causes**
Due to CA's anti-phishing mechanism, sensitive words contained in domain names, such as "bank" and "pay", can cause security review failure. Some less commonly used root domain names may also result in review failure. For example, root domain names suffixed with .pw, such as `www.qq.pw` and `www.qcloud.pw`, will not pass the review.
The following are sensitive words that may cause domain names to fail the security review. They are only examples, and the specific sensitive words are defined by CA.
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

- **Solutions**
We recommend changing the host name in the domain name and trying to submit the order again. If the problem persists after you change the host name several times, we recommend that you choose a paid certificate product or use a different primary domain name to apply for a certificate.
>?Because DV SSL certificates are quickly issued through automatic authentication without manual intervention, we use stringent sensitive words filters to set the verification standard.



