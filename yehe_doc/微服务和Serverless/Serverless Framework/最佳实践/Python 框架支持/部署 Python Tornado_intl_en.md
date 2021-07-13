## Operation Scenarios

Tencent Cloud Tornado Serverless Component supports deploying RESTful API services. Currently, only Tornado v3.* and below is supported. Sync rather than async operations are supported.

## Prerequisites
**1. Install Tornado and create a Python file**, such as `app.py`:
```pyyhon
from tornado.web import RequestHandler

class IndexHandler(RequestHandler):
    def get(self):
        self.write('hello word tornado')


url = [
        (r'/', IndexHandler),
    ]
```
**2. Install the dependencies required by Python in the project directory**; for example, this example requires `Tornado`, which can be installed through `pip`:
```
pip install Tornado -t ./
```
If the connection is exceptional, you can consider using a source in Mainland China, such as:
```
pip install Tornado -t ./ -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## Directions
#### Installation
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:

```shell
$ npm install -g serverless
```

#### Configuration
Create the `serverless.yml` file locally:
```shell
$ touch serverless.yml
```
Configure `serverless.yml` as follows:
```yml
TornadoTest:
  component: '@serverless/tencent-tornado'
  inputs:
    region: ap-guangzhou
    functionName: tornadoFunctionTest
    tornadoProjectName: myTornado
    code: ./
    functionConf:
      timeout: 10
      memorySize: 256
      environment:
        variables:
          TEST: vale
      vpcConfig:
        subnetId: ''
        vpcId: ''
    apigatewayConf:
      protocols:
        - http
      environment: release

```
>!
>- The `tornadoProjectName` here must be the same as the project name.
>- `tornadoProjectName` is actually the route list of your application files. Please make sure that the file can be referenced externally through `filename.url`.

[Detailed Configuration >>](https://github.com/serverless-tencent/tencent-tornado/blob/master/docs/configure.md)

#### Deployment



Deploy by running the `sls` command, and you can add the `--debug` parameter to view the information during the deployment process:
```shell
$ sls --debug
```

#### Removal

You can run the following commands to remove the deployed service:
```shell
$ sls remove --debug
```

#### Account configuration (optional)

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:
```shell
$ touch .env # Tencent Cloud configuration information
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
