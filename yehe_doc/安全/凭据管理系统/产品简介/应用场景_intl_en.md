## Managing Secrets Centrally
- **Use case**: to achieve agile development, there will be lots of sensitive information (i.e., account information, tokens, certificates, SSH keys, and API keys) in the system. Therefore, there is a need to store, retrieve, use, and manage sensitive secrets through their lifecycle.
- **Use case example**: managing secrets through their lifecycle, such as storing encrypted secrets of sensitive configuration for multiple applications, and querying and managing secrets.
- **Risk**: hardcoding of sensitive secrets, disorganized permission management, and difficult management of hosted secrets.
- **Solution**: developers can go to the [SSM console](https://console.cloud.tencent.com/ssm) or use the SDK or CLI to create, use, and store secrets of sensitive configuration. By using SSM together with CAM and CloudAudit, business users can manage enterprise secrets centrally through their lifecycle.

![](https://main.qcloudimg.com/raw/85adda96af872f373f1d7a1241466f46.png)
## Managing Sensitive Secret Retrieval
- **Use case**: during access to an application or service, users need to create certificates (i.e., passwords, tokens, certificates, SSH keys, or API keys) for authentication. Normally, confidential information is embedded in the configuration file of the application, which offers lower security. SSM enables you to effectively avoid risks such as the hardcoding of sensitive secrets.
- **Use case example**: replacing database credentials, API keys, and account passwords.
- **Risk**: information leakage of sensitive secrets.
- **Solution**: users can replace hard-coded secrets (including passwords) with SSM APIs in the code to facilitate dynamic secret queries. Since the secret does not contain sensitive information, keys will not be leaked.
![](https://main.qcloudimg.com/raw/32b29397aabbdde56a7b441353c7e939.png)

## Rotating Secrets
- **Use case**: to improve system security, sensitive secrets need to be updated periodically. Users can update secrets with SSM.
- **Use case example**: rotating secrets at the application layer.
- **Risk**: during secret rotation, the update needs to be synced across dependent applications and configurations. For a multi-application system, it is easy to miss an application, possibly resulting in application interruption.
- **Solution**: you can add a secret version on the SSM console, or call APIs to update the content of the target secret. Users can decide whether to rotate secrets fully or for beta tests to sync the update across all dependent application points.
![](https://main.qcloudimg.com/raw/eb105214ca80e8dc4007d387354cceb7.png)
