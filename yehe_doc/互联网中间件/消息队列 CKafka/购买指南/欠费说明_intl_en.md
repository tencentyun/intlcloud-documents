## Expiration Alerts
Starting from 7 days before the Ckafka instance expires, you will receive an expiration alert every other day. Tencent Cloud account creator and and all collaborators will be notified via **email and SMS**.

## Arrears Alerts
Starting on the day when the CKafka instance expires, you will receive an arrears alert every other day. Tencent Cloud account creator and all collaborators will be notified via **email and SMS**.


## Repossession Mechanism
- Seven days before the Ckafka instance expires, you will receive a renewal reminder. 
- If your account balance is sufficient and auto-renewal is enabled, the device will be automatically renewed on the expiry date of the CKafka instance.
- If the CKafka instance is not renewed within 7 days (inclusive) after expiration, it will be disabled at midnight on the 8th day (devices are disconnected and shut down, CKafka services are suspended, and only data and configurations are retained).
After shutdown, the CKafka instance will be **forcibly unmounted** from upstream and downstream components. Upon renewal, its mounting relationship **cannot be restored** and must be reconfigured.
- If the CKafka instance is not renewed within 14 days (inclusive) after expiration, its resources will be released at midnight on the 15th day, and **data will be cleared and cannot be restored**.

