### 1. Domain name statuses in whois
When viewing whois information of a domain name, there is a **Domain Name Status** bar which shows the current status of the domain name. A domain name can have more than one status. Knowing the meaning of various statuses helps you understand the reason for using domain names, so that you can take appropriate measures in time.

There are several situations: Statuses that start with "client" are initiated by the registrar, and those start with "server" are initiated by CNNIC (China Internet Network Information Center).
ACTIVE (OK): Normal status. This indicates that no action is required and no protection measure is configured. When the domain is in other statuses, OK is not displayed, but that does not definitely mean the domain is abnormal. 
INACTIVE: Domain name is inactive. This indicates that DNS server is not provided during the registration, and the domain name cannot be resolved.

**When a domain name is locked for security reasons, the following statuses may be displayed:**
**client Delete Prohibited:** Delete prohibition set by the registrar.
**server Delete Prohibited:** Delete prohibition set by the Registry.
**client Update Prohibited:** Update prohibition set by the registrar. This indicates that you are not allowed to change the domain name information, but you can set or update the resolution records.
**server Update Prohibited:** Update prohibition set by the Registry. This indicates that you are not allowed to change the domain name information, but you can set or update the resolution records.
**client Transfer Prohibited:** Transfer prohibition set by the registrar. This indicates that the domain name cannot be transferred to another registrar.
**server Transfer Prohibited:** Transfer prohibition set by the Registry. The Registry may attach this status to some domain names that are within 60 days after registration or register change. In such cases, it is automatically removed after 60 days. This status can also be set because the domain name is involved in arbitration or litigation. Likewise, it is automatically removed after the arbitration or litigation process.


**Other statuses regarding resolution prohibition and renew prohibition include:**
**client Renew Prohibited:** Renew prohibition set by the registrar. This indicates that the domain name cannot be renewed. The domain name may be in arbitration. You can contact the registrar to find the reason.
**server Renew Prohibited:** Renew prohibition set by the Registry. This indicates that the domain name cannot be renewed. The domain name may be in arbitration. You can contact the registrar to find the reason.
**client Hold:** Domain name resolution held by the registrar. You must contact the registrar to remove this status.
**server Hold:** Domain name resolution held by the Registry. This status occurs when the identity verification for a .com/.cn/.net domain name fails. It is removed if the identity verification is approved.
**pending Transfer:** Indicates that the domain name is being transferred to another registrar.
**pending Verification:** Registration verification period. This indicates that the domain name is subjected to the identity verification. You must provide the verification material within five days after you purchase your domain name. The status turns to ServerHold in five days if the identity verification fails.

### 2. Domain name expiration statuses

A. The domain name will be in REGISTRAR HOLD (held by registrar) status within 1-45 days after it expires.
B. When REGISTRAR HOLD status ends, the domain name will go into a 30-day redemption period, in which case the status becomes REDEMPTION PERIOD (grace period).
C. When REDEMPTION PERIOD ends, the domain name will go into a 6-day pending deletion period, and it will be deleted after 6 days. In this case, the status turns to PENDING Delete (being deleted), and the domain name will become available again for registration after deletion.
D. The status REGISTRAR/REGISTRY LOCK means the domain name is locked by the registrar/registry to prevent transfer to another registrar after it expires.

For more information, see [Tencent Cloud DNS](https://cloud.tencent.com/document/product/302) and [Domain Name Identity Verification](https://cloud.tencent.com/document/product/242/6707).
If you have any other questions, [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=16&level2_id=17&level1_name=%E5%85%B6%E4%BB%96%E6%9C%8D%E5%8A%A1&level2_name=%E5%9F%9F%E5%90%8D).






