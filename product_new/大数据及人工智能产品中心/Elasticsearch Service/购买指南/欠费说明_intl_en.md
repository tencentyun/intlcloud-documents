### Repossession mechanism
- The system will send you a renewal notification within 7 days prior to the expiry of your ES cluster.
- If your account balance is sufficient and you have enabled auto-renewal, your ES cluster will be auto-renewed on the date of expiry.
- If your ES cluster is not renewed prior to or upon expiry, the system will disable it upon expiry (your cluster will become inaccessible, and only data will be retained).
- Within 7 days of expiry, you can still renew your ES cluster to resume access to it, and the renewed instance will be deemed to have been renewed on the expiry of the previous period.
- If your ES cluster is not renewed within 7 days after expiry, the system will start to release the resources at midnight on the 8th day after expiry, and **the data in your ES cluster will be irreversibly purged**.

## Pay-as-you-go
### Alert for arrears
For resources billed on a pay-as-you-go basis, fees are deducted on the hour. When your account balance falls below zero, the system will notify the creator, global resource collaborators, and financial collaborators of your Tencent Cloud account via email and SMS.
### Arrears processing
Starting from the moment when your account balance falls below zero, your ES cluster can be used and billed for **another 2 hours**.
After 2 hours, your ES cluster will be suspended and billing will be stopped.
After the suspension of your ES cluster,
- If you top up your account within 24 hours to a positive balance, your ES cluster will continue to be billed and become accessible.
- Otherwise, your ES cluster will be inaccessible.
- If your account balance remains negative for 24 hours, your pay-as-you-go ES cluster will be repossessed, and all data will be cleared and cannot be recovered.
The system will notify the creator, global resource collaborators, and financial collaborators of your Tencent Cloud account of the repossession of your ES cluster via email and SMS.
