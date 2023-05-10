Renewing an SSL certificate is equivalent to applying for a new one in the console, and you need to install and deploy it on the server. The new certificate does not affect the use of the existing one.

> **Notes**
> 
> - If you need to modify the certificate information, apply for a new one.
> - Renewing a certificate is equivalent to issuing a new one, and you need to replace the existing one with the new one.
> - Renewing a free certificate is free of charge. Specifically, you can reapply for a certificate as instructed in [Renewal Process for Free DV SSL Certificates](https://www.tencentcloud.com/document/product/1007/53633).


## Advantages of Renewal

Renewing the existing certificate holds the following advantages over purchasing a new one:  

### Simplified renewal procedure

Instead of entering application information again, you only need to confirm the original certificate's application data pulled automatically by the system and proceed with the payment. After making the payment, upload the confirmation letter and wait for certificate review.

> **Notes**
> 
> After renewing a WoTrus international standard certificate or DNSPod Chinese SM (SM2) certificate, you can directly enter the domain identity verification process without uploading the confirmation letter again.
> 


### Extra-prolonged certificate validity after renewal

After renewal, the remaining validity period of the original certificate will roll to the validity period of the new certificate.

> **Notes**
> 
> - The quick renewal option will become available **within 30 calendar days before** a paid certificate expires, and the validity period of a renewed certificate **cannot exceed 398 days**.
> - The expiration reminder will be sent on the second calendar day after the quick renewal option becomes available. Renew your certificate as soon as possible upon receiving the reminder.


## Renewal Process for Paid Certificates

### Step 1. Enter the certificate renewal entry
1. For a paid certificate, the quick renewal option will become available **one month before its expiration date**. You can open the **Quick Renewal** window by clicking **Quick Renewal** in the **Status** column of the certificate in **My Certificates** in the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl).

2. In the SSL certificate renewal pop-up window, confirm the information and click **Renew** to enter the renewal page.


### Step 2. Confirm the renewal information and make the payment
1. When renewing a certificate, you do not need to enter the certificate information again. A new certificate will be generated after the renewal, so you need to configure a CSR file for the new certificate.

  - You can automatically generate a CSR file through the system (**this option is recommended, and the CSR and private key can be generated**).

  - You can also upload a CSR file (**no private key can be generated with this option**).

2. After confirming the information, select the renewal period and click **Quick Payment** to enter the payment process.

3. Confirm the certificate information, click **Purchase**, and make the payment.


### Step 3. Submit the certificate for review

> **Notes**
> 
> - It is estimated to take **3–5 business days** to issue an OV certificate and **5–7 business days** to issue an EV one.
> - It is estimated to take **10 minutes to 24 hours** to issue a DV certificate.


#### Renewing a paid WoTrus OV/EV certificate

A renewed WoTrus OV/EV certificate will be issued only after manual approval and domain validation.

> **Notes**
> 
> After you applied, there will be a manual review, during which you will receive a call from the US to your organization's business registration number.
> 


#### Renewing a DNSPod Chinese SM (SM2) OV/EV certificate

A renewed DNSPod Chinese SM (SM2) OV/EV certificate will be issued only after manual approval and domain validation.

> **Notes**
> 
> - The first domain validation will remain valid for 13 months from approval, during which no domain validation will be performed if you apply for a DNSPod Chinese SM (SM2) OV/EV SSL certificate with the same organization name for the domain.
> - The certificate will be issued only after manual approval and domain validation.
> - Manual approval will not be required if you apply for a certificate with the same information after having successfully applied for a certificate of the same type.


#### Renewing a paid OV/EV certificate of another brand
1. After purchasing a certificate successfully, a new certificate in **Pending confirmation letter upload** status will be generated in the certificate list in the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl). Then, click **Upload Confirmation Letter** to enter the confirmation letter details page.    

2. Click to **download the confirmation letter template**, enter the required information, print it out, and affix the official seal.

3. Click **Upload**.

4. After the confirmation letter is uploaded, the **Certificate Status** will change to **Pending validation**, and you need to wait for the verification call from the reviewer as well as the domain confirmation email.


#### Renewing a paid DV certificate
1. After purchasing a certificate successfully, a new certificate in **Pending validation** status will be generated in the certificate list in the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl). Then, click **Details** to enter the **Certificate Details** page.   

2. Add a DNS record based on the validation value on the **Certificate Details** page.

3. Wait for scan and validation by the CA. The certificate will be issued immediately after approval.


## Certificate Installation Documentation

After the certificate is issued successfully, you need to reinstall it based on its encryption standard type and server type.

> **Notes**
> 
> The quick HTTPS feature helps you upgrade from HTTP to HTTPS without tedious SSL certificate deployment.
> 

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


