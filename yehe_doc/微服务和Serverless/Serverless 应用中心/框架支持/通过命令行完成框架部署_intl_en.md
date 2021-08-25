In addition to the console, you can also quickly deploy a web framework on the command line. This document describes how to use the [HTTP component](https://github.com/serverless-components/tencent-http/blob/master/docs/configure.md) of Serverless Framework to complete the local deployment of web applications.

### Prerequisites
You have activated the service and completed the [permission configuration](https://intl.cloud.tencent.com/document/product/1040/36793) for Serverless Framework.

### Supported frameworks[](id:framework)



| Supported Framework | Document |
|---------|--------- |
| Express |[Quickly Deploying Express Framework](https://intl.cloud.tencent.com/document/product/1040/37354)|
| Koa |[Quickly Deploying Koa Framework](https://intl.cloud.tencent.com/document/product/1040/36792)|
| Egg |[Quickly Deploying Egg Framework](https://intl.cloud.tencent.com/document/product/1040/36795)|
| Next.js |[Quickly Deploying Next.js Framework](https://intl.cloud.tencent.com/document/product/1040/36705)|
| Nuxt.js |[Quickly Deploying Nuxt.js Framework](https://intl.cloud.tencent.com/document/product/1040/37355)|
| Nest.js |[Quickly Deploying Nest.js Framework](https://intl.cloud.tencent.com/document/product/1040/41601)|
| Flask |[Quickly Deploying Flask Framework](https://intl.cloud.tencent.com/document/product/1040/37042)|
| Django |[Quickly Deploying Django Framework](https://intl.cloud.tencent.com/document/product/1040/36798)|
| Laravel |[Quickly Deploying Laravel Framework](https://intl.cloud.tencent.com/document/product/1040/36863)|

### Directions

1. Develop an application locally
Complete the development locally according to your actual business scenario. For more information, please see the documents in the [Supported frameworks](#framework) section.

2. Configure the .yml file
   Create a `serverless.yml` file in the project root directory and write the configuration by referring to the following sample. For the full configuration, please see [Configuration Document](https://github.com/serverless-components/tencent-http/blob/master/docs/configure.md). 
<dx-codeblock>
::: yml
# serverless.yml
component: http # Component name, which is required
name: webDemo # Component instance name, which is required

inputs:
  region: ap-guangzhou # Function region
  src: # Deploy the file code under `src`, package it into a zip file, and upload it to the bucket
    src: ./ # The file directory that needs to be packaged locally
    exclude: # Excluded files or directories
      - .env
      - 'node_modules/**'
  faas: # Function configuration
    framework: express # Select the framework. Express is used here as an example
    runtime: Nodejs12.16
    name: webDemo # Function name
    timeout: 10 # Timeout period in seconds
    memorySize: 512 # Memory size, which is 512 MB by default
    layers:
      - name: layerName #  Layer name
        version: 1 # Version

  apigw: #  # The HTTP component will create an API Gateway service by default
    isDisabled: false # Specify whether to disable automatic API Gateway creation
    id: service-xxx # API Gateway service ID. If you leave it empty, a gateway will be automatically created
    name: serverless # API Gateway service ID
    api: # Relevant configuration of the created API
      cors: true # Specify whether to allow CORS
      timeout: 15 # API timeout period
      name: apiName # API name
      qualifier: $DEFAULT # Version associated with the API
    protocols:
      - http
      - https
    environment: test
:::
</dx-codeblock>

3. After the creation is completed, run `sls deploy` in the root directory to deploy. The component will automatically generate the `scf_bootstrap` bootstrap file for deployment according to the selected framework.
>! As the bootstrap file logic is strongly related to your business logic, the generated default bootstrap file may cause the framework start to fail. We recommend you manually configure the bootstrap file according to your actual business needs. For more information, please see the deployment guide document of each framework.
>

#### Sample `scf_bootstrap`:
- express:
```sh
#!/usr/bin/env bash

/var/lang/node12/bin/node app.js
```

- koa
```sh
#!/usr/bin/env bash

/var/lang/node12/bin/node app.js
```

- egg
<dx-codeblock>
::: js
#!/var/lang/node12/bin/node

/**
 * Node path in docker: /var/lang/node12/bin/node
 * As only `/tmp` is readable/writable in SCF, two environment variables need to be modified at startup
 * `NODE_LOG_DIR` changes the default node write path of `egg-scripts` (~/logs) to `/tmp`
 * `EGG_APP_CONFIG` changes the default directory of the Egg application to `/tmp`
 */

process.env.EGG_SERVER_ENV = 'prod';
process.env.NODE_ENV = 'production';
process.env.NODE_LOG_DIR = '/tmp';
process.env.EGG_APP_CONFIG = '{"rundir":"/tmp","logger":{"dir":"/tmp"}}';

const { Application } = require('egg');

// If you deploy `node_modules` through layers, you need to modify `eggPath`
Object.defineProperty(Application.prototype, Symbol.for('egg#eggPath'), {
  value: '/opt',
});

const app = new Application({
  mode: 'single',
  env: 'prod',
});

app.listen(9000, '0.0.0.0', () => {
  console.log('Server start on http://0.0.0.0:9000');
});
:::
</dx-codeblock>



- nextjs
<dx-codeblock>
::: js
#!/var/lang/node12/bin/node

/*
# As the HTTP passthrough function runs based on the docker image, the listening address must be 0.0.0.0, and the port 9000
*/
const { nextStart } = require('next/dist/cli/next-start');
nextStart(['--port', '9000', '--hostname', '0.0.0.0']);
:::
</dx-codeblock>

- nuxtjs
<dx-codeblock>
::: js

#!/var/lang/node12/bin/node

/*
# As the HTTP passthrough function runs based on the docker image, the listening address must be 0.0.0.0, and the port 9000
*/
require('@nuxt/cli')
  .run(['start', '--port', '9000', '--hostname', '0.0.0.0'])
  .catch((error) => {
    require('consola').fatal(error);
    require('exit')(2);
  });
:::
</dx-codeblock>

- nestjs
```sh
#!/bin/bash

# SERVERLESS=1 /var/lang/node12/bin/npm run start -- -e /var/lang/node12/bin/node
SERVERLESS=1 /var/lang/node12/bin/node ./dist/main.js
```

- flask
```sh
#!/bin/bash

# As the HTTP passthrough function runs based on the docker image, the listening address must be 0.0.0.0, and the port 9000
/var/lang/python3/bin/python3 app.py
```

- django
<dx-codeblock>
::: sh
  

#!/bin/bash

# As the HTTP passthrough function runs based on the docker image, the listening address must be 0.0.0.0, and the port 9000
/var/lang/python3/bin/python3 manage.py runserver 0.0.0.0:9000
:::
</dx-codeblock>

- laravel
<dx-codeblock>
::: sh

#!/bin/bash

#######################################
# Inject environment variables in the serverless environment
#######################################
# Inject the SERVERLESS flag
export SERVERLESS=1
# Modify the template compilation cache path, as only `/tmp` is readable/writable in SCF
export VIEW_COMPILED_PATH=/tmp/storage/framework/views
# Modify `session` to store it in the memory (array type)
export SESSION_DRIVER=array
# Output logs to `stderr`
export LOG_CHANNEL=stderr
# Modify the application storage path
export APP_STORAGE=/tmp/storage

# Initialize the template cache directory
mkdir -p /tmp/storage/framework/views

# As the HTTP passthrough function runs based on the docker image, the listening address must be 0.0.0.0, and the port 9000
# Path of the executable file in the cloud: /var/lang/php7/bin/php
/var/lang/php7/bin/php artisan serve --host 0.0.0.0 --port 9000
:::
</dx-codeblock>
