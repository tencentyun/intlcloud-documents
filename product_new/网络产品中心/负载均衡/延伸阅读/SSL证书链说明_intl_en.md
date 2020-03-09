## Definition of SSL certificate chain

There are two types of certificate authorities (CAs): root CAs and intermediate CAs. For an SSL certificate to be trusted, it must be issued by a CA included in the trusted store connected to by the device.
	
If the certificate is not issued by a trusted CA, the connecting device (e.g., a web browser) will check whether the certificate is issued by a trusted CA until no trusted CA can be found.
	
The list of SSL certificates goes from root certificate to intermediate certificate and then to end-user certificate.

## Example of SSL certificate chain
	
Assume that you purchase a certificate from Qcloud CA and the domain name is `example.qcloud`.

Qcloud is not a root certificate authority. In other words, its certificate is not directly embedded in your web browser and cannot be explicitly trusted.

- Qcloud utilizes a certificate issued by Alpha, an intermediate Qcloud CA.
- Alpha utilizes a certificate issued by Beta, an intermediate Qcloud CA.
- Beta utilizes a certificate issued by Gamma, an intermediate Qcloud CA.
- Gamma utilizes a certificate issued by the Root of Qcloud.
- The Root of Qcloud is a root CA. Its certificate is directly embedded in your web browser and can be explicitly trusted.

In the above example, SSL certificate chain is represented by 6 certificates:
1. End-user certificate: issued to `example.qcloud` by Qcloud CA.
2. Intermediate certificate 1: issued to `example.qcloud` by Alpha, an intermediate Qcloud CA.
3. Intermediate certificate 2: issued to Alpha by Beta, an intermediate Qcloud CA.
4. Intermediate certificate 3: issued to Beta by Gamma, an intermediate Qcloud CA.
5. Intermediate certificate 4: issued to Gamma by the Root of Qcloud.
6. Root certificate: issued by and to the Root of Qcloud.

Certificate 1 is called end-user certificate, certificates 2–5 are called intermediate certificates, and certificate 6 is called root certificate.

When you install your end-user certificate `example.qcloud`, you must bundle all intermediate certificates and install them along with the end-user certificate. If the SSL certificate chain is invalid or broken, your certificate will no longer be trusted by some devices.







