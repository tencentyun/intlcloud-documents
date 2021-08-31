## Symptoms
After the SSL certificate is deployed, the <span ><img src="https://main.qcloudimg.com/raw/fd19301d82877dddfb19dbba29366b17.png" style="margin-bottom:-5px;"/></span> icon and the “Not Secure” warning are displayed in the address bar when you access the website over HTTPS. If you click <span ><img src="https://main.qcloudimg.com/raw/fd19301d82877dddfb19dbba29366b17.png" style="margin-bottom:-5px;"/></span>, a warning in red, “Your connection is not secure”, is displayed, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2d888b282338233cc992a8761d5bd400.png)

## Possible Causes
- **Expired SSL certificate**: To ensure the security of private keys, SSL certificates are only effective for a period of time. According to the latest international standard, an SSL certificate can be effective for one year at most. If your SSL certificate has expired but is not replaced in time, the “Not secure” warning in red will be displayed on your website.
- **Insecure website content**: If your website has configured an SSL certificate, but calls external resources such as images and JavaScript files that do not use HTTPS, “Your connection is not secure” may be displayed on your website. If users choose to load the insecure content, the browser will further display the red “Not Secure” warning.


## Solutions
### Expired SSL certificate
Replace the expired SSL certificate as soon as possible. Then, reapply for a new certificate and deploy it to the website server. The following documents are for your reference:
1. [Selecting an Installation Type for an SSL Certificate](https://intl.cloud.tencent.com/document/product/1007/30173)


### Insecure website content
You can copy the external link to the address bar and append an “s” to the “http” to see whether the external link supports HTTPS access.
- If yes, change “http” to “https” in the code directly.
- If not, download the resources to the local server, modify the resource path to that on your server, and use a relative path such as `image/button.gif`, or a complete HTTPS URL such as `https://***/image/button.gif`.

