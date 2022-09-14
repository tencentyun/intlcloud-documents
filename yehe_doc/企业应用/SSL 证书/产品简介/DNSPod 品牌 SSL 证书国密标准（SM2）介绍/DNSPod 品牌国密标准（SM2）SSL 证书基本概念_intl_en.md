## Introduction to DNSPod SM2 certificate
SM algorithms (Chinese cryptographic algorithms) form strong foundations for ensuring autonomous and controllable network security in China. SM2 algorithm, as one of them, has been gradually popularized in the network security application field "HTTPS encryption". It leverages autonomous and controllable cryptology to protect important information transfer data on the Internet, playing a strategic role for more autonomous and controllable network security in China. Several policies have been introduced for wider and deeper application of SM algorithms in finance and other key sectors.

DNSPod SM2 certificates can fulfill the SM algorithm localization and compliance requirements that government bodies, public institutions, large state-owned enterprises, financial institutions and banks, and other clients in key sectors must follow. It also provides the "SM2/RSA" dual-certificate service to make website systems automatically adaptive to and compatible with all browsers, balancing SM algorithm compliance and universal application.
>!
>- Currently, SM certificates cannot be integrated with Tencent Cloud **CLB, CDN, DDoS Mitigation, WAF, and CSS**. For integration with other products, submit a ticket or view relevant documentation for confirmation.
>- Currently, SM certificates cannot be installed on **Tomcat Server**, **GlassFlash Server**, **JBoss Server**, **Jetty Server**, **IIS Server**, and **Weblogic Server**.


## SSL certification and encryption implementation of SM algorithms
The SSL handshake process of an SM certificate is as follows:
1. Communicate the Hello information to negotiate the cipher suite, and communicate a random number to check whether the session is reused.
2. Communicate necessary parameters and negotiate the pre-master secret.
3. Communicate certificate information for authentication.
4. Generate the master secret based on the pre-master secret and the communicated random number.
5. Send security parameters to the record layer.
6. Check whether the security parameters calculated by both parties are consistent, and whether the handshake process is authentic and complete.

To realize the above handshake process, both the client (browser) and the server need to support SM algorithms. Although SM2, SM3 and SM9 algorithms have been included in ISO systems one after another, it is still a long process to achieve wide compatibility between clients and servers. In this process, the application of SM algorithms can be further pushed by making both browsers and servers support SM algorithms and their SSL certificates based on technical solutions.
Thus, to implement SSL certification and HTTPS encryption of SM algorithms on servers, website operators needs to apply for SM-based SSL certificates from CAs accredited by MIIT of the People's Republic of China (DNSPod, for example). Then, they need to install the certificates on web servers that support SM-based certificates.
When a user visits a website that has installed SM-based certificates with an SM encrypted browser, data will be transferred between the browser and the server with SM algorithm-based encryption, implementing SSL certification and encryption of the SM algorithm.


