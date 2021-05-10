## Operation Scenarios
The RESTful API template uses the Tencent SCF component and its trigger capabilities for easy creation, configuration, and management of a RESTful API application in Tencent Cloud. You can use the Serverless SCF component to quickly construct a RESTful API application and perform `GET` and `PUT` operations.

## Directions

### 1. Install

Install Serverless Framework:
```console
$ npm install -g serverless
```

### 2. Configure

Directly download the sample by running the following command:

```console
serverless create --template-url https://github.com/serverless/components/tree/v1/templates/tencent-python-rest-api
```
The directory structure is as follows:
```
.
├── code
|   └── index.py
└── serverless.yml
```

Currently, the SCF component supports v2; therefore, the `serverless.yml` file has been modified to the following:

```yml
# serverless.yml 

component: scf 
name: apidemo 
org: test 
app: scfApp 
stage: dev 

inputs:
  name: myRestAPI
  enableRoleAuth: true
  src: ./code
  handler: index.main_handler
  runtime: Python3.6
  region: ap-guangzhou
  description: My Serverless Function
  memorySize: 128
  timeout: 20
  events:
      - apigw:
          name: serverless
          parameters:
            protocols:
              - http
            serviceName: serverless
            description: the serverless service
            environment: release
            endpoints:
              - path: /users/{user_type}/{action}
                method: GET
                description: Serverless REST API
                enableCORS: TRUE
                serviceTimeout: 10
                param:
                  - name: user_type
                    position: PATH
                    required: 'TRUE'
                    type: string
                    defaultValue: teacher
                    desc: mytest
                  - name: action
                    position: PATH
                    required: 'TRUE'
                    type: string
                    defaultValue: go
                    desc: mytest
```

View the `code/index.py` code, and you can see the API's parameter input and return logic:

```python
# -*- coding: utf8 -*-

def teacher_go():
    # todo: teacher_go action
    return {
        "result": "it is student_get action"
    }

def student_go():
    # todo: student_go action
    return {
        "result": "it is teacher_put action"
    }

def student_come():
    # todo: student_come action
    return {
        "result": "it is teacher_put action"
    }

def main_handler(event, context):
    print(str(event))
    if event["pathParameters"]["user_type"] == "teacher":
        if event["pathParameters"]["action"] == "go":
            return teacher_go()
    if event["pathParameters"]["user_type"] == "student":
        if event["pathParameters"]["action"] == "go":
            return student_go()
        if event["pathParameters"]["action"] == "come":
            return student_come()
```

### 3. Deploy

Deploy by running the `sls deploy` command, and you can add the `--debug` parameter to view the information during the deployment process:

If you have not [logged in to](https://intl.cloud.tencent.com/login) or [signed up for](https://intl.cloud.tencent.com/register) a Tencent Cloud account, you can directly log in or sign up:

```text
$ sls deploy

serverless ⚡ framework
Action: "deploy" - Stage: "dev" - App: "scfApp" - Instance: "myRestAPI"

FunctionName: myRestAPI
Description:  My Serverless Function
Namespace:    default
Runtime:      Python3.6
Handler:      index.main_handler
MemorySize:   128
Triggers: 
  apigw: 
    - http://service-jyl9i6mc-1258834142.gz.apigw.tencentcs.com/release/users/{user_type}/{action}

31s › myRestAPI › Success
```

### 4. Test

You can run the following commands to test the returned result of the RESTful API:

>If you have not installed `curl` on Windows, you can directly open the corresponding link in a browser to view the returned result.

```console
$ curl -XGET http://service-9t28e0tg-1250000000.gz.apigw.tencentcs.com/release/users/teacher/go

{"result": "it is student_get action"}
```

```console
$ curl -PUT http://service-9t28e0tg-1250000000.gz.apigw.tencentcs.com/release/users/student/go

{"result": "it is teacher_put action"}
```

### 5. Remove

You can run the following command to remove the RESTful API application:

```console
$ sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Removing any previously deployed API. api-37gk3l8q
  DEBUG ─ Removing any previously deployed service. service-9t28e0tg
  DEBUG ─ Removing function
  DEBUG ─ Request id
  DEBUG ─ Removed function myRestAPI successful

  7s » myRestAPI » done
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
>
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
