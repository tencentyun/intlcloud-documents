## TCSS Overview
TCSS provides rich security features such as container asset management, image security, and runtime intrusion detection. It safeguards containers through their entire lifecycle from image generation and storage to runtime and helps you set up a container security protection system.
## Why TCSS
A variety of risks are involved throughout the lifecycle of a container, including:
- Runtime environment security risks, such as vulnerabilities in OS components, unnecessary ports opened due to improper configuration, improper user access permissions, and shared OS kernel.
- Image security risks, such as vulnerabilities in the image, malware, key in plaintext, improper image configuration, and use of non-trusted images.
- Container security risks, such as vulnerabilities in the application, embedded viruses and trojans, and improper container resource configuration.

TCSS can safeguard containers against the above risks throughout their lifecycle.

## Features
### Asset management
TCSS leverages the automatic asset inventory feature to visualize key assets, such as containers, images, image repositories, and servers.

### Image security
TCSS scans images and image repositories for vulnerabilities, trojans, viruses, sensitive information, and more.

### Runtime security
TCSS identifies hacker attacks adaptively, monitors and protects container runtime security in real time, and utilizes diversified security features, including container escape, process blocklist/allowlist, and file access control.

### Security baseline
TCSS supports CIS Benchmarks for containers, images, servers, and other container environment configurations, displays multidimensional baseline compliance of container assets, and helps set up baseline configurations in the container running environment.

### Cluster security
TCSS supports scanning clusters for vulnerabilities and configuration risks automatically or manually and aggregates the data of risky clusters in the business environment and risks in each cluster.

## Additional Services
- To fix environment consistency issues during user development, testing, and Ops and offer a container-centered, highly scalable, and high-performance container management service based on native Kubernetes, see [Tencent Kubernetes Engine](https://intl.cloud.tencent.com/document/product/457).
- To create dedicated instances in multiple regions around the world to pull container images nearby faster at lower bandwidth costs, see [Tencent Container Registry](https://intl.cloud.tencent.com/document/product/1051).
