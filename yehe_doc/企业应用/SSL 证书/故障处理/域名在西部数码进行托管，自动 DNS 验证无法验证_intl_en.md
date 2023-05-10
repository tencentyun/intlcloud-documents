## Symptom

The domain hosted with www.west.cn failed the automatic DNS validation.

## Solutions

On the DNS server of www.west.cn, the TXT record value added for the domain cannot be validated, and the CNAME validation will not be redirected to automatically. Therefore, the ownership of domains hosted with www.west.cn cannot be verified.
You can solve the issue in either of the following ways:
- Point the DNS server address of the domain to the DNSPod server address and perform DNS query in Tencent Cloud. 
  

   > **Notes**
   > 
   > Different DNSPod plans correspond to different DNS addresses.
   > 

- Verify the domain ownership through automatic file validation.
