## 1. BACKGROUND

This Module applies if you use Tencent Container Security Service (“**Feature**”). This Module is incorporated into the Data Processing and Security Agreement located at (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)”). Terms used but not defined in this Module shall have the meaning given to them in the DPSA. In the event of any conflict between the DPSA and this Module, this Module shall apply to the extent of the inconsistency.

## 2. PROCESSING

We will process the following data in connection with the Feature:

| **Personal Information**                                     | **Use**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Asset Basic Data:** Basic information of your servers, containers, images and clusters (asset fingerprint information (resource monitoring, accounts, ports, software applications, processes, databases, web applications, web services, web frameworks, web sites, Jar packages startup services, scheduled tasks, environment variables, kernel modules), basic information of image repository (image repository address, repository type, image name, image ID, image version, image size, security risks (including security vulnerabilities, Trojan viruses, sensitive information), construction history) | We only process this data for the purposes of providing the Feature to you.<br/>Please note that this data is stored and backed up in our TencentDB for MongoDB (MongoDB) and TencentDB for MySQL (MySQL) features, temporarily stored and backed up in our Cloud Object Storage (COS) feature,  and integrated with the relevant Hosting Service (as defined in the Privacy Policy module for this Feature) you are subscribed to. If you have purchased our Tencent Kubernetes Engine (TKE) cluster, basic information of image repository is also shared with us upon your authorization, for the purpose of providing the Feature to you (including to conduct security checks). |
| **Console Configuration Data**: <br/><li>Configuration of image, cluster, vulnerability, baseline, file,  log detection: regular detection, ignore vulnerability / baseline, your confirmation to trust file or isolate file, intercept process, intercept image, intercept container network access)<li>Whitelist configuration for container escape, bounce shell, file check, abnormal process, file tampering, high-risk system drop call and other intrusion prevention features: whitelist conditions, effective mirror range<br/>Other configuration information: automatic server upgrade protection settings, automatic renewal settings, alarm settings | We only process this data for the purposes of providing the Feature to you in accordance to your specific configuration.<br/>Please note that this data is stored and backed up in our TencentDB for MongoDB (MongoDB) and TencentDB for MySQL (MySQL) features, and integrated with the relevant Hosting Service (as defined in the Privacy Policy module for this Feature) you are subscribed to. |

## 3. SERVICE REGION

As specified in the DPSA.

## 4. SUB-PROCESSORS

As specified in the DPSA.

## 5. DATA RETENTION

We will store personal data processed in connection with the Feature as follows:

| **Personal Information**              | **Retention Policy**                                         |
| ------------------------------------- | ------------------------------------------------------------ |
| Asset Basic Data<br/>[Security Event Data] | We retain such data for a minimum of 180 days. We retain such data until you terminate your use of the relevant Hosting Service(s), in which case we will temporarily retain this data in our COS feature delete the same for (i) 30 days thereafter or (ii) the minimum number of days required to meet the 180-days minimum data retention threshold (as applicable). |
| Console Configuration Data            | Stored until you request for deletion, upon which such data will be deleted within 30 working days. Where you do not request for deletion, such data will be deleted after 1 month of termination of your use of this Feature, unless otherwise required by applicable data protection laws. |

You can request deletion of such personal data in accordance with the DPSA.

## 6. SPECIAL CONDITIONS

You must ensure that this Feature is only used by end users who are of at least the minimum age at which an individual can consent to the processing of their personal data. This may be different depending on the jurisdiction in which an end user is located.

This Feature is not intended for the processing of sensitive data. You must ensure that this Feature is not used to transfer or otherwise process any sensitive data by you or your end users.
