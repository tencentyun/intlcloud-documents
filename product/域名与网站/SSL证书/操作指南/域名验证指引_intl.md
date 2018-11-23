To apply for a DV certificate, you can verify the ownership of domain name in the following ways:

### 1 Manual DNS verification
Verify the domain name ownership by resolving the specified DNS record. The resolution format can be specified as `Host -> TXT record type -> record value`.

For example, to add a DNS record of TXT type for domain name www.domain.com, for which you're applying for a certificate, the resolution format is: `www.domain.com –> TXT –> 201704262209564gw0...hj37i4xai8m7uii2a23l`:

![](https://main.qcloudimg.com/raw/88ddec5704c06a811f789bcde7d6fab9.png)

The following describes the steps required on Tencent Cloud DNS platform:

#### 1.1 Add a domain name

Click **Add Resolution**, enter the primary domain name `domain.com` to be resolved in the pop-up window, and click **OK**

![](https://main.qcloudimg.com/raw/96822fe8c2b7b53870a0488f69db557d.png)

#### 1.2 Add a resolution record

Click **Resolution** for the domain name you just added.  

![](https://main.qcloudimg.com/raw/63910230c0120875d5c730583338699d.png)

Click **Add Record**  

![](https://main.qcloudimg.com/raw/f933ee8ef54a53496cb60adb0f3fb9f0.png)

#### 1.3 Add the specified TXT record

TXT record is used to identify and describe a domain name:

- **Select TXT as the record type**
- Fill in the record based on the certificate details, such as `_dnsauth`
- Select **Default** as line type
- The record value is the text provided by the system. In this example, it is `201712270743...t5bfctnq`. Note: **The record value entered must be complete**
- Select 600 seconds by default for TTL

![](https://main.qcloudimg.com/raw/a54456bbbac2ef3b99b38e526c1d6be2.png)

The page after the resolution is added is as follows:
![](https://main.qcloudimg.com/raw/0e4c416a842754b43c84668518c16200.png)

The system regularly checks the TXT record value of www.domain.com. If it is found matching the specified value, the domain name ownership verification is completed.

### 2. Automatic DNS verification
> Note: Only applicable to the domain names resolved with Tencent Cloud DNS

If a domain name for which you are applying for a certificate has been resolved on the Tencent Cloud DNS platform, you can choose automatic verification.
The system automatically adds the specified DNS record for the domain name. If the record is found matching the specified value, it is automatically cleared when the domain name ownership verification is completed.

### 3. File verification

#### 3.1 Create a file in the specified directory
Create a file according to the specified file directory, name, and content. For example

| File Directory | File Name | File Content |
|---------|---------|---------|
| /.well-known/pki-validation | fileauth.txt | 201608241742072yvt8bxp9jv0ycginrnnebwgy1nvwgvxtssucy39w7b20nelfa |

If the domain name for which you're applying for file verification is `example.www.domain.com`, access the URL `http://example.www.domain.com/.well-known/pki-validation/fileauth.txt` or `https://example.www.domain.com/.well-known/pki-validation/fileauth.txt` for verification.  

> For a second-level domain name beginning with www, such as `www.domain.com`, in addition to the file verification for the domain name, the file verification for its primary domain name `domain.com` is required. The verification value and method are the same as those for the second-level domain name file verification.  

If the domain name for which you're applying for file verification is a wildcard domain name - `*.domain.com`, access the URL `http://domain.com/.well-known/pki-validation/fileauth.txt` or `https://domain.com/.well-known/pki-validation/fileauth.txt` for verification.

You can obtain `201608241742072yvt8bxp9jv0ycginrnnebwgy1nvwgvxtssucy39w7b20nelfa` by accessing the URL.

> It allows both HTTP access and HTTPS access.
> File verification does not support any redirect, and direct response to status code 200 and file content is needed.

#### 3.2 Wait for approval
After creating the file, wait for the scanning and approval of the CA. When the certificate is issued, the files and directories can be cleared.

#### 3.3 .well-known directory cannot be created in Windows system
In Windows, you cannot create files and folders beginning with a dot, such as `.log`, by `right-clicking => New`, and you will be prompted to enter a file name if doing so.
You can create files and folders through a command line:

New Folder
```
mkdir .well-known
```

