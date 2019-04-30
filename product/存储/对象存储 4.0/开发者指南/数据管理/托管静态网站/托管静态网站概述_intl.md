## Concept

A static website is a website that contains static content (such as HTML) or client scripts. Users can configure static websites for buckets with a custom domain name through the console. A dynamic website contains server scripts such as PHP, JSP, or ASP.NET, and needs to be processed on a server. You can host static websites on Tencent Cloud COS, but cannot write server scripts. When deploying a dynamic website, you are recommended to use a CVM for server code deployment.

## Example

A user created a bucket named examplebucket-1250000000 and uploaded the following file: 

```shell
index.html
404.html
403.html
test.html
docs/a.html
images/
```

### Static website

**Before enabled**: Access the bucket via the following default domain name. When a download prompt pops up, save the `index.html` file to the local.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/index.html
```

**After enabled**: Access the bucket via the following access node, and then you can view the content of `index.html` directly in the browser.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/index.html
```

### Forced HTTPS

**Before enabled**: When the request source is HTTP, the access node URL keeps the HTTP unencrypted transport protocol:

```shell
http://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```

**After enabled**: The access node always maintains the HTTPS encrypted transport protocol regardless of whether the request source is HTTP or HTTPS:

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com
```

### Index document

An index file, the homepage of the static website, is a page returned when the root directory or any subdirectory of a website is requested, and is usually named `index.html`.
When you access a static website via a bucket access domain name, such as `https://examplebucketbucket-1250000000.cos-website.ap-guangzhou.myqcloud.com`, and no specific page is requested, the Web server will return the homepage.

When your user accesses any directory (including the root directory) in a bucket using a URL ended with `/`, the index document in that directory is matched automatically. `/` is not mandatory in the root URL, so the index document is returned in response to either of the following URLs.

```shell
http://www.examplebucket.com/
http://www.examplebucket.com
```

> !If a folder is created in the bucket, the index file needs to be added at each level of the folder.

### Error document

Suppose that when you visit the following page before configuring the error document, a 404 status code is returned, and the default error information displays in the page.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/webpage.html
```

When you visit the following page after configuring the error document, a 404 status code is also returned, but the specific error information displays in the page.

```shell
https://examplebucket-1250000000.cos-website.ap-guangzhou.myqcloud.com/webpage.html
```

### Redirection rules

#### Configure error code redirection

If the webpage.html document is set to **Private Read/Write**, when a user tries to access it, a 403 error is returned.
After the 403 error code is redirected to 403.htm, the browser will return the content of 403.html.
If you do not configure a 403.html document, the browser will return an error document or default error message.
![](https://main.qcloudimg.com/raw/7dc917ba95af42438b6ab2c7604666d3.png)

#### Configure prefix match

1. When you rename a folder from `docs/` to `documents/`, the user will get an error when accessing the `docs/` folder. So, you can redirect the request with the prefix `docs/` to `documents/`.
![](https://main.qcloudimg.com/raw/e3b5c9004a67d020928bd0035b820715.png)
2. When you delete the `images/` folder (i.e., deleting all objects with the prefix `images/`), you can add a redirection rule to redirect requests for any object with the prefix `images/` to `test.html`.
![](https://main.qcloudimg.com/raw/b6672acf43149267a837027911923f9b.png)

