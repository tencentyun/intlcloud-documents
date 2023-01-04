Image security quickly checks local images and repository images for vulnerabilities, trojans, viruses, sensitive data, and more.

## Image security risks
- An image is a static representation of a container, and its security determines the security of container runtime.
- Image security risks originate from the creation process, acquisition source, and acquisition means. An image may be risky in the following cases:
 - The image contains vulnerabilities or is embedded with malicious scripts, which means that the generated container may contain vulnerabilities or be maliciously exploited.
>? For example, an attacker constructs a special compressed image file and triggers the vulnerability during compilation to get the permission to execute arbitrary code. 

 - If `USER` is not specified in the image, the container created from the image will be run by the root user by default. When the container is attacked, the access of the root user to the host may be compromised. 
 - Data may be leaked if the image file storing fixed passwords or other sensitive data is published. 
 - The attack surface will be expanded if unnecessary applications such as SSH and Telnet are added when the image is written.

## Repository image security risks
As a tool to set up private image repositories, an image repository is mainly subject to security risks from itself and transfer security risks during image pull.
- Repository security: If an image repository, especially a private one, is controlled by a malicious attacker, all its images will be at risk.
>? For example, if port 2357 is opened due to improper configuration in a private image repository, the repository will be exposed to the public network, which means that attackers can directly access it and tamper with its content, causing security risks. 

- Image pull security: Image security also concerns the container image integrity from the image repository to the user end.
>? For example, if a user pulls an image in plaintext, the interaction with the image repository will be vulnerable to man-in-the-middle attacks. In this case, the pulled image will be tampered with during transfer, or a malicious image with the same name will be released, causing security risks to the image repository and user.
