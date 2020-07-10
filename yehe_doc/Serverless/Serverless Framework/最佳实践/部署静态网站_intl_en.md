## Operation Scenarios
You can connect the static website component to the Tencent Cloud COS component in order to quickly deploy a static website in COS and generate a domain name for access over the public network.

You can host your custom webpage in COS and generate a domain name for access over the public network as instructed in [Directions](#caozuo). Based on the static website component, you can build a blog system (such as [Hexo](https://intl.cloud.tencent.com/document/product/1040/36749)) more easily; you can also add certain extensions to it so as to support frontend frameworks (such as Vue and React).

<span id="caozuo"></span>
## Directions
### 1. Install

Install Serverless through npm:

```console
$ npm install -g serverless
```

### 2. Create

Create a `my-website` folder locally:

```console
$ mkdir my-website
$ cd my-website
```

Create a corresponding `serverless.yml` file in the folder and store the static webpage in the `code` directory. The directory structure is as follows:

```console
$ touch serverless.yml
```

```
|- code
  |- index.html
|- serverless.yml

```

 The `code` directory should store the corresponding HTML/CSS/JavaScript resource files or a complete React application.
Download the [sample HTML code](https://tinatest-1251971143.cos.ap-beijing.myqcloud.com/index.html) and add the following code to the `index.html` file:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello, Tencent Cloud</title>
</head>
<body>
Hello, Tencent Cloud
</body>
</html>
```

### 3. Configure

Configure the `serverless.yml` file as follows:

```yml

# serverless.yml

component: website # Name of the imported component, which is required. The `tencent-website` component is used in this example
name: websitedemo # Name of the instance created by this `website` component, which is required
org: test # Organization information, which is optional. The default value is the `APPID` of your Tencent Cloud account
app: websiteApp # Website application name, which is optional
stage: dev # Information for identifying environment, which is optional. The default value is `dev`

inputs:
  src:
    src: ./code
    index: index.html
    # dist: ./dist
    # hook: npm run build
    # websitePath: ./
  region: ap-guangzhou
  bucketName: my-bucket
  protocol: https

```


### 4. Deploy

If you have not [logged in to](https://intl.cloud.tencent.com/login) or [signed up for](https://intl.cloud.tencent.com/register) a Tencent Cloud account, you can directly log in or sign up:

Deploy by running the `sls deploy` command, and you can add the `--debug` parameter to view the information during the deployment process:

```console
$ sls deploy
  
region:  ap-guangzhou
website: https://my-bucket-1258834142.cos-website.ap-guangzhou.myqcloud.com
  
22s › myWebsite › done

```


### 5. Remove

Run the following command to remove the project:
```console
sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Starting Website Removal.
  DEBUG ─ Removing Website bucket.
  DEBUG ─ Removing files from the "my-bucket-1300415943" bucket.
  DEBUG ─ Removing "my-bucket-1300415943" bucket from the "ap-guangzhou" region.
  DEBUG ─ "my-bucket-1300415943" bucket was successfully removed from the "ap-guangzhou" region.
  DEBUG ─ Finished Website Removal.

  3s › myWebsite › done
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
