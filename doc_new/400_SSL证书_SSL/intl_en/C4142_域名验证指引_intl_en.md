## Scenario

This document guides you through how to verify your ownership of a domain name after applying for a DV certificate.
> Please complete the verification as soon as possible. If you fail to do so within 3 days or the verification fails, the CA will reject your certificate application.

The ownership of a domain name can be verified by:
- [Manual DNS verification](#ManualVerification)
- [Automatic DNS verification](#AutomaticVerification)
- [File verification](#FileVerification)

## Prerequisites

- For [manual DNS verification](#ManualVerification), you need to complete the application for a DV certificate first.
- For [automatic DNS verification](#AutomaticVerification), you need to use a domain name resolved by Tencent Cloud DNS.
- For [file verification](#FileVerification), you need to obtain the username and password for logging in to the server.

## Directions

<span id="ManualVerification"></span>
### Manual DNS Verification

> This DNS verification method is detailed by taking the Tencent Cloud DNS platform as an example.

<span id="CertificateDetails"></span>
#### Viewing Certificate Details

1. Log in to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl).
2. On the "Certificate List" page, select the ID of the DV certificate to be viewed to enter the "Certificate Details" page, as shown below:
![Certificate details](https://main.qcloudimg.com/raw/bd0916bedfa69d445f13fea3ac4f5e18.png)
3. View the certificate status in the basic information section on the "Certificate Details" page.
You can verify the domain name ownership by resolving the specified DNS record. The resolution format can be specified as "**Host name > TXT record type > record value**".
For example, add a TXT record to the domain name `www.domain.com` for certificate application with the specified resolution format of "`www.domain.com` > TXT > 20181227220956......hj37i4xai8m7uii2a23l".
> To add the record, click "**Add a Domain Name > DNS Record**".

#### Adding a Domain

1. Switch to the [Tencent Cloud DNS Console](https://console.cloud.tencent.com/cns) and click **Add a Resolution** in the "DNS List", as shown below:
![Add a resolution](https://main.qcloudimg.com/raw/9f5031f4203529117fc9d892b112666c.png)
2. In the "Add a Resolution" window that pops up, enter the primary domain name to be resolved, such as "domain.com".
3. Click **OK** to finish the addition.

#### Adding a DNS Record

1. In the row of the newly added domain name, click **Resolution**, as shown below:
![Resolution](https://main.qcloudimg.com/raw/1799b5eaa63550d1d774e67af62eefe7.png)
2. On the resolution page, click **Add a Record** to display a new record line, as shown below:
![Add a record](https://main.qcloudimg.com/raw/138e707b024c57a9f7e7b2adb02ab172.png)
Key parameters are as follows:
 - Host name: Enter according to the [certificate details](#CertificateDetails), such as "\_dnsauth".
 - Record type: Select "**TXT**".
 - Line type: Select "Default".
 - Record value: The text content provided by the system, **which must be entered completely**. Enter in according to the [certificate details](#CertificateDetails).
 - TTL (seconds): Select the default value of 600 seconds.
3. Click **Save**.
4. In the "Successfully added" prompt box that pops up, click **Got it**, and the record list shows the information of the newly added record, which means that the addition is completed, as shown below:
![](https://main.qcloudimg.com/raw/1a20f029b797d1e5f8e8583516f8972e.png)
The system regularly checks the TXT record value of the certificate domain name such as `www.domain.com`. If it is found matching the specified value, the domain name ownership verification is completed.

<span id="AutomaticVerification"></span>
### Automatic DNS Verification

> This DNS verification method is limited to domain names resolved by Tencent Cloud DNS.

If the domain name for which you are applying for a certificate has been resolved by Tencent Cloud DNS, you can choose automatic verification.
The system automatically adds the specified DNS record for the domain name. If the record is found matching the specified value, it is automatically cleared when the domain name ownership verification is completed.

<span id="FileVerification"></span>
### File Verification

#### Creating a File in the Specified Directory

1. Log in to the server.
2. Create the specified file in the root directory of the website, including the file directory, name, and content.
 >The website root directory refers to the folder where you store the website programs on the server. Its name may be wwwroot, htdocs, public_html, or webroot.

For example, create a file as shown in the table below:
<table>
<tr><th>File Directory</th><th>Filename</th><th>File Content</th></tr>
<tr><td>/.well-known/pki-validation</td><td>fileauth.txt</td><td>201808241742072yvt8bxp9jv0ycginrnnebwgy1nvwgvxtssucy39w7b20nelfa</td></tr>
</table>
3. Open a browser and access the corresponding URL based on the type of the domain name to be verified.
**URL format**: `http://domainname/filedirectory/filename` or `https://domainame/filedirectory/filename`.
Access the URL to get the content of the file, such as `201608241742072yvt8bxp9jv0ycginrnnebwgy1nvwgvxtssucy39w7b20nelfa`.
 - If the domain name for which you are applying for file verification is `example.www.domain.com`, access the URL `http://example.www.domain.com/.well-known/pki-validation/fileauth.txt` or `https://example.www.domain.com/.well-known/pki-validation/fileauth.txt` for verification.
 >For a second-level domain name beginning with www such as `www.domain.com`, add [file verification](#FileVerification) to the domain name first and then add the file to its primary domain name `domain.com` for [file verification](#FileVerification) as instructed in the **URL format** section, and the verification value is displayed as the same.
 - If the domain name for which you are applying for file verification is a wildcard domain name - `*.domain.com`, access the URL `http://domain.com/.well-known/pki-validation/fileauth.txt` or `https://domain.com/.well-known/pki-validation/fileauth.txt` for verification.
>
> - Both HTTP and HTTPS are supported, and either of them can be accessed.
> - File verification does not support any redirect, and direct response to status code 200 and file content is needed.

#### Waiting for Review

Please wait patiently for scan and review by the CA. For example, a **DV certificate** is generally issued in 10 minutes - 24 hours. Once the certificate is issued, the file and directory can be deleted.

#### Note

On Windows, you need to create a file and folder that begin with a dot by running the command line.
For example, to create a `.well-known` folder, run the following command in the command line window.
```
mkdir .well-known
```
> If anything goes wrong during this procedure, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).
