## Operation Scenarios
After quickly constructing a Serverless website service through Serverless Component, if you want to configure a custom domain name and support HTTPS access, you can do so in the following two ways: 

## Prerequisites
- A website service has been deployed, and the website hosting address at COS/API Gateway has been obtained. For the specific deployment method, please see [Deploying Hexo Blog](https://intl.cloud.tencent.com/document/product/1040/36749).
- You already have a custom domain name (such as www.example.com).
- If you need HTTPS access, you can apply for a certificate and [get the certificate ID](https://console.cloud.tencent.com/ssl) (such as `certificateId` of `axE1bo3)`.



## Method 1: Configuring Support for HTTPS Access to Custom Domain Name Through CDN
Before configuration, you need to make sure that you have completed identity verification for your account and [activated the CDN service](https://console.cloud.tencent.com/cdn).

### Adding configuration

In `serverless.yml`, add CDN custom domain name configuration:
```yml         
# serverless.yml

component: tencent-website
name: myWebsite
org: test
app: websiteApp
stage: dev

inputs:
  src:
    src: ./public
    index: index.html
    error: index.html
  region: ap-guangzhou
  bucketName: my-hexo-bucket
  protocol: https
  # New CDN custom domain name configuration
  hosts:
    - host: www.example.com # Custom domain name to be configured
      https:
        switch: on
        http2: off
        certInfo:
          certId: 'abc'
          # certificate: 'xxx'
          # privateKey: 'xxx'

```
[View full configuration item description >>](https://github.com/serverless-components/tencent-website/blob/master/docs/configure.md)

### Deploying service
Deploy by running the `sls deploy` command again, and you can add the `--debug` parameter to view the information during the deployment process:

>?`sls` is short for the `serverless` command.

```bash
$ sls deploy 
  
  myWebsite: 
    url:  https://my-hexo-bucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
    env: 
    host: 
      - https://www.example.com (CNAME: www.example.com.cdn.dnsv1.com)
  17s › myWebsite › done
```
### Adding CNAME
After the deployment is completed, you can see a CNAME domain name suffixed with `.cdn.dnsv1.com` in the output on the command line. Set the corresponding CNAME at your DNS service provider as instructed in [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121). After it takes effect, you can access the custom HTTPS domain name.

## Method 2: Configuring Custom Domain Name Through API Gateway
### Adding configuration
In `serverless.yml`, add API Gateway custom domain name configuration. This document uses the egg.js framework as an example, and the configuration is as follows:
```yml
# serverless.yml

component: apigateway # Component name, which is required. `apigateway` is used in this example
name: restApi # Instance name, which is required
org: orgDemo # Organization information, which is optional. The default value is the `appid` of your Tencent Cloud account
app: appDemo # Application name, which is optional
stage: dev # Information for identifying environment, which is optional. The default value is `dev`

inputs:
  region: ap-shanghai
  protocols:
    - http
    - https
  serviceName: serverless
  environment: release
  customDomain:
    - domain: www.example.com
      # If you want to add `https`, you need to get authenticated with Tencent Cloud SSL Certificates Service to get the `cettificateId` first
      certificateId: abcdefg
      protocols:
        - http
        - https
  endpoints:
    - path: /users
      method: POST
      function:
        functionName: myFunction
        
```
[View full configuration item description >>](https://github.com/serverless-components/tencent-apigateway/blob/master/docs/configure.md)
### Deploying service
Deploy by running the `sls deploy` command again, and you can add the `--debug` parameter to view the information during the deployment process:

>? `sls` is short for the `serverless` command.

```bash
$ sls deploy 
  restApi: 
    protocols: 
      - http
      - https
    subDomain:     service-lqhc88sr-1250000000.sh.apigw.tencentcs.com
    environment:   release
    region:        ap-shanghai
    serviceId:     service-lqhc88sr
    apis: 
      - 
        path:   /users
        method: POST
        apiId:  api-e902tx1q
    customDomains: 
      - www.example.com (CNAME: service-lqhc88sr-1250000000.sh.apigw.tencentcs.com) 
  8s › restApi › done
```
### Adding CNAME record
After the deployment is completed, you can see a CNAME domain name suffixed with `.apigw.tencentcs.com` in the output on the command line. Once the corresponding CNAME is set and takes effects at your DNS service provider, you can access the custom HTTPS domain name.
