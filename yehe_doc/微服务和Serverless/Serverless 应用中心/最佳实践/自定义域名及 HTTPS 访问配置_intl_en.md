## Operation Scenarios
After quickly constructing a Serverless website service through Serverless Component, if you want to configure a custom domain name and support HTTPS access, you can do so in the following two ways: 

## Prerequisites
- A website service has been deployed, and the website hosting address at COS/API Gateway has been obtained. For the specific deployment method, please see [Deploying Hexo Blog](https://intl.cloud.tencent.com/document/product/1040/36749).
- You already have a custom domain name (such as www.example.com). If the domain name is used for Mainland China services, ICP filing is required.
- If you need HTTPS access, you can apply for a certificate and [get the certificate ID](https://console.cloud.tencent.com/ssl) (such as `certificateId` of `axE1bo3)`.



## Method 1: Configuring Support for HTTPS Access to Custom Domain Name Through CDN
Before configuration, you need to make sure that you have completed identity verification for your account and [activated the CDN service](https://console.cloud.tencent.com/cdn).

### Adding configuration

In `serverless.yml`, add CDN custom domain name configuration:
```yml         
# serverless.yml

component: website
name: myWebsite
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
Deploy by running the `sls` command, and you can add the `--debug` parameter to view the information during the deployment process:


>? `sls` is short for the `serverless` command.

```bash
$ sls --debug
  DEBUG ─ Resolving the template's static variables.
  DEBUG ─ Collecting components from the template.
  DEBUG ─ Downloading any NPM components found in the template.
  DEBUG ─ Analyzing the template's components dependencies.
  DEBUG ─ Creating the template's components graph.
  DEBUG ─ Syncing template state.
  DEBUG ─ Executing the template's components graph.
  DEBUG ─ Preparing website Tencent COS bucket my-hexo-bucket-1250000000.
  DEBUG ─ Bucket "my-hexo-bucket-1250000000" in the "ap-guangzhou" region already exist.
  DEBUG ─ Setting ACL for "my-hexo-bucket-1250000000" bucket in the "ap-guangzhou" region.
  DEBUG ─ Ensuring no CORS are set for "my-hexo-bucket-1250000000" bucket in the "ap-guangzhou" region.
  DEBUG ─ Ensuring no Tags are set for "my-hexo-bucket-1250000000" bucket in the "ap-guangzhou" region.
  DEBUG ─ Configuring bucket my-hexo-bucket-1250000000 for website hosting.
  DEBUG ─ Uploading website files from /Users/tina/Documents/hexoblog/hexo/public to bucket my-hexo-bucket-1250000000.
  DEBUG ─ Starting upload to bucket my-hexo-bucket-1250000000 in region ap-guangzhou
  DEBUG ─ Uploading directory /Users/tina/Documents/hexoblog/hexo/public to bucket my-hexo-bucket-1250000000
  DEBUG ─ The CDN domain www.example.com has existed.
  DEBUG ─ Updating...
  DEBUG ─ Waiting for CDN deploy success..
  DEBUG ─ CDN deploy success to host: www.example.com
  DEBUG ─ Setup https for www.example.com...
  DEBUG ─ Website deployed successfully to URL: https://my-hexo-bucket-1250000000.cos-website.ap-guangzhou.myqcloud.com.
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
restApi:
  component: "@serverless/tencent-apigateway"
  inputs:
    region: ap-shanghai
    protocols:
      - http
      - https
    serviceName: serverless
    environment: release
    endpoints:
      - path: /users
        method: POST
        function:
          functionName: myFunction # The function name to which the gateway connects
    # Add API Gateway custom domain name configuration
    customDomain:
      - domain: www.example.com
        certificateId: axE1bo3
        protocols:
          - https
```
[View full configuration item description >>](https://github.com/serverless-components/tencent-apigateway/blob/master/docs/configure.md)
### Deploying service
Deploy by running the `sls` command, and you can add the `--debug` parameter to view the information during the deployment process:

>? `sls` is short for the `serverless` command.

```bash
$ sls --debug
  DEBUG ─ Resolving the template's static variables.
  DEBUG ─ Collecting components from the template.
  DEBUG ─ Downloading any NPM components found in the template.
  DEBUG ─ Analyzing the template's components dependencies.
  DEBUG ─ Creating the template's components graph.
  DEBUG ─ Syncing template state.
  DEBUG ─ Executing the template's components graph.
  DEBUG ─ Starting API-Gateway deployment with name restApi in the ap-shanghai region
  DEBUG ─ Using last time deploy service id service-lqhc88sr
  DEBUG ─ Updating service with serviceId service-lqhc88sr.
  DEBUG ─ Endpoint POST /users already exists with id api-e902tx1q.
  DEBUG ─ Updating api with api id api-e902tx1q.
  DEBUG ─ Service with id api-e902tx1q updated.
  DEBUG ─ Deploying service with id service-lqhc88sr.
  DEBUG ─ Deployment successful for the api named restApi in the ap-shanghai region.
  DEBUG ─ Start unbind all exist domain for service service-lqhc88sr
  DEBUG ─ Start bind custom domain for service service-lqhc88sr
  DEBUG ─ Custom domain for service service-lqhc88sr created successfullly.
  DEBUG ─ Please add CNAME record service-lqhc88sr-1250000000.sh.apigw.tencentcs.com for www.example.com.
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
