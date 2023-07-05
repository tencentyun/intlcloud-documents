
## Overview
This document describes how to validate a domain when you apply for a certificate or add a domain in the certificate management console and the domain validation mode is automatic file validation.

>!Automatic file validation applies only to multi-year international standard certificates and non-wildcard certificates.
>
## Validation Rules
### Domain name validation rules
During automatic file validation, pay attention to the following:
>!
>- Due to SSL certificate domain validation policy changes, Tencent Cloud discontinued the file validation mode for wildcard certificates on **November 21, 2021**. For more information, please see [Domain Validation Policy Update](https://intl.cloud.tencent.com/document/product/1007/40857).
>- If the domain that you apply for is a primary domain, **www** must also be validated. For example, if the domain applied for is `tencent.com`, `www.tencent.com` must also be validated.
>- If the domain that you apply for contains **www**, the domain name following **www** must also be validated, regardless of the domain levels. For example, if the domain applied for is `www.a.tencent.com`, `a.tencent.com` must also be validated.
>- If the domain that you apply for does not contain **www** and is not a primary domain, only the current domain needs to be validated. For example, if the domain applied for is `cloud.tencent.com`, only `cloud.tencent.com` needs to be validated.

### CA validation rules
- During DNS query, you must recursively query the authoritative NS server of each domain on the authoritative root server, and then query the corresponding A, AAAA, or CNAME records from the NS server.
- If the DNS service supports DNSSEC, you must verify the signing information of the response data.
- If the queried domain is an IP address, verify the content via IP access.
- The standard HTTP/HTTPS default port must be adopted for access.
- Up to two 301/302 redirections are supported. The redirection destination IP and the validated domain must be in the same primary domain.
- In the final validation result, the status code 200 must be returned.
- For HTTPS access, certificate errors can be ignored.

## Directions

### Step 1. View validation information
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview). In the left sidebar, click **My Profile** to go to the **My Profile** page.
2. On the **My Profile** page, click the name of the organization for which domain information is to be validated. Then you can view the information of administrators that have been applied for.
3. Click the name of the administrator whose domain information is to be validated. The **Review Information** page is displayed.

4. Click the **Domain Information* tab, select the domain to be validated, and click **View Validation**.

5. On the **Validate Domain** page, follow the instructions on the page to complete validation within a specific period of time.


### Step 2. Add file validation
1. Log in to the server and ensure that the A record is added for your domain and the A record points to the server.
>?If your domain name is hosted with Tencent Cloud, point the domain name to your server. For more information, please see **A Record**.
>
2. Start a web service on the server (or use the web service where the business is running), listen on port 80 or 443, and set the reverse proxy address of the file validation path to the reverse proxy address provided in **Step 1: View validation information (as shown in the figure in substep 5 in step 1)**.
Tencent Cloud provides the following web service configuration guidelines for your reference:
  -  NGINX reverse proxy configuration
  -  Apache reverse proxy configuration

>?
>- Both HTTP and HTTPS are supported, and either can be accessed.
>- A configured reverse proxy cannot be deleted or modified. After being deleted or modified, a reverse proxy becomes invalid.
>- Up to two 301/302 redirections are supported. The redirection destination IP and the validated domain must be in the same primary domain. For a domain name starting with "www", such as `www.a.tencent.com`, file validation is required for the domain name itself as well as `a.tencent.com`.
>
3. After configuring the reverse proxy, wait for the CA to complete the file validation. After the file validation is passed, the domain is approved.
4. On the **Validate Domain** page, you can click **Validate** to validate the domain configuration.

