### What is the private key password for an SSL certificate?
An SSL certificate uses public key encryption and symmetric key encryption to encrypt data transmission between the client and server, so as to ensure data confidentiality and integrity as well as identity authenticity of the communicating parties. Private key disclosure for an SSL certificate will result in disclosed keys of encrypted sessions, posing the risk of website data leakage. A private key password for the SSL certificate provides an additional layer of security to the private key.

When you apply for a Tencent Cloud SSL certificate, a private key password option will be available. If you specify a private key password, the private key file in the issued SSL certificate will be protected with this password. If you do not specify a private key password, a private key password will be automatically generated, and the private key password file (e.g., `keystorePass.txt`) will be contained in the package.


### When will I use a private key password?
Generally, you need to use a private key password when installing an SSL certificate to a web service. For example, when you install an SSL certificate on a Tomcat server, the field `keystorePass=` represents the private key password.

### What should I pay attention to regarding a private key password?
- If you want to specify a private key password when applying for a Tencent Cloud SSL certificate, set a complex one.
- Keep your private key password properly for security of your SSL certificate.
- Keep your private key password confidential. Tencent Cloud will not store your private key password. For more information, see [Forgot Your Private Key Password?](https://intl.cloud.tencent.com/document/product/1007/30191).
