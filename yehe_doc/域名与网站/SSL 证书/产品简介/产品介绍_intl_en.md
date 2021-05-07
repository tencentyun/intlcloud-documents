## Overview
SSL Certificates are also known as digital certificates. Tencent Cloud works with well-known Certificate Authorities (CA) to allow users to apply for, manage, and deploy free/paid SSL certificates, which enable HTTPS to identify identities and encrypt data for your websites, apps, and web APIs.


## SSL and HTTPS
An encrypted HTTP protocol based on the SSL certificate for secure data transmission enables a site to be switched from Hypertext Transfer Protocol (HTTP) to Hyper Text Transfer Protocol over Secure Socket Layer (HTTPS).

After you purchase an SSL certificate via Tencent Cloud, you can ask CA to sign and issue it through the SSL Certificate Service console. Once the certificate is issued, you can download and deploy it to the web service of your server. Alternatively, you can deploy it to your Tencent Cloud resources with one click. In this way, your web services or cloud resources can transfer data over HTTPS.


## Advantages of HTTPS
<table>
<thead>
  <tr>
    <th width="20%">Advantage</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Anti-hijacking/tampering/listening</td>
    <td>HTTPS encrypts data transferred between the server and client for your websites, apps, and web APIs to prevent your data from being hijacked, tampered, or listened to.</td>
  </tr>
  <tr>
    <td>Improving rankings in SEO</td>
    <td>HTTPS websites are more trusted by search engines. Therefore, your websites can be collected faster and rank higher.</td>
		</tr>
		  <tr>
    <td>Increasing PV</td>
    <td>Users trust HTTPS websites more. Therefore, they will feel securer to visit your websites and thus your PV can be increased.</td>
		</tr>
		  <tr>
    <td>Avoiding phishing websites</td>
    <td>The green icon on the HTTPS address bar helps users identify phishing websites, protecting user and business interests and enhancing user trust.</td>
		</tr>
		</thead>
</table>

## Supported Certificate Types and Brands

Tencent Cloud supports the following encryption standards of certificates:

<table>
<thead>
  <tr>
    <th>Encryption Standard</th>
    <th>Certificate Type</th>
    <th>Certificate Brand</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>International standard</td>
    <td>DV, OV, EV, OV Pro, EV Pro</td>
    <td>SecureSite, GeoTrust, TrustAsia, GlobalSign, Wotrus</td>
  </tr>
  <tr>
    <td>Chinese cryptographic standard</td>
    <td>DV, OV, EV</td>
    <td>DNSPod</td>
		</tr>
</table>


## Certificate Type Description
The following table describes the trust levels and use cases of the three certificate types:
<table>
<thead>
  <tr>
    <th>SSL Certificate Type</th>
    <th>Trust Level</th>
		<th>Use Case</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>DV</td>
    <td>Average</td>
		 <td>For general websites. The certificate can be issued if the website authenticity is verified.</td>
  </tr>
  <tr>
    <td>OV</td>
    <td>High</td>
				 <td>For organization websites. The certificate can only be issued if the organization is verified, making it more restrictive and secure.</td>
		</tr>
		  <tr>
    <td>EV</td>
    <td>Highest</td>
		 <td>Usually for banks, securities companies, and other financial institutions. It requires rigorous auditing to ensure the highest security. The address bar turns green after the EV SSL certificate is deployed.</td>
		</tr>
</table>

## References
When purchasing a certificate, you can refer to the following documents:
- [Certificate Type Selection Cases](https://intl.cloud.tencent.com/document/product/1007/37811)
- [Certificate Brands](https://intl.cloud.tencent.com/document/product/1007/37810)

