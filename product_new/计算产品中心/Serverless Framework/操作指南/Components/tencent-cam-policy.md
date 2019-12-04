# Tencent-cam-policy

Easily provision Tencent CAM policy using [Serverless Components](https://github.com/serverless/components).
&nbsp;
&nbsp;
1. [Install](#1-install)
2. [Create](#2-create)
3. [Configure](#3-configure)
4. [Deploy](#4-deploy)
5. [Remove](#5-remove)

&nbsp;


### 1. Install

```shell
$ npm install -g serverless
```

### 2. Create

Just create a `serverless.yml` file

```shell
$ touch serverless.yml
$ touch .env      # your Tencent api keys
```

If you don't have a Tencent Cloud account, you could [sign up](https://intl.cloud.tencent.com/register) first.  

If you already login in, find  `TENCENT_SECRET_ID` and `TENCENT_SECRET_KEY`  in [Tencent Console](https://console.cloud.tencent.com/cam/capi).

```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
TENCENT_APP_ID=123
```

### 3. Configure

```yml
# serverless.yml

myPolicy:
  component: "@serverless/tencent-cam-policy"
  inputs:
    name: my-policy
    description: A policy created by Serverless Components
    policy:
      statement:
        - effect: allow
          action:
            - cos:GetService
          resource: '*'

```
* [Click here to view the configuration document](https://github.com/serverless-tencent/tencent-cam-policy/blob/master/docs/configure.md)



### 4. Deploy

```console
$ sls --debug

  DEBUG ─ Resolving the template's static variables.
  DEBUG ─ Collecting components from the template.
  DEBUG ─ Downloading any NPM components found in the template.
  DEBUG ─ Analyzing the template's components dependencies.
  DEBUG ─ Creating the template's components graph.
  DEBUG ─ Syncing template state.
  DEBUG ─ Executing the template's components graph.

  myPolicy: 
    id: 27710257

  7s › myPolicy › done
 
```

&nbsp;

### 5. Remove
```console
$ sls remove --debug

  DEBUG ─ Flushing template state and removing all components.

  1s › myPolicy › done


```

### New to Components?

Checkout the [Serverless Components](https://github.com/serverless/components) repo for more information.
