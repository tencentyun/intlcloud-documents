
## Overview
This document describes how to validate a domain when you apply for a certificate or add a domain in the SSL Certificate Service console and the domain validation mode is file validation.

## Validation Rules
### Domain validation rules
During file validation, pay attention to the following:
>!
>- Due to changes of the policies for SSL certificate domain validation, Tencent Cloud discontinued the file validation mode for wildcard certificates on **November 21, 2021**. For more information, see [Domain Ownership Validation Policy Update](https://intl.cloud.tencent.com/document/product/1007/40857).
>- If the domain that you apply for is a primary domain, **www** must also be validated. For example, if the domain applied for is `tencent.com`, `www.tencent.com` must also be validated.
>- If the domain that you apply for contains **www**, the domain name following **www** must also be validated, regardless of the domain levels. For example, if the target domain is `www.a.tencent.com`, `a.tencent.com` must also be validated.
>- If the domain that you apply for does not contain **www** and is not a primary domain, only the current domain needs to be validated. For example, if the target domain is `cloud.tencent.com`, only `cloud.tencent.com` needs to be validated.
>

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
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview).
2. Select a certificate in the **Validating** state. On the **Validate Domain** page displayed, follow instructions on the page to complete validation within a specific period of time.

### Step 2. Add a file record
1. Log in to the server and make sure that the domain name points to the server and the corresponding website is enabled.
>? If your **DNS Service Provider** is Tencent Cloud, for how to point the domain to your server, see A Record.
>
2. Create the specified file in the root directory of the website, including the file directory, name, and content.
>?
>- The website root directory refers to the folder where you store the website programs on the server. Its name may be `wwwroot`, `htdocs`, `public_html`, or `webroot`.
>- Ensure that the website port is set to 80 or 443.
> 
 - **Example**
The root directory of your website is `C:/inetpub/wwwroot`. You can create a file as shown in the following table in the `wwwroot` folder.
<table>
<tr><th>File Directory</th><th>File Name</th><th>File Content</th></tr>
<tr><td>/.well-known/pki-validation</td><td>The file content shown on the validation page. Example: A32CF****7EEtrust-provider.comTT**bu6</td><td>201908060**alzeo</td></tr>
</table>
 - **Note**
    - The above is for reference only, and both the filename and content are random values. The values shown on your validation page shall prevail.
    - On Windows, you need to create a file and folder that begin with a dot by running commands.
 For example, to create a `.well-known` folder, open a command prompt window and execute the command `mkdir .well-known` to create it. See the following figure.
 ![](https://qcloudimg.tencent-cloud.cn/raw/92896d96c4909390ed1e92a60155b2ff.png)
3. On the **Validate Domain** page, you can click **View Domain Ownership Validation Status** to check whether the configuration is successful.
>?
>- Both HTTP and HTTPS are supported, and either can be accessed.
>- File verification does not support any redirection. Instead, it directly returns the status code 200 and file content.
>- For a domain name starting with "www", such as `www.a.tencent.com`, file validation is required for the domain name itself as well as `a.tencent.com`.
> 
4. Wait for the CA's review. After the certificate is issued or the domain name information is approved, the file and directory can be cleared.



