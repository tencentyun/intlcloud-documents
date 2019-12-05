# Tencent-cam-role

Easily provision Tencent CAM roles using [Serverless Components](https://github.com/serverless/components).

&nbsp;



&nbsp;

1. [Install](#1-install)
2. [Create](#2-create)
3. [Configure](#3-configure)
4. [Deploy](#4-deploy)
4. [Remove](#5-remove)

&nbsp;


### 1. Install

```shell
$ npm install -g serverless
```

### 2. Create

Just create a `serverless.yml` file

```shell
$ touch serverless.yml
$ touch .env      # configure your Tencent api keys
```
Add the access keys of a [Tencent CAM Role](https://console.cloud.tencent.com/cam/capi) with `AdministratorAccess` in the `.env` file, using this format: 

```
# .env
TENCENT_SECRET_ID=XXX
TENCENT_SECRET_KEY=XXX
TENCENT_APP_ID=123
```
* If you don't have a Tencent Cloud account, you could [sign up](https://intl.cloud.tencent.com/register) first. 

### 3. Configure

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
 
 * [Click here to view the configuration document](https://github.com/serverless-tencent/tencent-cam-role/blob/master/docs/configure.md)


### 4. Deploy

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

&nbsp;

### 5. Remove
```shell
$ sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Removing role c0hhdv-qt9mh6xj from region ap-guangzhou.
  DEBUG ─ Role c0hhdv-qt9mh6xj successfully removed from region ap-guangzhou.

  1s › myRole › done

```

### New to Components?

Checkout the [Serverless Components](https://github.com/serverless/components) repo for more information.
