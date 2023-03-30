<!DOCTYPE html>

**Try it now with [our Demo](https://tencent-im-chat.myshopify.com/), password is `tencentim`.**

## Introduction

Shopify, the world's leading e-commercial SaaS platform, with numbers of merchants building their online shops based on it globally. Meanwhile, according to [Gartner](https://www.gartner.com/en/documents/4006202), Tencent Cloud Chat became the champion in the Chinese market and one of the most competent providers in Communication Platform as a Service (CPaaS) in the global market.

Naturally, it comes to us to bring you the solution of building the chat widget on your Shopify online store based on Tencent Cloud Chat, in order to convert more online shop visitors to your customers, and deliver personal customer support at any scale no matter where they are from.

After the integration, the effect is shown below. Also, you can experience it with [our Demo](https://tencent-im-chat.myshopify.com/), password is `tencentim`.

![](https://qcloudimg.tencent-cloud.cn/raw/d35bb915f4b1933d03e92e3efdcb53c5.jpg)

## What you'll learn

In this tutorial, we will discuss how to build this chat box on your Shopify online store with the codes we provided.

- Initialize a Shopify app.
- Building this app with the codes, related to the chat module, we provided.
- Install this app to your Shopify store.
- Enable it to communicate with your existing chat APP, for agent serving purposes.

![](https://qcloudimg.tencent-cloud.cn/raw/57ade5963f456ff2050a3c83fa97b47a.png)

>?
>
>For the agent side shows on the left of the picture above, you can implement it with our [TUIKit](https://www.tencentcloud.com/document/product/1047/45907#part-4.-using-tuikit-component-library-to-implant-im-capabilities-in-half-a-day) or [DEMO](https://www.tencentcloud.com/document/product/1047/45907#part-3.-using-the-demo) easily, or you can build your own APP with our [Chat SDK](https://www.tencentcloud.com/document/product/1047/45907#part-5.-self-implementing-integration).

## Requirements

- You've [created a Tencent Cloud Chat APP](https://www.tencentcloud.com/document/product/1047/34577), with the specific SdkAppID.
- You've built a chat APP with the [SDKs](https://www.tencentcloud.com/document/product/1047/34552) we provided, binding with this SdkAppID. It's recommended to build it based [on our DEMO](https://www.tencentcloud.com/document/product/1047/45907), if you do not have one.
- You've created a [Shopify Partner account](https://www.shopify.com/partners?shpxid=881a4b68-1240-4F49-9BED-7B203FC08769) and a [development store](https://shopify.dev/apps/tools/development-stores#create-a-development-store-to-test-your-app).
- You've installed [Node.js](https://nodejs.org/en/download/) 14.13.1 or higher.
- You've installed a Node.js package manager: either [npm](https://docs.npmjs.com/getting-started), [Yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable) 1.x, or [pnpm](https://pnpm.io/installation).
- You've installed [Git](https://git-scm.com/).
- You're using the latest version of [Chrome](https://www.google.com/chrome/) or [Firefox](https://www.firefox.com.cn/?utm_medium=referral&utm_source=mozilla.org).
- You've installed an Online Store 2.0 theme, such as [Dawn](https://shopify.dev/themes/tools/dawn), that uses [JSON templates](https://shopify.dev/themes/architecture/templates/json-templates).
- You have at least [Ruby](https://www.ruby-lang.org/en/downloads/) 2.7.5 installed on your system.

> ?
>
> The Shopify Partner account used in this tutorial is only for developing your own app purposes, you don't need to publicize this app to the Shopify App store.
>
> The development store is only for testing and previewing your app while developing, we will guide you to install your app to your online store by the end of this tutorial.

## Let's get started

### Step 1: Create a new Shopify app

You can create a new Shopify app using an npm, yarn, or pnpm command. Using npm as an example in this tutorial.

1. Navigate to the directory where you want to create your app. Your app will be created in a new subdirectory.

2. Run one of the following commands to create a new app, and select `node` as the template.

```shell
npm init @shopify/app@latest
```

A new app is created, and Shopify CLI is installed along with all of the dependencies that you need to build Shopify apps. Shopify CLI is also added as a dependency in your app's package.json.

The following image shows an app being successfully created in the terminal:

![](https://qcloudimg.tencent-cloud.cn/raw/345f191f1afba4529e73e55c320f5b0c.png)

### Step 2: Start a local development server

After your app is created, you can work with it by building the app and starting a local development server.

Shopify CLI uses [ngrok](https://ngrok.com/) to create a tunnel that allows your app to be accessed using a unique HTTPS URL. You need to [create an ngrok account](https://ngrok.com/) and [auth token](https://dashboard.ngrok.com/get-started/your-authtoken) to preview your app using Shopify CLI.

1. Navigate to your newly-created app directory.

```shell
cd your-app
```

2. To start a local server for your app, run the following command:

```shell
npm run dev
```

Shopify CLI walks you through the following:

- Logging into your [Shopify Partner account](https://help.shopify.com/partners/about?shpxid=8894c954-8476-4D3A-E976-20C989E45FC1) and, if needed, selecting a Partner organization
- Creating an app in the Partner Dashboard, and connecting your local app files to the app
- Storing your ngrok token, and then creating a tunnel between your local environment and the development store using ngrok

> ?
>
> If you encounter ngrok errors in your browser when you try to preview your app or app extension, then consider using a tunnel created with your own tunneling software instead. Shopify recommends using [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/do-more-with-tunnels/trycloudflare/).
> To use your own tunnel, pass your tunnel URL and port to the `dev` command with the [--tunnel-url flag](https://shopify.dev/apps/tools/cli/commands#dev-flags).

The following image shows a development server being started using `dev`:

![](https://qcloudimg.tencent-cloud.cn/raw/f7d1cc2f5bf1d00df94edeca620e0bfb.png)

### Step 3: Install your app on your development store

With the server running, open the URL in the App URL section of the terminal output in the previous step.

The URL follows the format `https://[tunnel_url]?shop=[dev_store].myshopify.com&host=[host]`, where `[host]` is the base64-encoded [host](https://shopify.dev/apps/tools/app-bridge/retrieve-the-host) parameter used by App Bridge, and represents the container the app is running in.

When you open the URL, you're prompted to install the app on your development store.

Click **Install app** to install the app in the store.

![](https://qcloudimg.tencent-cloud.cn/raw/5f9b47b9b819dc73516c668fa55b4a39.png)

![](https://qcloudimg.tencent-cloud.cn/raw/9c889967df7f18e5afc6d8635d17261a.png)

### Step 4: Modify the frontend code in this admin dashboard

> ?
>
> This step is optional, mainly to replace the default app page on admin with the configuration guidance page.

1. Replace the `web/frontend/pages/index.jsx` file.

<a href="https://comm.qq.com/im/static-files/shopify/index.jsx" download="index.jsx">Download the new file</a>, named it as `index.jsx` and replace the file of `web/frontend/pages/index.jsx`.

2. Add the guide page.

<a href="https://comm.qq.com/im/static-files/shopify/Guide.jsx" download="Guide.jsx">Download the file</a>, named it as `Guide.jsx`, and move it into `web/frontend/components/Guide.jsx`.

3. Add a line of export class to `web/frontend/components/index.js`.

```js
export { Guide } from "./Guide";
```

4. Add the file resources to `web/frontend/assets`.

- [Logo](https://qcloudimg.tencent-cloud.cn/raw/2040c1d22e582bf0fa6a7fbde0123623.png), named as `logo.png`.

- [Demo instructions](https://dscache.tencent-cloud.cn/upload/uploader/demo-6c67169d12f8aa159f0a0c80b5d781c1789d1534.png), named as `demo.png`.

Add the export to `web/frontend/assets/index.js`.

```js
export { default as logo } from "./logo.png";
export { default as demoImage } from "./demo.png";
```

Now, the updating of the admin page is finished, you can refresh the page and see the following page.

![](https://qcloudimg.tencent-cloud.cn/raw/6767b5b8244e009617b0b70d5cb9af6e.png)

### Step 5: Create a new extension

This extension will be the chat box widget shown at the bottom right of the online store.

You'll use Shopify CLI to generate a new extension first.

1. Navigate to the directory of the app that you want to add your extension to.

2. Run the following command to start creating the extension, choose `Theme app extension` as the `Type of extension`.

```shell
npm run shopify app generate extension
```

> ?
>
> Please make sure you use [Shopify CLI](https://shopify.dev/apps/tools/cli) 3.0 or higher, if this command does not work.

![](https://qcloudimg.tencent-cloud.cn/raw/248b068600a171152bd78ca6ef896de1.png)

After your theme app extension is created, you can preview your changes in real time by starting a local development server.

The `dev` command returns a preview URL that reloads local changes, allowing you to preview changes in real time using the store's data. This preview is only available in Google Chrome.

1. Navigate to your app directory.

2. Run one of the following commands:

```shell
npm run dev
```

3. Follow the instructions in the CLI output to enable your theme app extension and set it up in the host theme.

4. Click the URL that's printed at the bottom of the CLI output to preview your extension.

![](https://qcloudimg.tencent-cloud.cn/raw/ca8e56554349dcd6692f6cf83a65b988.png)

### Step 6: Modify the code of extension to build a chat box widget

1. [Download our sample code package](https://comm.qq.com/im/static-files/shopify/live-chat.zip).

2. Unzip it.

3. Move and replace the `assets` and `blocks` directory to `extensions/(your extension directory)`, and it will be like:

![](https://qcloudimg.tencent-cloud.cn/raw/dee33e53ea2775465a0cac38a962935c.png)

### Step7: Start up a server to generate UserSig for each UserID

As you can see in our [DEMO](https://tencent-im-chat.myshopify.com/) (password is `tencentim`), visitors are supposed to start a chat with their email address, and this field will be the user ID for you app of Tencent Cloud Chat.

Both `UserID` and `UserSig` are needed for login before chatting, while the `UserSig` is [generated with `UserID`, `SECRETKEY` and `SDKAppID` dynamically](https://www.tencentcloud.com/document/product/1047/34385).

As a result, you should start up a server to generate `UserSig` from `UserID`, while the `SECRETKEY` and `SDKAppID` have been stored on your server for safety purposes.

You could build this service by yourself or using the serverless template we provided.

The communication between the chat box and your server should use RESTful API, with POST request.

The following shows request parameters from the chat widget. The `Content-Type` is `application/json`.

```JSON
{
   "userID": "The User ID"
}
```

The response body from your server should be like following:

```JSON
{
   "userID": "",
   "userSig": ""
}
```

#### Set up the `UserSig` generation service with serverless function

You are also encouraged to use our template to create a serverless function on Tencent Cloud, if you find complicating to build such a `UserSig` generation service.

1. Navigate to the console of [Tencent Cloud Serverless Cloud Function](https://console.tencentcloud.com/scf/list?rid=15&ns=default), choose a region and click `Create`.

![](https://qcloudimg.tencent-cloud.cn/raw/5e54b2075445bb3afbf929fe34da9ddf.png)

2. Search by keyword, `usersig`, choose the following one, then click `Next`.

![](https://qcloudimg.tencent-cloud.cn/raw/c18c26ae96fa70e013a03d9391a363e6.png)

3. Specify the `Function name` based on your needs.

4. Click the `Advanced configuration` module and add the following `Environment configuration`.

| key        | value                                                |
| ---------- | ---------------------------------------------------- |
| SDK_APP_ID | (Your SDKAppID)                                      |
| SECRET     | (The `Key` shows on the main page of the IM console) |

![](https://qcloudimg.tencent-cloud.cn/raw/e88ce09332eab52a7d1f254e9011cbe4.png)

5. After deployment, create a trigger for it by clicking `Trigger management` on the left bar, then click `Create trigger`. Use the default settings on the modal opened, then click `Submit`.

> It might require granting permissions to `API Gateway` first, please follow the instructions to grant.

![](https://qcloudimg.tencent-cloud.cn/raw/f8622716857a8091362b9c943b931c13.png)

![](https://qcloudimg.tencent-cloud.cn/raw/d54e8116000039413f462e694481c841.png)

6. Find the URL of the API created from `Function management` => `Function codes` => `Access path`. This URL will be used in the following steps.

![](https://qcloudimg.tencent-cloud.cn/raw/d5c9be992d0fda56914cee9b029a17c2.png)

7. [Optional] You can test it by [`Postman`](https://www.postman.com/).

![](https://qcloudimg.tencent-cloud.cn/raw/eb68db16ba8c50da4b9ccf0896130895.png)

### Step 8: Configure this extension

Run the following commands to start the extension:

```shell
npm run dev
```

Click the second URL that's printed at the bottom of the CLI output to set up the extension.

![](https://qcloudimg.tencent-cloud.cn/raw/4e9a53c8cbb7fb3255633045d7f77e0d.png)

Switch to 'App embeds' on the left menu, and enable 'Tencent Chat Widget'.

Fill in the settings related to it. The detailed introduction for each field shows below the image.

![](https://dscache.tencent-cloud.cn/upload/uploader/demo-6c67169d12f8aa159f0a0c80b5d781c1789d1534.png)

| Field                  | Description                                                  | Required |
| ---------------------- | ------------------------------------------------------------ | -------- |
| SDKAppID               | The `SDKAppID` from [Tencent Cloud Chat console.](https://console.tencentcloud.com/im/detail) | true     |
| Usersig generation URL | The service to generate Usersig for each UserID. The URL of the API was created from step 7. | true     |
| Agent User ID          | The User ID of the customer support agent. The user who visitors chat with. | true     |
| LOGO URL               | The logo shows on the title bar.                             | false    |
| First line             | The first line of the title.                                 | false    |
| Second line            | The second line of the title.                                | false    |

After the configuration, click the `Save` button on the top right.

Now, you can click the third URL that's printed at the bottom of the CLI output to preview the extension.

![](https://qcloudimg.tencent-cloud.cn/raw/e4533cd7984d1186346a7d1cee6e2eb9.png)

Make sure the chat widget works well. You can refer to our [sample codes](https://dscache.tencent-cloud.cn/upload/uploader/live-chat-217421bd865a83d605482d79af50b53c7af9af53.zip), if errors are encountered.

## Step 9: Deploy the chat widget extension

After your chat widget extension is ready for online stores, you can deploy the latest code and make the app extension public to the development store.

1. Navigate to your app directory.

2. Run the following commands:

```shell
npm run deploy
```

3. After you deploy the extension to Shopify, navigate to your app in the [Partner Dashboard](https://partners.shopify.com/2612231/apps), click `Extensions`, and click the draft version that you previously created.

4. Click `Create version` to create a version of your theme app extension.

5. Click `Publish` beside the version that you want to publish, and click `Publish` in the popup modal to confirm.

### Step 10: Install this app to your online store

1. From the Shopify Partner Dashboard, go to [Apps](https://partners.shopify.com/current/apps) and then select your newly created app from the list.

2. In the sidebar, click **Distribution**.

3. Select "Single-merchant install link" as the distribution method.

![](https://qcloudimg.tencent-cloud.cn/raw/d2b5b6a3cfaaaf86f4beba510f93679f.png)

4. Generate the install link for your Shopify store, by entering your `myshopify.com` domain here.

![](https://qcloudimg.tencent-cloud.cn/raw/3218249fea1bbc96bcfce5ad2d1f76f3.png)

5. Use the generated link to install the app in your current store.

![](https://qcloudimg.tencent-cloud.cn/raw/55a5beeecccc9ec15aa326d35a3ba74d.png)

6. Enable and configure the widget on the `Themes` section of your admin dashboard. The steps of enabling and configuring the widget can refer to step 8.

![](https://qcloudimg.tencent-cloud.cn/raw/4e41660310a80f2866b6462d90dd57bf.png)

## Conclusion

That's all you need to add a Tencent Cloud Chat widget to your Shopify store.

If there's anything unclear or you have more thinkings about the integration with Shopify, feel free to contact us!
