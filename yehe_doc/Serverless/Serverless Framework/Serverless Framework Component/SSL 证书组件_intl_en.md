## Operation Scenarios
Tencent Cloud SSL Certificates provides one-stop services for Secure Sockets Layer (SSL) certificates, including certificate application, management, and deployment.

## Directions
### Installation
Use npm to install Serverless globally:

```console
$ npm install -g serverless
```

### Configuration
Create the `serverless.yml` file locally:
```console
$ touch serverless.yml
```
Configure `serverless.yml` as follows:
```yml
# serverless.yml
SSLTest:
  component: "@serverless/tencent-ssl"
  inputs:
    domain: any******s.cn
    dvAuthMethod: DNS
    email: serv*******exe.cn
    phone: 135******691
    validityPeriod: 12
    alias: Test certificate
```
>!
>- You can only apply for one-year free DV certificates for domain names.
>- You can only create and remove certificates but cannot renew or reissue them.
>- For domain names resolved at Tencent Cloud, this component supports automatic DNS verification for certificates; for other domain names, after you apply for a certificate, it needs to be verified before it can be used. For more information, please see [Domain Name Verification Guide](https://intl.cloud.tencent.com/document/product/1007/30168).


### Deployment


Deploy by running the `sls` command, and you can add the `--debug` parameter to view the information during the deployment process:

```console
$ sls --debug

  DEBUG ─ Resolving the template's static variables.
  DEBUG ─ Collecting components from the template.
  DEBUG ─ Downloading any NPM components found in the template.
  DEBUG ─ Analyzing the template's components dependencies.
  DEBUG ─ Creating the template's components graph.
  DEBUG ─ Syncing template state.
  DEBUG ─ Executing the template's components graph.
  DEBUG ─ Applying Certificate ...
  DEBUG ─ Applyed Certificate ...

  SSLTest: 
    CertificateId:                    blnwqO0v
    Please add the resolution record: 
      Domain:      an********cn
      Host record: _dnsauth
      Record type: TXT
      Value:       20200316*********k6y8kmutd

  1s › SSLTest › done
```

### Removal

```console
$ sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Removing ...
  DEBUG ─ Removing CertificateId blfZE0B8

  3s › SSLTest › done
```

### Account configuration (optional)
Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:

```console
$ touch .env # Tencent Cloud configuration information
```

Configure Tencent Cloud's `SecretId` and `SecretKey` information in the `.env` file and save it:
```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
>?
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

### More components

You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).
