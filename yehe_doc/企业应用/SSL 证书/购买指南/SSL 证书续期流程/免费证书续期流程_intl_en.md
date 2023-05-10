Due to changes in Apple and Google root store policies, global CAs have ceased issuing SSL certificates with a validity period greater than two years since September 1, 2020. Therefore, renewing an SSL certificate is equivalent to applying for a new one in the console, and the old certificate will not have a longer validity period. After the new certificate is issued, you need to reinstall it on the server, which takes effect upon deployment.
For detailed directions on how to install a certificate, see [Installing Certificate](https://write.woa.com/#certificate). If the old certificate is within the validity period, its use will not be affected.

> **Notes**
> 
>  Renewing a free certificate is free of charge.
> 


## Renewal Process for Free Certificates

### Step 1. Quickly apply for a new free certificate
1. For a free certificate, the quick renewal option will become available **one month before its expiration date**. You can open the **Quick Certification Reapplication** page by clicking **Quick Renewal** in the **Status** column of the certificate in **My Certificates** in the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl).

2. On the **Submit Information** page, confirm your application and click **Next** to enter the **Select Validation Method** page.

### Step 2. Validate the domain
1. On the **Select Validation Method** page, select the validation method.

  - **Adds DNS validation automatically**: For more information, see [Details](https://www.tencentcloud.com/document/product/1007/53635).
    

      > **Notes**
      > 
      > If the domain applied for has been successfully hosted in the [DNSPod console](https://console.cloud.tencent.com/cns/domains), DNS validation can be added automatically.
      > 

  - **DNS validation**: For more information, see [DNS Validation](https://intl.cloud.tencent.com/document/product/1007/45895).

  - **File validation**: For more information, see [File Validation](https://intl.cloud.tencent.com/document/product/1007/43542).

2. Complete the domain identity verification as prompted by **Validation Instruction**.
   

   > **Notes**
   > Click **View Domain Validation Status** to view the current status of the domain validation. 
   >   - Validating: The system is validating the domain.
   >   - Pending validation: The domain validation operation is to be added.
   >   - Validation timeout: The system validation failed after more than 30 seconds.
   >   - Passed: The domain validation has been passed.
   >   - Failed: The domain validation is not completed within the validation period.

3. After the domain validation is passed, the CA will issue the certificate within 24 hours.


## Download and Deployment
- After the domain validation is completed, log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), select the issued certificate, and click **Download** to download and install it. For detailed directions, see [Installing Certificate](https://write.woa.com/#certificate).

- You can directly deploy a certificate on a Tencent Cloud service as instructed in [Selecting an Installation Type for an SSL Certificate](https://intl.cloud.tencent.com/document/product/1007/30173).


## Certificate Installation Documentation

After the certificate is issued successfully, you need to reinstall it based on the server type.

> **Notes**
> The quick HTTPS feature helps you upgrade from HTTP to HTTPS without tedious SSL certificate deployment.

- International standard certificates:

  - Linux system:

    - [Installing an SSL Certificate on an Apache Server (Linux)](https://intl.cloud.tencent.com/document/product/1007/30953)

    - [Installing an SSL Certificate on an Nginx Server](https://intl.cloud.tencent.com/document/product/1007/30954)

    - [Installing an SSL Certificate (JKS Format) on a Tomcat Server](https://www.tencentcloud.com/document/product/1007/50805)

    - [Installing an SSL Certificate (PFX Format) on a Tomcat Server](https://intl.cloud.tencent.com/document/product/1007/30956)

    - [Installing an SSL Certificate on a GlassFish Server](https://intl.cloud.tencent.com/document/product/1007/36565)

    - [Installing an SSL Certificate on a JBoss Server](https://intl.cloud.tencent.com/document/product/1007/36566)

    - [Installing an SSL Certificate on a Jetty Server](https://intl.cloud.tencent.com/document/product/1007/36567)

  - Windows system:

    - [Install a certificate on an IIS server](https://intl.cloud.tencent.com/document/product/1007/30955)

    - [Installing a Certificate on WebLogic Servers](https://intl.cloud.tencent.com/document/product/1007/38093)

    - [Installing an SSL Certificate on an Apache Server (Windows)](https://intl.cloud.tencent.com/document/product/1007/50198)

    - [Installing an SSL Certificate (JKS Format) on a Tomcat Server](https://intl.cloud.tencent.com/document/product/1007/43804)


## FAQs
- [Quota of Free SSL Certificates](https://intl.cloud.tencent.com/document/product/1007/51464)

- [Can the TXT Records for Domain Name Resolution Configured in the Certificate Be Deleted?](https://intl.cloud.tencent.com/document/product/1007/37851)

- [Forgot Your Private Key Password?](https://intl.cloud.tencent.com/document/product/1007/30191)

