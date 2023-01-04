
## Container image protection
Images are vulnerable to application vulnerabilities, viruses, trojans, and sensitive information leakage. TCSS supports thorough image checks throughout the lifecycle from build and shipping to running. It can detect security risks to images and control image running. It also allows you to customize rules to protect images.
![](https://qcloudimg.tencent-cloud.cn/raw/acb3edc93a5a7925e99837d04961b8f8.png)

## Container escape attack detection
Containers are poorly isolated, and attackers can utilize sensitive path mounting and vulnerabilities to escape to the host, which directly affects the confidentiality, integrity, and availability of the underlying infrastructure. TCSS supports detecting a variety of escapes, such as:
- Escape caused by the container running in privileged mode.
- Container escape caused by dangerous mounting (mounting of the Docker socket and proc file system of the host).
- Privilege escalation caused by the switch from a general account to a root account during the container process.
- Capability privilege escalation during the container process.
- Mount file namespace isolation broken during the container process.
- Blocklist limits broken by seccomp syscall during the container process.
- Modification of a host file not mounted to the container during the process (such as CVE-2019-5736).

![](https://qcloudimg.tencent-cloud.cn/raw/1b098eaad28a236682b7815ed314d78c.png)
