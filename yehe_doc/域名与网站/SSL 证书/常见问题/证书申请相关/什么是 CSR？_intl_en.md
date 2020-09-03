### What is CSR?

CSR is short for Certificate Signing Request. To obtain an SSL certificate, you need to first generate a CSR file and submit it to the certificate authority (CA). A CSR file contains a public key and a distinguished name and is usually generated from a web server. A pair of public and private keys for encryption and decryption will be created at the same time.

Relevant organization information is required to create a CSR. The web server creates a distinguished name based on the information provided to identify the certificate. The organization information includes the following items:

**Country or region code**
The code of the country/region where your organization is legally registered, in the 2-letter format defined by the International Organization for Standardization (ISO).

**Province, city, or autonomous region**
The province, city, or autonomous region where your organization is located.

**City/region**
The city/region where your organization is registered.

**Organization**
The legal registered name of your business.

**Departments within the organization**
This field is used to differentiate departments within an organization, such as "the engineering department" or "the human resources department".

**Common name**
The name entered in the CSR common name field must be the Fully Qualified Domain Name (FQDN) of the website to which you apply the certificate, such as "www.domainnamegoeshere".

However, Tencent Cloud generates CSR online without you having to generate and submit CSR files. To apply for a domain validated certificate, you simply need to submit a common name.