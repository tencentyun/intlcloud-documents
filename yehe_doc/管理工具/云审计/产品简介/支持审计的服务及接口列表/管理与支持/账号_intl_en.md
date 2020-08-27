Tencent Cloud Account Center provides services such as account information management, identity verification information change, and account security management. After signing up for a Tencent Cloud account, you can manage your accounts in the Account Center Console conveniently and efficiently, saving your maintenance time costs.

Account operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
| -------------------------- | -------- | ---------------------------- |
| Applying for account deregistration               | account  | ApplyAccountDeactivation     |
| Associating account with secondary confirmation information        | account  | BindAccountByTicket          |
| Associating account with email address            | account  | BindMailAccount              |
| Binding token              | account  | BindToken                    |
| Modifying email account password           | account  | ChangeMailPassword           |
| Logging in to account        | account  | ConsoleLogin                 |
| Creating identity verification FaceIn token | account  | CreateAuthDetectToken        |
| Modifying user email address               | account  | ModifyMail                   |
| Modifying user mobile number           | account  | ModifyPhoneNum               |
| Viewing API key plaintext          | account  | QueryKeyBySecretId           |
| Setting unusual login location protection           | account  | SetOffsiteLoginFlag          |
| Setting security protection               | account  | SetSafeAuthFlag              |
| Submitting bank card authentication information             | account  | SubmitBankAuthInfo           |
| Submitting FaceIn identity verification information       | account  | SubmitDetectAuthInfo         |
| Submitting basic information for organizational identity verification   | account  | SubmitEnterpriseBaseAuthInfo |
| Submitting Midas identity verification information         | account  | SubmitMidasAuthInfo          |
| Submitting basic information for personal identity verification   | account  | SubmitPersonalBaseAuthInfo   |
| Submitting top-up authentication information               | account  | SubmitTopUpAuthInfo          |
| Unbinding account            | account  | UnbindAccount                |
| Unbinding token              | account  | UnbindToken                  |
| Updating organization contact information         | account  | UpdateEnterpriseContact      |