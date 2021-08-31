## Error Description
After the SSL certificate is deployed in IIS, a 404 error is reported when you access resources.

## Possible Causes
- The websites bound to HTTP and HTTPS are different.
- The website configuration is incorrect.

## Solutions
After the certificate is successfully deployed, resources can be accessed over HTTP but not HTTPS (with a 404 error). In this case, if you have configured the SSL certificate in IIS and enabled port 443 in the firewall, you can troubleshoot as follows:
- The website’s root directory can be set differently for HTTP and HTTPS. On the IIS server, check how port 443 is bound and confirm whether the website bound to port 443 is the same as that bound to HTTP port 80.
- When you check the port binding, check whether the IP address and hostname of the website are correct.



