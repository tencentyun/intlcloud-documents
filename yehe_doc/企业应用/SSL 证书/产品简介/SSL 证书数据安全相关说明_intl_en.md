### Uploading certificates
When you upload SSL certificates in the SSL Certificates Service console, HTTPS is used for communication throughout the process, and the OV SSL certificates issued by SecureSite are used for encryption to ensure data communication security.

### Hosting certificates
- The certificates uploaded are stored in Tencent Cloud’s databases and are encrypted using the Advanced Encryption Standard and Cipher Block Chaining. The key is 128 bits long, which would take 210.4 billion years to break even using the most powerful computer we have currently.
- To improve the availability and security of certificate data, Tencent Cloud has deployed three certificate databases across two regions, including a primary database, a hot backup database, and a cold backup database. They use private networks, have no externally exposed APIs, and are protected by Secure Tencent Gateway (STGW).
- There are 6 backend servers for SSL certificates, which are accessed via a load balancer to ensure API stability.

### Accessing and reading certificates
- **Accessing**
SSL Certificate Service has integrated resource-level CAM. It’s backed by a well-established access management system that allows you to grant different access to different certificates on a per sub-account basis to prevent malicious revocation, deletion, etc.
- **Reading**
Certificate reading by other Tencent Cloud services (e.g., Anti-DDoS):
 - SSL Certificate Service is interconnected with Tencent Cloud services including CLB, CDN, WAF, Anti-DDOS, CSS, etc., which can read SSL certificates via private APIs when necessary.
 - The certificate reading process is also protected by STGW. Other Tencent Cloud services are supposed to read the certificates only when necessary. Requests are validated and authenticated to prevent unauthorized and unnecessary access.
