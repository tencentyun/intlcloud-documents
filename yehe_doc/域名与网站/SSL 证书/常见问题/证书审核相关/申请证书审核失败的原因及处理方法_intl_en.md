### Causes and handling methods for certificate review failures
This topic describes the possible causes and handling methods for certificate review failures.

#### Verification file configuration error
>!It is recommended that you run the `curl -k -v` or `wget -S` command to verify whether the file URL is valid for both HTTPS and HTTP.

- **Causes**
If you choose file verification for domain name verification when submitting SSL certificate order for review, the domain name may fail the verification due to the following possible causes:
 - HTTPS access is enabled for some pages of the site. However, the verification file is deployed only under the HTTP service path, not under the HTTPS service path. As a result, the verification file will not be found when being requested through HTTPS.
 - When the verification file is accessed, the site returns an error code.
 - The CDN service is enabled, but the verification file is not synchronized to CDN servers outside Mainland China.
- **Solutions**
 - Deploy the verification file under the HTTP and HTTPS service paths, and confirm that it can be accessed through HTTPS. Alternatively, temporarily disable the HTTPS service for all pages of the site.
 - Confirm that the correct verification file content can be directly accessed through the verification file URL specified by the CA, instead of through redirection or other methods.
>!Check whether the browser address changes to determine whether redirection occurs.
>
 - Synchronize the verification file to CDN servers outside Mainland China, or temporarily disable the CDN acceleration service outside Mainland China.
>!If modification operations cannot be performed on the CDN servers, it is recommended that you use DNS verification for domain name verification instead.

#### DNS configuration error
- **Causes**
If you choose DNS verification for domain name verification when submitting SSL certificate order for review, the review may fail due to the following possible causes:
 - The DNS resolution record value is configured incorrectly.
 - For non-existent host records, domain name resolution services of certain service providers provide query return values that are not as expected. As a result, the CA determines that the return values are incorrect.
 - The DNS resolution record times out. After you submit certificate order for review, you will have 3 calendar days to add DNS resolution records, otherwise the review will fail.
 - The dynamic domain name resolution service is enabled. However, the corresponding TXT resolution record value is not synchronized to the DNS servers outside Mainland China in time.
- **Solutions**
 - Configure correct DNS host records and record values.
 - Ignore the error prompts related to domain name resolution configuration, configure DNS resolution records as required, and complete domain name verification.
 - Resubmit the certificate order for review and add DNS resolution records within 3 calendar days.
 - Confirm that the dynamic resolution service works properly and ensure that it can resolve newly added TXT resolution records properly outside Mainland China.
>!If you change an existing TXT record value, the time when the changed value takes effect is determined by the TTL value. However, if you add a new TXT record value, the new value takes effect in seconds. Therefore, it is recommended that you complete the domain name verification by adding a TXT record value and delete the TXT resolution record information after the domain name passes verification.

#### Empty or invalid company phone number
For OV and EV SSL certificates, if you leave the company phone number field empty or set it to an invalid phone number when submitting the certificate order for review, the review will fail.
- **Causes**
For OV and EV SSL certificates, the company phone number field is required. If it is left empty or set to an invalid value, you need to reset it.
- **Solutions**
Enter the correct company phone number by which you can be contacted during organization information verification by the CA.

#### CSR file already used in other orders
- **Causes**
To ensure certificate key security, CSR information that has been used in earlier orders cannot be reused in new orders.
- **Solutions**
If you have used a CSR file in a successfully submitted order before, generate a new CSR file for each subsequent order. This ensures that each SSL certificate has its unique key pair, improving the security of your SSL certificates.

#### Incorrect format of the domain name bound with the certificate
- **Causes**
A valid domain name can be up to 64 characters in length and contain only letters, digits, and hyphens (-).
- **Solutions**
Check that the domain name information in the CSR file and order is correct.

#### Empty or incorrect primary domain name
- **Causes**
The `Common Name` field is empty or not correctly set when the CSR file is created.
>!The `Common Name` field must be set to one of the bound domain names.
- **Solutions**
It is recommended that you use the online CSR file generation feature provided by the system.

#### Domain name security review failure
When you apply for an SSL certificate, you may receive review results.

- **Causes**
Due to CA's anti-phishing mechanism, sensitive words contained in domain names, such as "bank" and "pay", can cause security review failures. Specific sensitive words are defined by the CA. Some less commonly used root domain names may also result in review failures. For example, root domain names suffixed with .pw, such as `www.qq.pw` and `www.qcloud.pw`, will not pass the review.
- **Solutions**
It is recommended that you change the host name in the domain name and try to submit the order again. If the problem persists after you change the host name several times, it is recommended that you choose a paid certificate product or use another primary domain name to apply for a certificate.
>!Because DV SSL certificates are quickly issued through automatic authentication without manual intervention, we use stringent sensitive words filters to set the verification standard.


