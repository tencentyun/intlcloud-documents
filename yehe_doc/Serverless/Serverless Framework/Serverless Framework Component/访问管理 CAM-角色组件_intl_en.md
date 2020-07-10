## Operation Scenarios
The CAM-role component is one of the basic components in the `serverless-tencent` component library. Through this component, you can create, configure, and manage CAM roles with speed and ease.

## Directions

Through the CAM-role component, you can perform a complete set of operations on a CAM role, such as creation, configuration, deployment, and deletion. The supported commands are as follows:


#### Installation

Install Serverless through npm:

```console
$ npm install -g serverless
```

#### Creation

Create `serverless.yml` and `.env` files locally:

```console
$ touch serverless.yml
$ touch .env # Tencent Cloud configuration information
```

Configure Tencent Cloud's `APPID`, `SecretId`, and `SecretKey` information in the `.env` file and save it:
```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
TENCENT_APP_ID=123
```
>?
> - If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
> - If you already have a Tencent Cloud account,
you can get `APPID`, `SecretId`, and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

#### Configure

Configure `serverless.yml` as follows:

```yml
# serverless.yml

myRole:
  component: "@serverless/tencent-cam-role"
  inputs:
    roleName: QCS_SCFExcuteRole
    service:
      - scf.qcloud.com
      - cos.qcloud.com
    policy:      
      policyName:
        - QCloudResourceFullAccess
        - QcloudAccessForCDNRole
```

 
[Detailed Configuration >>](https://github.com/serverless-tencent/tencent-cam-role/blob/master/docs/configure.md)

 
#### Deployment

Deploy by running the following command and view the information during the deployment process:

```shell
$ sls --debug

  DEBUG ─ Resolving the template's static variables.
  DEBUG ─ Collecting components from the template.
  DEBUG ─ Downloading any NPM components found in the template.
  DEBUG ─ Analyzing the template's components dependencies.
  DEBUG ─ Creating the template's components graph.
  DEBUG ─ Syncing template state.
  DEBUG ─ Executing the template's components graph.
  DEBUG ─ Syncing role c0hhdv-qt9mh6xj in region ap-guangzhou.
  DEBUG ─ Updating policy for role c0hhdv-qt9mh6xj.
  DEBUG ─ Saved state for role c0hhdv-qt9mh6xj.
  DEBUG ─ Role c0hhdv-qt9mh6xj was successfully deployed to region ap-guangzhou.
  DEBUG ─ Deployed role roleId is 4611686018427945536.

  myRole: 
    roleName:    QCS_SCFExcuteRole
    description: This is tencent-cam-role component.
    roleId:      4611686018427945536
    service: 
      - cos.qcloud.com
      - scf.qcloud.com
    policy: 
      policyId: 
        - 16313162
        - 2
      policyName: 
        - QCloudResourceFullAccess
        - QcloudAccessForCDNRole

  17s › myRole › done

```



#### Removal
```shell
$ sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Removing role c0hhdv-qt9mh6xj from region ap-guangzhou.
  DEBUG ─ Role c0hhdv-qt9mh6xj successfully removed from region ap-guangzhou.

  1s › myRole › done

```
