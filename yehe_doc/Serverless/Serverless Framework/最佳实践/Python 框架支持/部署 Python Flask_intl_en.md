
## Operation Scenarios
Tencent Cloud [Flask](https://github.com/pallets/flask) Serverless Component supports deploying RESTful API services but does not support Flask Command.
>!Any Python server framework that supports Web Server Gateway Interface (WSGI) can be deployed through this component, such as Falcon.

## Prerequisites
 Before using this component, you need to initialize a Flask project first and then add `Flask` and `werkzeug` to the dependent file `requirements.txt` as follows: 
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
### Installation
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:

```shell
npm install -g serverless
```

### Configuration
Create a `serverless.yml` file in the project root directory:
```shell
touch serverless.yml
```

Configure `serverless.yml` as follows:

```yml
# serverless.yml

component: flask
name: flashDemo
org: orgDemo
app: appDemo
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

[Detailed Configuration >>](https://github.com/serverless-components/tencent-flask/blob/master/docs/configure.md)

### Deployment

Run the following command to deploy by scanning code:

```console
sls deploy
```

>?To grant persistent permission, please see [Account Configuration](#account).

### Removal

You can run the following command to remove the deployed service:

```console
sls remove
```

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

