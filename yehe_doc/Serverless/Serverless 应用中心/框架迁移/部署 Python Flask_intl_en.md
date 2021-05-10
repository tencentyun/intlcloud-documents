
## Overview
Tencent Cloud [Flask](https://github.com/pallets/flask) Serverless Component supports deploying RESTful API services but does not support Flask Command.
>!Any Python server framework that supports Web Server Gateway Interface (WSGI) can be deployed through this component, such as Falcon.

## Prerequisites
1. Before using this component, please make sure that you have installed the Python environment locally.
2. Initialize a Flask project first and then add `Flask` and `werkzeug` to the dependent file `requirements.txt` as follows: 
```txt
Flask==1.0.2
werkzeug==0.16.0
```
Meanwhile, add the API service `app.py`. The following code is for reference only:
```python
from flask import Flask, jsonify
app = Flask(__name__)

@app.route("/")
def index():
    return "Hello Flask"

@app.route("/users")
def users():
    users = [{'name': 'test1'}, {'name': 'test2'}]
    return jsonify(data=users)

@app.route("/users/<id>")
def user(id):
    return jsonify(data={'name': 'test1'})
```

## Directions

>?The following steps are mainly for deployment on the command line. For deployment in the console, please see [Console Deployment Guide](https://intl.cloud.tencent.com/document/product/1040/39132).

### 1. Install Serverless CLI
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:

```shell
npm install -g serverless
```

### 2. Initialize the Flask template project (optional)
If you don't have a local Flask project, you can initialize a Flask project with the following commands (if you already have one, you can ignore this step):
```
serverless init flask-starter --name example
cd example
```

### 3. Configure the .yml file
Create a `serverless.yml` file in the project root directory and paste the following configuration template into it to implement basic project configuration.
>?You can add more configuration items in `serverless.yml` based on your actual deployment needs. For more information on the configuration of the .yml file, please see [Flask Component Configuration](https://github.com/serverless-components/tencent-flask/blob/master/docs/configure.md).

```sh
touch serverless.yml
```

```yml
#serverless.yml
component: flask
name: flashDemo
stage: dev

inputs:
  src:
    hook: 'pip install -r requirements.txt -t ./'
    dist: ./
    exclude:
      - .env
  region: ap-guangzhou
  runtime: Python3.6
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```

### 4. Deploy the application
Deploy by running the `sls deploy` command, and you can add the `--debug` parameter to view the information during the deployment process:

```
sls deploy --debug
```
After the deployment is completed, access the application by accessing the output API Gateway link.

### 5. Monitor the OPS
After the deployment is completed, you can log in to the [Serverless Framework console](https://console.cloud.tencent.com/ssr) to view the basic information of the application and monitor logs.


<span id="account"></span>
### Account configuration (optional)

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:

```shell
touch .env # Tencent Cloud configuration information
```

Configure Tencent Cloud's `SecretId` and `SecretKey` information in the `.env` file and save it:

```text
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```

>?
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).

