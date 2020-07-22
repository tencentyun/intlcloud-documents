## Operation Scenarios
Serverless Framework enables you to build your own Serverless components or project templates and publish them in the Serverless Registry for use by your team and others. This document describes how to develop your own templates through Registry and reuse them.

## Prerequisites
You have [installed Serverless Framework](https://intl.cloud.tencent.com/document/product/1040/37034) on at least the following versions:

```shell
$ serverless –v
Framework Core: 1.74.1 (standalone)
Plugin: 3.6.14
SDK: 2.3.1
Components: 2.31.6
```

## Directions
### Initializing template project with Registry

#### 1. View available components or templates
You can view available components or templates in the following two ways:

1. Access the [Serverless Registry](https://registry.serverless.com) page.
2. Run the `sls registry` command to list all recommended components or project templates:

```
$ sls registry

serverless ⚡ registry

Featured Components:

  apigateway - https://github.com/serverless-components/tencent-apigateway
  cdn - https://github.com/serverless-components/tencent-cdn
  cos - https://github.com/serverless-components/tencent-cos
  django - https://github.com/serverless-components/tencent-django/
  ...

Featured Templates:

  fullstack - Deploy a full stack application.
  fullstack-nosql - Deploy a nosql full stack application.
  ocr-app - Deploy a serverless OCR application.

Serverless › Find more here: https://registry.serverless.com
```

#### 2. Initialize a project from the template
Once you have determined the project template to be used, you can use the built-in `init` command to initialize your project. The `init` command will automatically download the template you select from the Registry and create a project folder for you in the following steps:

```
$ sls init fullstack # Create a project by using the `fullstack` project template
$ cd  fullstack # Enter the project folder
```

#### 3. Quickly deploy your project
After the initialization is completed, you can develop your project in the local project folder and quickly deploy it in the cloud by running the `sls` command:

```
$ sls deploy --all # Deploy the entire `fullstack` project
```

### Developing your own template through Registry
It is very easy to publish the project you deploy based on Serverless Component as a template. You do not need to make any changes to the project; instead, you simply need to add a `serverless.yml` file (or modify the existing `serverless.yml` file) and add some template metadata that you want to tell the Registry as described below:

```text
# serverless.yml
name: fullstack # Project template name
displayName: fullstack application # Name of the project template displayed in the console
author: Tencent Cloud, Inc. # Author name
org: Tencent Cloud, Inc. # Organization name, which is optional
type: template # Project type, which can be either `template` or `component`. It is `template` here
description: Deploy a full stack application. # Describe your project template
description-i18n:
  zh-cn: Quickly deploy a full-stack application # Description
keywords: tencent, serverless, express, website, fullstack # Keywords
repo: https://github.com/serverless-components/tencent-fullstack # Source code
readme: https://github.com/serverless-components/tencent-fullstack/tree/master/README.md # Detailed description file
license: MIT # Copyright notice
src: # Describe the files in the project to be published as a template
  src: ./ # Specify a relative directory, the files under which will be published as a template
  exclude: # Describe the files in the specified directory to be excluded
    # The following files are typically excluded
    # 1. Files containing `secrets`
    # 2. Files managed by `.git` git source code
    # 3. Third-party dependencies such as `node_modules`
    - .env
    - '**/node_modules'
    - '**/package-lock.json'
```

After the `serverless.yml` file is configured, you can use the `sls registry publish` command to publish the project to the Registry as a template, so that others can reuse it by entering its name.
