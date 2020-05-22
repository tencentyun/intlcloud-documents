## Operation Scenarios

The SCF component is one of the basic components in the `serverless-tencent` component library. Through this component, you can create, configure, and manage SCF functions with speed and ease.

## Directions

Through the SCF component, you can perform a complete set of operations on a function, such as creation, configuration, deployment, and deletion. The supported commands are as follows:

#### Installation

Install Serverless through npm:
```console
$ npm install -g serverless
```

#### Creation
```
$ mkdir my-function
$ cd my-function
```
The contents of the directory are as follows:

```
|- code
  |- index.js
|- serverless.yml
```
 
For this example, you can use the following demo as `index.js`:
```javascript
'use strict';
exports.main_handler = async (event, context, callback) => {
    console.log("%j", event);
    return "hello world"
};

```

#### Configuration

Create the `serverless.yml` file locally:

```console
$ touch serverless.yml
```
Configure `serverless.yml` as follows:
```yml
# serverless.yml
myFunction1:
  component: "@serverless/tencent-scf"
  inputs:
    name: myFunction1
    codeUri: ./code       # Code directory
    handler: index.main_handler
    runtime: Nodejs8.9
    region: ap-guangzhou
    description: My Serverless Function
    memorySize: 128
    timeout: 20
    # Configure the files or directories that you want to ignore when creating the zip package (optional)
    exclude:
      - .gitignore
      - .git/**
      - node_modules/**
      - .serverless
      - .env
    include:
          - /Users/dfounderliu/Desktop/temp/.serverless/myFunction1.zip
    environment:
      variables:
        TEST: vale
    vpcConfig:
      subnetId: ''
      vpcId: ''

myFunction2:
  component: "@serverless/tencent-scf"
  inputs:
    name: myFunction2
    codeUri: ./code

```
> You can view the list of all available attributes in `serverless.yml` in [Detailed Configuration](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md).


#### Deployment

If you haven't [logged in to](https://intl.cloud.tencent.com/login) or [signed up for](https://intl.cloud.tencent.com/register) a Tencent Cloud account, do so first.

Deploy by running the `sls` command, and you can add the `--debug` parameter to view the information during the deployment process:

```console
$ sls --debug

  DEBUG ─ Resolving the template's static variables.
  DEBUG ─ Collecting components from the template.
  DEBUG ─ Downloading any NPM components found in the template.
  DEBUG ─ Analyzing the template's components dependencies.
  DEBUG ─ Creating the template's components graph.
  DEBUG ─ Syncing template state.
  DEBUG ─ Starting Website Removal.
  DEBUG ─ Removing Website bucket.
  DEBUG ─ Removing files from the "my-bucket-1300415943" bucket.
  DEBUG ─ Removing "my-bucket-1300415943" bucket from the "ap-guangzhou" region.
  DEBUG ─ "my-bucket-1300415943" bucket was successfully removed from the "ap-guangzhou" region.
  DEBUG ─ Finished Website Removal.
  DEBUG ─ Executing the template's components graph.
  DEBUG ─ Compressing function myFunction file to /Users/dfounderliu/Desktop/temp/code/.serverless/myFunction.zip.
  DEBUG ─ Compressed function myFunction file successful
  DEBUG ─ Uploading service package to cos[sls-cloudfunction-ap-guangzhou-code]. sls-cloudfunction-default-myFunction-1572519895.zip
  DEBUG ─ Uploaded package successful /Users/dfounderliu/Desktop/temp/code/.serverless/myFunction.zip
  DEBUG ─ Creating function myFunction
  DEBUG ─ Created function myFunction successful

  myFunction: 
    Name:        myFunction
    Runtime:     Nodejs8.9
    Handler:     index.main_handler
    MemorySize:  128
    Timeout:     3
    Region:      ap-guangzhou
    Role:        QCS_SCFExcuteRole
    Description: This is a template function
    UsingCos:    true

  6s › myFunction › done

```

#### Removal

```console
$ sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Removed function myFunction successful

  1s › myFunction › done

```

#### Account configuration (optional)

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:

```console
$ touch .env # Tencent Cloud configuration information
```

Configure Tencent Cloud `SecretId` and `SecretKey` information in the `.env` file and save it:
```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
>
> - If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management
](https://console.cloud.tencent.com/cam/capi).
